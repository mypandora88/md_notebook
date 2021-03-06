## Markdown语法
### 通用部分：
- 转义字符：\\
- 标题：\#表示
- 字体：\*表示，分别可以表示斜体、粗体、斜粗体
- 分隔线：3个及以上\-表示，最好上下均留空行
- 删除线：2端各加上2个\~
- 无序列表：\*或\+或\-后接空格
- 有序列表：数字加上\.
- 列表中间添加另外一个元素：使用TAB制表符
- 表格：\| 来分列（-:或:-或:-:区分对齐），\-来分行
- 换行：2个空格加回车（严格，有些编辑器只需要回车就行）
- 段落：2行文字之间有空行就是一个新段落
- 块引用：\>表示，2个或以上\>可实现嵌套
- 图片：! \[替代文字](地址 "属性（鼠标悬停时显示）")
- 链接：\[链接文本](网址 "属性（鼠标悬停时显示）")，链接中的空格最好使用%20表示
- 引用式链接：第一部分\[链接文本]\[链接编号]，第二部分可写在未尾\[链接编号]: 网址
- 网址和电子邮件地址：\<网址或邮箱>
- 带链接图片：\[图片格式](网址)
- 脚注：第一部分在需要添加脚注文字后加上\[\^脚注名(数字或单词)]，第二部分可写在未尾\[\^脚注名]: 脚注内容
- 代码块：使用3个反引号\`\`\`把代码包在里面
- 任务列表：\-加空格加上\[ ]，任务完成\[x]
- 公式：行中公式\$z=x+y\$，独立公式\$\$z=x+y\$\$
 
### HTML标签：
- 下划线：\<u>文本\</u>
- 换多行：\<br>

### 基本公式
- 上下标：\^表示上标，\_表示下标，多个字符用{}
$$ x_1^2=(1+e_x)^{-2xy^w} $$
- 括号和分隔符：()、\[\] 和 \| 表示符号本身，使用 \\{\\} 来表示 {}，使用\\left和\\right显示大号的括号和分隔符。如果仅有单边，用\\left.匹配
- 分数：\\frac\{分子\}\{分母\}，如果是单字母，直接\\frac ab
$$ f(x,y,z) = 3y^2z \left( 3+\frac{7x+5}{1+y^2} \right) $$
$$ \left. \frac{d_u}{d_x} \right| _{x=0} $$
- 空格：\\,或者\\;或者\\quad 或者 \\qquad，对应不同宽度
- 开方：\\sqrt \[根指数，省略时为2] {被开方数}
$$ \sqrt{2} \quad and \quad \sqrt[n]{3} $$
- 向量：\\vec{向量}
- 省略号：\\ldots 表示与文本底线对齐的省略号，\\cdots表示与文本中线对齐的省略号，不加最后s表示单省略号
$$ \vec{a} \cdot \vec{b}=0 $$
- 微积分：\\partial表示微分，\\int\_积分下限\^积分上限 {被积表达式}，oint表示不定积分
$$ \partial x^y \quad and \quad \int_0^1 x^2dx $$
- 累加：\\sum\_{下标表达式}\^{上标表达式} {累加表达式}
$$ \sum_{i=1}^n \frac{1}{i^2} $$
- 对数、三角运算符：\\log、\\lg、\\ln、\\sin、\\cos、\\tan、\\cot
- 戴帽符号：\\dot{x}
- 希腊字母：直接输入\\对应的英文（根据首字母判定大小写）
$$ \log a \quad \sin \theta \quad \dot{X} $$
- 加减乘除符号：\\times，\\div，\/，\\pm
$$ x \times y=z \quad x \div y=z \quad x/y=z \quad x \pm y=z $$
- 大于小于号：\\leq，\\geq，\\neq，\\approx
$$ \leq、\geq、\neq、\approx $$
- 上下划线：\\overline{}和\\underline{}
$$ \overline{x^2+a+b} $$

### 希腊字母
|第一列|第二列|第三列|
|----|----|----|
|Α  α  alpha|Ι  ι  iota|Ρ  ρ  rho|
|Β  β  beta|Κ  κ  kappa|Σ  σ, ς  sigma|
|Γ  γ  gamma|Λ  λ  lambda|Τ  τ  tau|
|Δ  δ  delta|Μ  μ  mu|Υ  υ  upsilon|
|Ε  ε  epsilon|Ν  ν  nu|Φ  φ  phi|
|Ζ  ζ  zeta|Ξ  ξ  xi|Χ  χ  khi|
|Η  η  eta|Ο  ο  omicron|Ψ  ψ  psi|
|Θ  θ  theta|Π  π  pi|Ω  ω  omega|


### 使用小技巧：
- 将本地图片转化成网络图片（图片还是存储在本地硬盘上）

步骤：
1. 自己在家用服务器上搭建一个静态html网站
2. 在根目录下建立md_attachments文件夹
3. 图片上传到这个文件夹里面，对应的图片网络地址(**注意后缀的大小写**)为： 
 > ```https://ddns.smpi.top:10000/md_attachments/IMG_0306.png```
 4. 将本地地址修改成上面网络地址就可以了，可以批量替换
 > 替换前：```![](https://ddns.smpi.top:10000/md_attachments/```
 > 
 > 替换后：```![](https://ddns.smpi.top:10000/md_attachments/```

- 字体颜色、字体定义

\<font color=yellow>我是黄色\</font>

\<font face="黑体">我是黑体\</font>

\<font size=5>我是尺寸\</font>

\<font face="逐浪立楷" color=green size=5>我是逐浪立楷，绿色，尺寸为5\</font>
