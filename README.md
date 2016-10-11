# GMT FAQ

Q：使用psxy或其他类似命令时，出现

    psxy: Mismatch between actual (1) and expected (2) fields near line 10 (skipped)

A：出现该错误的原因是当前命令需要两列数据，而在第10行左右数据只有一列。此时需要人工检查一下第10行附近的数据。需要注意，这里的第10行不一定是准确数字。

-----

Q：在使用地图投影时，为何无法给坐标轴加标签？命令如下::

    gmt psbasemap -R0/10/0/10 -JM10c -B1 -Bx+l"Latitude" -By+"Longtitude" > a.ps

A：从绘图效果中可以看出，“Latitude”和“Longtitude”是没有加进去的。这不是Bug，而是一个Feature。因为对于使用地图投影绘制的地图，从“火车道”边框或标注上的“度”符号都可以直观的知道这是一个地图投影而不是笛卡尔投影。而对于地图投影来说，X方向是经度、Y方向是纬度，是基本常识，给坐标轴加label反而是多此一举，故而对于地图投影来说，坐标轴是不能加label的。如果执意要给坐标轴加label，只能用pstext手动添加。

----

Q：在Windows下写了bat脚本，执行bat脚本时黑屏一闪而过，看不到出错信息。

A：在脚本的最后加上 `pause` 即可

----

Q：出现如下错误:

    Long input record (xxx bytes) was truncated to first xx bytes!

A：出现该错误的原因是输入数据的一行超过特定的长度（一般是512字符），此时GMT会对输入数据做截断。出现该错误的常见原因是在将多个记录通过管道传递给命令时，记录末尾的换行符丢失，导致多个记录连成一行传递给命令。

----

Q：安装GMT后用 `pscoast` 绘图时出现如下错误::

    pscoast: GSHHG version 2.2.0 or newer is needed to use coastlines with GMT.
    Get and install GSHHG from ftp://ftp.soest.hawaii.edu/gshhg/.
    pscoast: Could not find file [GSHHG crude resolution shorelines]
    pscoast: No GSHHG databases available - must abort

A： `pscoast` 能够正常运行的前提是：

1. 在 `$GMTHOME/share/coast` 目录下能够找到GSHHG数据文件（一堆以.nc结尾的文件）
2. GSHHG数据文件有可读权限
3. GSHHG数据文件的版本号大于2.2.0
4. 系统的netCDF软件在编译时支持netCDF4格式

针对以上几点，如果出现了题中所说的错误，可以通过如下方式逐一排除：

1. 检查 `$GMTHOME/share/coast` 目录下是否有GSHHG数据文件
2. 在 `share/coast` 目录下执行 `ls -l` 检查数据文件是否有可读权限
3. 打开 `README.TXT` 里，版本号是否大于2.2.0
4. 终端执行 `nc-config --has-nc4` 以检查netCDF软件是否支持netCDF4格式，若为 `yes` 则表示支持

---

Q：如何让刻度线朝向图的内部？

A：将刻度线的长度设置为负值即可。GMT4 用户可以用 `gmtset TICK_LENGTH -0.2c`，GMT5用户可以用 `gmt set MAP_TICK_LENGTH_PRIMARY -5p` 。

---

Q：如何设置网格线的属性，比如线型、颜色等？
A：GMT5用户可以用 `gmt set MAP_GRID_PEN_PRIMARY 1p,gray,-` 来修改网格线属性。

---

Q：如何将纵坐标上下反转，即 Y 轴从上到下依次增大？
A：设置 `-J` 时把对应轴的长度设置为负值，比如 `-JX10c/-5c` 

---

gsview可以查看中文，ps2raster报错 
最后一行多了-K

---

gsview可以查看中文，ps2raster不报错，不显示中文
ps2raster 或者说 psconvert 本质上是调用了 ghostscript 来实现图片格式转换，-C 的作用是将额外的参数传递给 ghostscript，-sFONTPATH=xxx这个实际上是 ghostscript 的参数。但是我们为了中文支持如果已经写了一个环境变量GS_FONTPATH为C:\Windows\Fonts了，是不是应该全局生效，这个传参就不需要了？

---

特殊符号，如角标，百分号等的表示

---

经纬度表示为度°分′秒″或表示为ddd.x°/在GMT绘图时，如何在经纬度轴上添加上N,E的标注

---

如何地图色填图
分段数据前 > -G<color>

---

请问GMT可以在画站点的同时把站点名也标注上吗？

---

surface插值后的黑色区域如何处理？

---

makecpt的-D强制把超过范围的值设为最大，最小值

---

如何控制边框的线条的粗细

---
grdimage出现密集格网
xyz2grd的格网间距选错了

---

如何在JX投影下表示地理坐标

---

如何去掉某一方向上的刻度线，只保留边框？
两遍psbasemap

---

关于缺少数据的问答栏。比如国界、省界、海岸线、国内城市坐标这一类。

---

GMT的输入数据有什么格式要求/画线首尾相连了
分段数据用>隔开

---

如何提取自己数据的某一列/某一行/计算行数
awk
---

如何提取多边形内/缓冲区内的数据
gmtselect

---

从Linux到windows的txt脚本文件中文乱码
改文件编码格式为ANSI/GB2312

---

awk里怎么能把数据按照科学计数法的格式输出，而不是按纯数值。
 AWK printf


32位XP系统下GMT的安装

---
GMT Fatal Error: No SI/US keyword in GMT configuration file <COLOR_BACKGROUND = black>

---

Option -M is deprecated

---

Z-slice with dz=0

---

grdimage: Intensity file has improper dimensions! /重采样时格网个数差1行1列

---

ps2raster -A -P earth.ps 
earth.ps: GMT PS format detected but file is not finalized. Maybe a -K in excess? No output created."

---

mismatch between actual (2) and expected (3) fields near line 3811
