#安装Maven
安装步骤：
1. 解压 apache-maven-3.9.9-bin.zip
	1. bin目录：存放的是可执行命令（mvn命令重点关注）
	2. conf目录：存放Maven的配置文件（setting.xml配置文件后期需要修改）
	3. lib目录：存放Maven依赖的jar包（Maven也是使用java开发的，所以它也依赖其他的jar包）
2. 配置本地仓库:
	1. 在自己计算机上新一个目录（本地仓库，用来存储jar包）
	![[新建mvn_repo包.png]]
	2. 修改 conf/settings.xml 中的  localRepository  为一个指定目录。
	![[更改setting.xml文件中的localRepository.png]]
`<localRepository>D:\develop\apache-maven-3.9.9\mvn_repo</localRepository>`
3. 配置阿里云私服：修改 conf/settings.xml中的 mirrors 标签，为其添加如下子标签
```XML
<mirror>
    <id>alimaven</id>
    <name>aliyun maven</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
    <mirrorOf>central</mirrorOf>
</mirror>
```
注意配置的位置，在`<mirrors> ... </mirrors>`中间添加配置

4. 配置环境变量:
	1. MAVEN_HOME 为maven的解压目录，并将其bin目录加入PATH环境变量
	2. 在Path中进行配置。 PATH环境变量的值，设置为：%MAVEN_HOME%\bin
![[配置环境变量.png]]
![[配置maven环境变量.png]]


检查mvn是否安装成功：
命令为：**`mvn -v`**
![[检测maven是否安装成功.png]]