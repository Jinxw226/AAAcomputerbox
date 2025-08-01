#mysql安装教程
安装教程链接：
https://heuqqdmbyk.feishu.cn/wiki/ZRSFwACsRiBD2NkV7bmcrJhInme

> [!NOTE]
> 8.4以上版本的不需要my.ini文件

- 安装步骤：
	- 第一步：官网下载安装包：[MySQL :: MySQL Downloads](https://www.mysql.com/cn/downloads/)
	- 第二步：环境配置
	![[环境变量.png]]
	在`系统变量`**中新建`MYSQL_HOME`
	![[mysql_home.png]]
	在**`系统变量`**中找到并**双击`Path`
	![[mysql_path.png]]
	![[新建环境变量mysql.png]]
	如果提示`Can't connect to MySQL server on '``localhost``'`则证明添加成功；
	![[初始化.png]]
	如果提示`mysql不是内部或外部命令，也不是可运行的程序或批处理文件`则表示添加添加失败，请重新检查步骤并重试。
	- 第三步：初始化
		以管理员身份，运行命令行窗口：
	```SQL
	mysqld --initialize-insecure
	```
	稍微等待一会，如果出现没有出现报错信息，则证明data目录初始化没有问题，此时再查看MySQL目录下已经有data目录生成。
	tips：如果出现如下错误
	![[初始化过程出现如下错误.png]]
	是由于权限不足导致的，以管理员方式运行 cmd
	- 第四步：注册mysql服务
	```SQL
	mysqld -install
	```
	- 第五步：启动mysql服务
	```SQL
	net start mysql  // 启动mysql服务
	    
	net stop mysql  // 停止mysql服务
	```
	- 第六步：修改默认账户密码
	```SQL
	mysqladmin -u root password 1234
	```
	- 第七步：登录
	```SQL
	mysql -uroot -p1234
	```
	![[登录mysql.png]]
	- 其他：退出mysql
	```SQL
	exit
	```
	- 其他：卸载mysql
		1. 敲入`net stop mysql`，回车。
		2. 再敲入`mysqld -remove mysql`，回车。

  

3. 最后删除MySQL目录及相关的环境变量。

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