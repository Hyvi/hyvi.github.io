---
title: "Team Topologies 团队拓扑"
date:  2021 年 9 月 28 日 星期二 05 时 55 分 42 秒 CST
draft: false
description: "Conway's law、Dunbar 鄧巴係數、Team Fist Mindset、Minimal  Cognitive Load"
---

起初，对"Cognitive Load" 一词非常好奇，又了解到在 Matthew Skelton 的 [《高效能团队模式》](https://book.douban.com/subject/35528423/) 中介绍其与团队的建设有密切的联系，在查找书籍过程中，也有读后感的文章对此书进行了总结，比如 [Team Topologies - 團隊優先思考模式](https://lab.howie.tw/2020/11/Team-Topologies-team-first-mindset.html)，觉得非常好，得好好细读，一直放在浏览器标签上舍不得关闭，今早早起趁此赶紧消化下，顺便记录下来，往后查阅。



## 名字解释
文章涉及几个专业名词。

| 名词                    | 解释                                                                                                                                                                                                               |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Conway's Law            | 組織內團隊組成的架構，就會直接影響你的軟體系統架構會長成什麼樣子。因為團隊架構決定溝通模式，溝通模式就會影響軟體系統架構                                                                                           |
| Dunbar 鄧巴係數         | 团队中可以深入互相信任且 share working memory 的人数基本上大概是 5 个人左右，极限就是 15 人。而能互相信任的上限大概是 50 个人， 当超过 150 人时就已经高过了社交认知的上限，就连要记住对方的名字都难。                |
| Team Fist Mindset       | 团队优先思考模式，                                                                                                                                                                                                 |
| Minimal  Cognitive Load | 話說我們每個人的 working memory 其實是很有限的，所以要慎選佔用我們記憶體的事物                                                                                                                                     |
| 谷仓效应                | 各部门就像一间「小公司」，各自为政、自负盈亏，只专注在自身的营运利益，而非整个企业的利益，最终导致整个组织功能失调、企业走向衰败。                                                                                 |
| Stream-aligned Team     | organized around the flow of work and has the ability to deliver value directly to the customer or end user. ![](https://www.scaledagileframework.com/wp-content/uploads/2021/02/Organize_Agile_Teams_F01_WEB.png) |


## Team Dynamics
Team dynamics describe the behavior relationship between  the member of a group .

Team dynamics are the unconscious, psychological forces that influence the direction of a team's behaviour and performance. They are like undercurrents in the sea, which can  carry boats in a different direction to the one they intend to sail .

Google 内部研究，影响 Team Dynamics 的因素有哪些？

- Team Size
- Team Lifespan
- Team Relationship
- Team Cognition 团队的认知

好的团队基础就是小巧精干且长存的团队。5-9 人， 固定的团队成员一起为了一个目标工作得时间至少一年以上。

## Tunkman's stages of group development
这个说明了为什么团队至少一年以上。从团队组成到真的可以产出绩效，至少经历以下四个阶段

![](https://s3-us-west-2.amazonaws.com/courses-images/wp-content/uploads/sites/1972/2017/07/04222605/Screen-Shot-2017-08-04-at-3.25.50-PM.png)

- Forming
- Storming
- Norming
- Performing

来自 [Principles of Management](https://courses.lumenlearning.com/suny-principlesmanagement/)

## Team Fist Mindset
团队优先思考模式， 是什么？

- 团队对某个软件负责，并且持续的关注与改善
- Daily  要承诺参与并且不要迟到
- 团队对于内部事务要持续讨论
- 专注于 Team Goal
- 帮助他人移除 blocking thing
- Mentor 新人，相互帮助成长
- 避免争输赢的争论，要能包容探索各种可能性的言论

## Minimal Cognitive Load （最小化的认知负担）
如果要让团队能以高效的模式运转，首先要以小巧精干的长期的团队为单元，并且限制或与减少不必要的沟通。随着系统越来越复杂，团队与团队之间要建立沟通的规范。

- Intrinsic Cognitive Load
- Extraneous Cognitive Load
- Germane Cognitive Load


![](https://1.bp.blogspot.com/-HQWt_LjHo0Q/X6c-P4Ssg1I/AAAAAAAB-MQ/oU1sws5oUmop3JIUDCwmN4lePx8EtEUOgCLcBGAsYHQ/s1600/screenshot_20190725-081022.jpg)


如何最小化认知负担？

- 好的 IDE 和 tool 或者是培训来降低 Intrinsic Cognitive Load
- 通过 SOP 或者专业的 Infra Team / DevOps Team 来帮助建设优化开发部署流程，消减工程师的 Extraneous Cognitive Load
- 让工程师更专注于产生价值的 Germane Cognitive Load， 设计更好的系统来解决客户的问题。

另外，Three ways to reduce team cognitive load and improve flow<sup>[2]</sup>:

- Create well-defined team interaction patterns
- Use independent,stream-aligned teams<sup>[1]</sup>
- Build the thinnest viable platform (TVP)

## 团队的拆分
按照康威定律，团队的切分与组织的沟通模式会决定你的系统架构

## 好的 API
好的 API 是团队间的好的沟通模式，如果没有可能造成`谷仓效应`。 怎么定义好的 API：

- OPENAPI 定义 API
- 使用文档
- 好的用户体验
- 版本
- 最佳实践和使用规范
- Work Info （未来的路线和 bug 修复时间）

把其他团队当成顾客。


## 参考
[1] Organizing Agile Teams and ARTs: Team Topologies at Scale Overview

[2] Matthew Skelton and Manuel Pais: Forget monoliths vs. microservices. Cognitive load is what matters

[3] Justin Kitagawa: Platforms at Twilio: Unlocking Developer Effectiveness

[4] 阿贝好威： Team Topologies - 團隊優先思考模式
