资源管理器

+ Redo Log
+ Undo Log

# 可串行化调度

```
START TRANSACTION;
UPDATE account SET balance = balance + 100.00 WHERE name = 'Tom'

```

# 四大属性

+ Atomicity：原子性
+ Consistency：一致性
+ Isolation：隔离性。多个事务在并发执行过程中得到的结果，和串行执行的结果一致。
+ Durability：持久性


# 写读冲突

## 脏读（Dirty Read）

+ 事务A，小明给账户存款100元
+ 事务B，小明查询小明存款

在提交之前，另一个事务读存款？100还是200？

如果读到200，又回滚了，就是脏读。

> 隔离级别：Read Uncommitted（读未提交）


> 解决方法：Read Committed隔离级别（读已提交状态）
## 不可重复读（Non-repeatable Read）

在一个事务两次读之间，另一个事务写了。

> 读要上锁

> 解决方法：Repetable Read 隔离级别

## 幻读（Repeatable Read）

现在可重复读了，但是存在幻读。

在一个事务内，两次读取同一个范围的数据，第二次读取的结果包含了第一次未出现的新数据行。这通常发生在一个事务读取某个数据范围后，另一个事务插入了新的数据行，当第一个事务再次读取相同范围时，发现了这些“幻影”数据行。

查询时，被插入新的记录

> 解决方法：Serializable 隔离级别
# 写写冲突

## 脏写

更新时，谁在后面执行，就成了谁的值。
![](assets/Pasted%20image%2020241016083917.png)

# 隔离性（Isolation）

+ 串行调度
+ 可串行化调度

# 串行调度

给定一个并发调度S，存在一个串行调度S'.在任何数据库状态下，按照调度S和调度S'执行后的结果都是相同的。

此时调度S 被称之为可串行化调度（serializable schedule）

![](assets/Pasted%20image%2020241016085359.png)


## 冲突可串行化调度

定义：冲突可串行化调度，是从冲突的角度出发，针对一个调度S 去发现其等价的串行调度S’ 来确定S 是一个可串行化调度。 

+ 一次操作交换定义为交换事务调度序列中相邻的两个操作，一个交换操作可以将一个调度A变成另外 一个调度B。
+ 当交换不会影响两个调度的一致性时，定义该交换得到的两个调度是等价的，该交换为等价交换。 
+ 等价操作 
	+ 交换连续两个相同数据读取操作的顺序:RT1(A) RT2(A) 
	+ 交换连续两个不同数据读写操作的顺序:RT1(A) WT2(B)；WT1(A) RT2(B)；WT1(A) WT2(B) 
+ 非等价操作 – 交换连续两个相同数据的读写、写写操作: RT1(A) WT2(A)；WT1(A) RT2(A)；WT1(A) WT2(A)

## 冲突可串行化调度的验证

![](assets/Pasted%20image%2020241016085814.png)

# 数据库原子性和持久性实现及故障恢复

## 原子性
两种策略
+ 事务运行期间不刷盘，故障系统重启后自动保证原子性
+ 事务运行期间刷盘，故障系统重启需回滚该事务
## 持久性
+ 事务完成时刷盘，故障系统重启后自动保持持久性
+ 事务完成时不刷盘，故障系统重启后需重做该事务

![](assets/Pasted%20image%2020241016090941.png)

![](assets/Pasted%20image%2020241016091312.png)

![](assets/Pasted%20image%2020241016091923.png)

![](assets/Pasted%20image%2020241016092014.png)

窃取内存占用小


日志内容顺序写入，保证了高效的写入速度。
数据库可以通过对日志的分析实现对 事务的回滚（原子性）或重做（持久性）

![](assets/Pasted%20image%2020241016092549.png)

Write Ahead Log
+ 逻辑日志：记录事务中的高层抽象逻辑操作
+ 物理日志：数据页面的

+ 幂等性
	+ 物理满足，逻辑不满足、
+ 失败可重做

Redo必须物理日志
Undo逻辑日志


# 影子拷贝方法

+ No-Steal/FORCE性质的算法
	+ 不要Redo/Undo
+ 事务修改在拷贝数据库上
+ 提交事务时，切换数据库指针

+ Steal/Force性质的算法
	+ 一直刷盘
+ 不需要Redo
+ 要Undo
	+ 事物执行中刷了


+ No-Steal 执行中不落盘
# 基于Undo的恢复

![](assets/Pasted%20image%2020241019143238.png)
## 基于Redo的恢复

![](assets/Pasted%20image%2020241019143124.png)


