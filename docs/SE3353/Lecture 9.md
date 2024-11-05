# Web Service

## Simple Object Access Protocol（简单对象访问协议）

Web服务描述文件（WSDL文件）

`wsimport`命令行工具：这个工具的作用是读取Web服务描述语言（WSDL）文件，并生成相应的Java stubs（存根）和Java API，这些生成的代码可以用于创建Web服务的客户端。通过这些客户端代码，开发者可以像调用本地方法一样调用远程的Web服务。

WSDL，全称为Web Services Description Language（Web服务描述语言），是一种XML格式的文件，用于描述Web服务的功能、接口和绑定信息。WSDL为开发者提供了一种标准化的方式来发布和发现Web服务，以及定义Web服务的请求和响应消息格式。

JAX-WS（Java API for XML Web Services）是Java平台中用于构建和运行Web服务的API。它允许开发者使用Java语言来创建符合SOAP（Simple Object Access Protocol）和WSDL（Web Services Description Language）标准的Web服务。

# Rest

Representable State Transfer

+ Representable
	+ All data are resources. Representation for client
	+ Each resource can have different representations
	+ Each resource has its own 

Server is stateless
