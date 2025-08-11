#阿里云OSS秘钥配置

由于在开发的时候，我们将访问阿里云OSS的AccessKeyId，AccessKeySecret都配置在了系统的环境变量中了。那现在项目部署到了Linux服务器中，调用阿里云OSS进行文件上传时，程序就会获取Linux系统中的环境变量。所以此时，我们需要将AccessKeyId，AccessKeySecret配置为Linux系统的环境变量。

1). 查看Windows系统之前配置的环境变量

```YAML
echo %OSS_ACCESS_KEY_ID%
echo %OSS_ACCESS_KEY_SECRET%
```

我们将上述自己的 AccessKeyId 与 AccessKeySecret 复制出来，然后在linux系统中配置环境变量。

2). 执行如下指令：

```YAML
# 仅在当前会话中有效
export OSS_ACCESS_KEY_ID="密钥id"
export OSS_ACCESS_KEY_SECRET="密钥"
source /etc/profile
```

**注意!!!：**上述的绿色背景部分，是自己的阿里云OSS账号的 OSS_ACCESS_KEY_ID， OSS_ACCESS_KEY_SECRET，一个字符都不能错，在记事本中将命令组装好，然后再到命令行中执行。

执行完毕后，将finalShell的窗口关闭掉，重新打开一个新窗口（让环境变量生效），重新运行项目测试。