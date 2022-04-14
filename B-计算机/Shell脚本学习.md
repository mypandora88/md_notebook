## Shell脚本学习
### 变量及使用
#### 定义变量
定义变量时，变量名不加美元符号（$，PHP语言中变量需要），如：  
> ```your_name="runoob.com"```    (**变量名和等号之间不能有空格**)

变量名的命名须遵循如下规则：
- 命名只能使用英文字母，数字和下划线，首个字符不能以数字开头。
- 中间不能有空格，可以使用下划线 _。
- 不能使用标点符号。
- 不能使用bash里的关键字（可用help命令查看保留关键字）。

除了显式地直接赋值，还可以用语句给变量赋值，如：
> ```
> for file in `ls /etc`
> 或者
> for file in $(ls /etc)
> ```
> 
> 以上语句将 /etc 下目录的文件名循环出来。

#### 引用变量
使用一个定义过的变量，只要在变量名前面加美元符号即可，如：
> ```
> your_name="qinjx"
> echo $your_name
> echo ${your_name}
> ```
> 加花括号是为了帮助解释器识别变量的边界，推荐给所有变量加上花括号，这是个好的编程习惯。

#### 只读变量
> ```readonly myUrl```

#### 删除变量
> ```unset variable_name```

### Shell字符串
字符串可以用单引号，也可以用双引号，也可以不用引号。

单引号字符串的限制：
- 单引号里的任何字符都会原样输出，单引号字符串中的变量是无效的；
- 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用。

双引号的优点：
- 双引号里可以有变量
- 双引号里可以出现转义字符

### Shell数组
bash支持一维数组（不支持多维数组），并且没有限定数组的大小。
#### 宝义数组
在 Shell 中，用括号来表示数组，数组元素用"空格"符号分割开。例如：```array_name=(value0 value1 value2 value3)```

或者
```
array_name=(
value0
value1
value2
value3
)
```

或者
```
array_name[0]=value0
array_name[1]=value1
array_name[n]=valuen
```

#### 读取数组
- 读取数组元素值的一般格式是
> ```valuen=${array_name[n]}```  
> 下标n用@表示可以获取所有元素
- 取得数组元素的个数：
> ```length=${#array_name[@]}```
- 取得数组单个元素的长度
> ```lengthn=${#array_name[n]}```

### Shell注释
以 # 开头的行就是注释，会被解释器忽略。

### Shell 传递参数
我们可以在执行 Shell 脚本时，向脚本传递参数，脚本内获取参数的格式为：$n。n 代表一个数字，1 为执行脚本的第一个参数，2 为执行脚本的第二个参数，以此类推……

### Shell运算符
Shell 和其他编程语言一样，支持多种运算符，包括：
- 算数运算符 ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211230142332.png)
- 关系运算符 ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211230142443.png)
- 布尔运算符 ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211230142504.png)
- 字符串运算符 ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211230142613.png)
- 文件测试运算符 ![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211230142634.png)

### Shell test 命令
Shell中的 test 命令用于检查某个条件是否成立，它可以进行数值、字符和文件三个方面的测试。
- 数值测试
> -eq	等于则为真  
> -ne	不等于则为真  
> -gt	大于则为真  
> -ge	大于等于则为真  
> -lt	小于则为真  
> -le	小于等于则为真

- 字符串测试
> =	等于则为真  
> !=	不相等则为真  
> -z 字符串	字符串的长度为零则为真  
> -n 字符串	字符串的长度不为零则为真

- 文件测试
> -e 文件名	如果文件存在则为真  
> -r 文件名	如果文件存在且可读则为真  
> -w 文件名	如果文件存在且可写则为真  
> -x 文件名	如果文件存在且可执行则为真  
> -s 文件名	如果文件存在且至少有一个字符则为真  
> -d 文件名	如果文件存在且为目录则为真  
> -f 文件名	如果文件存在且为普通文件则为真  
> -c 文件名	如果文件存在且为字符型特殊文件则为真  
> -b 文件名	如果文件存在且为块特殊文件则为真

### Shell流程控制
#### if else
```
if condition
then
    command1 
    command2
    ...
    commandN 
fi
```
或者
```
if condition
then
    command1 
    command2
    ...
    commandN
else
    command
fi
```
或者
```
if condition1
then
    command1
elif condition2 
then 
    command2
else
    commandN
fi
```

#### for循环
```
for var in item1 item2 ... itemN
do
    command1
    command2
    ...
    commandN
done
```

#### while 语句
```
while condition
do
    command
done
```

#### 无限循环
```
while true
do
    command
done
```

#### 跳出循环
在循环过程中，有时候需要在未达到循环结束条件时强制跳出循环，Shell使用两个命令来实现该功能：break和continue。
- break命令：跳出所有循环（终止执行后面的所有循环）。
- continue命令：continue命令与break命令类似，只有一点差别，它不会跳出所有循环，仅仅跳出当前循环。

### Shell 函数
linux shell 可以用户定义函数，然后在shell脚本中可以随便调用。

shell中函数的定义格式如下：
```
[ function ] funname [()]
{
    action;
    [return int;]
}
```

说明：
- 可以带function fun() 定义，也可以直接fun() 定义,不带任何参数。
- 参数返回，可以显示加：return 返回，如果不加，将以最后一条命令运行结果，作为返回值。 return后跟数值n(0-255

### Shell 输入/输出重定向
- 输出重定向：使用>，如果不希望文件内容被覆盖，可以使用 >> 追加到文件末尾
> ```command1 > file1```   
> 上面这个命令执行command1然后将输出的内容存入file1。

- 输入重定向：和输出重定向一样，Unix 命令也可以从文件获取输入，语法为：
> ```command1 < file1```  
> 本来需要从键盘获取输入的命令会转移到文件读取内容。

- 不显示内容
> ```command > /dev/null```
> 
> ```command > /dev/null 2>&1``` 屏蔽 stdout 和 stderr
### Shell 文件包含
和其他语言一样，Shell 也可以包含外部脚本。这样可以很方便的封装一些公用的代码作为一个独立的文件。
```
. filename   # 注意点号(.)和文件名中间有一空格
或
source filename
```
### Shell标准输入输出
shell程序中 2> /dev/null 代表什么意思？答案：Linux下的 0 1 2文件描述符
-  1 是标准输出（stdout）
> 把标准输出结果重定向到 list.txt文件里面。
> ```
> linux@ubuntu:~$ ls 1>list.txt
> linux@ubuntu:~$ cat list.txt 
> Desktop
> Documents
> Downloads
> ```
-  2 是标准错误输出（stderr）
> 同上，不过由于没有错误，没有任何输出
-  0 是标准输入（stdin）
> &是不是很像取地址符号，我们往标准输入 echo 一个字符串，然后屏幕就打印了这个字符串出来。就是这么简单，就是这么讲道理。