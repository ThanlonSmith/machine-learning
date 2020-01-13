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