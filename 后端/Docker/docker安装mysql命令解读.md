#命令解读

```PowerShell
docker run -d \
  --name mysql \
  -p 3307:3306 \
  -e TZ=Asia/Shanghai \
  -e MYSQL_ROOT_PASSWORD=123 \
  mysql:8
```

> **解读：**
> 
> - `docker run -d` ：创建并运行一个容器，`-d`则是让容器以后台进程运行
> - `--name mysql` : 给容器起个名字叫`mysql`，你可以叫别的
> - `-p 3307:3306` : 设置端口映射。
>     - **容器是隔离环境**，外界不可访问。但是可以**将宿主机端口映射容器内到端口**，当访问宿主机指定端口时，就是在访问容器内的端口了。
>     - 容器内端口往往是由容器内的进程决定，例如MySQL进程默认端口是3306，因此容器内端口一定是3306；而宿主机端口则可以任意指定，一般与容器内保持一致。
>     - 格式： `-p 宿主机端口:容器内端口`，示例中就是将宿主机的3307映射到容器内的3306端口
> - `-``e` `TZ=Asia/Shanghai` : 配置容器内进程运行时的一些参数
>     - 格式：`-e KEY=VALUE`，KEY和VALUE都由容器内进程决定
>     - 案例中，`TZ=Asia/Shanghai`是设置时区；`MYSQL_ROOT_PASSWORD=123`是设置MySQL默认密码
> - `mysql:8` : 设置**镜像**名称，Docker会根据这个名字搜索并下载镜像
>     - 格式：`REPOSITORY:TAG`，例如`mysql:8.0`，其中`REPOSITORY`可以理解为镜像名，`TAG`是版本号
>     - 在未指定`TAG`的情况下，默认是最新版本，也就是`mysql:latest`

镜像的名称不是随意的，而是要到DockerRegistry中寻找，镜像运行时的配置也不是随意的，要参考镜像的帮助文档，这些在DockerHub网站或者软件的官方网站中都能找到。

如果我们要安装其它软件，也可以到DockerRegistry中寻找对应的镜像名称和版本，阅读相关配置即可。