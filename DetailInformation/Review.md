# Review
所谓Review，就是在头脑中对过去所做的事情重新“过”一遍。它通过对过去的思维和行为进行回顾、反思和探究，实现能力的提升。

对于一个固定的项目或一段特定的时间，都可以进行Review

- 项目（事情）预期的目标是什么
- 现状如何
- 执行过程分析
- 决定是如何做出的，有没有其他可能
- 相比之前，有做出什么改变，基于什么做出的改变，改变是否能达成正面影响

# 1、聚元好车
- 预期：搭建普通的二手车App
- 现状：达到期望值
- 过程分析：

  1. 页面搭建的时候确定整体架构，需求改变时临时更改架构.
  2. 精细界面使用代码搭建，简易界面使用xib实现，在保证代码易更改的同时加快开发速度
  3. 使用RAC进行解耦，达到预期效果
  4. 对于可复用的代码块，向其中加入太多方法之后，变得冗余，后期已提出到Pod中，分类分区分块进行使用。
  6. 使用BugTag来进行UI界面分析，加速UI细节调试
  7. 使用UIDebuggingInformationOverlay进行UI分析，暂未达成明显效果

- 改善可能：

  1. 构建APP架构的时候记录当前构建，并在需要时候进行迭代，便于后期优化。
  2. 自动化测试可以进行尝试

# 2、一次谈话
- 缺陷型：社会性差，正面表达自己的不满，提出的问题自己没有解决方法
- 优化方案：
  1. 提出问题的时候拿出至少一个解决方法
  
  2. 不正面表达不满
  
  3. 同事交流多文档，少口头直接交流  
