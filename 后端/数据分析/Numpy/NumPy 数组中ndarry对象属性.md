#numpy数据 #ndarry对象属性
NumPy 的数组中比较重要 ndarray 对象属性有：

|属性|说明|
|---|---|
|`ndarray.ndim`|数组的秩（rank），即数组的维度数量或轴的数量。|
|`ndarray.shape`|数组的维度，表示数组在每个轴上的大小。对于二维数组（矩阵），表示其行数和列数。|
|`ndarray.size`|数组中元素的总个数，等于 `ndarray.shape` 中各个轴上大小的乘积。|
|`ndarray.dtype`|数组中元素的数据类型。|
|`ndarray.itemsize`|数组中每个元素的大小，以字节为单位。|
|`ndarray.flags`|包含有关内存布局的信息，如是否为 C 或 Fortran 连续存储，是否为只读等。|
|`ndarray.real`|数组中每个元素的实部（如果元素类型为复数）。|
|`ndarray.imag`|数组中每个元素的虚部（如果元素类型为复数）。|
|`ndarray.data`|实际存储数组元素的缓冲区，一般通过索引访问元素，不直接使用该属性。|
实例：
```python
import numpy as np
a = np.arange(24)  
print(a.ndim)  # 1   现在又有一个维度
b = a.reshape(2, 4, 3)  #b 现在拥有三个维度
print(b.ndim)  #3
c = np.array([[1,2,3],[4,5,6]])  
print (c.shape)   #(2, 3)
c.shape = (3, 2)
print(a)
# [[1 2]
#  [3 4]
#  [5 6]]
d = c.reshape(3, 2)
print(d)
# 数组的 dtype 为 int8（一个字节）  
x = np.array([1,2,3,4,5], dtype = np.int8)  
print (x.itemsize)  # 1
# 数组的 dtype 现在为 float64（八个字节）
y = np.array([1,2,3,4,5], dtype = np.float64)  
print (y.itemsize)  # 8
```
ndarray.flags 返回 ndarray 对象的内存信息，包含以下属性：

|属性|描述|
|---|---|
|C_CONTIGUOUS (C)|数据是在一个单一的C风格的连续段中|
|F_CONTIGUOUS (F)|数据是在一个单一的Fortran风格的连续段中|
|OWNDATA (O)|数组拥有它所使用的内存或从另一个对象中借用它|
|WRITEABLE (W)|数据区域可以被写入，将该值设置为 False，则数据为只读|
|ALIGNED (A)|数据和所有元素都适当地对齐到硬件上|
|UPDATEIFCOPY (U)|这个数组是其它数组的一个副本，当这个数组被释放时，原数组的内容将被更新|
实例：
```python
import numpy as np 
 
x = np.array([1,2,3,4,5])  
print (x.flags)
```
结果：
```
  C_CONTIGUOUS : True
  F_CONTIGUOUS : True
  OWNDATA : True
  WRITEABLE : True
  ALIGNED : True
  WRITEBACKIFCOPY : False
  UPDATEIFCOPY : False
```