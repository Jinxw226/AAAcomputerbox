# 利用脚手架创建Vue项目

创建一个工程化的Vue项目，执行命令：`npm create vue@3.3.4

![[vue项目创建.png]]**详细步骤说明：**
- `Project name：`------------------》项目名称，默认值：vue-project，可输入想要的项目名称。
- `Add TypeScript?` ----------------》是否加入TypeScript组件？默认值：No。
- `Add JSX Support?` --------------》是否加入JSX支持？默认值：No。
- `Add Vue Router...`--------------》是否为单页应用程序开发添加Vue Router路由管理组件？默认值：No。
- `Add Pinia ...`----------------------》是否添加Pinia组件来进行状态管理？默认值：No。
- `Add Vitest ...`---------------------》是否添加Vitest来进行单元测试？默认值：No。
- `Add an End-to-End ...`-----------》是否添加端到端测试？默认值No。
- `Add ESLint for code quality?` ---》是否添加ESLint来进行代码质量检查？默认值：No。

**提示：**执行上述指令，将会安装并执行 create-vue，它是 Vue 官方的项目脚手架工具

项目创建完成以后，进入`vue-project01` 项目目录，执行命令安装当前项目的依赖：`npm install`
![[npminstall.png]]创建项目以及安装依赖的过程，都是需要联网的。【如果网络不太好，可能会造成依赖下载不完整报错，继续再次执行 命令安装。】

这是我们创建的第一个项目结构，接下来呢，我们来介绍一下这个项目的结构。如图所示：
![[vue项目结构.png]]在上述的目录中，我们以后操作的最多的目录，就是src目录，因为我们需要在这个目录下来编写前端代码。

# 启动项目
- **方式一：命令行**
启动项目，我们可以在命令行中执行命令：`npm run dev`，就可以启动Vue项目了。
- **方式二：Vscode图形化界面**
点击NPM脚本中的dev后的运行按钮，就可以启动项目。
![[vscode启动vue项目.png]]

# Vue项目开发流程
![[Vue项目开发流程.png]]其中`*.vue`是Vue项目中的组件文件，在Vue项目中也称为单文件组件（[SFC](https://cn.vuejs.org/guide/scaling-up/sfc.html)，Single-File Components）。Vue 的单文件组件会将一个组件的逻辑 (JS)，模板 (HTML) 和样式 (CSS) 封装在同一个文件里（`*.vue`）
![[Pasted image 20250726163347.png]]