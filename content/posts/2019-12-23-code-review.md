---
title: "Code Review 开始"
date: 2019-12-23T20:27:25+08:00
draft: false
tags: 
- 管理
categories: 
- Tech 
featured_image: 
description: 
---
# 简介 
整个golang团队20多人，没有code review ，对项目质量、对结果产出、对新人的成长，对团队交流的氛围影响大。 看过[Google 代码评审规范](https://www.infoq.cn/article/QJi1Kqm4pH3UNAqNzl3l)，解决了我之前一些疑问和也让我坚定的去Code Review。  
当没有code review时候，要求重构，而重构价值是释放历史包袱，并没有产生任何其他价值  

- 我们的提交是这样的  

```golang
3b8e45c - Slove Confilct -  2 weeks ago -
0a39ecd - FIXS: vendor -  2 weeks ago -
7817d14 - debug -  2 weeks ago -
67539e2 - debug -  2 weeks ago -
9044356 - Slove Confilct -  2 weeks ago -
d47db91 - FIXS: ss -  2 weeks ago -
8913c30 - Slove Confilct -  2 weeks ago -
2d407d2 - FIXS: logger -  2 weeks ago -
```

``` golang
b9af055 - 打印日志 -  7 weeks ago - 
1124e92 - 打印日志 -  7 weeks ago - 
88d0eac - 修改log -  7 weeks ago - 
ad0b3dd - 修改日志 -  7 weeks ago - 
4aa0740 - 答应日志 -  7 weeks ago - 
824658a - 修改日志 -  7 weeks ago - 
178c30c - 打印日志 -  7 weeks ago - 
```
> 在pull request的时候，认真review下所有的commit，该合并得合并，该修改得修改

- 我们的命名是这样的  
  这里不截图纪念了. 

- 我们的代码分支和发版是这样的  
  本地打包,更恶心的是代码不提交本地打包的.  

- 我们的单元测试是这样的  
  几乎没有  

我们开始要做Code Review， 从哪里开始了？  
# 方式
谁对谁在什么时候用什么方式去做什么？

## 第一个“谁”

### 代码评审员
如果项目存在两人或者两人以上开发 

- 如果开发提交代码，则应用项目负责人  
- 如果应用负责人也参与开发，则由另外任一一位开发做一次review，然后上一级的负责人做第二次review。 

如果应用负责人和开发是同一个人，这时候为“小组Leader”   

### 自动Lint工具
借助自动化完成代码最基本的审核， 比如reviewdog & golangci-lint， 更多相关知识[Github Action-golangci-lint](https://github.com/reviewdog/action-golangci-lint)   



## 第二个“谁”
业务开发人员对应用提交的pull request 

## 什么时候
提交Review时的当天或者第二天须完成

## 什么方式
依照代码审核规范， 目前缺少自己的审核规范，
类似规范参考

- 代码审查规范
  - [Google 代码评审规范](https://www.infoq.cn/article/QJi1Kqm4pH3UNAqNzl3l)  
  - [谷歌工程实践 by jimmysong][google-golang-practice]
- [How Thanos Would Program in Go](https://www.bwplotka.dev/2020/how-thanos-would-program-in-go/)

## 做什么
阅读提交的代码并给出建议完成审核

# 落地

## reviewdog & golangci-lint在gitlab上配置实践
熟悉github action方式， 借鉴其优点； 在一个项目中实践，然后推广到其他项目中。

- 如何做到所有项目不需要自行配置或者简单的配置（比如增加一个配置现成的文件），并且使用同一个套代码检查标准？ 
- 目前没有非常成熟的方案，需要花费一些时间去解决现有开源方案中的问题。
    - *reviewdog 结合 golangci-lint 使用，修改其输出格式, [more link][golangci-lint-fmt]*
      在[presto-pay][presto_pay]是使用golangci-lint,但是reviewdog在官网上没有golangci-lint的案例

**失败**

- golangci-lint自身大而全的能力，导致其功能本身不稳定，不如golint或errcheck那么纯粹 

## reviewdog & golint/errcheck/govet/... 在 gitlab 上配置实践

```yml

reviewdog:
  stage: review
  image: golang:latest
  before_script:
    - curl -sfL https://raw.githubusercontent.com/reviewdog/reviewdog/master/install.sh| sh -s -- -b $(go env GOPATH)/bin v0.10.0
    # - curl -sSfL https://raw.githubusercontent.com/golangci/golangci-lint/master/install.sh | sh -s -- -b $(go env GOPATH)/bin v1.27.0
    - go get -u golang.org/x/lint/golint
    - go get -u github.com/kisielk/errcheck
    - export GITLAB_API="https://examplegitlab.com/api/v4"  
  script:
    - golint ./... | reviewdog -f=golint -diff="git diff master" -reporter=gitlab-mr-discussion  -fail-on-error=true
    - ( errcheck -asserts -ignoretests -blank $(go list ./... | grep -v /vendor/) 2>&1 || true ) | reviewdog -name=errcheck -efm="%f:%l:%c:%m" -reporter=gitlab-mr-discussion -level=warning -fail-on-error=true
    # - ( golangci-lint run --out-format=line-number ./... 2>&1 || true ) | reviewdog -f=golangci-lint --name=golangci-lint  -diff="git diff master" -reporter=gitlab-mr-discussion -fail-on-error=true
  only:
    - merge_requests
```

更多： 

- reviewdog 结合各种错误检查，详细见: [reviewdog.yml][reviewdog_for_go_tools]
- 使用预设的errformat, 例如通过参数`-f=golangci-lint`，更多的预设errformat使用 `reviewdog -list` 查看， 点击链接[ go.go ][go-fmt]
- 在gitlab里配置参考gitlab上的工程：[reviewdog test][reviewdog-test]
- exit code的处理 
  -  errcheck 命令在检查到 err 时，exit code为0 （通过echo $?查看, 更多查看[Chapter 6. Exit and Exit Status][exit_and_status]）
  -  reviewdog默认的 exit code 为0， 当加上 -fail-on-error=true时候则会返回1（当检查到不规范的时候）
  -  errcheck | reviewdog  根据现象是当errcheck 的 exit code 为1时，job会失败。 解决办法是 ( errcheck 2>&1 || true ) | reviewdog

在这个过程中，不断增加的检查机制, 并说明理由\目的

[thanos](https://github.com/thanos-io/thanos) 代码规范推荐的代码 linter 工具 `go vet`, 同时也推荐 golangci-lint, 
但 golangci-lint 无法配置的原因, 将考虑一个个配置其默认的 [linter](https://golangci-lint.run/usage/linters/) , 建议参考Thanos 里配置的 [linters](https://www.bwplotka.dev/2020/how-thanos-would-program-in-go/#golangci-lint)

- govet
- errcheck
- staticcheck
- unused
- gosimple
- structcheck
- varcheck
- ineffassign
- deadcode
- typecheck

### golint 

### errcheck

### go vet

# TODO
反复阅读代码评审规范.
不断增加或修正 linter

# 参考
1. reviewdog
  https://github.com/reviewdog/reviewdog#reporter-github-pullrequest-review-comment--reportergithub-pr-review 

2. golangci-lint
  https://github.com/golangci/golangci-lint


[go-fmt]: https://github.com/reviewdog/errorformat/blob/master/fmts/go.go

[reviewdog-test]: https://gitlab.com/Hyvi/reviewdog-test/-/blob/gitlab-ci-test2/.gitlab-ci.yml

[golangci-lint-fmt]: https://gitlab.com/Hyvi/reviewdog-test/-/blob/gitlab-ci-test2/.gitlab-ci.yml

[presto_pay]: https://github.com/calmato/presto-pay/blob/master/api/user/Makefile

[exit_and_status]: https://www.tldp.org/LDP/abs/html/exit-status.html#EXITSTATUSREF

[reviewdog_for_go_tools]: https://gitlab.com/reviewdog/reviewdog/-/blob/master/.reviewdog.yml

[google-golang-practice]: https://jimmysong.io/eng-practices/

<br>

<center>  ·End·  </center>
