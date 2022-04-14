## Linux系统及常用命令
[教程](https://www.runoob.com/linux/linux-tutorial.html)
- 云服务器（Elastic Compute Service, ECS）
- 虚拟专用服务器（Virtual Private Server,VPS ）

### Linux启动过程
1. 内核的引导
2. 运行 init
3. 系统初始化
4. 建立终端 
5. 用户登录系统  
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211225082222.png)

### 目录结构
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211225082409.png)

### Linux 文件基本属性
- chown (change owner) ： 修改所属用户与组。
- chmod (change mode) ： 修改用户的权限。

在 Linux 中第一个字符代表这个文件是目录、文件或链接文件等等。
- 当为 d 则是目录
- 当为 - 则是文件；
- 若是 l 则表示为链接文档(link file)；
- 若是 b 则表示为装置文件里面的可供储存的接口设备(可随机存取装置)；
- 若是 c 则表示为装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)。

接下来的字符中，以三个为一组，且均为 rwx 的三个参数的组合。其中， r 代表可读(read)、 w 代表可写(write)、 x 代表可执行(execute)。 要注意的是，这三个权限的位置不会改变，如果没有权限，就会出现减号 - 而已。
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211225093839.png)

### Linux文件属主和属组:
更改文件属性
- chgrp：更改文件属组
> 语法：  
> chgrp \[-R] 属组名 文件名  
> 参数选项  
> -R：递归更改文件属组，

- chown：更改文件属主，也可以同时更改文件属组
> 语法：  
> chown \[–R] 属主名 文件名  
> chown \[-R] 属主名：属组名 文件名

- chmod：更改文件9个属性
> Linux文件属性有两种设置方法，一种是数字，一种是符号。  
> Linux 文件的基本权限就有九个，分别是 owner/group/others(拥有者/组/其他) 三种身份各有自己的 read/write/execute 权限。  
> r:4   w:2   x:1  
> user：用户  group：组  others：其他   那么我们就可以使用 u, g, o 来代表三种身份的权限。
> 例如：```chmod u=rwx,g=rx,o=r tesh.sh```

### Linux 文件与目录管理
- 绝对路径：
> 路径的写法，由根目录 / 写起，例如： /usr/share/doc 这个目录。

- 相对路径：
> 路径的写法，由 . 写起，例如由 /usr/share/doc 要到 /usr/share/man 底下时，可以写成： cd ../man 这就是相对路径的写法。

- 处理目录的常用命令
> ls（英文全拼：list files）: 列出目录及文件名  
>> -a ：全部的文件，连同隐藏文件( 开头为 . 的文件) 一起列出来(常用)  
>> -d ：仅列出目录本身，而不是列出目录内的文件数据(常用)  
>> -l ：长数据串列出，包含文件的属性与权限等等数据；(常用)
>
> cd（英文全拼：change directory）：切换目录  
> pwd（英文全拼：print work directory）：显示目前的目录  
> mkdir（英文全拼：make directory）：创建一个新的目录  
>> -m ：配置文件的权限喔！直接配置，不需要看默认权限 (umask) 的脸色～  
>> -p ：帮助你直接将所需要的目录(包含上一级目录)递归创建起来！
>
> rmdir（英文全拼：remove directory）：删除一个空的目录  
> cp（英文全拼：copy file）: 复制文件或目录  
> rm（英文全拼：remove）: 删除文件或目录  
>> -f ：就是 force 的意思，忽略不存在的文件，不会出现警告信息；  
>> -i ：互动模式，在删除前会询问使用者是否动作  
>> -r ：递归删除啊！最常用在目录的删除了！这是非常危险的选项！！！
>
> mv（英文全拼：move file）: 移动文件与目录，或修改文件与目录的名称
>> -f ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；  
>> -i ：若目标文件 (destination) 已经存在时，就会询问是否覆盖！  
>> -u ：若目标文件已经存在，且 source 比较新，才会升级 (update)

- 文件内容查看
> cat  由第一行开始显示文件内容  
> tac  从最后一行开始显示，可以看出 tac 是 cat 的倒着写！  
> nl   显示的时候，顺道输出行号！  
> more 一页一页的显示文件内容  
>>  空白键 (space)：代表向下翻一页；  
>>  回车键（Enter）：代表向下翻『一行』；
>
> less 与 more 类似，但是比 more 更好的是，他可以往前翻页！  
>> 空白键    ：向下翻动一页；  
>> \[pagedown]：向下翻动一页；  
>> \[pageup]  ：向上翻动一页；
>
> head 只看头几行  
>> ```head -n 20 /etc/man.config```
>
> tail 只看尾巴几行
>> ```tail -n 20 /etc/man.config```

### Linux系统用户账号的管理
- 添加新的用户账号
> 使用useradd命令，其语法如下：useradd 选项 用户名  
> 
> -d 目录 指定用户主目录，如果此目录不存在，则同时使用-m选项，可以创建主目录。  
> 例如：```useradd –d  /home/sam -m sam```

- 删除帐号
> 删除一个已有的用户账号使用userdel命令，其格式如下：userdel 选项 用户名  
> 
> 常用的选项是 -r，它的作用是把用户的主目录一起删除  
> 例如：```userdel -r sam```

- 修改帐号
> 修改已有用户的信息使用usermod命令，其格式如下：usermod 选项 用户名 
>  
> 常用的选项包括-c, -d, -m, -g, -G, -s, -u以及-o等，这些选项的意义与useradd命令中的选项一样，可以为用户指定新的资源值。  
> 例如：```usermod -s /bin/ksh -d /home/z –g developer sam```

- 用户口令的管理
> 指定和修改用户口令的Shell命令是passwd。命令的格式为：passwd 选项 用户名
> 
> 可使用的选项：  
> -l 锁定口令，即禁用账号。  
> -u 口令解锁。  
> -d 使账号无口令。  
> -f 强迫用户下次登录时修改口令。  
> 
> 如果默认用户名，则修改当前用户的口令。  

- Linux系统用户组的管理
> **增加**一个新的用户组使用groupadd命令，其格式：groupadd 选项 用户组 
> -g GID 指定新用户组的组标识号（GID）。  
> -o 一般与-g选项同时使用，表示新用户组的GID可以与系统已有用户组的GID相同。 
> 例如：```groupadd -g 101 group2```，此命令向系统中增加了一个新组group2，同时指定新组的组标识号是101。
> 
> 如果要**删除**一个已有的用户组，使用groupdel命令，其格式如下：groupdel 用户组
> 
> **修改**用户组的属性使用groupmod命令，其格式如下：groupmod 选项 用户组  
> 例如：```groupmod –g 10000 -n group3 group2``` 此命令将组group2的标识号改为10000，组名修改为group3。

- 与用户账号有关的系统文件
> /etc/passwd文件是用户管理工作涉及的最重要的一个文件。
> 
> Linux系统中的每个用户都在/etc/passwd文件中有一个对应的记录行，它记录了这个用户的一些基本属性。这个文件对所有用户都是可读的。
> 
> /etc/passwd中一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：
> 用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell  
> 例如：sam:x:200:50:Sam san:/home/sam:/bin/sh

- 与用户组账号有关的系统文件
> 用户组的所有信息都存放在/etc/group文件中
> 
> 此文件的格式也类似于/etc/passwd文件，由冒号(:)隔开若干个字段，这些字段有：组名:口令:组标识号:组内用户列表
> 例如：users::20:root,sam

### Linux磁盘管理
Linux 磁盘管理常用三个命令为 df、du 和 fdisk：
- df（英文全称：disk full）：列出文件系统的整体磁盘使用量
> -a ：列出所有的文件系统，包括系统特有的 /proc 等文件系统；  
> -k ：以 KBytes 的容量显示各文件系统；  
> -m ：以 MBytes 的容量显示各文件系统；  
> -h ：以人们较易阅读的 GBytes, MBytes, KBytes 等格式自行显示；  
> -H ：以 M=1000K 取代 M=1024K 的进位方式；  
> -T ：显示文件系统类型, 连同该 partition 的 filesystem 名称 (例如 ext3) 也列出；  
> -i ：不用硬盘容量，而以 inode 的数量来显示

- du（英文全称：disk used）：检查磁盘空间使用量
> -a ：列出所有的文件与目录容量，因为默认仅统计目录底下的文件量而已;  
> -h ：以人们较易读的容量格式 (G/M) 显示；  
> -s ：列出总量而已，而不列出每个各别的目录占用容量；  
> -S ：不包括子目录下的总计，与 -s 有点差别。  
> -k ：以 KBytes 列出容量显示；  
> -m ：以 MBytes 列出容量显示；  

- fdisk：用于磁盘分区
> -l ：输出后面接的装置所有的分区内容。若仅有 fdisk -l 时， 则系统将会把整个系统内能够搜寻到的装置的分区均列出来。
> 
> 实例：  
> fdisk /dev/sda(**不要加上数字**)之后输入m，可以看到命令介绍   
> d 表示删除一个partition  
> n 表示增加一个partition  
> p 在屏幕上显示分割表  
> q 不保存离开fdisk  
> w 保存离开fdisk  

- 磁盘格式化 
> 格式化的命令非常的简单，使用 mkfs（make filesystem） 命令。
> 
> -t ：可以接文件系统格式，例如 ext3, ext2, vfat 等(系统有支持才会生效)  
> 例如：```mkfs -t ext4 /dev/hdc6```

- 磁盘添加Lable
> ```e2label /dev/sdb1 wdc-1t```

- 磁盘挂载与卸除
> Linux 的磁盘挂载使用 mount 命令，卸载使用 umount 命令。  
> 
> 磁盘挂载语法：mount \[-t 文件系统] \[-L Label名] \[-o 额外选项] \[-n]  装置文件名  挂载点  
> 例如：```mount /dev/hdc6 /mnt/hdc6```
> 
> 磁盘卸载命令 umount ，语法：umount [-fn] 装置文件名或挂载点  
> -f ：强制卸除！可用在类似网络文件系统 (NFS) 无法读取到的情况下；  
> -n ：不升级 /etc/mtab 情况下卸除。

### 有用的快捷键
- \[Tab] 有『命令补全』与『文件补齐』的功能
- \[Ctrl]+ C 如果在Linux 底下输入了错误的指令或参数，想让当前的程序『停掉』的话，可以输入：
- \[Ctrl]-d 『键盘输入结束(End Of File, EOF 或 End Of Input)』的意思
- \[shift]+{\[PageUP]|\[Page Down]} 翻页

### Linux常用命令及操作
#### Linux关机重启
不管是重启系统还是关闭系统，首先要运行 ```sync``` 命令，把内存中的数据写到磁盘中。

- 关机的命令有 ```shutdown –h now```或者```halt```或者```poweroff``` 或者```init 0```
- 重启系统的命令有 ```shutdown –r now```或者```reboot```或者```init 6```

定时开关机  
```shutdown -r 00:00:01``` 定时重启  
```shutdown +5 "System will shutdown after 5 minutes"```  指定5分钟后关机 ,同时送出警告信息给登入用户


#### vi/vim 的使用
基本上 vi/vim 共分为三种模式，分别是命令模式（Command mode），输入模式（Insert mode）和底线命令模式（Last line mode）。 这三种模式的作用分别是：
- 命令模式：
> 用户刚刚启动 vi/vim，便进入了命令模式。  
> 此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。
> 
> 以下是常用的几个命令：  
> i 切换到输入模式，以输入字符。  
> x 删除当前光标所在处的字符。  
> : 切换到底线命令模式，以在最底一行输入命令。

- 输入模式
> 在命令模式下按下i就进入了输入模式。在输入模式中，可以使用以下按键：
> 
> 字符按键以及Shift组合，输入字符  
> ENTER，回车键，换行  
> BACK SPACE，退格键，删除光标前一个字符  
> DEL，删除键，删除光标后一个字符  
> 方向键，在文本中移动光标  
> HOME/END，移动光标到行首/行尾  
> Page Up/Page Down，上/下翻页  
> Insert，切换光标为输入/替换模式，光标将变成竖线/下划线  
> ESC，退出输入模式，切换到命令模式

- 底线命令模式
> 在命令模式下按下:（英文冒号）就进入了底线命令模式。底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。
> 
> 在底线命令模式中，基本的命令有（**已经省略了冒号**）：  
> q 退出程序  
> w 保存文件  
> 按ESC键可随时退出底线命令模式。

#### apt 命令
apt（Advanced Packaging Tool）是一个在 Debian 和 Ubuntu 中的 Shell 前端软件包管理器。

apt 命令提供了查找、安装、升级、删除某一个、一组甚至全部软件包的命令，而且命令简洁而又好记。

apt 命令执行需要超级管理员权限(root)。

语法：apt \[options] \[command] \[package ...]

常用命令：
- 列出所有可更新的软件清单命令：```sudo apt update```
- 升级软件包：```sudo apt upgrade```
- 列出可更新的软件包及版本信息：```apt list --upgradeable```
- 升级软件包，升级前先删除需要更新软件包：```sudo apt full-upgrade```
- 安装指定的软件命令：```sudo apt install <package_name>```
- 安装多个软件包：```sudo apt install <package_1> <package_2> <package_3>```
- 更新指定的软件命令：```sudo apt update <package_name>```
- 显示软件包具体信息,例如：版本号，安装大小，依赖关系等等：```sudo apt show <package_name>```
- 删除软件包命令：```sudo apt remove <package_name>```
- 清理不再使用的依赖和库文件: ```sudo apt autoremove```
- 移除软件包及配置文件: ```sudo apt purge <package_name>```
- 查找软件包命令： ```sudo apt search <keyword>```
- 列出所有已安装的包：```apt list --installed```
- 列出所有已安装的包的版本信息：```apt list --all-versions```

#### su命令
su（英文全拼：switch user）命令用于变更为其他使用者的身份，除 root 外，需要键入该使用者的密码。

例如：```su root``` 表示切换到root用户

#### crontab定期任务
![](https://ddns.smpi.top:10000/md_attachments/Pasted%20image%2020211225144056.png)

- 参数：
> -e : 执行文字编辑器来设定时程表，内定的文字编辑器是 VI，如果你想用别的文字编辑器，则请先设定 VISUAL 环境变数来指定使用那个文字编辑器(比如说 setenv VISUAL joe)  
> -r : 删除目前的时程表  
> -l : 列出目前的时程表

- 注意：
> 当程序在你所指定的时间执行后，系统会发一封邮件给当前的用户，显示该程序执行的内容，若是你不希望收到这样的邮件，请在每一行空一格之后加上 > /dev/null 2>&1 即可，如：  
> ```20 03 * * * /var/www/runoob/test.sh > /dev/null 2>&1 ```

- 脚本无法执行问题:
> 如果我们使用 crontab 来定时执行脚本，无法执行，但是如果直接通过命令（如：./test.sh)又可以正常执行，这主要是因为无法读取环境变量的原因。
>   
> 解决方法：  
> 1、所有命令需要写成绝对路径形式，如: /usr/local/bin/docker。
> 
> 2、在 shell 脚本开头使用以下代码：
> ``` 
> #!/bin/sh
> 
> . /etc/profile
> . ~/.bash_profile
> ```
> 
> 3、在 /etc/crontab 中添加环境变量，在可执行命令之前添加命令 . /etc/profile;/bin/sh，使得环境变量生效  
> ```20 03 * * * . /etc/profile;/bin/sh /var/www/runoob/test.sh```

- 系统级任务需要直接编辑/etc/crontab文件
> ```0 7    1 * *   root    /home/pi/script/系统自动更新并重启.sh```

#### tree命令
能将文件做成列表树展现出来默认情况下 ,tree命令无法显示中文文件或文件夹名 ,会是一串转义字符 ,可以使用tree -N就能正常显示

```tree > /home/pi/tree.txt``` 可以进行导出

#### find命令
Linux find 命令用来在指定目录下查找文件。任何位于参数之前的字符串都将被视为欲查找的目录名。如果使用该命令时，不设置任何参数，则 find 命令将在当前目录下查找子目录与文件。并且将查找到的子目录和文件全部进行显示。

- 语法：  
> find   path   -option   \[   -print ]   \[ -exec   -ok   command ]   {} \\;

- 常用参数：
> -ipath p, -path p : 路径名称符合 p 的文件，ipath 会忽略大小写  
> 
> -name name, -iname name : 文件名称符合 name 的文件。iname 会忽略大小写  
> 
> -size n : 文件大小 是 n 单位，b 代表 512 位元组的区块，c 表示字元数，k 表示 kilo bytes，w 是二个位元组。  
> 
> -type c : 文件类型是 c 的文件。(d: 目录 c: 字型装置文件 b: 区块装置文件 p: 具名贮列 f: 一般文件)
> 
> -ctime n : 在过去n天内被修改过的文件
> 
> -atime n : 在过去n天内被读取过的文件

- 实例
> 将当前目录及其子目录下所有文件后缀为 .c 的文件列出来:    
> ```find . -name "*.c"```
> 
> 将当前目录及其子目录中的所有文件列出：  
> ```find . -type f```
> 
> 查找系统中所有文件长度为 0 的普通文件，并列出它们的完整路径：  
> ```find / -type f -size 0 -exec ls -l {} \;```

#### 备份压缩命令
- zip命令
> zip 是个使用广泛的压缩程序，压缩后的文件后缀名为 .zip。  
> 
> 常用参数：  
> -q 不显示指令执行过程。  
> -r 递归处理，将指定目录下的所有文件和子目录一并处理。  
> -d 从压缩文件内删除指定的文件。  
> -m 将文件压缩并加入压缩文件后，删除原始文件
> 
> 将 /home/html/ 这个目录下所有文件和文件夹打包为当前目录下的 html.zip：  
> ```zip -q -r html.zip /home/html```
> 
> 从压缩文件 cp.zip 中删除文件 a.c  
> ```zip -dv cp.zip a.c```

- unzip命令
> 实例：  
> 查看压缩文件中包含的文件：  
> ```unzip -l abc.zip```

-gzip命令
> gzip是个使用广泛的压缩程序，文件经它压缩过后，其名称后面会多出".gz"的扩展名。
> 
> -d 解开压缩文件。  
> -l 列出压缩文件的相关信息。  
> -r 递归处理，将指定目录下的所有文件及子目录一并处理。  
> --best 此参数的效果和指定"-9"参数相同。  
> --fast 此参数的效果和指定"-1"参数相同。  
> -v 显示指令执行过程。
> 
> 实例：  
>``` gzip *```  压缩目录下的所有文件  
> ```gzip -dv *``` 解压文件，并列出详细信息

- tar命令
> Linux tar（英文全拼：tape archive ）命令用于备份文件。tar 是用来建立，还原备份文件的工具程序，它可以加入，解开备份文件内的文件。
> 
> 实例:  
> 压缩文件 非打包  
> ```tar -czvf test.tar.gz a.c```压缩 a.c文件为test.tar.gz
> 
> 列出压缩文件内容  
> ```tar -tzvf test.tar.gz```
> 
> 解压文件  
> ```tar -xzvf test.tar.gz```

#### mail命令
mail 查看邮件
> mail 查看所有邮件  
> d 1-100 删除1-100邮件  
> q 保存退出

#### touch命令
touch命令有两个功能:
- 一是用于把已存在文件的时间标签更新为系统当前的时间（默认方式） ,它们的数据将原封不动地保留下来
- 二是用来创建新的空文件。

#### clear命令
清屏或者用快捷键ctrl+l

#### data命令
Linux date命令可以用来显示或设定系统的日期与时间

#### echo命令
echo命令常用的用法是在终端打印字符串。我们还可以将字符串打印到我们自定义的文件中 ,即重定位。
- 直接显示 ```echo "this is my test"```
- 创建带有内容的文件 ```echo "this is my test" > a.txt```
- 文件后面追加内容 ```echo "this is my second add" >> a.txt```

#### cat命令
cat（英文全拼：concatenate）命令用于连接文件并打印到标准输出设备上。

- 参数说明：
> -n 或 --number：由 1 开始对所有输出的行数编号。  
> -b 或 --number-nonblank：和 -n 相似，只不过对于空白行不编号。

- 范例
> 把 textfile1 和 textfile2 的文档内容加上行号（空白行不加）之后将内容附加到 textfile3 文档里：  
> ```cat -b textfile1 textfile2 >> textfile3```
> 
> 清空 /etc/test.txt 文档内容：  
> ```cat /dev/null > /etc/test.txt```

#### ln命令
ln（英文全拼：link files）命令是一个非常重要命令，它的功能是为某一个文件在另外一个位置建立一个同步的链接。

当我们需要在不同的目录，用到相同的文件时，我们不需要在每一个需要的目录下都放一个必须相同的文件，我们只要在某个固定的目录，放上该文件，然后在 其它的目录下用ln命令链接（link）它就可以，不必重复的占用磁盘空间。

语法：ln \[参数]\[源文件或目录]\[目标文件或目录]

硬链接的意思是一个档案可以有多个名称。软链接的方式则是产生一个特殊的档案，该档案的内容是指向另一个档案的位置。硬链接是存在同一个文件系统中，而软链接却可以跨越不同的文件系统。

- 软链接：
> 1. 软链接，以路径的形式存在。类似于Windows操作系统中的快捷方式
> 2. 软链接可以 跨文件系统 ，硬链接不可以
> 3. 软链接可以对一个不存在的文件名进行链接
> 4. 软链接可以对目录进行链接

- 硬链接：
> 1. 硬链接，以文件副本的形式存在。但不占用实际空间。
> 2. 不允许给目录创建硬链接
> 3. 硬链接只有在同一个文件系统中才能创建

#### sftp命令
- ```sftp pontos@172.86.125.117``` 之后输入密码进行登陆
- ```sftp -oPort=10022 root@192.168.0.254``` 非22端口需指定
- ```get /etc/supervisor/file.conf /etc/``` 下载文件到/etc文件夹下 
- ```get -r /etc/supervisor /etc/``` 下载文件夹
- ```put```为上传

#### wget命令
下载到当前目录  
```wget http://cn.wordpress.org/wordpress-4.9.4-zh_CN.tar.gz```

下载并改名  
```wget -O wordpress.tar.gz  http://cn.wordpress.org/wordpress-4.9.4-zh_CN.tar.gz```

#### dpkg命令
dpkg 是Debian package的简写，为”Debian“ 操作系统 专门开发的套件管理系统，用于软件的安装，更新和移除。
- 安装命令：```dpkg -i ~/Download/mozybackup_i386.deb```
- 列出与该包先关联的文件：```dpkg -L package```
- 移除软件（保留配置）：```dpkg -r package```
- 移除软件（不保留配置）：```dpkg -P package```

#### timedatectl命令
- 查看时区：```timedatectl```
- 设置时区：```timedatectl set-timezone Asia/Shanghai```
- 查看所有时区：```timedatectl list-timezones```