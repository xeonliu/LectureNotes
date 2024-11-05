# Micro Services

SQL有Query Plan，相当于抽象语法树，所以可以。
Redis根据缓存查询组，不大合理。

Self-Contained Appilications
可维护性和容错性更高

## With Spring Cloud

注册中心。WSDL等类似位置。

所有用户取注册中心去找所需的服务，然后去调用对应的微服务。

微服务把自己的信息告诉Service Registry

Gateway不说访问端口，说访问名字。问Registry。
Client代码可以不变。 
![](assets/Pasted%20image%2020241105102704.png)

Gateway还可以Load Balance

Service Discovery，Load-Balancing，Circuit Breaking， Distributed Tracing, and monitoring

独立数据库+消息队列

互相通信问题变大。

其实多服务可靠性要减小。

网关记录了名字和位置，位置是注册到注册中心上的

Spring中Eureka。

![](assets/Pasted%20image%2020241105104023.png)