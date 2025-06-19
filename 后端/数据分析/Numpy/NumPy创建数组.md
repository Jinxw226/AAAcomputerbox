#NumPy #NumPy创建数组
## Empty
ndarray 数组除了可以使用底层 ndarray 构造器来创建外，也可以通过以下几种方式来创建。
```python
numpy.empty(shape, dtype = float, order = 'C')
```
参数说明：

|参数|描述|
|---|---|
|shape|数组形状|
|dtype|数据类型，可选|
|order|有"C"和"F"两个选项,分别代表，行优先和列优先，在计算机内存中的存储元素的顺序。|
实例：
```python
import numpy as np 
x = np.empty([3,2], dtype = int) 
print (x)  #给出随机的几个数构成的二维三行两列的数组
#元素为随机值，因为他们未有初始化
```

## Zeros
创建指定大小的数组，数组元素以 0 来填充：
```python
numpy.zeros(shape, dtype = float, order = 'C')
```
参数说明：

|参数|描述|
|---|---|
|shape|数组形状|
|dtype|数据类型，可选|
|order|'C' 用于 C 的行数组，或者 'F' 用于 FORTRAN 的列数组|
实例：
```python
import numpy as np
 
# 默认为浮点数
x = np.zeros(5) 
print(x)   #[0. 0. 0. 0. 0.]
 
# 设置类型为整数
y = np.zeros((5,), dtype = int) 
print(y)   #[0 0 0 0 0]
 
# 自定义类型
z = np.zeros((2,2), dtype = [('x', 'i4'), ('y', 'i4')])  
print(z)   
#  [[(0, 0) (0, 0)]
#   [(0, 0) (0, 0)]]
```

## Ones
创建指定形状的数组，数组元素以 1 来填充：
```python
numpy.ones(shape, dtype = None, order = 'C')
```
参数说明：

|参数|描述|
|---|---|
|shape|数组形状|
|dtype|数据类型，可选|
|order|'C' 用于 C 的行数组，或者 'F' 用于 FORTRAN 的列数组|
实例：
```python
import numpy as np

# 默认为浮点数
x = np.ones(5) 
print(x)  #[1. 1. 1. 1. 1.]
 
# 自定义类型
x = np.ones([2,2], dtype = int)
print(x)
# [[1 1]
#  [1 1]]
```
## Zeros_like
- numpy.zeros_like 用于创建一个与给定数组具有相同形状的数组，数组元素以 0 来填充。
- numpy.zeros 和 numpy.zeros_like 都是用于创建一个指定形状的数组，其中所有元素都是 0。
- 它们之间的区别在于：numpy.zeros 可以直接指定要创建的数组的形状，而 numpy.zeros_like 则是创建一个与给定数组具有相同形状的数组。

```python
numpy.zeros_like(a, dtype=None, order='K', subok=True, shape=None)
```
参数说明：

| 参数    | 描述                                                         |
| ----- | ---------------------------------------------------------- |
| a     | 给定要创建相同形状的数组                                               |
| dtype | 创建的数组的数据类型                                                 |
| order | 数组在内存中的存储顺序，可选值为 'C'（按行优先）或 'F'（按列优先），默认为 'K'（保留输入数组的存储顺序） |
| subok | 是否允许返回子类，如果为 True，则返回一个子类对象，否则返回一个与 a 数组具有相同数据类型和存储顺序的数组   |
| shape | 创建的数组的形状，如果不指定，则默认为 a 数组的形状。                               |
实例：
```python
import numpy as np
# 创建一个 3x3 的二维数组
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# 创建一个与 arr 形状相同的，所有元素都为 0 的数组
zeros_arr = np.zeros_like(arr)
print(zeros_arr)
#[[0 0 0]
# [0 0 0]
# [0 0 0]]
```
## Ones_like
- numpy.ones_like 用于创建一个与给定数组具有相同形状的数组，数组元素以 1 来填充。
- numpy.ones 和 numpy.ones_like 都是用于创建一个指定形状的数组，其中所有元素都是 1。
- 它们之间的区别在于：numpy.ones 可以直接指定要创建的数组的形状，而 numpy.ones_like 则是创建一个与给定数组具有相同形状的数组。
```python
numpy.ones_like(a, dtype=None, order='K', subok=True, shape=None)
```
实例：
```python
import numpy as np
# 创建一个 3x3 的二维数组
arr = np.array([[1, 2, 3], [4, 5, 6], [7, 8, 9]])

# 创建一个与 arr 形状相同的，所有元素都为 1 的数组
ones_arr = np.ones_like(arr)
print(ones_arr)
#[[1 1 1]
# [1 1 1]
# [1 1 1]]

```