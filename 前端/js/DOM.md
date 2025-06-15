#dom
DOM: Document Object Model  文档对象模型
将标记语言的各个组成部分封装为对应的对象：
- Document: 整个文档对象
- Element: 元素对象
- Attribute: 属性对象
- Text: 文本对象
- Comment: 注释对象
![[DOM树.png]]

如何获取DOM对象
- document.querySelector(‘选择器’)
- doucment.querySelectorAll('选择器')
```html javascript
<body>
     <h1 id="title1">111111</h1>
     <h1>222222</h1>
     <h1>333333</h1>
</body>
<script>
     //修改第一个h1标签中的文本内容
     //1.获取DOM对象
     // let h1 = document.querySelector('#title1')
     let h1 = document.querySelector('h1')// 获取所有h1中第一个h1标签
     let hs = document.querySelectorAll('h1')// 获取所有h1成一个数组
     //2.调用DOM对象中的属性或方法
     h1.innerHTML = 'Hello World'
     // 获取这个数组中第二个元素
     hs[1].innerHTML = 'Jinx'
</script>
```
![[DOM演示结果.png]]