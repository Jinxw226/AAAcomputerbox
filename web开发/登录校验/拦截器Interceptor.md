#拦截器 #Interceptor #nterceptor #登录校验 
- 概念：是一种动态拦截方法调用的机制，类似于过滤器。
- 拦截器是Spring框架中提供的，用来动态拦截控制器方法的执行。
- 拦截器的作用：拦截请求，在指定方法调用前后，根据业务需要执行预先设定的代码。

![[拦截器Interceptor.png]]

下面我们通过快速入门程序，来学习下拦截器的基本使用。拦截器的使用步骤和过滤器类似，也分为两步：
1. 定义拦截器
	1. preHandle
	2. postHandle
	3. afterCompletion
2. 注册配置拦截器

**1). 自定义拦截器**

实现HandlerInterceptor接口，并重写其所有方法

```Java
//自定义拦截器
@Component
public class DemoInterceptor implements HandlerInterceptor {
    //目标资源方法执行前执行。 返回true：放行    返回false：不放行
    @Override
    public boolean preHandle(HttpServletRequest request, HttpServletResponse response, Object handler) throws Exception {
        System.out.println("preHandle .... ");
        
        return true; //true表示放行
    }

    //目标资源方法执行后执行
    @Override
    public void postHandle(HttpServletRequest request, HttpServletResponse response, Object handler, ModelAndView modelAndView) throws Exception {
        System.out.println("postHandle ... ");
    }

    //视图渲染完毕后执行，最后执行
    @Override
    public void afterCompletion(HttpServletRequest request, HttpServletResponse response, Object handler, Exception ex) throws Exception {
        System.out.println("afterCompletion .... ");
    }
}
```

注意：

- preHandle方法：目标资源方法执行前执行。 返回true：放行 返回false：不放行
- postHandle方法：目标资源方法执行后执行
- afterCompletion方法：视图渲染完毕后执行，最后执行
  
**2). 注册配置拦截器**

在 `com.itheima`下创建一个包，然后创建一个配置类 `WebConfig`， 实现 `WebMvcConfigurer` 接口，并重写 `addInterceptors` 方法

```Java
@Configuration  
public class WebConfig implements WebMvcConfigurer {

    //自定义的拦截器对象
    @Autowired
    private DemoInterceptor demoInterceptor;

    
    @Override
    public void addInterceptors(InterceptorRegistry registry) {
       //注册自定义拦截器对象
        registry.addInterceptor(demoInterceptor).addPathPatterns("/**");//设置拦截器拦截的请求路径（ /** 表示拦截所有请求）
    }
}
```

# 拦截器-拦截路径

首先我们先来看拦截器的拦截路径的配置，在注册配置拦截器的时候，我们要指定拦截器的拦截路径，通过`addPathPatterns("要拦截路径")`方法，就可以指定要拦截哪些资源。

在入门程序中我们配置的是`/**`，表示拦截所有资源，而在配置拦截器时，不仅可以指定要拦截哪些资源，还可以指定不拦截哪些资源，只需要调用`excludePathPatterns("不拦截路径")`方法，指定哪些资源不需要拦截。

```Java
@Configuration  
public class WebConfig implements WebMvcConfigurer {

    //拦截器对象
    @Autowired
    private DemoInterceptor demoInterceptor;

    @Override
    public void addInterceptors(InterceptorRegistry registry) {
        //注册自定义拦截器对象
        registry.addInterceptor(demoInterceptor)
                .addPathPatterns("/**")//设置拦截器拦截的请求路径（ /** 表示拦截所有请求）
                .excludePathPatterns("/login");//设置不拦截的请求路径
    }
}
```


在拦截器中除了可以设置`/**`拦截所有资源外，还有一些常见拦截路径设置：

|   |   |   |
|---|---|---|
|拦截路径|含义|举例|
|/*|一级路径|能匹配/depts，/emps，/login，不能匹配 /depts/1|
|/**|任意级路径|能匹配/depts，/depts/1，/depts/1/2|
|/depts/*|/depts下的一级路径|能匹配/depts/1，不能匹配/depts/1/2，/depts|
|/depts/**|/depts下的任意级路径|能匹配/depts，/depts/1，/depts/1/2，不能匹配/emps/1|

# 拦截器-执行流程
![[filter和interceptor执行流程.png]]