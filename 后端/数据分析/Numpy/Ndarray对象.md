#Ndarray
ndarry：N维数组对象 ndarray，它是一系列同类型数据的集合，以 0 下标为开始进行集合中元素的索引。
- ndarray 对象是用于存放同类型元素的多维数组。
- ndarray 中的每个元素在内存中都有相同存储大小的区域。
- ndarray 内部由以下内容组成：
	- 一个指向数据（内存或内存映射文件中的一块数据）的指针。
	- 数据类型或 dtype，描述在数组中的固定大小值的格子。
	- 一个表示数组形状（shape）的元组，表示各维度大小的元组。
	- 一个跨度元组（stride），其中的整数指的是为了前进到当前维度下一个元素需要"跨过"的字节数。

ndarray 的内部结构:
![[ndarray内部结构.png]]

创建一个ndarray只需要调用NumPy中的array函数：
```python
numpy.array(object, dtype = None, copy = True, order = None, subok = False, ndmin = 0)
```
**参数说明：**

| 名称     | 描述                             |
| ------ | ------------------------------ |
| object | 数组或嵌套的数列                       |
| dtype  | 数组元素的数据类型，可选                   |
| copy   | 对象是否需要复制，可选                    |
| order  | 创建数组的样式，C为行方向，F为列方向，A为任意方向（默认） |
| subok  | 默认返回一个与基类类型一致的数组               |
| ndmin  | 指定生成数组的最小维度                    |
实例：
```python
import numpy as np
a = np.array([[1, 2], [3, 4]])
b = np.array([1, 2, 3])
c = np.array([1, 2, 3, 4, 5], ndmin = 2)
d = np.array([1, 2, 3], dtype = complex)
print(a)
# [[1  2]
#  [3  4]]
# 二维
print(b)
# [1 2 3]
print(c)
# [[1 2 3 4 5]]
# 二维
print(d)
# [1.+0.j 2.+0.j 3.+0.j]
```