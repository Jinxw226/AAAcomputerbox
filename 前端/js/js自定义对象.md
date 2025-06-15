#js自定义对象
js自定义对象尽量不要使用箭头函数，this指定容易有误区
```javascript
  let user = {
    name: '令狐冲',
    gender: '男',
    job: '讲师',
    //方式一
    sing() {
      alert(this.name + '在唱歌')
    },
    //方式二
    singer: function () {
      alert(this.name + '在唱歌')
    }
  }
```

调用方法：
	对象名.属性名
	对象名.方法名()
