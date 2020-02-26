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
print(staff.values)
print(type(staff.values))
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200226191219763.png)