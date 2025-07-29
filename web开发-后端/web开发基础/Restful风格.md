#Restful风格
![[Restful风格.png]]
后端开发人员：必须严格遵守提供的接口文档进行后端功能开发（保障开发的功能可以和前端对接）
而在前后端进行交互的时候，我们需要基于当前主流的REST风格的API接口进行交互。

- REST（Representational State Transfer），表述性状态转换，它是一种软件架构风格。
![[传统url风格和restful风格.png]]**注意事项：**
- REST是风格，是约定方式，约定不是规定，可以打破
- 描述模块的功能通常使用复数，也就是加s的格式来描述，表示此类资源，而非单个资源。如：users、emps、books…

Rest风格的四种请求方式：
- GET 查询
- POST 新增
- PUT 修改
- DELETE 删除