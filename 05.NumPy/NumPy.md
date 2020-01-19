##### 5. Numpy
###### 5.1 Numpy简介
Numpy(Numerical Python)是一个开源的高性能的科学计算和数据分析库，用于快速处理任意维度的数组。并且，Numpy支持常见的数组和矩阵操作。Numpy使用ndarray对象来处理多为数组，ndarray对象是一个快速灵活的大数据容器。
###### 5.2 ndarray简介
Python中有列表，可当数组使用。Python中也有array模块，但是不支持多维数组。并且列表和array模块都没有科学运算函数。所以，Python不适合做矩阵等科学计算。Numpy没有使用Python本身的数组机制，而是提供了ndarray这个n维数组类型对象，ndarray不仅能够很方便地对数组进行存取，而且拥有丰富的科学计算函数，如向量的加法、减法、乘法等。下面通过实例演示创建一个ndarray多维数组：
```py
# 导入numpy函数库并指定库的别名
import numpy as np
# 创建一维数组
array1 = np.array([1, 2, 3, 4])
# 创建二维数组
array2 = np.array([[1, 2, 3, 4],[5, 6, 7, 8]])
# 创建三维数组
array3 = np.array([[[1, 2, 3, 4],[5, 6, 7, 8],[9, 10, 11, 12]],[[1, 2, 3, 4],[5, 6, 7, 8],[9, 10, 11, 12]]])
```
```py
array1：array([1, 2, 3, 4])
array2：array([[1, 2, 3, 4],
       [5, 6, 7, 8]])
array3：array([[[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]],

       [[ 1,  2,  3,  4],
        [ 5,  6,  7,  8],
        [ 9, 10, 11, 12]]])
```
###### 5.3 ndarray与list执行效率的对比
使用Python的list可以作为一维数组，通过列表的嵌套可以实现多维数组。那为什么还要使用Numpy的ndarray，其实使用ndarray处理数组，其效率要比list要高很多，下面通过例子来比较下两者的执行效率：
```py
import random
import numpy as np
# 定义一个空列表用于存放(数组)元素
lst = []
# 向lst中添加一千万个元素
for i in range(10000000):
    lst.append(random.random())
%time sum01 = sum(lst) # 使用Python中的sum函数对数组元素进行求和；%time是魔法方法，可以查看当前行代码运行一次需要花费的时间。
lst2 = np.array(lst) # 将lst的存储方式转换成ndarray中的存储方式
%time sum02 = np.sum(lst2) # 使用ndarray中的sum对同样的数组进行求和
```
```py
第一次运行上面的代码：
CPU times: user 40.8 ms, sys: 70 µs, total: 40.8 ms
Wall time: 40.9 ms
CPU times: user 4.07 ms, sys: 0 ns, total: 4.07 ms
Wall time: 3.87 ms

第一次运行上面的代码：
CPU times: user 41.1 ms, sys: 0 ns, total: 41.1 ms
Wall time: 41.1 ms
CPU times: user 3.86 ms, sys: 0 ns, total: 3.86 ms
Wall time: 3.87 ms

第三次运行上面的代码：
CPU times: user 40.8 ms, sys: 87 µs, total: 40.9 ms
Wall time: 40.9 ms
CPU times: user 4.23 ms, sys: 31 µs, total: 4.26 ms
Wall time: 4.07 ms
```
很明显使用numpy的ndarray对数组求和的效率要比原生Python的sum函数求和高10倍以上。<font color='red'>**机器学习最大的特点是需要对大量的数据做运算，**</font>如果没有一个快速的解决方案，那么可能Python在机器学习领域就达不到很好的效果。Numpy专门对ndarray的操作和运算进行设计，所以，数组的存储效率和输入输出性能远优于Python中的嵌套列表。数组越大，Numpy的优势就越明显。
###### 5.4 ndarray的优势
- 内存块风格：ndarray在存储数据的时候是直接存储，Python的list中的数据不是直接存储，需要先找寻一个地址，然后通过地址找到需要的内容。<font color='red'>**ndarray中的所有元素的类型都是相同的**</font>，所以ndarray在存储元素时，内存是可以连续的。而<font color='red'>**Python中list中的元素是任意的，所以只能通过寻址的方式找到下一个元素**</font>。ndarray在通用性上要输于list，但在科学计算中，Numpy的ndarray就可以省掉很多循环语句，代码使用方面比Python的list要简洁。
- ndarray支持并行化运算(向量化运算)：Numpy内置并行运算功能，当系统有多个核心时，做运算会自动做并行运算。
- 效率远高于纯Python代码，Numpy底层使用C语言编写，内部解除GIL（全局解释器锁），其对数组的操作速度不受Python GIL的影响。
###### 5.5 ndarray数组的属性
数组的维度：
```py
# 导入numpy模块并为模块设置别名
import numpy as np
# 创建一个维度是3行4列的ndarray数组
array01 = np.array([
    [80, 78, 98, 88],
    [89, 87, 89, 78],
    [78, 84, 89, 87]
])
array01.shape
```
```py
Out[]：(3, 4)
```
数组的维数：
```py
# 导入numpy模块并为模块设置别名
import numpy as np
# 创建一个维度是3行4列的ndarray数组
array01 = np.array([
    [80, 78, 98, 88],
    [89, 87, 89, 78],
    [78, 84, 89, 87]
])
array01.ndim
```
```py
Out[]：2
```
数组中的元素数量：
```py
# 导入numpy模块并为模块设置别名
import numpy as np
# 创建一个维度是3行4列的ndarray数组
array01 = np.array([
    [80, 78, 98, 88],
    [89, 87, 89, 78],
    [78, 84, 89, 87]
])
array01.size
```
```py
Out[]：12
```
一个数组元素的长度（字节）：
```py
# 导入numpy模块并为模块设置别名
import numpy as np
# 创建一个维度是3行4列的ndarray数组
array01 = np.array([
    [80, 78, 98, 88],
    [89, 87, 89, 78],
    [78, 84, 89, 87]
])
array01.itemsize
```
```py
Out[]：8
```
数组元素的类型：
```py
# 导入numpy模块并为模块设置别名
import numpy as np
# 创建一个维度是3行4列的ndarray数组
array01 = np.array([
    [80, 78, 98, 88],
    [89, 87, 89, 78],
    [78, 84, 89, 87]
])
array01.dtype
```
```py
Out[]：dtype('int64')
```
###### 5.6 ndarray数组的形状
一维数组：
```py
import numpy as np
a = np.array([1, 2, 3, 4, 5])
print(a)
print(a.shape)
```
```py
[1 2 3 4 5]
(5,) # 表示一维数组，5：数组中有5个元素
```
二维数组：
```py
import numpy as np
b = np.array([
    [1, 2, 3, 4, 5],
    [4, 5, 6, 7, 8]
])
print(b)
print(b.shape)
```
```py
[[1 2 3 4 5]
 [4 5 6 7 8]]
(2, 5) # 有两个元素，表示的是二维数组。2：二维数组中有两个一维数组；5：一维数组中有5个元素
```
三维数组（三维数组是二维数组的叠加）：
```py
import numpy as np
c = np.array([
    [[1, 2, 3, 4, 5],
    [4, 5, 6, 7, 8]],
    [[9, 10, 11, 12, 13],
    [14, 15, 16, 17, 18]]
])
print(c)
print(c.shape)
```
```py
[[[ 1  2  3  4  5]
  [ 4  5  6  7  8]]
 [[ 9 10 11 12 13]
  [14 15 16 17 18]]]
(2, 2, 5) # 第一个2：有2个二维数组；第二个2：二维数组中有2个一维数组；3：在一维数组中有3个元素
```
###### 5.7 ndarray数组的类型
不指定数组类型(整型)：
```py
import numpy as np
a = np.array([
    [[1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,17]],
    [[1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,12]]
])
a.dtype
```
```py
dtype('int64')
```
不指定数组类型(小数)：
```py
import numpy as np
a = np.array([
    [[1.1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,17]],
    [[1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,12]]
])
a.dtype
```
```py
dtype('float64')
```
如果不指定，整型默认是int64，小数默认是float64。如果指定数组类型：

指定数组类型，将整型指定为float64类型：
```py
import numpy as np
a = np.array([
    [[1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,17]],
    [[1, 2, 3, 4, 5, 6],
    [7, 8, 9, 10, 11,12],
    [12, 13, 14, 15, 16,12]]
], dtype=np.float64)
print(a)
a.dtype
```
```py
[[[ 1.  2.  3.  4.  5.  6.]
  [ 7.  8.  9. 10. 11. 12.]
  [12. 13. 14. 15. 16. 17.]]

 [[ 1.  2.  3.  4.  5.  6.]
  [ 7.  8.  9. 10. 11. 12.]
  [12. 13. 14. 15. 16. 12.]]]
dtype('float64')
```
不指定数组类型（字符串）：
```py
import numpy as np
a = np.array(['I', 'Like' ,'qianqian'])
a
```
```py
array(['I', 'Like', 'qianqian'], dtype='<U8')
```
指定数组类型（字符串）：
```py
import numpy as np
a = np.array(['I', 'Like' ,'qianqian'], dtype=np.string_)
a
```
```py
array([b'I', b'Like', b'qianqian'], dtype='|S8') # S：String；8：数组中最长字符串是8个字母
```

###### 5.8 ndarray数组的生成
从已存在的数组中生成数组的两种方法，`numpy.array`和`numpy.asarray`方法，下面通过一个小案例来区别这两种方法：

`首先创建一个数组作为已存在数组：`
```py
import numpy as np
a = np.array([[1, 2, 3, 4, 5, 6],[7,8,9,10,11,112]])
a
```
```py
array([[  1,   2,   3,   4,   5,   6],
       [  7,   8,   9,  10,  11, 112]])
```
`使用array在原有数组的基础上生成数组（深度拷贝）：`
```py
a1 = np.array(a) # 深拷贝
a1[0, 0] = 0
a
```
```py
array([[  1,   2,   3,   4,   5,   6],
       [  7,   8,   9,  10,  11, 112]])
```
`使用asarray在原有数组的基础上生成数组：（浅拷贝）`
```py
a2 = np.asanyarray(a) # 浅拷贝
a2[0, 0] = 0
a
```
```py
array([[  0,   2,   3,   4,   5,   6],
       [  7,   8,   9,  10,  11, 112]])
```
生成固定范围的数组：

`创建等差数列的数组，指定数量，使用的函数是：linspace(start, stop, num=50, endpoint=True, retstep=False, dtype=None,axis=0)`
```py
import numpy as np
arr = np.linspace(0,21,6) # start:0,序列的起始值; stop:20,序列的终止值; num:5, 要生成的等间隔样例数量, 默认是50。endpoint:序列中是否是否包含stop值，默认是True
arr
```
```py
array([ 0. ,  4.2,  8.4, 12.6, 16.8, 21. ])
```
`创建等差数列的数组，指定步长，使用的函数：arange(start=None, *args, **kwargs)`
```py
import numpy as np
arr = np.arange(0, 20, 2, dtype=np.int64) # step:2,步长；dtype:数据类型
arr
```
```py
array([ 0,  2,  4,  6,  8, 10, 12, 14, 16, 18])
```
`创建等比数列，使用的函数：logspace(start, stop, num=50, endpoint=True, base=10.0, dtype=None,axis=0)`
```py
import numpy as np
# 注意这里是生成10的多少次方
arr = np.logspace(0, 2, 3) # num是要生成等比数列的数量；0、2的意思分别是10的0次方～10的2次方；3：生成3个数
arr
```
```py
array([  1.,  10., 100.])
```