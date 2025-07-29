#nodejs安装 #nodejs
- Node.js 是一個開源的跨平台 JavaScript 執行環境，由 Linux 基金會的協作項目計劃促成。OpenJS 基金會是包括 Node.js 在內的重要開源 JavaScript 項目的首要家園。
- 下载链接：[下载 | Node.js 中文网](https://nodejs.cn/download/)
- 下载步骤：
1) . 双击msi文件，勾选我接受
![[nodejs安装第一步.png]]
2) 选择安装到一个，*没有中文，没有空格** 的目录下（新建一个文件夹NodeJS）
![[nodejs安装第二步.png]]
3) 点击 Next，下一步下一步的安装即可。
![[nodejs安装第三步.png]]
4) 验证NodeJS的环境变量
NodeJS 安装完毕后，会自动配置好环境变量，我们验证一下是否安装成功，通过： `node -v`
![[验证nodejs是否安装成功.png]]
5) 配置npm的全局安装路径
![[配置npm的全局安装路径.png]]
使用 **管理员身份** 运行命令行，在命令行中，执行如下指令：

```Java
npm config set prefix "D:\develop\NodeJS"
```
**注意：D:\develop\NodeJS  这个目录是NodeJS的安装目录 !!!!!**
**注意：D:\develop\NodeJS  这个目录是NodeJS的安装目录 !!!!!**
**注意：D:\develop\NodeJS  这个目录是NodeJS的安装目录 !!!!!**

6) . 切换为淘宝镜像，加速下载：

```Java
npm config set registry https://registry.npmmirror.com
```
