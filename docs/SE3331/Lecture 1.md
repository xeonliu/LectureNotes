MIT
OS & 分布式

ICS ：Fork 系统调用
CSE：
OS：深度

Interactracting set odf components with a specified behavior at hte _interface_ with its _environment_

Linux 驱动 56%
2千万
车 一个亿，接近老鼠基因组

系统的14个属性

## Correctness

已知就是Feature

undefined behavior

```C
char* str;
char* str_end;
str + len > str_end
```

## Latency

很难优化，光速限制

## Throughput / Capacity

A Number of transactions
CPU越做越大，制程难以缩小

## Scalability

随Core增加Lock耗时变多
加人效率不一定增加

CPU通信开销增大

## Performance Isolation

其他进程侵占性能
Noisy Neighbor

## Utilization

数据中心CPU利用率不高
与Performance Isolation有冲突

## Energy Efficiently

精确控制前后台调度，控制功耗

## Compatibility

兼容性

Intel's Itanium, 64-bit, not compatible to x86, died.

## Usability

交互好不好用

## Consistency

数据库变化要观测到

## Fault Tolerance

系统容错性如何
Cosmic Radiation

DDR3，读取内存翻转

## Security

偷密钥

## Privacy

无痕浏览

# System Complexity

## Emergent Properties

突发的限制

Ethernet的载波监听冲突检测

- 同时发消息就取消
- 最小的包要满足一定大小来确保检测对方是否冲突
- 升级后，距离增加，导致需要padding

## Propagation of Effects

蝴蝶效应

呼叫转移（Call Forwarding）

CNDB隐藏电话（Call Number Delivery Blocking）

ACB自动回拨（Automatic Callback）

IB（列电话清单）

- 循环的呼叫转移？
- 隐藏电话的自动回拨，导致电话出现在清单上
