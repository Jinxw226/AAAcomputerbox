#Axios
Axios: 对原生的[[Ajax]]进行了封装 简化书写 快速开发
官网：[Axios中文文档 | Axios中文网](https://www.axios-http.cn/)
步骤：
- 引入Axios的 js 文件（参照官网）
- 使用Axios发送请求，并获取响应结果

`<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

```javascript
axios({
	method: 'GET',
	url: 'https://web-server.itheima.net/emps/list'
}).then((result) => {
	console.log(result.data);
}).catch((err) => {
	alert(err);
})
```
then：成功回调函数
catch：失败回调函数
method：请求方式，GET / POST
url：请求路径
data：请求数据(POST)
params：发送请求时携带的url参数 如：...?key=val

简化写法
格式：axios.请求方式(url , data , config )
```javascript
axios.get('https://mock.apifox.cn/m1/3083103-0-default/emps/list').then((result) => {
	console.log(result.data)
}).catch((err) => {
	console.log(err)
})
```
```javascript
axios.post('https://mock.apifox.cn/m1/3083103-0-default/emps/update'.'id = 1').then((result) => {
	console.log(result.data)
}).catch((err) => {
	console.log(err)
})
```