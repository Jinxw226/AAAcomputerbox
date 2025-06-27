#springboot #springboot配置文件
- SpringBoot项目提供了多种属性配置方式（properties、yaml、yml）
![[properties配置文件.png]]

`application.yaml` , `application.yml` 这两个配置文件的后缀名虽然不一样，但是里面配置的内容形式都是一模一样的。
我们可以来对比一下，采用 `application.properties` 和 `application.yml` 来配置同一段信息(数据库连接信息)，两者之间的配置对比：
![[properties对比配置.png]]![[yaml、yml配置文件.png]]

在项目开发中，我们==推荐使用application.yml配置文件==来配置信息，简洁、明了、以数据为中心。

## yml配置文件：
- 格式：
	- 大小写敏感
	- 数值前边必须有空格，作为分隔符
	- 使用缩进表示层级关系，缩进时，不允许使用tab键，只能用空格（idea中会自动将Tab转换为空格）
	- 缩进的空格数目不重要，只要相同层级的元素左侧对齐即可
	- ’#‘ 表示注释，从这个字符一直到行尾，都会被解析器忽略
### yml中常见的数据格式：
- 对象/Map集合
```YAML
user:
  name: zhangsan
  age: 18
  password: 123456
```
- 数组/List/Set集合
```YAML
hobby: 
  - java
  - game
  - sport
```

> [!NOTE]
> 在yml格式的配置文件中，如果配置项的值是以 0 开头的，值需要使用 '' 引起来，因为以0开头在yml中表示8进制的数据。