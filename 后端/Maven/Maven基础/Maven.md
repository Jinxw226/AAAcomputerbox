#Maven 
Maven 是一款用于管理和构建Java项目的工具，是apache[^1]旗下的一个开源项目
		它基于项目对象模型POM（project object model）的概念，通过一小段描述信息来管理项目的构建
![[Maven.png]]
仓库：用于储存资源，管理各种jar[^2]包
- 本地仓库：自己计算机上的一个目录
- 中央仓库：由Maven团队维护的全球唯一的   仓库地址：[Central Repository:](https://repo1.maven.org/maven2/)
- 远程仓库（私服）：一般由公司团队搭建的私有仓库
	![[maven仓库.png]]
Maven官网：[Welcome to Apache Maven – Maven](https://maven.apache.org/)
Maven的作用：
- 依赖管理：方便快捷的管理项目依赖的资源（jar）
			在maven项目中的 pom.xml 文件中配置下面代码（仅示例）
```xml
<dependencies>  
    <dependency>        
	    <groupId>commons-io</groupId>  
        <artifactId>commons-io</artifactId>  
        <version>2.16.1</version>  
    </dependency>
</dependencies>
```

- 项目构建：标准化的跨平台（Linux、 Windows、 MacOs）的自动化项目构架方式
	编译 compile        测试 test        打包 package         发布  deploy

- 统一项目结构：提供标准、统一的项目结构    
	java文件下存放的是java文件  resources文件下存放的是相关的配置文件
![[基于Maven统一的项目结构.png]]

[^1]: Apache 软件基金会，成立于 1999 年 7 月，是目前世界上最大的最受欢迎的开源软件基金会，也是一个专门为支持开源项目而生的非营利性组织。
	开源项目: [Welcome to The Apache Software Foundation](https://apache.org/index.html#projects-list)

[^2]: jar: Java ARchive, Java归档 是一种与平台无关的文件格式 它允许将多个文件合并成一个单一的文件 通常用于封装Java类和相关资源
