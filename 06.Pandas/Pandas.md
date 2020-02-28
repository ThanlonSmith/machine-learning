###### 6.1 Pandas介绍
Pandas由WesMcKinney开发，是一种专门用于数据挖掘的库。其以Numpy库为基础，借力Numpy模块在计算方面性能高的优势来增强性能。也基于matplotlib库，能够简便绘图，并且有着独特的数据结构。
###### 6.2 使用Pandas的优势
Numpy已近可以帮助我们解决问题，能够结合Matplotlib解决部分数据的展示等问题，那为什么要使用Pandas，使用它的优势主要有以下几个部分：
- 增强图表的可读性
- 便捷的数据处理能力
- 读取文件特别方便
- 封装了Matplotlib的画图和Numpy的计算

###### 6.3 Pandas数据结构
Pandas一共有三种数据结构，分别是Series、DataFrame和MultiIndex。<font color='red'>**三者分别是一维数据结构、二维数据结构和三维数据结构**</font>。

**➢ Series结构**

Series是一个类似于一维数组结构，它能够保存任何数据类型的数据，如整数、字符串、浮点数等，<font color='red'>**主要由一组数据和与之相关联的数组两部分组成**</font>。

Series的创建(通过已有数据创建)：
```py
import pandas as pd
# data：传入的数据，可以是ndarray、list等
# index：索引，必须是唯一且与数据的长度相等，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
# dtype：数据类型
pd.Series(data=None, index=None, dtype=None)
```
- 指定内容默认索引创建
```py
import pandas as pd
import numpy as np
pd.Series(data=np.arange(10))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226190604648.png)
- 指定索引创建
```py
import pandas as pd
pd.Series(data=[6, 7, 8, 9, 10], index=[0, 1, 2, 3, 4])
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226190429355.png)
- 通过字典数据创建
```py
import pandas as pd
pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226190341382.png)
为更方便地操作Series对象中的索引和数据，Series中提供两个属性，分别是index和values。Series的属性：
- index
```py
import pandas as pd
staff = pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
print('职员的姓名：',staff[0])
print('职员的年龄：',staff['age'])
print(staff.index)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226185011234.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- values
```py
import pandas as pd
staff = pd.Series(data={'name': 'thanlon', 'age': 24, 'address': '中国上海'})
print(staff.values) # <class 'numpy.ndarray'>
```

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220033836.png)

**➢ DataFrame结构：**

DataFrame是一个类似于二维数组或表格的对象，既有行索引和列索引。DataFrame的创建：
```py
import pandas as pd
# index：行标签，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
# columns：列标签，如果没有传入索引参数，则默认会自动创建一个从0～N的整数索引
pd.DataFrame(data=None, index=None, columns=None)
```
`例一：`
```py
import pandas as pd
import numpy as np
pd.DataFrame(data=np.random.randn(2, 3))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226220012790.png)
`例二：`
```py
# 分别使用numpy和pandas生成学生的成绩表，生成10个同学的6个科目的成绩
import numpy as np
score = np.random.randint(0, 100, (10, 6))
print(score)
score_df = pd.DataFrame(score)
score_df
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226215940943.png)
增加行列索引：
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
print(score)
score_df = pd.DataFrame(score)
print(score_df)
# 构建行索引序列
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
# 构建列索引序列
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
# 添加行索引
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226215857988.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
DataFrame的属性：
- shape：查看几行几列
```py
'''
查看几行几列
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.shape)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221157145.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- index：获取行索引列表
```py
'''
获取行索引列表
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.index)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221304861.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- columns：获取列索引列表
```py
'''
获取列索引列表
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.columns)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226221350659.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- values：获取数组的值
```py
'''
获取数组的值
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
print(data.values)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226223102602.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- T：转置
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.T
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225156343.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- head(n)：查看前n行，<font color='red'>**如果不传入n，默认是5行。如果数据没有5行，则默认查看所有行。**</font>
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.head(4)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225418173.png)
- tail(n)：查看后n行，<font color='red'>**如果不传入n，默认是5行。如果数据没有5行，则默认查看所有行。**</font>
```py
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data.tail(2)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226225603674.png)

DataFrame索引的设置：
- 修改行列索引值
```py
'''
必须整体全部修改，不能使用索引方式改局部，如data.index[0] = '学生_1'
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
stu1 = ['学生_'+str(i+1) for i in range(score_df.shape[0])]
data.index = stu1
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226235552359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- 重设索引
```py
'''
使用reset_index(drop=False)，可以用来设置新的下标索引，drop：默认是False，不删除原来的索引，如果为True，删除原来的索引值
不删除原来的索引
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data = data.reset_index()
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227000425781.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
```py
'''
使用reset_index(drop=False)，可以用来设置新的下标索引，drop：默认是False，不删除原来的索引，如果为True，删除原来的索引值
删除原来的索引
'''
import numpy as np
import pandas as pd
score = np.random.randint(60, 100, (9, 6))
score_df = pd.DataFrame(score)
subjects = ['语文', '数学', '英语', '历史', '政治', '数学']
stu = ['学生'+str(i+1) for i in range(score_df.shape[0])]
data = pd.DataFrame(data=score,  index=stu, columns=subjects)
data = data.reset_index(drop=True)
data
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227000436682.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
- 以某列值设置为新的索引
```py
'''
设置新的索引：set_index(keys, drop=True)
keys：列索引名称或列索引名称的列表
drop：boolean类型，默认是True，当做新的索引，删除原来的列
以月份设置新的索引
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017,2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index('month') # 设置单个索引
df
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227092651430.png)
```py
'''
设置新的索引：set_index(keys, drop=True)
keys：列索引名称或列索引名称的列表
drop：boolean类型，默认是True，当做新的索引，删除原来的列
以年份和月份设置新的索引
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month']) # 设置多个索引，要使用列表
df 
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227092707450.png)

**➢ MultiIndex结构**

MultiIndex是三维的数据结构，即多级索引，也称为层次化的索引。<font color='red'>**层次化索引是pandas的重要功能，可以在Series、DataFrame对象上拥有2个及其以上的索引**</font>。除了通过修改DataFrame数据结构变成MulitiIndex结构，还可以直接创建。

MultiIndex的创建：
```py
import pandas as pd
arrays = [['thanlon', 'kiku', 'kili'], [22, 23, 24]]
pd.MultiIndex.from_arrays(arrays=arrays, names=('name', 'age'))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227104914950.png)
MultiIndex的特性：
```py
'''
index
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105622126.png)
```py
'''
index.names
'''
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.names
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105702906.png)
```py
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.levels
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105730475.png)
```py
import pandas as pd
df = pd.DataFrame({
    'month': [1, 2, 3, 4],
    'year': [2017, 2018, 2019, 2020],
    'sale': [66, 77, 88, 99]
})
df = df.set_index(['year', 'month'])
df.index.codes
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227105805806.png)

**➢ Panel结构(Panel已被废弃，这里只作了解)**

Panel是MultiIndex的前身，Panel的创建：
```py
'''
pandas.Panel(data-None, items=None, major_axis=None, minor_axis=None)：存储3维数组的Panel结构
data：ndarray或者DataFrame，表示整体的数据
items：索引或类似数组的对象，axis=0
major_axis：索引或类似数组的对象，axis=1
minor_axis：索引或类似数组的对象，axis=2
'''
import pandas as pd
import numpy as np
# 24个数，第一个维度是4，第二个维度是3，第三个维度是2，三维
data = np.arange(24).reshape(4, 3, 2)
items = list('ABCD')  # ['A', 'B', 'C', 'D']
major_axis = pd.date_range('20200227', periods=3) # DatetimeIndex(['2020-02-27', '2020-02-28', '2020-02-29'], dtype='datetime64[ns]', freq='D')
minor_axis = ['first', 'second']
pd.Panel(data=data, items=items, major_axis=major_axis, minor_axis=minor_axis)
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200227130454778.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
Panel数据的查看：
```py
 import pandas as pd
import numpy as np
# 24个数，第一个维度是4，第二个维度是3，第三个维度是2，三维
data = np.arange(24).reshape(4, 3, 2)
items = list('ABCD')  # ['A', 'B', 'C', 'D']
major_axis = pd.date_range('20200227', periods=3) # DatetimeIndex(['2020-02-27', '2020-02-28', '2020-02-29'], dtype='datetime64[ns]', freq='D')
minor_axis = ['first', 'second']
p = pd.Panel(data=data, items=items,
             major_axis=major_axis, minor_axis=minor_axis)
p[:, :, 'first']  # :表示取所有
p['A', :, :]
```

###### 6.6 Pandas绘图
**➢ Pandas.Series绘图**

绘制折线图：
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='line')  # s.plot.line()，s.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228205458917.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
绘制柱状图：
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='bar')
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020022821033337.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
s = pd.Series(data=data)
print(s)
s.plot(kind='barh')
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228210426563.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
绘制直方图：
```py
import pandas as pd
import numpy as np
import random
data = []
for i in np.arange(0, 100, 10):
    data.append(random.randint(10, 20))
data = np.random.normal(1.75, 1, 10000) 
s = pd.Series(data=data)
print(s)
s.plot(kind='hist')
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228213939462.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
**➢ Pandas.DataFrame绘图**

绘制折线图：
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 2)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='line')  # df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228201352644.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
绘制柱状图：
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='bar')  # df.plot.line()，df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228212151840.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
df = pd.DataFrame(data=data)
df.plot(kind='barh')  # df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228212400359.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
绘制直方图：
```py
import pandas as pd
import numpy as np
data = np.random.randn(10, 3)  # 从标准动态分布中返回一个或多个样本值
print(data)
df = pd.DataFrame(data=data)
print(df)
df.plot(kind='hist')  # df.plot()函数的参数kind默认是'line'
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200228215053951.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)