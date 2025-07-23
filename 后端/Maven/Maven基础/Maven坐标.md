#Maven坐标 
- Maven中的坐标是资源（jar）的唯一标识，通过该坐标可以唯一定位资源位置
- 使用坐标来 ==定义项目== 或 ==引入项目中需要的依赖==

Maven坐标的主要组成：
- groupId：定义当前Maven项目隶属组织名称（通常是域名反写，如：com.baidu   com.jigdong ）
- artifactId：定义当前Maven项目的名称（通常是模块名称，如： order-service、 goods-service）
- version：定义当前项目版本号
	- SNAPSHOT：功能不稳定，尚处于开发中的版本，即快照版本
	- RELEASE：功能趋于稳定，当前更新停止，可以用于发行的版本
 	