
# WebSocket

An application protocol that provides *full-dulplex* communications between two peers over the *TCP protocol*

In a WebSocket application, the server publishes a WebSocket **endpoint**, and the client uses the endpoint URI to 

+ The Client initiates the handshake by sending a request to a WebSocket endpoint using its URI
# Java EE / Jakarata EE 方式

> 整合进SpringBoot [Springboot整合websocket(附详细案例代码)_springboot websocket-CSDN博客](https://blog.csdn.net/weixin_46425661/article/details/141897511)

`import jakarta.websocket.server.ServerEndpoint;`

`@ServerEndpoint` 注解来创建一个WebSocket服务器端点

```
GET /path/to/websocket/endpoint HTTP/1.1
```

```java
@ServerEndpoint("/echo")
public class EchoEndpoint {
 @OnMessage
 public void onMessage(Session session, String msg) {
   try {
     session.getBasicRemote().sendText(msg); 
   } catch (IOException e) { ... }
 } 
}
```

![](assets/Pasted%20image%2020240930142632.png)


```java
@ServerEndpoint("/receive")
public class ReceiveEndpoint {
 @OnMessage
 public void textMessage(Session session, String msg) 
 { System.out.println("Text message: " + msg); } 

 @OnMessage
 public void binaryMessage(Session session, ByteBuffer msg) 
 { System.out.println("Binary message: " + msg.toString()); } 

 @OnMessage
 public void pongMessage(Session session, PongMessage msg) 
 { 
    System.out.println("Pong message: " +   
              msg.getApplicationData().toString()); 
 } 
}
```

股票广播推送
+ EndPoint
+ Listener
+ ReportBean
```java
@ServerEndpoint("/dukeetf")
public class ETFEndpoint {
    private static final Logger logger =
                          Logger.getLogger("ETFEndpoint");
    static Queue<Session> queue = new ConcurrentLinkedQueue<>();
    
    public static void send(double price, int volume) {
        String msg = String.format("%.2f, %d", price, volume);
        try {
            for (Session session : queue) {
                //循环播送
                session.getBasicRemote().sendText(msg);
                logger.log(Level.INFO, "Sent: {0}", msg);
            }
        } catch (IOException e) {
            logger.log(Level.INFO, e.toString());
        }
    }
```

```java
@WebListener
public class ETFListener implements ServletContextListener {	
	private Timer timer = null;

	public void contextInitialized(ServletContextEvent event) {
		timer = new Timer(true);
		event.getServletContext().log("The Timer is started");
		timer.schedule(new ReportBean(event.getServletContext()), 0, 1000);
		event.getServletContext().log("The task is added");
	}	
}
```

在HTTP握手时获取Session

```java
@Configuration public class GetHttpSessionConfig extends ServerEndpointConfig.Configurator { /** * 注意: 每一个客户端发起握手,端点就有一个新的实列，那么引用的这个配置也是新的实列，这里sec的用户属性也不同就不会产生冲突。 * 修改握手机制 就是第一次http发送过来的握手 * @param sec 服务器websocket端点的配置 * @param request * @param response */ @Override public void modifyHandshake(ServerEndpointConfig sec, HandshakeRequest request, HandshakeResponse response) {
```

确保端点被注册！

```java
import org.springframework.context.annotation.Bean; import org.springframework.context.annotation.Configuration; import org.springframework.web.socket.server.standard.ServerEndpointExporter; /** * WebSocketConfig类的主要功能是配置和管理WebSocket端点， * 确保它们在应用程序启动时被正确初始化和注册，以便能够处理WebSocket连接和通信。 * * @author qf * @since 2024/08/29 20:02 */ @Configuration public class WebSocketConfig { /** * 该方法用来创建并返回一个ServerEndpointExporter实例。 * 这个实例的作用是扫描并自动配置所有使用@ServerEndpoint注解标记的WebSocket端点 * * @return ServerEndpointExporter：这是一个用于自动检测和管理WebSocket端点的类。 * 通过将其实例化并配置为Spring管理的Bean，可以确保所有WebSocket端点在应用程序启动时被自动初始化和注册。 */ @Bean public ServerEndpointExporter serverEndpointExporter(){ return new ServerEndpointExporter(); } }
```

然后创建EndPoint与上述说法相同



# Serialize
为 ServerEndpoint 指定 Encoder

还可以指定Decoder，要实现一个`willDecode`方法。

```java
public class MessageATextEncoder implements Encoder.Text<MessageA> {
 @Override
 public void init(EndpointConfig ec) { }

 @Override
 public void destroy() { }

 @Override
 public String encode(MessageA msgA) throws EncodeException {
   // Access msgA's properties and convert to JSON text... 
   return msgAJsonString; 
 } 
}
```


订阅机制，广播推送

# SpringBoot 方法

[Getting Started | Using WebSocket to build an interactive web application (spring.io)](https://spring.io/guides/gs/messaging-stomp-websocket)

[Overview STOMP (Simple Text Oriented Messaging Protocol):: Spring Framework](https://docs.spring.io/spring-framework/reference/web/websocket/stomp/overview.html)

•In Spring’s approach to working with STOMP messaging, STOMP messages can be routed to [@Controller](https://docs.spring.io/spring/docs/current/javadoc-api/org/springframework/stereotype/Controller.html) classes.

Login高优先级。

