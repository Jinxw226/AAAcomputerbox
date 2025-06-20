#NumPy迭代数组
## nditer
NumPy 迭代器对象 ==numpy.nditer ==提供了一种灵活访问一个或者多个数组元素的方式。
迭代器最基本的任务的可以完成对数组元素的访问。
实例：
```python
import numpy as np
 
a = np.arange(6).reshape(2,3)
print ('原始数组是：')
print (a)
print ('\n')
print ('迭代输出元素：')
for x in np.nditer(a):
    print (x, end=", " )
print ('\n')

# 原始数组是：
# [[0 1 2]
#  [3 4 5]]
# 迭代输出元素：
# 0, 1, 2, 3, 4, 5,
```
C-order行优先   Fortran列优先  T转置
实例：
```python
import numpy as np
a = np.arange(6).reshape(2,3)
for x in np.nditer(a.T):
    print (x, end=", " )
print ('\n')  #0, 1, 2, 3, 4, 5,
for x in np.nditer(a.T.copy(order='C')):
    print (x, end=", " )
print ('\n')  #0, 3, 1, 4, 2, 5,
```
思路解析：
初始化数组为
[[0 1 2]
 [3 4 5]]
 a.T转置视图（不是副本），内存布局为Fortran顺序（列优先）
 [[0 3]
  [1 4]
  [2 5]]
Fortran顺序 → 按列迭代：`列0: [0,1,2]` → `列1: [3,4,5]`
a.T.copy(order='C')创建了C顺序（行优先）的副本
[[0 3]  # 行0
 [1 4]  # 行1
 [2 5]] # 行2
按行迭代：**0→3→1→4→2→5**

### 控制遍历顺序：
- `for x in np.nditer(a, order='F'):`Fortran order，即是列序优先；
- `for x in np.nditer(a.T, order='C'):`C order，即是行序优先；

可以通过显式设置，强制nditer对象使用某种顺序
实例：
```python
import numpy as np 
 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print ('原始数组是：')
print (a)
print ('\n')
print ('以 C 风格顺序排序：')
for x in np.nditer(a, order =  'C'):  
    print (x, end=", " )
print ('\n')
print ('以 F 风格顺序排序：')
for x in np.nditer(a, order =  'F'):  
    print (x, end=", " )
```
输出结果：
```
原始数组是：
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]


以 C 风格顺序排序：
0, 5, 10, 15, 20, 25, 30, 35, 40, 45, 50, 55, 

以 F 风格顺序排序：
0, 20, 40, 5, 25, 45, 10, 30, 50, 15, 35, 55,
```

### 修改数组中元素的值
  nditer 对象有另一个可选参数 op_flags。 默认情况下，nditer 将视待迭代遍历的数组为只读对象（read-only），为了在遍历数组的同时，实现对数组元素值的修改，必须指定 readwrite 或者 writeonly 的模式。

实例：
```python
import numpy as np
 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print ('原始数组是：')
print (a)
print ('\n')
for x in np.nditer(a, op_flags=['readwrite']): 
    x[...]=2*x 
print ('修改后的数组是：')
print (a)
```

输出结果为：
```
原始数组是：
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]


修改后的数组是：
[[  0  10  20  30]
 [ 40  50  60  70]
 [ 80  90 100 110]]
```

### 使用外部循环
nditer 类的构造器拥有 flags 参数，它可以接受下列值：

|参数|描述|
|---|---|
|`c_index`|可以跟踪 C 顺序的索引|
|`f_index`|可以跟踪 Fortran 顺序的索引|
|`multi_index`|每次迭代可以跟踪一种索引类型|
|`external_loop`|给出的值是具有多个值的一维数组，而不是零维数组|
实例：
```python
import numpy as np 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print ('原始数组是：')
print (a)
print ('\n')
print ('修改后的数组是：')
for x in np.nditer(a, flags =  ['external_loop'], order =  'F'):  
   print (x, end=", " )
```

输出结果为：
```
原始数组是：
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]


修改后的数组是：
[ 0 20 40], [ 5 25 45], [10 30 50], [15 35 55],
```

### 广播迭代
实例：
```python
import numpy as np 
 
a = np.arange(0,60,5) 
a = a.reshape(3,4)  
print  ('第一个数组为：')
print (a)
print  ('\n')
print ('第二个数组为：')
b = np.array([1,  2,  3,  4], dtype =  int)  
print (b)
print ('\n')
print ('修改后的数组为：')
for x,y in np.nditer([a,b]):  
    print ("%d:%d"  %  (x,y), end=", " )
```

输出结果：
```
第一个数组为：
[[ 0  5 10 15]
 [20 25 30 35]
 [40 45 50 55]]


第二个数组为：
[1 2 3 4]


修改后的数组为：
0:1, 5:2, 10:3, 15:4, 20:1, 25:2, 30:3, 35:4, 40:1, 45:2, 50:3, 55:4,
```