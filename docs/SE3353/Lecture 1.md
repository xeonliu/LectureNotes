HTTP Session State

# 有状态服务

有状态要消耗资源
购物车有状态

ABC访问一个只能放两个的玩意？
```
A   访问A
A B 访问B
C B 访问C
C A 访问A
```
LRU，写入硬盘。Swap Out。
实例池的大小，默认500。
保证内存不崩，虽然Swap会使得速度变慢。

# 无状态服务
登录操作，前一次登录失败不影响。

# Spring Bean Scopes

`@Scope` Annotation

+ `singleton` 整个容器中只有一个
+ `prototype` 一个调用（invoke）产生一个新的对象
	+ Controller调用Service
+ `request`一个HTTP请求创建一个对象
+ `session`一个Session一个
+ `application`一个应用一个
+ `websocket`
![](assets/Pasted%20image%2020240923153055.png)
```java
@RestController
@Scope("prototype")
public class UserController {
	@Autowired
	UserService userService
	@Override
	
}

@Service
public class UserService {
	
}
```

Database Connection Pool Size

```
connections = ((core_count*2) // 线程数？
+ effective_spindle_count) //有效硬盘数
```

连接数与用户数无关

[数据库连接池数量配置公式_连接池的公式数据库-CSDN博客](https://blog.csdn.net/Receptive2WE/article/details/122421718)

`@Lookup`注解：当组合情况下，对象声明周期不同时，可以使用它从单例获取动态的东西

```java
@Component
public class SingletonBean {
    
    @Lookup
    protected SessionBean createSessionBean() {
        return null; // 实际的返回值由Spring处理
    }
    
    public void someMethod() {
        SessionBean sessionBean = createSessionBean();
        // 使用sessionBean
    }
}

```