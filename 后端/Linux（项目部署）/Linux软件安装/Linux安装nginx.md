#Linux安装nginx #Linux 

Nginx的安装包，从官方下载下来的是c语言的源码包，我们需要自己编译安装。具体操作步骤如下：

1). 安装Nginx运行时需要的依赖

```Shell
yum install -y pcre pcre-devel zlib zlib-devel openssl openssl-devel
```

安装C语言的编译环境.

```Shell
yum install gcc-c++
```

2). 上传Nginx的源码包
![[Pasted image 20250809224859.png]]

3). 解压源码包到当前目录

```Shell
tar -zxvf nginx-1.20.2.tar.gz
```

4). 进入到解压目录后，执行指令

```Shell
#进入解压目录
cd nginx-1.20.2

#执行命令配置, 生成Makefile文件
./configure --prefix=/usr/local/nginx
```

5). 执行命令进行编译和安装

```Shell
#编译
make

#编译安装
make install
```

# 启动nginx

进入到nginx安装目录`/usr/local/nginx`，启动nginx服务

```Shell
cd /usr/local/nginx/
sbin/nginx
```

启动完毕之后，我们可以通过 `ps` 指令查询当前系统中的nginx进程，从而确认nginx是否启动 。
![[Pasted image 20250809230059.png]]

然后，我们就可以打开浏览器，访问服务器上的nginx 。
![[Pasted image 20250809230116.png]]

注意：如果无法访问，记得查看防火墙是否放开nginx80端口！！！