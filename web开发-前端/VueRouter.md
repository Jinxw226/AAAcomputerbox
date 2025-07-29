#VueRouter 

- Vue Router：Vue的官方路由。 为Vue提供富有表现力、可配置的、方便的路由。
- Vue中的路由，主要定义的是==路径==与==组件==之间的对应关系。
- 官网：[入门 | Vue Router](https://router.vuejs.org/zh/guide/)
![[asset/VueRouter.png]]VueRouter主要由以下三个部分组成，如下所示：
![[vuerouter三个组成部分.png]]
- VueRouter：路由器类，根据路由请求在路由视图中动态渲染选中的组件
- `<router-link>`：请求链接组件，浏览器会解析成`<a>`
- `<router-view>`：动态视图组件，用来渲染展示与路由路径对应的组件

嵌套路由：
注意在app.vue和layout.vue中都需要`<router-view>`标签来显示
示例：
```JavaScript
import { createRouter, createWebHistory } from 'vue-router'

import IndexView from '@/views/index/index.vue'
import ClazzView from '@/views/clazz/index.vue'
import DeptView from '@/views/dept/index.vue'
import EmpView from '@/views/emp/index.vue'
import LogView from '@/views/log/index.vue'
import StuView from '@/views/stu/index.vue'
import EmpReportView from '@/views/report/emp/index.vue'
import StuReportView from '@/views/report/stu/index.vue'
import LayoutView from '@/views/layout/index.vue'
import LoginView from '@/views/login/index.vue'

const router = createRouter({
  history: createWebHistory(import.meta.env.BASE_URL),
  routes: [
    {
     path: '/', 
     name: '',
     component: LayoutView,
     redirect: '/index', //重定向
     children: [
      {path: 'index', name: 'index', component: IndexView},
      {path: 'clazz', name: 'clazz', component: ClazzView},
      {path: 'stu', name: 'stu', component: StuView},
      {path: 'dept', name: 'dept', component: DeptView},
      {path: 'emp', name: 'emp', component: EmpView},
      {path: 'log', name: 'log', component: LogView},
      {path: 'empReport', name: 'empReport', component: EmpReportView},
      {path: 'stuReport', name: 'stuReport', component: StuReportView},
     ]
    },
    {path: '/login', name: 'login', component: LoginView}
  ]
})

export default router
```