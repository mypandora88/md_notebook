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

### 绘制三角函数圆
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

其中：
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

- 查看AutoCAD命令
> 以 "line" 命令为例，首先我们要确定输入哪些参数。打开 AutoCAD ，在控制台中输入line回车，看到提示输入一个点，这就是我们要给出的第一个参数。
> 
> 按提示输入点后，又提示再输入一个点，这是我们要给出的第二个参数。
> 
> 输入好第二个点后，提示再输一个点，会再画一条线，这时我们不想继续画，输入回车结束命令。这是我们要给出的第三个参数。
> 
> 这样，我们就确定了要输出的三个参数，分别是两个点和一个回车。因此本例中，我们用两个列表来表示点，用一个**空字符串来表示回车**（ AutoLisp 的约定）。
> 
> ```(command "line" '(-120 0) '(120 0) "")```

- 列表
> 列表分为标准表、引用表和点对
> 
- osnap 函数，用于捕捉点。
- rtos 函数和一系列字符串转换函数，用于字符串与数字转换。
- polar 函数和一系数相关的图形处理函数，用于确定点的位置、距离、角度等。