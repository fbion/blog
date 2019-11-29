---
title: "分解任务"
date: 2019-10-28T13:58:58+08:00
draft: true
categories:
- tech
---

这篇谈点虚的, 在接到一个大而抽象的任务的时候如何把它分解到一个个子任务, 进而合理得安排时间把工作完成.

多年前刚毕业工作的时候, 有一段时间总感觉自己思路特别混乱, 再加上那会性格也属于比较急躁的类型, 做事有点像没头苍蝇,
同一时间考虑得很多(性能, 扩展性, 可维护性, 个人洁癖...), 虽然从结果看, 那会每个项目最后做的评价都不错, 但自己并不满意:

- 花的时间太多(都能在 dead line 内完成, 但业余花了太多时间走弯路)
- 最后的成果达不到个人心中的高度

原因:

- 知识储备不够
- 对一个项目各部分的主次优先级分得不够

本文结合几个具体例子, 总结下最近几年自己对项目规划方面的思考. 在我的场景里, 主要考虑几个方面:

- resource (人手, 计算/存储资源的消耗)
- complexity  (实现的复杂度? 使用方的复杂度?)
- scalibility (是否有 scalable 的需求, scale out or up?)
- maintainability (monitoring, alerting, CI, CD...)

## data infrastructure 的建设

## 升级到 python3 

## 迁移到 kubernetes

## 集成 opentracing