#js事件监听
语法：事件源 . addEventListener ('事件类型'，事件触发执行的函数)
事件监听三要素：
- 事件源：哪个[[DOM]]元素触发了事件，要获取dom元素
- 事件类型：用什么方式触发，比如：鼠标单击 click
- 事件触发执行的函数：要做什么事
```html
<body>
     <input type="button" id="btn1" value="点我一下试试1">
     <input type="button" id="btn2" value="点我一下试试2">
</body>
<script>
     //事件监听 - addEveryListener 可以多次绑定同一事件
     document.querySelector('#btn1').addEventListener('click',function(){
          console.log('试试就试试');
     })
     document.querySelector('#btn1').addEventListener('click',function(){
          console.log('试试就试试11');
     })
     //事件绑定-早期写法 - onclick （如果多次绑定同一事件，只会执行最后一次绑定（覆盖））
     document.querySelector('#btn2').onclick = () => {
          console.log('试试就试试');
     }
     document.querySelector('#btn2').onclick = () => {
          console.log('试试就试试22');
     }
</script>
```
点第一个按钮：试试就试试 
			 试试就试试11
点第二个按钮：试试就试试22