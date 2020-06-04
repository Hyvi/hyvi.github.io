---
title: "Golang Pprof 使用梳理"
date: 2020-04-16T09:11:28+08:00
draft: false
tags:
categories:
featured_image:
description:
---
# 背景
当前碰到的问题：

- 部分服务 CPU 负载比较高
- 服务内存使用量比较大
- 服务高延迟（内存 CPU 负载都不高情况）

golang 开发中有一些定位这些问题的套路和工具，在本文中汇总，记录并不断改进解决问题的思路。

从两个方面考虑：

- 系统监控统计级别数据指标
    - goroutine 数量
    - 堆 (heap) 内存使用量
    - 栈 (stack) 内存使用量
    - 其他...（待补充）
- 问题定位所需的详细数据
    - 获取系统实时堆内存分配详细信息：具体到这个内存在哪里分配的。
    - 获取系统实时所有 goroutine 调用堆栈信息：具体到这个 goroutine 是在哪里启动的，以及当前在干什么
    - 获取系统实时堆内存调优辅助统计信息： 具体是在哪里分配了多少内存，以及 TOP N 分别是哪些，甚至是每个内存分配的来源图

# Diagnostics

## 获取系统实时堆内存分配详情
``` golang
// 引入 pprof
import "net/http/pprof"
// 在 http router 上加入
this.debugMux.HandleFunc("/debug/pprof/", http.HandlerFunc(pprof.Index))
```

`curl -XGET "http://192.168.149.150:8080/debug/pprof/heap?debug=2"` 获取 heap 内存的详细信息，其中 8080 是你开启的 http server 的端口，debug=2 意味着需要输出详细信息

## 获取系统实时所有 goroutine 调用栈信息
通过`curl -XGET "http://192.168.149.150:8080/debug/pprof/goroutine?debug=2"`拿到的就是 goroutine 的详细信息

## 获取系统实时堆内存调优辅助统计信息
`go tool pprof -inuse_space http://192.168.149.150:8080/debug/pprof/heap`，进入 pprof 交互模式后，可以通过 top, tree 等进一步查看统计信息，同时，也可以通过 png 命令，将内存信息输出成图片，以图片的形式显示内存的分配、占用情况

## 获取 trace 数据
通过：`curl -XGET "http://127.0.0.1:8080/debug/pprof/trace?seconds=30" -o 002_trace_2017_09_08.out`我们将获取一个 30 秒的 trace 数据 (trace_02.out)，通过`go tool trace 002_trace_2017_09_08.out`

也是各种坑， 比如页面打开空白： [gotip tool trace xxx.out](https://github.com/golang/go/issues/25151)

## profile
侧重于统计程序各 goroutine 自身的运行状况，更加适用于分析针对 cpu 密集型逻辑导致的 latency 过高问题

### cpu
### heap
pprof 的top会列出5个统计数据： 

- flat: 本函数占用的内存量
- flat%: 本函数内存占使用中内存总量的百分比
- sum%: 前面每一行flat百分比的和
- cum： 是累计量，假如main函数调用了函数f, 函数f占用的内存量，也会记进来
- cum%: 是累计量占总量的百分比 

Memory profiling records the stack trace when a heap allocation is made

Stack allocations are assumed to be free and are not tracked in the memory profile. 

Memory profiling, like CPU profiling is sample based, by default memory profiling samples 1 in every 1000 allocations this rate can be changed.

Because of memory profiling is samples based and because it tracks allocation not use , using memory profiling to determine your Application's overall memory usage is difficult .

#### Head "不能" 定位内存泄漏
![](https://segmentfault.com/img/remote/1460000019222668?w=1008&h=868/view)

1. 该goroutine只调用了少数几次，但是消耗大量的内存
2. 该goroutine调用次数非常多，虽然协程调用过程中消耗的内存不多，但该调用路径上，协程数量巨大，造成大量的内存消耗，并且这些goroutine由于某种原因无法退出，占用的内存不会释放。

第二种情况， 就是**goroutine泄漏**， 这是通过heap无法发现的, 所以heap在定位内存泄漏这件事情上，发挥作用不大。

#### goroutine泄漏怎么导致内存泄漏

- 每个goroutine占用2kb内存
- goroutine执行过程中存在一些变量，如果这些变量指向堆中的内存，GC会认为这些内存仍在使用，不会对其进行回收，这些内存无法使用，造成内存泄漏
    a. goroutine本身的栈占用的空间
    b. goroutine中的变量所占用的堆内存，这一部分是能通过heap profile体现出来的。

### threadcreate
### goroutine
### block
### mutex
实践web方式[Mutex profle](https://rakyll.org/mutexprofile/)

~~里面提到的PPT在本地分析不出数据, ~~, 因为没有用goroutine

```golang
for _, f := range factors(n) {
  mu.Lock()
  m[f]++
  mu.Unlock()
}
```


```golang
mu.Lock()
for _, f := range factors(n) {
  m[f]++
}
mu.Unlock()
```
## Trace

### Synchronization blocking profile
来自rhys Hiltner 分析.

the thing that we are spending here is seconds that we're spent waiting. we have kind of the goroutine name at the top of the stack.

关于方框中“of"前面的的0, 表示 ”zero time was spent inside of the box of 4.43. [来自 Profiling and Optimizing Go,关于Type:CPU的图解，时间： 11:00]（ https://www.youtube.com/watch?v=N3PWzBeLX2M )

### goroutines 
goroutines that were running in that propram during those few seconds that i was recoording and listed. 

根据Execution time\Network wait time\Sync block time\Blocking syscall time\Sechedule wait time的情况后，可以通过graph图了解goroutine详细情况。`参考[10]`
## Flame
```bash
pprof -http "localhost:12345" 'http://127.0.0.1:53668/block?id=19105152&raw=1'
```
查看goroutine中执行时间。 

在参考[7]的视频11:43开始实际操作使用Flame定位程序执行慢的问题。

## Debugging
## Runtime statistics and events
# 实践
定位高延迟的服务。

使用 logrus 打印日志文件，其中 Logrus 使用全局锁导致，goroutine 之间竞争写锁。

```golang

func (entry *Entry) write() {
	entry.Logger.mu.Lock()
	defer entry.Logger.mu.Unlock()
	serialized, err := entry.Logger.Formatter.Format(entry)
	if err != nil {
		fmt.Fprintf(os.Stderr, "Failed to obtain reader, %v\n", err)
	} else {
		_, err = entry.Logger.Out.Write(serialized)
		if err != nil {
			fmt.Fprintf(os.Stderr, "Failed to write to log, %v\n", err)
		}
	}
}

```
在这篇 [Is there a golang logging library around that doesn't lock the calling goroutine for logging?](https://www.reddit.com/r/golang/comments/6irpt1/is_there_a_golang_logging_library_around_that/dj8m1sk/) 链接里也提到 logrus 写锁怎么处理

- 协程异步写日志，但是会占内存
- 换 zap 库

其实并没有解答为什么延迟非常高的问题。

# 参考
1. go tool proof 郝琳的中文说明 #TODO
  https://github.com/hyper0x/go_command_tutorial/blob/master/0.12.md

2. Profiling Go Programs 官方 Blog #TODO
  https://blog.golang.org/pprof

3. 一次 Golang 程序内存泄漏分析之旅
  http://lday.me/2017/09/02/0012_a_memory_leak_detection_procedure/ 链接访问有点问题，可以用 google cache 查看文字

4. 一次 Golang 程序延迟过大问题的定位过程
  http://lday.me/2017/09/13/0013_a_latency_identification_procedure/

5. go tool trace
  https://making.pusher.com/go-tool-trace/ #TODO

6. Go 程序的性能监控与分析 pprof
  https://www.cnblogs.com/sunsky303/p/11058808.html

7. Rhys Hiltner - An Introduction to "go tool trace"
  https://www.youtube.com/watch?v=V74JnrGTwKA

8. 关于Go程序调式、分析和优化 来自Brad Fitzpatrick的分享 #TODO
  https://studygolang.com/articles/4716

9. Golang remote profiling and flamegraphs, 对各种图阐述的比较清晰
  https://matoski.com/article/golang-profiling-flamegraphs/

10. Using Go 1.10 new trace features to debug an integration test,  这边文章描述了trace使用过程，赞 
  https://medium.com/@cep21/using-go-1-10-new-trace-features-to-debug-an-integration-test-1dc39e4e812d 

11. Profiling Go programs with pprof #TODO
  https://jvns.ca/blog/2017/09/24/profiling-go-with-pprof/

12. rakyll blog #TODO
  https://rakyll.org/archive/
<br>

13. Diagnostics 官文 #TODO
  https://golang.org/doc/diagnostics.html

14. 实战Go内存泄漏 
  https://segmentfault.com/a/1190000019222661
<center>  ·End·  </center>
