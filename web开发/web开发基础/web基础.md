#B/S架构 #C/S架构
- 静态资源：在服务器上存储的不会改变的数据，通常不会根据用户的请求而变化。如HTML、CSS、JS 以及图片、音频、视频等这些资源，我们都称为**静态资源**。
- 动态资源：在服务器端上存储的，会根据用户请求和其他数据动态生成的，内容可能会在每次请求时都发生变化。比如：Servlet、JSP等(负责逻辑处理)。而Servlet、JSP这些技术现在早都被企业淘汰了，现在在企业项目开发中，都是直接基于==[[Spring]]框架来构建动态资源==
- BS架构：Browser/Server，浏览器/服务器架构模式。客户端只需要浏览器，应用程序的逻辑和数据都存储在服务端。
    - 优点：维护方便
    - 缺点：体验一般
- CS架构：Client/Server，客户端/服务器架构模式。需要单独开发维护客户端。
    - 优点：体验不错
    - 缺点：开发维护麻烦
![[web基础.png]]