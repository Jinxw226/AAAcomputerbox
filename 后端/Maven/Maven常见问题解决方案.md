- 产生原因：由于网络原因，依赖没有下载完整导致的，在maven仓库中生成了xxx.lastUpdated 文件，该文件不删除，不会重新下载
- 解决方案：
	1. 根据maven依赖的坐标，找到仓库中对应的xxx.lastUpdated文件，删除，删除之后重新加载项目即可
	2. 通过命令*（del /s .lastUpdated）批量递归删除指定目录下的xxx.lastUpdated文件，删除之后重新加载项目即可*

> [!NOTE] 注意！！！
> 重新加载依赖，依赖下载了之后，maven面板可能还会报红，此时可以关闭IDEA，重新打开IDEA加载此项目即可

![[Maven常见问题.png]]