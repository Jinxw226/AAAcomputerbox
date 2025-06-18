#NumPy #arange
## arange
```python
numpy.arange(start, stop, step, dtype)
```
参数说明：

| 参数      | 描述                                   |
| ------- | ------------------------------------ |
| `start` | 起始值，默认为`0`                           |
| `stop`  | 终止值（不包含）                             |
| `step`  | 步长，默认为`1`                            |
| `dtype` | 返回`ndarray`的数据类型，如果没有提供，则会使用输入数据的类型。 |
实例：
```python
import numpy as np
# 设置了 dtype
x = np.arange(5, dtype =  float)  
y = np.arange(10, 20, 2)
print (x)   #[0.  1.  2.  3.  4.]
print (y)   #[10  12  14  16  18]
```

## linspace
用于创建一个一维数组，数组是等差数列构成的，格式如下：
```python
np.linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None)
```
参数说明：

|参数|描述|
|---|---|
|`start`|序列的起始值|
|`stop`|序列的终止值，如果`endpoint`为`true`，该值包含于数列中|
|`num`|要生成的等步长的样本数量，默认为`50`|
|`endpoint`|该值为 `true` 时，数列中包含`stop`值，反之不包含，默认是True。|
|`retstep`|如果为 True 时，生成的数组中会显示间距，反之不显示。|
|`dtype`|`ndarray` 的数据类型|
实例：
```python
import numpy as np
a = np.linspace(1,10,10)
b = np.linspace(1,10,50)
c = np.linspace(1,1,10)
d = np.linspace(10, 20,  5, endpoint =  False)  
e =np.linspace(1,10,10,retstep= True)
print(a)
print(b)
print(c)
print(d)
print(e)
```
![[linspace实例结果.png]]

## logspace
numpy.logspace 函数用于创建一个于等比数列。格式如下：
```python
np.logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None)
```
base 参数意思是取对数的时候 log 的下标。

| 参数         | 描述                                                |
| ---------- | ------------------------------------------------- |
| `start`    | 序列的起始值为：base ** start                             |
| `stop`     | 序列的终止值为：base ** stop。如果`endpoint`为`true`，该值包含于数列中 |
| `num`      | 要生成的等步长的样本数量，默认为`50`                              |
| `endpoint` | 该值为 `true` 时，数列中中包含`stop`值，反之不包含，默认是True。         |
| `base`     | 对数 log 的底数，默认底数是10。                               |
| `dtype`    | `ndarray` 的数据类型                                   |
实例：
```python
import numpy as np
# 默认底数是 10
a = np.logspace(1.0,  2.0, num =  10)  
b = np.logspace(0,9,10,base=2)
print(a)  
# [ 10.           12.91549665     16.68100537      21.5443469  27.82559402   
#   35.93813664   46.41588834     59.94842503      77.42636827    100.    ]
print(b)   #[  1.   2.   4.   8.  16.  32.  64. 128. 256. 512.]
```