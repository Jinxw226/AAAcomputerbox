**代码实现如下：**
在 src 下定义 views 目录，在 views 目录中定义文件 `UserList.vue`， 然后，我们就可以将之前实现的Vue案例中的代码，基于Vue工程化的形式来实现一遍。 (之前实现的这个页面，在资料中已经提供了：`1.工程化-案例-素材.html`)
1). 把原来定义的CSS样式代码，拷贝到 `<style></style>` 标签中。
2). 把页面的`<div id="app"></div>` 中的页面展示的html标签代码，拷贝到 `<template></template>` 标签中。
3). 将页面的JS代码，按照组合式API的形式，在 `<script></script>` 中定义出来。
4). 而由于在这个案例中，需要用到`axios`来发送异步请求，所以还需要安装 `axios`。
![[安装axios.png]]**具体代码如下：**
`views/UserList.vue` 代码如下：
```HTML
<script setup>
//引入ref
import { ref, onMounted } from 'vue'
import axios from 'axios'

//声明数据变量 userList, name, gender, job
const userList = ref([])
const name = ref('')
const gender = ref('')
const job = ref('')

//声明函数,基于axios查询数据
const search = () => {
  //发送请求
  axios.get(`https://web-server.itheima.net/emps/list?name=${name.value}&gender=${gender.value}&job=${job.value}`).then(res => {
    //将查询到的数据赋值给userList
    userList.value = res.data.data
  })
}

//定义钩子函数 onMounted
onMounted(() => {
  //调用search函数
  search()
})
</script>

<template>
  <div id="center">
    姓名: <input type="text" name="name" v-model="name">

    性别:
    <select name="gender" v-model="gender">
      <option value="1">男</option>
      <option value="2">女</option>
    </select>

    职位:
    <select name="job" v-model="job">
      <option value="1">班主任</option>
      <option value="2">讲师</option>
      <option value="3">其他</option>
    </select>

    <input class="btn" type="button" value="查询" @click="search">
  </div>
  
  <table>
    <tr>
      <th>序号</th>
      <th>姓名</th>
      <th>头像</th>
      <th>性别</th>
      <th>职位</th>
      <th>入职时间</th>
      <th>更新时间</th>
    </tr>

    <!-- v-for 用于列表循环渲染元素 -->
    <tr v-for="(user, index) in userList" :key="user.id">
      <td>{{index + 1}}</td>
      <td>{{user.name}}</td>
      <td> <img :src="user.image"> </td>
      <td>
        <span v-if="user.gender == 1">男</span>
        <span v-else-if="user.gender == 2">女</span>
        <span v-else>其他</span>
      </td>
      <td>
        <span v-show="user.job == 1">班主任</span>
        <span v-show="user.job == 2">讲师</span>
        <span v-show="user.job != 1 && user.job != 2">其他</span>
      </td>
      <td>{{user.entrydate}}</td>
      <td>{{user.updatetime}}</td>
    </tr>
  </table>
</template>

<style scoped>
  table,th,td {
    border: 1px solid #000;
    border-collapse: collapse;
    line-height: 50px;
    text-align: center;
  }

  #center,table {
    width: 60%;
    margin: auto;
  }

  #center {
    margin-bottom: 20px;
  }

  img {
    width: 50px;
  }

  input,select {
    width: 17%;
    padding: 10px;
    margin-right: 30px;
    border: 1px solid #ccc;
    border-radius: 4px;
  }

  .btn {
    background-color: #ccc;
  }
</style>
```

  

然后在 `App.vue` 中，将 `UserList.vue` 引入进来。

```HTML
<script setup>
import UserList from './views/user/UserList.vue'
</script>

<template>
   <UserList></UserList>
</template>

<style scoped>

</style>
```