#JSON  #parse #stringify
在 JavaScript 中，_JSON.parse_ 和 _JSON.stringify_ 是处理 JSON 数据的两个核心方法，分别用于解析 JSON 字符串和序列化 JavaScript 对象。它们在数据传输、存储以及与其他系统交互中非常重要。

## JSON.parse 的用法

_JSON.parse_ 用于将 JSON 字符串解析为 JavaScript 对象。它接受一个 JSON 格式的字符串作为参数，并返回对应的 JavaScript 对象。

示例：
```js
const jsonString = '{"name": "John", "age": 30}';
const jsonObject = JSON.parse(jsonString);

console.log(jsonObject); // { name: 'John', age: 30 }
console.log(jsonObject.name); // John
console.log(jsonObject.age); // 30
```

注意事项：

- JSON 字符串的键和值必须使用双引号包裹。
- 支持解析数字、布尔值和 _null_，但不支持其他类型。
- 如果 JSON 格式不正确（如使用单引号或多余的逗号），会抛出 _SyntaxError_。

高级用法：_JSON.parse_ 支持一个可选的 _reviver_ 参数，用于对解析后的值进行转换。

```js
const jsonString = '{"age": 30}';
const parsed = JSON.parse(jsonString, (key, value) => {
if (key === 'age') return value + 5;
	return value;
});
console.log(parsed); // { age: 35 }
```

## JSON.stringify 的用法

_JSON.stringify_ 用于将 JavaScript 对象转换为 JSON 字符串。它接受一个对象作为参数，并返回对应的 JSON 字符串。

示例：
```js
const obj = { name: 'John', age: 30 };
const jsonString = JSON.stringify(obj);

console.log(jsonString); // '{"name":"John","age":30}'
```

注意事项：

- 基本类型（如字符串、数字、布尔值）会被直接转换为 JSON 格式的字符串。
- _undefined_、_Symbol_ 和函数会被忽略或替换为 _null_。
- 循环引用的对象会抛出 _TypeError_。

高级用法：_JSON.stringify_ 支持两个可选参数 _replacer_ 和 _space_。
- _replacer_ 用于筛选或转换对象的属性。
```js
const obj = { name: 'John', age: 30, gender: 'male' };
const jsonString = JSON.stringify(obj, ['name', 'age']);
console.log(jsonString); // '{"name":"John","age":30}'
```

- _space_ 用于美化输出，指定缩进的空格数或字符串。
```js
const obj = { name: 'John', age: 30 };
const jsonString = JSON.stringify(obj, null, 2);
console.log(jsonString);
/*
{
"name": "John",
"age": 30
}
*/
```

常见应用场景

1. **数据传输**：在客户端和服务器之间传递数据时，通常使用 JSON 格式。_JSON.stringify_ 将对象序列化为字符串发送，_JSON.parse_ 将接收到的字符串解析为对象。
2. **本地存储**：在浏览器的 _localStorage_ 或 _sessionStorage_ 中存储对象时，需使用 _JSON.stringify_ 序列化对象，取出时再用 _JSON.parse_ 解析。
3. **深拷贝**：通过 _JSON.stringify_ 和 _JSON.parse_ 的组合，可以实现对象的深拷贝。

```js
const original = { name: 'John', details: { age: 30 } };
const copy = JSON.parse(JSON.stringify(original));
copy.details.age = 35;

console.log(original.details.age); // 30
console.log(copy.details.age); // 35
```