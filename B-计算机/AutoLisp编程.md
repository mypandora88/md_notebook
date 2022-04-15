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
