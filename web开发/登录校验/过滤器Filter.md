#filter #登录校验 #Filter #过滤器
- 概念：Filter表示过滤器，是 JavaWeb三大组件(Servlet、Filter、Listener)之一。
- 过滤器可以把对资源的请求拦截下来，从而实现一些特殊的功能
    - 使用了过滤器之后，要想访问web服务器上的资源，必须先经过滤器，过滤器处理完毕之后，才可以访问对应的资源。
- 过滤器一般完成一些通用的操作，比如：登录校验、统一编码处理、敏感字符处理等。


# Filter快速入门

下面我们通过Filter快速入门程序掌握过滤器的基本使用操作：

- 第1步，定义过滤器 ：1.定义一个类，实现 Filter 接口，并重写其所有方法。
- 第2步，配置过滤器：Filter类上加 @WebFilter 注解，配置拦截资源的路径。引导类上加 @ServletComponentScan 开启Servlet组件支持。

```java
package com.itjf.filter;  
  
import jakarta.servlet.*;  
import jakarta.servlet.annotation.WebFilter;  
import lombok.extern.slf4j.Slf4j;  
  
import java.io.IOException;  
  
@Slf4j  
@WebFilter(urlPatterns = "/*")// 拦截所有请求  
public class DemoFilter implements Filter {  
  
    // 初始化方法，会在web服务器启动的时候执行，只执行一次  
    @Override  
    public void init(FilterConfig filterConfig) throws ServletException {  
        log.info("init 初始化过滤器方法");  
    }  
  
    //拦截到请求之后执行，会执行多次  
    @Override  
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {  
        log.info("拦截到了请求");  
        // 放行  
        filterChain.doFilter(servletRequest, servletResponse);  
    }  
  
    // 销毁方法，会在web服务器关闭的时候执行，只执行一次  
    @Override  
    public void destroy() {  
        log.info("destroy 销毁方法");  
    }  
}
```

==注意上面的implement Filter一定要选择servlet包中的filter==

- init方法：过滤器的初始化方法。在web服务器启动的时候会自动的创建Filter过滤器对象，在创建过滤器对象的时候会自动调用init初始化方法，这个方法只会被调用一次。
- doFilter方法：这个方法是在每一次拦截到请求之后都会被调用，所以这个方法是会被调用多次的，每拦截到一次请求就会调用一次doFilter()方法。
- destroy方法： 是销毁的方法。当我们关闭服务器的时候，它会自动的调用销毁方法destroy，而这个销毁方法也只会被调用一次。

配置过滤器

在定义完Filter之后，Filter其实并不会生效，还需要完成Filter的配置，Filter的配置非常简单，只需要在Filter类上添加一个注解：`@WebFilter`，并指定属性`urlPatterns`，通过这个属性指定过滤器要拦截哪些请求

```Java
@WebFilter(urlPatterns = "/*") //配置过滤器要拦截的请求路径（ /* 表示拦截浏览器的所有请求 ）
public class DemoFilter implements Filter {
    //初始化方法, web服务器启动, 创建Filter实例时调用, 只调用一次
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("init ...");
    }

    //拦截到请求时,调用该方法,可以调用多次
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain chain) throws IOException, ServletException {
        System.out.println("拦截到了请求...");
    }

    //销毁方法, web服务器关闭时调用, 只调用一次
    public void destroy() {
        System.out.println("destroy ... ");
    }
}
```

当我们在Filter类上面加了@WebFilter注解之后，接下来我们还需要在启动类上面加上一个注解`@ServletComponentScan`，通过这个`@ServletComponentScan`注解来开启SpringBoot项目对于Servlet组件的支持。

```Java
@ServletComponentScan //开启对Servlet组件的支持
@SpringBootApplication
public class TliasManagementApplication {
    public static void main(String[] args) {
        SpringApplication.run(TliasManagementApplication.class, args);
    }
}
```

> [!NOTE]
> **注意事项：**在过滤器Filter中，如果不执行放行操作，将无法访问后面的资源。 放行操作：`chain.doFilter(request, response);`


# Filter执行流程

![[Filter执行流程.png]]测试代码：

```Java
@WebFilter(urlPatterns = "/*") 
public class DemoFilter implements Filter {
    
    @Override //初始化方法, 只调用一次
    public void init(FilterConfig filterConfig) throws ServletException {
        System.out.println("init 初始化方法执行了");
    }
    
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        
        System.out.println("DemoFilter   放行前逻辑.....");

        //放行请求
        filterChain.doFilter(servletRequest,servletResponse);

        System.out.println("DemoFilter   放行后逻辑.....");
        
    }

    @Override //销毁方法, 只调用一次
    public void destroy() {
        System.out.println("destroy 销毁方法执行了");
    }
}
```

# Filter拦截路径

执行流程我们搞清楚之后，接下来再来介绍一下过滤器的拦截路径，Filter可以根据需求，配置不同的拦截资源路径：

|   |   |   |
|---|---|---|
|拦截路径|urlPatterns值|含义|
|拦截具体路径|/login|只有访问 /login 路径时，才会被拦截|
|目录拦截|/emps/*|访问/emps下的所有资源，都会被拦截|
|拦截所有|/*|访问所有资源，都会被拦截|

下面我们来测试"拦截具体路径"：

```Java
@WebFilter(urlPatterns = "/login")  //拦截/login具体路径
public class DemoFilter implements Filter {
    @Override
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {
        System.out.println("DemoFilter   放行前逻辑.....");

        //放行请求
        filterChain.doFilter(servletRequest,servletResponse);

        System.out.println("DemoFilter   放行后逻辑.....");
    }


    @Override
    public void init(FilterConfig filterConfig) throws ServletException {
        Filter.super.init(filterConfig);
    }

    @Override
    public void destroy() {
        Filter.super.destroy();
    }
}
```

# Filter-过滤器链

- 介绍：过滤器链指的是在一个web应用程序当中，可以配置多个过滤器，多个过滤器就形成了一个过滤器链。
- 顺序：注解配置的Filter，优先级是按照过滤器类名（字符串）的自然排序。

![[Filter过滤器链.png]]

> [!NOTE]
> 过滤器链上过滤器的执行顺序：注解配置的Filter，优先级是按照过滤器类名（字符串）的自然排序。 比如：
> 
> - AbcFilter
> - DemoFilter
> 
> 这两个过滤器来说，AbcFilter 会先执行，DemoFilter会后执行。


