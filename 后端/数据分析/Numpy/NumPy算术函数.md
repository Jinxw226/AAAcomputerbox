#NumPy算术函数
NumPy 算术函数包含简单的加减乘除: **add()**，**subtract()**，**multiply()** 和 **divide()**。

==需要注意的是数组必须具有相同的形状或符合数组广播规则。==

实例：
```python
import numpy as np 
 
a = np.arange(9, dtype = np.float_).reshape(3,3)  
print ('第一个数组：')
print (a)
print ('\n')
print ('第二个数组：')
b = np.array([10,10,10])  
print (b)
print ('\n')
print ('两个数组相加：')
print (np.add(a,b))
print ('\n')
print ('两个数组相减：')
print (np.subtract(a,b))
print ('\n')
print ('两个数组相乘：')
print (np.multiply(a,b))
print ('\n')
print ('两个数组相除：')
print (np.divide(a,b))
```

输出结果：
```
第一个数组：
[[0. 1. 2.]
 [3. 4. 5.]
 [6. 7. 8.]]


第二个数组：
[10 10 10]


两个数组相加：
[[10. 11. 12.]
 [13. 14. 15.]
 [16. 17. 18.]]


两个数组相减：
[[-10.  -9.  -8.]
 [ -7.  -6.  -5.]
 [ -4.  -3.  -2.]]


两个数组相乘：
[[ 0. 10. 20.]
 [30. 40. 50.]
 [60. 70. 80.]]


两个数组相除：
[[0.  0.1 0.2]
 [0.3 0.4 0.5]
 [0.6 0.7 0.8]]
```

### numpy.reciprocal()
numpy.reciprocal() 函数返回参数逐元素的倒数。如 **1/4** 倒数为 **4/1**。

实例：
```python
import numpy as np 
 
a = np.array([0.25,  1.33,  1,  100])  
print ('我们的数组是：')
print (a)
print ('\n')
print ('调用 reciprocal 函数：')
print (np.reciprocal(a))
#我们的数组是：
#[  0.25   1.33   1.   100.  ]
#调用 reciprocal 函数：
#[4.        0.7518797 1.        0.01     ]
```

### numpy.power()

numpy.power() 函数将第一个输入数组中的元素作为底数，计算它与第二个输入数组中相应元素的 幂。

实例：
```python
import numpy as np 
 
a = np.array([10,100,1000])  
print ('我们的数组是；')
print (a)
print ('\n') 
print ('调用 power 函数：')
print (np.power(a,2))
print ('\n')
print ('第二个数组：')
b = np.array([1,2,3])  
print (b)
print ('\n')
print ('再次调用 power 函数：')
print (np.power(a,b))
我们的数组是；
#[  10  100 1000]
#调用 power 函数：
#[    100   10000 1000000]
#第二个数组：
#[1 2 3]
#再次调用 power 函数：
#[        10      10000 1000000000]
```

### numpy.mod()

numpy.mod() 计算输入数组中相应元素的相除后的余数。 函数 numpy.remainder() 也产生相同的结果。

实例：
```python
import numpy as np
 
a = np.array([10,20,30]) 
b = np.array([3,5,7])  
print ('第一个数组：')
print (a)
print ('\n')
print ('第二个数组：')
print (b)
print ('\n')
print ('调用 mod() 函数：')
print (np.mod(a,b))
print ('\n')
print ('调用 remainder() 函数：')
print (np.remainder(a,b))

# 第一个数组：
# [10 20 30]
# 第二个数组：
# [3 5 7]
# 调用 mod() 函数：
# [1 0 2]
# 调用 remainder() 函数：
# [1 0 2]
```