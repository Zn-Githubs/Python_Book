# Numpy



Numpy

> NumPy(Numerical Python) 是 Python 语言的一个扩展程序库，支持大量的维度数组与矩阵运算，此外也针对数组运算提供大量的数学函数库。

### numpy.random

#### 随机选择

numpy.random.choice(.npy文件\[, num])默认选择一个

### 数组操作

#### numpy.unique

> numpy.unique 函数用于去除数组中的重复元素

```python
import numpy as np
A = [1, 2, 2, 5,3, 4, 3]
a = np.unique(A)
B= (1, 2, 2,5, 3, 4, 3)
b= np.unique(B)
C= ['fgfh','asd','fgfh','asdfds','wrh']
c= np.unique(C)
print(a)
print(b)
print(c)
# >>> 输出为 [1 2 3 4 5]
# >>> [1 2 3 4 5]
# >>> ['asd' 'asdfds' 'fgfh' 'wrh']
```
