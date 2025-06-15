弱类型语言，定义函数时，形参和返回值都无需指定类型
#js具名函数
```javascript
function name(形参1, 形参2, ...){
	return 
}
```
#js匿名函数 指的是一种没有名称的函数， 可以通过两种方式定义：函数表达式 和 箭头函数
```javascript
//函数表达式
let add = function (a, b){
	return a + b;
}
```
```javascript
//箭头函数
let add = (a, b) => {
	return a + b;
}
```