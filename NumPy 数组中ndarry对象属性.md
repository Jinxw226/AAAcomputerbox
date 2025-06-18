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
