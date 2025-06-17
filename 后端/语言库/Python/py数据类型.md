#py数据类型
python不用定义变量名，直接定义
```python
d = '小说'  #字符串string（由字母、数字、下划线组成）
e = 4      #整型int 长整型
f = 3.14   #浮点型float
g = 1 + 2i #复数a+bi complex
h = 0122L  #长整型
#python允许同时为多个变量赋值
a = b = c = 1
a, b, c = 1, 2, "john"
```
字串列表两种取值顺序：
- 从左到右索引默认0开始的，最大范围是字符串长度少1
- 从右到左索引默认-1开始的，最大范围是字符串开头
![[py字串两种取值顺序.png]]
```python
s = 'abcdef'
s[1:5]  #切片'bcde' 左闭右开

str = 'Hello World!' print str # 输出完整字符串 
print str[0] # 输出字符串中的第一个字符 
print str[2:5] # 输出字符串中第三个至第六个之间的字符串 
print str[2:] # 输出从第三个字符开始的字符串 
print str * 2 # 输出字符串两次 
print str + "TEST" # 输出连接的字符串
```
结果输出：
```
Hello World!
H
llo
llo World!
Hello World!Hello World!
Hello World!TEST
```


