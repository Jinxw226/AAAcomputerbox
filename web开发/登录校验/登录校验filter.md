#登录校验filter

**令牌校验Filter**

1. 所有的请求，拦截到了之后，都需要校验令牌吗 ？
    1. 答案：**登录请求例外**
2. 拦截到请求后，什么情况下才可以放行，执行业务操作 ？
    1. 答案：**有令牌，且令牌校验通过(合法)；否则都返回未登录错误结果**

![[filter登录令牌校验流程.png]]
基于上面的业务流程，我们分析出具体的操作步骤：
1. 获取请求url
2. 判断请求url中是否包含login，如果包含，说明是登录操作，放行
3. 获取请求头中的令牌（token）
4. 判断令牌是否存在，如果不存在，响应 401
5. 解析token，如果解析失败，响应 401
6. 放行

代码实现：
```java
package com.itjf.filter;  
  
import com.itjf.utils.JwtUtils;  
import jakarta.servlet.*;  
import jakarta.servlet.annotation.WebFilter;  
import jakarta.servlet.http.HttpServletRequest;  
import jakarta.servlet.http.HttpServletResponse;  
import lombok.extern.slf4j.Slf4j;  
  
import java.io.IOException;  
  
@Slf4j  
@WebFilter(urlPatterns = "/*")  
public class TokenFilter implements Filter {  
    @Override  
    public void doFilter(ServletRequest servletRequest, ServletResponse servletResponse, FilterChain filterChain) throws IOException, ServletException {  
        HttpServletRequest request = (HttpServletRequest) servletRequest;  
        HttpServletResponse response = (HttpServletResponse) servletResponse;  
        //1. 获取请求路径  
        String requestURI = request.getRequestURI(); // /login  
        //2. 判断请求路径是否是登录请求，如果包含/login。说明是登录操作，放行  
        if(requestURI.contains("/login")){  
            log.info("登录操作,放行");  
            filterChain.doFilter(request,response);  
            return;  
        }  
        //3.获取请求头中的token  
        String token = request.getHeader("token");  
        //4.判断token是否存在，如果不存在，说明用户没有登录，返回错误信息401状态码  
        if(token == null || token.isEmpty()){  
            log.info("令牌为空,用户未登录，请先登录");  
            response.setStatus(401);  
            return;  
        }  
        //5.如果存在，调用jwt工具类进行解析，如果解析失败，返回错误信息401状态码  
        try{  
            JwtUtils.parseToken(token);  
        }catch (Exception e){  
            log.info("令牌非法，响应401");  
            response.setStatus(401);  
            return;  
        }  
        //6.如果解析成功，说明登录成功，返回登录成功信息200状态码  
        log.info("令牌合法，放行");  
        filterChain.doFilter(request,response);  
    }  
}
```