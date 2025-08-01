#程序优化 #axios

1). 为了解决上述问题，我们在前端项目开发时，通常会定义一个请求处理的工具类 - `src/utils/request.js` 。 在这个工具类中，对axios进行了封装。 具体代码如下：

```JavaScript
import axios from 'axios'

//创建axios实例对象
const request = axios.create({
  baseURL: '/api',
  timeout: 600000
})

//axios的响应 response 拦截器
request.interceptors.response.use(
  (response) => { //成功回调
    return response.data
  },
  (error) => { //失败回调
    return Promise.reject(error)
  }
)

export default request
```

2). 而与服务端进行异步交互的逻辑，通常会按模块，封装在一个单独的API中，如：`src/api/dept.js`

```JavaScript
import request from "@/utils/request"

//列表查询
export const queryAllApi = () => request.get('/depts')
```

3). 修改 `src/views/dept/index.vue` 中的代码

现在就不需要每次直接调用axios发送异步请求了，只需要将我们定义的对应模块的API导入进来，就可以直接使用了。

```JavaScript
<script setup>
import {ref, onMounted} from 'vue'
import {queryAllApi} from '@/api/dept'

//声明列表展示数据
let deptList= ref([])

//动态加载数据-查询部门
const queryAll = async () => {
  const result = await queryAllApi()
  deptList.value = result.data
}

//钩子函数
onMounted(() => {
  queryAll()
})

// 编辑部门 - 根据ID查询回显数据
const handleEdit = (id) => {
  console.log(`Edit item with ID ${id}`);
  // 在这里实现编辑功能
};

// 删除部门 - 根据ID删除部门
const handleDelete = (id) => {
  console.log(`Delete item with ID ${id}`);
  // 在这里实现删除功能
};
</script>
```

做完上面这三步之后，我们打开浏览器发现，并不能访问到接口数据。原因是因为，目前请求路径不对。、

4). 在 `vite.config.js` 中配置前端请求服务器的信息
在服务器中配置代理proxy的信息，并在配置代理时，执行目标服务器。 以及url路径重写的规则。
![[配置前端请求服务器信息.png]]

```JavaScript
import { fileURLToPath, URL } from 'node:url'

import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'
import vueJsx from '@vitejs/plugin-vue-jsx'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [
    vue(),
    vueJsx(),
  ],
  resolve: {
    alias: {
      '@': fileURLToPath(new URL('./src', import.meta.url))
    }
  },
  server: {
    proxy: {
      '/api': {
        target: 'http://localhost:8080',
        secure: false,
        changeOrigin: true,
        rewrite: (path) => path.replace(/^\/api/, ''),
      }
    }
  }
})
```


为什么要配置/api路径？
为了区分客户端和服务器端发送的请求。