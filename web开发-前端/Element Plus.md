#ElementPlus 
- Element：是饿了么公司前端开发团队提供的一套基于 Vue3 的网站组件库，用于快速构建网页。
- Element 提供了很多组件（组成网页的部件）供我们使用。例如 超链接、按钮、图片、表格等等。
- 官方网站：[一个 Vue 3 UI 框架 | Element Plus](https://element-plus.org/zh-CN/)

# 快速入门
1) .创建vue项目
2) 参照官方文档安装Element Plus组件库（在当前工程的目录下）：
	`npm install element-plus --save`
3) main.js中进入Element Plus组件库（参照官方文档）以下为完整导入
```js
import { createApp } from 'vue'
import ElementPlus from 'element-plus'
import 'element-plus/dist/index.css'
import App from './App.vue'

const app = createApp(App)

app.use(ElementPlus)
app.mount('#app')
```
- 制作组件：访问官方文档，复制组件代码，调整