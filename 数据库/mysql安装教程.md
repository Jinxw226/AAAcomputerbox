#mysql安装教程
安装教程链接：
https://heuqqdmbyk.feishu.cn/wiki/ZRSFwACsRiBD2NkV7bmcrJhInme
- 安装步骤：
	- 第一步：官网下载安装包：[MySQL :: MySQL Downloads](https://www.mysql.com/cn/downloads/)
	- 第二步：环境配置
![[环境变量.png]]

```Java
mysql [-h数据库服务器的IP地址 -P端口号] -u用户名 -p密码 
```

`-p`直接输入密码具有不安全性
可以`mysql -u用户名 -p` 回车然后再继续输入密码
- h 参数不加，默认连接的是本地 127.0.0.1 的MySQL服务器
- P 参数不加，默认连接的端口号是 3306

> [!NOTE] 环境变量里面有很多选项，这里我们只用到`Path`这个参数。为什么在初始化的开始要添加环境变量呢？
> 
> 在黑框(即CMD)中输入一个可执行程序的名字，Windows会先在环境变量中的`Path`所指的路径中寻找一遍，如果找到了就直接执行，没找到就在当前工作目录找，如果还没找到，就报错。我们添加环境变量的目的就是能够在任意一个黑框直接调用MySQL中的相关程序而不用总是修改工作目录，大大简化了操作。