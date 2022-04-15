## AutoLisp编程
### 简介
AutoLisp 是由 Autodesk 公司开发的一种 LISP 程序语言， LISP 是 List Processor 的缩写，有时中文翻译成 表处理语言 。这种语言和 Python 、 Javascript 、 Matlab 等语言类似， LISP 也是一门解释型语言。 AutoCAD 软件中内置了 AutoLisp 语言解释器。因此，只要安装了 AutoCAD ，就可以直接执行 AutoLisp 程序。

### 特点
- AutoLisp 语言是一种函数式语言，一切都以函数给出，没有语句的概念和语法结构。
- AutoLisp 语言是表处理语言，函数的调用是通过表来完成的。表通过圆括号 () 来定义。
- AutoLisp 的程序和数据都是表结构，所以程序可以当作数据来处理，数据也可以当作程序来处理。

### 第一段 AutoLisp 脚本
AutoCAD 的控制台中，如果直接输入字母，可以调用 AutoCAD 命令。如果输入括号，则可以使用 AutoLisp 。

打开 AutoCAD ，在控制台（即输入命令的文本框）中输入```(alert "Hello, world!")```回车提交，发现弹出一个警告对话框，里面写着 Hello, world! 。

本程序中我们使用 AutoLisp 语言只写了一行语句。这行语句被圆括号 () 括起来，形成了一个所谓的 表 （也就是我们所说的“表处理语言”中的“表”）。这个 表 中有两个元素， alert 和 "Hello, world!" 。 其中 alert 是函数名，表示在这个语句中，我们要调用 alert 这个函数。 "Hello, world!" 是一个字符串（字符串是一种数据类型）。这个字符串作为 alert 这个函数的参数。

### LSP文件运行
用文本编辑软件新建一个文本文件，命名为 ```hello_world.lsp```，在文本文件中输入如下代码

```
(defun c:hello(/)
(alert "Hello, world!"))
```
打开 AutoCAD ，输入命令```appload```，加载刚创建的lsp文件，输入命令hello运行脚本。

在本例中， defun 定义了一个 lisp函数 。在 AutoLisp 中，以 c: 开头的函数表示注册一条可执行的命令。本例中 c:hello 就表示注册一个命令 hello ，这样可以直接运行命令。

```
(defun c:hello(/ name)  
(setq name (getstring "What's your name? "))  
(setq msg (strcat "Hello, " name))  
(write-line msg))
```
这段程序会要求输入名字，赋值给name，再将名字输出来（非弹出，而是显示在命令行）。

### 查看AutoCAD命令
以 "line" 命令为例，首先我们要确定输入哪些参数。打开 AutoCAD ，在控制台中输入line回车，看到提示输入一个点，这就是我们要给出的第一个参数。

按提示输入点后，又提示再输入一个点，这是我们要给出的第二个参数。

输入好第二个点后，提示再输一个点，会再画一条线，这时我们不想继续画，输入回车结束命令。这是我们要给出的第三个参数。

这样，我们就确定了要输出的三个参数，分别是两个点和一个回车。因此本例中，我们用两个列表来表示点，用一个**空字符串来表示回车**（ AutoLisp 的约定）。

```(command "line" '(-120 0) '(120 0) "")```

### 函数
- defun 函数，用于定义用户命令。
> ```(defun [函数名](/ [局部变量1] [局部变量2]) [表达式1] [表达式2] ... )```
> 
> 函数名： 函数名在定义时，如果采用 c: 开头，表示注册一个 AutoCAD 命令
> 
> 局部变量： 局部变量的含义是，这一变量在函数执行完毕后就被释放
> 
> 表达式： 当函数被调用时，表达式的内容被执行。

- setq 函数，用于为变量赋值。
> ```(setq [变量名1] [值1] [变量名2] [值2] ...)```
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415221101.png)

- getint 函数和一系列相关的 get 类输入函数，用于程序与用户交互。
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415221429.png)

- if 函数，用于条件判断。
> ```(if [布尔表达式] [条件为真执行] [条件为假执行])```
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415221514.png)

- command 函数，用于调用 AutoCAD 命令。
> ```(command [命令名] [参数1] [参数2] ...)```
> 
> 命令名： 即 AutoCAD 命令的名字，用一个字符串来表示，也就说要用双引号引起来。在本例中，我们使用了 "line" 、 "text" 、 "circle" 、 "arc" 几个命令。
> 
> 参数： 即在执行命令时，所需要用户输入的参数。

- osnap 函数，用于捕捉点。
> (osnap [点] [捕捉模式])
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415223818.png)

- rtos 函数和一系列字符串转换函数，用于字符串与数字转换。
> ```(rtos [实数] 2 [小数位数])``` 其中 2 就表示十进制模式
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415224005.png)

- polar 函数和一系数相关的图形处理函数，用于确定点的位置、距离、角度等。
> polar 是用极坐标的方式求点坐标的函数
> 
> ```(polar [基点] [方向角] [距离])```
> 
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415224118.png)

- entmake 函数
> 这个函数用于在 AutoCAD 中创建实体。该函数应用范围十分广泛。与教程上篇不同，这里没有采用 command 函数来创建实体，而是采用 entmake 函数，可以真接操作更底层的模型，执行更加快速。
> 
> ```(entmake [实体数据表]）```
> ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020220415225751.png)

- while 函数
> ```(while [表达式] [循环体])```
> 
> 如果循环体中有多个语句，则需要用 progn 函数把这些语句包裹起来，用法为
> 
> ```(progn 语句1 语句2 ...)```

- open 函数和 close 函数
> open 函数用于打开文件，相对应地， close 函数用于关闭文件。
> ```
> (setq [文件句柄] (open [文件名] [打开方式])
> (close [文件句柄])
> ```
> 文件句柄： 是一个变量，用于操作所打开的文件。
> 
> 文件名： 打开的文件名，应用绝对路径。
> 
> 打开方式： 打开文件的方式，有只读 "r" ，写 "w" ，附加 "a" 等。
> 
> 打开文件后，应养成关闭的良好习惯。

- read-line 函数
> 打开文件后，为了读取文件，我们通常使用 ```read-line``` 函数。
> 
> ```(setq [变量名] (read-line [文件句柄]))```
> 
> 即可把当前读到的文本文件的一行读出来，保存在变量中。

- assoc 函数
> 这一函数用于从关联表中查找内容。
> 
> ```(assoc [查找内容] [关联表])```
> 
> 关联表： 是一个由表组成的表
> 
> 查找内容： assoc 函数会在关联表中的每一个子表中，查找第一个元素，如果这个元素与查找内容相同，则将这个子表返回。

### 列表
#### 分类
列表分为标准表、引用表和点对。

**标准表**： 就是 AutoLisp 作为一种表语言所用的最常见的表。在这种表中，第一个元素为函数名，后面的元素为函数的参数。程序在解释时，会执行函数名所代表的函数。

**引用表**： 是一种特殊的表，其第一个元素不是函数名，不作为函数执行。与其它编程语言中的数组类似。

引用表有两种定义方式。
- 当其元素都是定值时，可以在圆括号前加一个单引号表示。例如```'(120 0)```
- 当其元素中有变量时，不应采用这种形式，而可以采用 ```list``` 函数来创建，其使用方法为```(list 120 0)```

**点对** ：点对是一种只有两个元素的表，在列表中间用一个圆点隔开。例如```'(120 . 0)```，常用于构建关联表。

#### 提取
对于列表中元素的提取，有两个函数 car 和 cdr 及它们的组合。

car 函数用于取出列表中的第一个数，如
```
(setq a '(1 2))
(setq b (car a))
```
这时 b 的值为 1。

cdr 函数用于排除列表中的第一个数，返回一个新列表。
```
(setq a '(1 2))  
(setq b (cdr a))  
(setq c '(1 . 2))  
(setq d (cdr c))
```
可以看到， b 返回的值为 (2) ，而 d 返回的值为 2 。这就是引用表与点对的区别。**点对只有两个元素，所以用 cdr 返回的不是表，而是它的右元素。而引用表中 cdr 返回的是只有一个元素的表。**

car 和 cdr 可以结合在一起递归调用。举例来说，函数 cadr 就是先执行一次 cdr ，去掉第一个元素，再执行一次 car ，取出第一个元素。也就是取出原表中的第二个元素。这在提取点的坐标时非常有用。例如
```
(setq p '(1 2 3))
(setq x (car p))
(setq y (cadr p))
(setq z (caddr p))
```
x 、y 、z 分别为点 p 的三个坐标值。

### 实例
#### 绘制三角函数圆
注意，请先关闭捕捉功能。否则某些点可能被错误捕捉。
```
(defun c:hello(/ rad)  
    (setq rad (getreal "input rad <1.0>:"))  
    (if (= rad nil) (setq rad 1.0))  
    (command "line" '(-120 0) '(120 0) "")  
    (command "text" '(110 -20) 10 0 "cos")  
    (command "line" '(0 -120) '(0 120) "")  
    (command "text" '(-30 110) 10 0 "sin")  
    (command "circle" '(0 0) 100)  
    (command "line" '(0 0) (polar '(0 0) rad 110) "")  
    (command "line" (polar '(0 0) rad 100) (osnap '(20 0) "per") "")  
    (command "line" (polar '(0 0) rad 100) (osnap '(0 20) "per") "")  
    (command "arc" "c" '(0 0) '(20 0) (polar '(0 0) rad 20))  
    (command "text" '(20 5) 10 0 (rtos rad 2 1))  
    (setq cos (car (polar '(0 0) rad 1)))  
    (setq sin (cadr (polar '(0 0) rad 1)))  
    (command "text" (list (- (* cos 100) 25) -15) 10 0 (rtos cos 2 4))  
    (command "text" (list -50 (* sin 100)) 10 0 (rtos sin 2 4))  
)
```
利用 AutoLisp语言自动画一个简单的三角函数圆，用户可以输入想计算三角函数的弧度值，得到相应的三角函数圆。