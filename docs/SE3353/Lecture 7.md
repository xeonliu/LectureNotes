# Multithreading in Java

## How to start a thread?

> Provide a Runnable object

The Runnable interface defines a single method, run, meant to contain the code executed in the thread. The Runnable object is passed to the Thread constructor


```java
public class HelloRunnable implements Runnable {
	public void run() {
		System.out.println("Hello from a thread!");
	}

	public static void main(String args[]) {
		(new Thread(new HelloRunnable())).start()
	}
}
```

> Subclass Thread

Thread itself implements `Runnable`

```java
public class HelloThread extends Thread {
	public void run() {}
	public static void main(String args[]) {
		(new HelloThread()).start();
	}
}
```


# Memcached

数据库的Cache，无法使用。Cache SQL语句？

Memory Cache，和程序不在一个进程，不好使。

但是跨进程优于跨机器。
而且可以存各式各样的数据，不用老是Join啥的。


这个PPT文档的主题是企业应用架构中的内存缓存（Memory Caching），由上海交通大学的Haopeng Chen教授制作。文档主要介绍了内存缓存在提高动态Web应用性能、减轻数据库负载方面的作用，并详细讲解了两种流行的内存缓存系统：MemCached和Redis。

主要内容包括：

1. **MemCached**：
    
    - 介绍MemCached，一个高性能的分布式内存对象缓存系统，用于加速动态Web应用。
    - 安装MemCached的步骤，包括使用Homebrew和Lunchy。
    - MemCached的工作原理。
    - 在Spring Web应用中使用MemCached缓存数据的示例代码，包括`Book`类、`SimpleBookRepository`接口和实现、`AppRunner`组件以及`Se33537SpringcacheApplication`主程序。
    - MemCached的存储命令（如`set`、`add`、`replace`、`append`、`prepend`、`cas`）和检索命令（如`get`、`gets`、`delete`、`incr/decr`）。
    - MemCached的内存管理和数据分布。
2. **Redis**：
    
    - 介绍Redis，一个高级的键值存储系统，也被称为NoSQL数据库，支持多种数据结构如字符串、哈希、列表、集合和有序集合。
    - Redis的安装和基本操作命令。
    - Redis中的数据结构，包括字符串、列表、集合、哈希和有序集合。
    - 在Spring应用中使用Redis缓存数据的示例，包括配置文件`application.properties`和`PersonDaoImpl`的实现。
    - 使用Redis进行消息传递的示例，包括`MessagingRedisApplication`、`Receiver`类和`MsgController`控制器。

最后，文档还提供了一些有用的参考资料链接，包括MemCached和Redis的官方文档、安装指南、Spring Data Redis的文档和示例项目等。

整个PPT文档的目的是通过介绍内存缓存的概念和实践，使听众能够根据业务需求设计并实现基于分布式缓存的数据访问方案，以优化数据访问性能。


Data Access GateWay？




