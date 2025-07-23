#filter #Interceptor #Filter和Interceptor区别

主要区别：

- **接口规范不同：过滤器需要实现Filter接口，而拦截器需要实现HandlerInterceptor接口。**
- **拦截范围不同：过滤器Filter会拦截所有的资源，而Interceptor只会拦截Spring环境中的资源。**