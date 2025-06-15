#安装Maven
安装步骤：
1. 解压 apache-maven-3.9.9-bin.zip
2. 配置本地仓库:修改 conf/settings.xml 中的  localRepository  为一个指定目录。
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
4. 配置环境变量:MAVEN_HOME 为maven的解压目录，并将其bin目录加入PATH环境变量