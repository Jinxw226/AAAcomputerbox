#http请求协议
GET方式请求协议：
![[GET方式请求协议.png]]
POST方式请求协议：
![[POST方式请求协议.png]]
- 请求行（与请求头之间空一行）：HTTP请求中的第一行数据。由：`请求方式`、`资源路径`、`协议/版本`组成（之间使用空格分隔）
	- 请求方式：GET
	- 资源路径：如图
	- 协议/版本：HTTP/1.1
- 请求头：key: value 的形式
![[常见的http请求头.png]]
- 请求体：存储请求参数
通过tomcat web服务器封装的请求头不必直接对协议进行操作，可以通过程序进行解析，让web开发更加便捷
```java
@RestController  //构建web服务的注解
public class RequestController {  
    @RequestMapping("/request")  
    public String request(HttpServletRequest request){  
        //1.获取请求方式  
        String method = request.getMethod();  
        System.out.println("请求方式:" + method);  
        //2.获取请求url地址  
        String url = request.getRequestURL().toString();
        //http://127.0.0.1:8080/request  
        System.out.println("请求地址:" + url);  
        String uri = request.getRequestURI();// /request  
        System.out.println("请求地址:" + uri);  
        //3.获取请求协议  
        String protocol = request.getProtocol();//HTTP/1.1  
        System.out.println("请求协议:" + protocol);  
        //4.获取请求参数 - name,age        
        String name = request.getParameter("name");  
        String age = request.getParameter("age");  
        System.out.println("name: " + name + " age: " + age);  
        //5.请求头  
        String accept = request.getHeader("Accept");  
        System.out.println("请求头:" + accept);  
        return "OK";  
    }  
}
```