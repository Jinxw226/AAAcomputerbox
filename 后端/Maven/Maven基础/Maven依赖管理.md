#依赖 
## 添加依赖
- 依赖：之当前项目运行所需要的jar包，一个项目中可以引入多个依赖
- 配置：
	1. 在pom.xml中编写`<dependencies>`标签
	2. 在`<dependencies>`标签中使用`<dependency>`引入坐标
	3. 定义坐标的 `groupId`、`artifactId`、`version`
	
```XML
<dependencies>
    <!-- 依赖 : spring-context -->
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>6.1.4</version>
    </dependency>
</dependencies>
```
4. 点击刷新按钮，引入最新加入的坐标   

注意事项：
1. 如果引入的依赖，在本地仓库中不存在，将会连接远程仓库 / 中央仓库，然后下载依赖（这个过程会比较耗时，耐心等待）
2. 如果不知道依赖的坐标信息，可以到 mvn 的中央仓库（[Maven Repository: Search/Browse/Explore](https://mvnrepository.com/)）中搜索

## 排除依赖
排除依赖：指主动断开依赖的资源，被排除的资源==无需指定版本==，配置完成后重新刷新
```xml
<!--排除依赖-->  
<exclusions>  
    <exclusion>        
	    <groupId>io.micrometer</groupId>  
        <artifactId>micrometer-observation</artifactId>  
    </exclusion>
</exclusions>
```