## Catia软件使用
CATIA是法国达索飞机公司开发的高档CAD/CAM软件。CATIA软件以其强大的曲面设计功能而在飞机、汽车、轮船等设计领域享有很高的声誉。CATIA的曲面造型功能体现在它提供了极丰富的造型工具来支持用户的造型需求。比如其特有的高次Bezier曲线曲面功能，次数能达到15，能满足特殊行业对曲面光滑性的苛刻要求。

### 安装
英文版win10系统安装后出现问号解决办法：
- 将 Region 里面的 Regional format 由 Recommended 改成 Chinese
- 将 Administrative language settings 里面的 non-Unicode 由 English 改成 Chinese

### 使用技巧
- 可以看左下角的提示
- 如果位置搞乱了，可以在自定义-工具栏里面点恢复位置
- 如果想草图旋转个90度，可以在进入草图之前点草图定位，V代表竖直方向，H代表水平方向

#### 鼠标使用
- 左键——选择
- 滚轮长按——移动
- 滚轮长按+右键按一下——上下拖动，放大缩小
- CTRL+滚轮
- 滚轮长按+右键长按——旋转
- 滚轮+CTRL
- 画图时鼠标点2下，可以达到重复使用这个命令的目的

#### 快捷键设置
工具——自定义——命令——加速器里面设置（可以双击命令快速定位）

- 功能区
> - 零件设计 ALT+1
> - 创成式外形设计 ALT+2
> - 装配设计 ALT+3
> - 工程制图 ALT+4

- 草图工具类
> - 进入草图 ALT+e
> - 退出草图 ALT+q
> - 圆 ALT+c
> - 矩形 ALT+r
> - 轮廓（画多段线）ALT+d
> - 约束 ALT+s
> - 定义的约束 CTRL+ALT+s
> - 构造/标准元素（虚实转换） ALT+g
> - 镜像 ALT+w
> - 草图分析 ALT+a
> - 快速修剪 ALT+x
> - 投影3D元素 ALT+t
> - 直线 ALT+L

- 视图类
> - 显示/隐藏 ALT+space
> - 法线视图（让草图正对着你，非草图模式时选择面，让面的垂直方向面对你）ALT+f
> - 全部适应（非草图模式时让图形剧中）ALT+z
> - 交换可视空间 ALT+j

- 三维绘图
> - 凸台 ALT+I
> - 倒圆角 ALT+o
> - 倒斜角 ALT+p

- 工程制图
> - 尺寸标注 CTRL+d
> - 角度标注 CTRL+a
> - 半径标注 CTRL+r
> - 直径标注 CTRL+ALT+r
> - 格式刷 ALT+m

- 装配设计
> - 快速多实例化 CTRL+d（系统自带）
> - 多实例化 CTRL+e（系统自带）

- 通用
> - 图形更新 CTRL+u（系统自带）
> - 隐藏/显示树 F3（系统自带）
> - 属性 ALT+enter（系统自带）
> - 重复命令 CTRL+y（系统自带）

### 草图工具
#### 约束
- 完合约束之后，会变绿色，紫色表示过约束
- 可约束长度、角度（先点一条线、再点另外一条线）
- 点2个点（或线）之后，右键相合（可以把2个对象重合起来）
- 也可以同时选中多个对象，一起做约束
- 如果要使用对称，先选择2边的线，再选择中间的线
- 固联约束：这个曲别针命令的功能是将所选图形固定的联合为一个整体，效果有二：a、所选的各图形之间的相对几何关系不可变更；b、所选图形的尺寸不可变更。下面举例说明：

### 工程图设计
#### 图框
编辑——图纸背景——几何图形创建

#### 视图
先插入正视图，再插入投影视图（垂直方向）和辅助视图（非垂直方向）

截面视图：在正视图上单击2点，并拖出方向后双击

偏移剖视图：创建

编辑——图纸背景——插入图框

#### 标注
修改标注尺寸：先点选点修改的尺寸，再点选起点终点之类的

形位公差标注：跟基准特征在一起

偏差：+0.035/0表示上偏差0.035，下偏差0

属性：属性中可以插入一些特殊符号，比如直径符号，在尺寸文本里面

标注零件序号：给零件编号

插入表：绘制表格

插入轴线、中心线：虚线，辅助线

创建区域填充：给图形填充

插入箭头

插入——生成——物料清单

### 实体设计
#### 拔模、盒体
拔模：将原来垂直向下的面变成斜向下  
盒体：将实体变成有一定厚度的盒体

#### 变换特征
包括平移、旋转、镜像、对称（镜像并删除原文件）

#### 变化特征
矩形阵列（可以选2个方向）、圆形阵列、缩放（以点缩放就是整体绽放，以面就是某个方向进行缩放）、仿射（同时对3个方向进行缩放）

### 创成式外形设计
点面复制——用来在曲线上生成多个等距点和法向平面

端点——用来创建极值点

### 装配设计
#### 原则
自上而下设计，也就是经常听起来高大上的Top-down 设计。简单的说就是先在软件中将装配体的**结构树**做出来，然后再对具体的分总成进行详细设计，在进行分总成设计时采用同样的自上而下设计，直到最底层的零件为止。

#### 层级
产品（product）——部件（componet）——零件（part）

#### 装配特征
可以进行孔槽的操作

### 其它
#### 测量间距
可以选择测量数据是一次性显示还是一直显示

#### 标注
插入——标注——文本

#### 应用材料
先选择实体，再应用材料（如果不显示，可能是视图模式不对）

#### 颜色、透明度
选中实体，右键属性选择颜色和透明度

#### CAD图形导入CATIA中
步骤：
- 最好把CAD保存为低版本，如2000。关闭CAD文件，直接把CAD文件的图标拖入CATIA中。此时CATIA会自动把CAD图纸转换成工程图。稍稍等一下就可以了。
- 转换完毕后，用鼠标左键圈选图纸，全部选中，然后CTRL+C。
- 切换到CATIA的草绘界面，CTRL+V，这时CAD就导入草绘中了。
> 注意：导入后最好先不要进行其他操作，直接点击工具栏上的回形针图标（固联），弹出窗口后直接点击确定。（这么操作是防止在以后的步骤中由于操作不当使草图中的元素移动。固联后用鼠标拖动导入的CAD文件，各部分元素会整体移动而不影响编辑。）

- 如果拷贝的对象不显示，可以右键点击该对象，定义工作对象。