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