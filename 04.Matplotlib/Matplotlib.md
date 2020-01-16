##### 4. Matplotlib
###### 4.1 初识Matplotlib
Matplotlib是一种可视化工具，可视化工具是数据挖掘中的关键辅助工具，可以清晰地将数据展现给我们，帮助我们调整分析方法。Matplotlib能够将数据进行可视化，更加直观的呈现给我们，使数据更加客观、更具有说服力。
###### 4.2 基础的绘图功能
matplotlib.pyplot模块包含了一系列类似于matlab的画图函数，使用的时候只需要导入：`import matplotlib.pyplot as plt`。

图形回执流程：
- 创建画布：`plt.figure()`
- 绘制图像：`plt.plot(x,y)`
- 显示图像：`plt.show()`

例：展示上海一周的天气温度

`参考代码：`	
```py
import matplotlib.pyplot as plt
# 创建画布
plt.figure(figsize=(8,4),dpi=100)
# 绘制上海一周的天气温度折线图
plt.plot([1,2,3,4,5,6,7],[11,13,15,17,8,4,3])
# 显示图像
plt.show()
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200113120941521.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

例２：画出某城市11点～12点这１小时内的每分钟的温度变化折线图，温度范围在15～18度之间（某城市温度变化图）

`参考代码：`	
```py
# 导入所需要模块
import random,matplotlib.pyplot as plt
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 创建画布
plt.figure(figsize=(8,4),dpi=100)
# 绘制图像
plt.plot(x,y)
# 展示图像
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200113133722304.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
例３：添加自定义ｘ和ｙ刻度

- ｘ要显示的刻度：`plt.xticks(x,**kwargs)`
- ｙ要显示的刻度：`plt.xticks(y,**kwargs)`

`参考代码：`
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=100)
# 绘图图像
plt.plot(x,y)
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::5],x_ticks_lable[::5]) # 坐标的刻度不可以通过字符串刻度进行修改，注意先修改成数字，再用字符串进行替换
plt.yticks(y_ticks_lable[::5])
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200114102134970.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
matplotlib是支持中文的，只是在配置信息里没有中文字体的相关信息。所以，我们需要解决中文显示的问题，解决方案１(这里使用ubuntu linux平台为例)：
```py
# 下载simhei字体
thanlon@thanlon-master:~$ wget http://z1.zhaodll.com:81/font/s/simhei.ttf.zip
thanlon@thanlon-master:~$ unzip simhei.ttf.zip
# 将字体拷贝到/usr/share/fonts/目录下
thanlon@thanlon-master:~$ sudo cp simhei.ttf /usr/share/fonts/
# 激活虚拟环境
thanlon@thanlon-master:~$ source PycharmProjects/venv/machine-learning/bin/activate
# 查看matplotlib配置文件的位置和配置文件的名称
(machine-learning) thanlon@thanlon-master:~$ ipython
Python 3.7.5 (default, Nov 20 2019, 09:21:52) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.11.1 -- An enhanced Interactive Python. Type '?' for help.

In [1]: import matplotlib as mpl                                                                              

In [2]: mpl.get_configdir()                                                                                   
Out[2]: '/home/thanlon/.config/matplotlib'

In [3]: mpl.matplotlib_fname()                                                                                
Out[3]: '/home/thanlon/.config/matplotlib/matplotlibrc'

In [4]: 
# 创建配置文件
thanlon@thanlon-master:~$ vim .config/matplotlib/matplotlibrc
# 键入下面的内容，记得重启电脑生效
thanlon@thanlon-master:~$ cat .config/matplotlib/matplotlibrc
font.family:sans-serif
font.sans-serif:SimHei
axes.unicode_minus:False
```
`成功解决中文显示问题：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200114174447109.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
解决方案２：
在Python脚本中动态设置matplotlibrc，可以避免由于改变配置带来的问题。有时候，字体更改后会导致坐标轴中的部分字符无法显示，此时需要更改axes.unicode_minus参数：
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
from pylab import mpl
# 设置中文字体
mpl.rcParams['font.sans-serif'] = ['SimHei']
#  设置正常显示符号
mpl.rcParams['axes.unicode_minus'] = False
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=100)
# 绘图图像
plt.plot(x,y)
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::5],x_ticks_lable[::5]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
# 图像显示
plt.show()
```
例４：以网格的方式显示

`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=100)
# 绘图图像
plt.plot(x,y)
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::5],x_ticks_lable[::5]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200114174826890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
例５：添加描述信息，添加x和y轴以及标题的描述信息，设置图像中字体的大小显示

`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=120)
# 绘图图像
plt.plot(x,y)
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::10],x_ticks_lable[::10]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
plt.xlabel('时间',fontsize=10) # 设置x轴描述信息和字体大小
plt.ylabel('温度',fontsize=10) # 设置y轴描述信息和字体大小
plt.title('中午12点整到13点整之间的温度变化',fontsize=10) # 设置标题轴描述信息和字体大小
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200115010303975.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
例６：图像保存
图像保存使用到	`plt.savefig('tmp.png')`，在使用`plt.show()`显示图像后会figure资源，所以在显示图像之后保存图像，就会保存一个空的图像。所以，我们需要在显示图像之前保存图像。
`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(60)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=120)
# 绘图图像
plt.plot(x,y)
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::10],x_ticks_lable[::10]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
plt.xlabel('时间',fontsize=10) # 设置x轴描述信息和字体大小
plt.ylabel('温度',fontsize=10) # 设置y轴描述信息和字体大小
plt.title('中午12点整到13点整之间的温度变化',fontsize=10) # 设置标题轴描述信息和字体大小
# 保存图像
plt.savefig('/home/thanlon/tmp.png') # 保存到制定目录
# 图像显示
plt.show()
```
`绘制的效果图与例５是一致的，这里查看一下保存的图像：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200115012133569.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

例７：在一个坐标系中绘制多个图像

`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(50)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=120)
# 绘图上海温度的折线图
plt.plot(x,y)
# 再增加一条北京的温度的数据
y_shanghai = [random.uniform(20,30) for i in x]
# 绘制北京温度的折线图
plt.plot(x,y_shanghai) # r表示红色，linestyle如果是空字符串，不会显示图像
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::10],x_ticks_lable[::10]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
plt.xlabel('时间',fontsize=10) # 设置x轴描述信息和字体大小
plt.ylabel('温度',fontsize=10) # 设置y轴描述信息和字体大小
plt.title('上海市和北京市中午12点到13点之间的温度变化',fontsize=10) # 设置标题轴描述信息和字体大小
# 保存图像
# plt.savefig('/home/thanlon/tmp.png') # 保存到指定目录
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200115091814824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
例８：在一个坐标系中绘制多个图像并设置图像风格

`颜色字符`：r表示红色，g表示绿色，b表示蓝色，w表示白色，c表示青色，m表示洋红，y表示黄色，k表示黑色。

`风格`：`-`表示实线，`- -`表示虚线，`-.`表示点划线，`:`表示点虚线，`''`表示留空、空格。

`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(50)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=120)
# 绘图上海温度的折线图
plt.plot(x,y)
# 再增加一条北京的温度的数据
y_shanghai = [random.uniform(20,30) for i in x]
# 绘制北京温度的折线图
plt.plot(x,y_shanghai,linestyle=':',color='r') # r表示红色，linestyle如果是空字符串，不会显示图像
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::10],x_ticks_lable[::10]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
plt.xlabel('时间',fontsize=10) # 设置x轴描述信息和字体大小
plt.ylabel('温度',fontsize=10) # 设置y轴描述信息和字体大小
plt.title('上海市和北京市中午12点到13点之间的温度变化',fontsize=10) # 设置标题轴描述信息和字体大小
# 保存图像
# plt.savefig('/home/thanlon/tmp.png') # 保存到指定目录
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020011509191939.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
例９：在一个坐标系中绘制多个图像并添加图例

位置的选择：
| 位置字符串   | 位置代码 |
| ------------ | -------- |
| best         | 0        |
| upper right  | 1        |
| upter left   | 2        |
| lower left   | 3        |
| lower right  | 4        |
| right        | 5        |
| center left  | 6        |
| center right | 7        |
| lower center | 8        |
| upper center | 9        |
| center       | 10       |
`参考代码：`	
```py
# 导入模块
import random
import  matplotlib.pyplot as plt
# 数据准备
x = range(45)
y = [random.uniform(15,18) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=120)
# 绘图上海温度的折线图
plt.plot(x,y,label='上海')
# 再增加一条北京的温度的数据
y_shanghai = [random.uniform(20,30) for i in x]
# 绘制北京温度的折线图
plt.plot(x,y_shanghai,linestyle=':',color='r',label='北京') # r表示红色，linestyle如果是空字符串，不会显示图像
# 构造ｘ轴刻度标签
x_ticks_lable = ['12点{}分'.format(i) for i in x]
# 构造ｙ轴刻度标签
y_ticks_lable =  x
# 修改ｘ,y轴坐标的刻度显示
plt.xticks(x[::10],x_ticks_lable[::10]) # 坐标的刻度不可以通过字符串刻度进行修改
plt.yticks(y_ticks_lable[::5])
plt.grid(True,linestyle = '--',alpha = 0.5) # True表示显示；linestyle表示显示的方式，如这里的虚线；alpha表示图形的透明度
plt.xlabel('时间',fontsize=10) # 设置x轴描述信息和字体大小
plt.ylabel('温度',fontsize=10) # 设置y轴描述信息和字体大小
plt.title('上海市和北京市中午12点到13点之间的温度变化',fontsize=10) # 设置标题轴描述信息和字体大小
# 显示图例
plt.legend(loc='best') # 自动选择最好的位置显示
# 保存图像
# plt.savefig('/home/thanlon/tmp.png') # 保存到指定目录
# 图像显示
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200115095523604.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

例 10：在多个坐标系中绘制多个图像

`参考代码：`	
```py
# 导入模块
import matplotlib.pyplot as plt
import random
# 准备数据
x = range(45)
y_shanghai = [random.uniform(15,20) for i in x]
y_beijing  = [random.uniform(20,30) for i in x]
# 创建画布
fig,axes = plt.subplots(nrows=1,ncols=2,figsize=(16,5),dpi=100)
# 绘制图像
axes[0].plot(x,y_shanghai,label = '上海')
axes[1].plot(x,y_beijing,label='北京',color='r',linestyle='--')
# 添加x与y轴的刻度
x_ticks_label = ['12点{}分'.format(i) for i in x] 
axes[0].set_xticks(x[::5])
axes[0].set_yticks(x[::5])
axes[0].set_xticklabels(x_ticks_label[::5])
axes[1].set_xticks(x[::5])
axes[1].set_yticks(x[::5])
axes[1].set_xticklabels(x_ticks_label[::5])
# 添加网格显示
axes[0].grid(True,linestyle='--',alpha=0.5)
axes[1].grid(True,linestyle='--',alpha=0.5)
# 显示图例
axes[0].legend(loc=0)
axes[1].legend(loc=0)
# 添加描述信息
axes[0].set_xlabel('时间')
axes[0].set_ylabel('温度')
axes[0].set_title('中午12点到13点上海的温度变化图',fontsize = 15)
axes[1].set_xlabel('时间')
axes[1].set_ylabel('温度')
axes[1].set_title('中午12点到13点北京的温度变化图',fontsize = 15)
# 图像保存
plt.savefig('/home/thanlon/tmp.png')
# 显示图像
plt.show()
```
`绘制的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020011521004815.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)

###### 4.3 常见图像的绘制
Matplotlib能够绘制<font color='red'>**折线图、散点图、柱状图、直方图、饼图**</font>。在选择以何种方式展示数据时，我们需要明确各种统计图的意义。

折线图：以折线的上升或下降来表示统计数量的增减变化的统计图。特点是能够显示数据的变化趋势，反应事物的变化情况。使用的的方法是：`plt.plot(x,y)`。

`参考代码：`
```py
# 导入相关模块
import matplotlib.pyplot as plt
import random
# 准备数据
x = range(9)
y = [random.randint(0,9) for i in x]
# 绘制画布
plt.figure(figsize=(8,4),dpi=100)
# 添加x，y刻度的显示
plt.xticks(x[::1])
plt.yticks(x[::1])
# 绘制图像
plt.plot(x,y)
# 添加网格显示
plt.grid(True,linestyle='--',alpha=0.5)
# 图像保存
plt.savefig('/home/thanlon/tmp.png')
# 图像显示
plt.show()
```
`折线图的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200116104859812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
散点图：用两组数据构成多个坐标点，考察坐标点的分布，判断了两变量之间是否存在某种关联，以及总结坐标点的分布模式。使用到的方法是：`plt.scatter(x,y)`。

`参考代码：`
```py
# 导入相关模块
import matplotlib.pyplot as plt
import random
# 准备数据
x = range(40)
y = [random.randint(1,49) for i in x]
# 绘制画布
plt.figure(figsize=(10,4),dpi=100)
# 添加x,y轴刻度的显示
plt.xticks(x[::1])
plt.yticks(range(50)[::5])
# 设置图像的标题
plt.title('常见图像的之散点图的绘制')
# 绘制图像
plt.scatter(x,y)
# 图像的显示
plt.show()
```
`散点图的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200116123150730.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
柱状图：排列在工作表的列或行中的数据可以绘制到柱状图中，特点是很容易看出数据的大小，适用于统计和对比数据。使用的方法是：`plt.bar(x,width,align='center',**kwargs)`。

`参考代码：`
```py
import matplotlib.pyplot as plt
# 数据的准备
x_movie_names = ['唐人街探案3', '姜子牙', '囧妈', '中国女排', '紧急救援', '熊出没·狂野大陆', '急先锋', '我在时间尽头等你', '妙先生', '抵达之谜']
x = range(len(x_movie_names))
y = [722193, 357767, 246846, 169509, 168038, 93609, 84625, 32234, 29082, 22227]
# 绘制画布
plt.figure(figsize = (15, 5), dpi = 100)
# 绘制图像
plt.bar(x, y, color = ['b', 'r' , 'g', 'y', 'c', 'm', 'y', 'k', 'c', 'g'], width=0.6)
# 添加x，y刻度的显示
# plt.xticks(x[::1], x_movie_names[::1])
plt.xticks(x, x_movie_names)
# 设置标题
plt.title('猫眼电影最受期待榜榜单', fontsize = 15)
# 添加网格
plt.grid(True, linestyle='--', alpha=0.5)
# 图像的显示
plt.show()
```
`柱状图的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200116134901255.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)
饼图：用于表示不同分类的占比情况，通过弧度大小来对比各种分类。使用的方法是：`matplotlib.pyplot.pie()`。

`参考代码：`
```py
import matplotlib.pyplot as plt
# 绘制画布
plt.figure(figsize=(4,4), dpi=100)
# 绘制图像
plt.pie([1, 2, 3, 10, 6, 7], labels=['娱乐', '育儿', '饮食', '房贷', '交通', '其它'], colors=['b', 'r' , 'g', 'y', 'c', 'm'], explode=[0, 0, 0, 0.1, 0, 0], autopct='%1.1f%%', shadow=False, startangle=10)
# 设置标题
plt.title("2020年2月份家庭支出")
# 图像显示
plt.show()
```
`饼图的效果图：`
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200116144646651.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L1RoYW5sb24=,size_16,color_FFFFFF,t_70)