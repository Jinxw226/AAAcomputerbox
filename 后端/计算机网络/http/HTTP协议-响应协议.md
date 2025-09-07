#http响应协议 #响应状态码 
![[http响应协议.png]]
- 响应行(以上图中红色部分)：响应数据的第一行。响应行由`协议及版本`、`响应状态码`、`状态码描述`组成
    - 协议/版本：HTTP/1.1
    - 响应状态码：200
    - 状态码描述：OK
- 响应头(以上图中黄色部分)：响应数据的第二行开始。格式为key：value形式
    - http是个无状态的协议，所以可以在请求头和响应头中设置一些信息和想要执行的动作，这样，对方在收到信息后，就可以知道你是谁，你想干什么
    - 常见的HTTP响应头有:
    ```Java
    Content-Type：表示该响应内容的类型，例如text/html，image/jpeg ；
    Content-Length：表示该响应内容的长度（字节数）；
    Content-Encoding：表示该响应压缩算法，例如gzip ；
    Cache-Control：指示客户端应如何缓存，例如max-age=300表示可以最多缓存300秒 ;
    Set-Cookie: 告诉浏览器为当前页面所在的域设置cookie ;
    ```
- 响应体(以上图中绿色部分)： 响应数据的最后一部分。存储响应的数据
    - 响应体和响应头之间有一个==空行隔开==（作用：用于标记响应头结束）

## 响应状态码
![[响应状态码.png]]
- 常见的响应状态码
![[常见的响应状态码.png]]
- 状态码大全：https://cloud.tencent.com/developer/chapter/13553

### 响应数据设置
- 方式一：HttpServletResponse 响应数据
```java
@RequestMapping("/response")  
public void Response(HttpServletResponse response) throws IOException {  
    //1.设置响应状态码，通常来说不用设定  
    response.setStatus(401);  
    //2.设置响应头  
    response.setHeader("name","itjf");  
    //3.设置响应体  
    response.getWriter().write("<h1>hello response</h1>");  
}
```
- 方式二：ResponseEntity 响应数据 Spring中提供的方式
```java
@RequestMapping("/response2")  
public ResponseEntity<String> response2() {  
    return ResponseEntity.status(401).header("name","javaweb-ai").body("<h1>hello response2</h1>");  
}
```


> [!NOTE] 注意！
> 响应状态码 和响应头如果没有特殊要求的话，通常不手动是设定，服务器会根据请求处理的逻辑，自动设置状态码和请求头
