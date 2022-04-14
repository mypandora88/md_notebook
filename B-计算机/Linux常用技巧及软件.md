## Linux常用技巧及软件
### 常用技巧
#### 快捷登陆
> 在putty软件快捷方式目标中加上:    
> ```空格root@172.245.137.144 -pw YtjwS3ROmOz6 -P 22```
> 
> 一台VPS登陆另一台VPS：  
> ```ssh root@172.86.74.61 -p 22``` (填写地址和端口号)

#### 更改默认22端口:  
> ```nano /etc/ssh/sshd_config```
> 默认端口为 22 ,去掉 \#Port 22 前面的 # 号 ,并在其下添加一行 Port 9999  
> 
> 防火墙先通过新端口 ```ufw allow 9999/tcp```
> 
> 重启 SSH 服务：```/etc/init.d/ssh restart```并测试能不能通过这个端口连接 ,如果能连接再禁用22端口:Port 22 前面加 \# 注释掉; 防火墙禁止 22 端口

#### 增删SWAP空间大小
Linux 系统中的 Swap 分区，即交换分区，类似于 Windows 的虚拟内存，其作用可简单的描述为：当系统的物理内存不够用的时候，将暂时不用的数据存放到交换空间所在的硬盘上，从而可以腾出内存来让别的程序运行。
- 添加 Swap 文件
> 先切换成root用户，随便进入一个目录用于后续存放 Swap 文件，也可以直接放在根目录，这里放在 /var 目录下。
> 
> ```cd /var```
> 
> 使用 dd 命令生成一个文件块，大小为自己想设置的 Swap 分区大小，这里生成一个名为 swapfile 的文件，大小设为 1G。
> 
> ```dd if=/dev/zero of=swapfile bs=1M count=1024```
> 
> 将该文件设为 Swap 文件（格式化）。
> 
> ```mkswap swapfile```
> 
> 激活 Swap 文件（启用虚拟内存）。
> 
> ```swapon swapfile```
> 
> 检查 Swap 是否正确。
> 
> ```swapon -s```
> 
> 另外为了安全建议将交换分区文件权限设为 0600 或 0644 ，执行以下命令。
> 
> ```chmod 0600 swapfile```
> 
> 添加开机自动挂载设置。
> 
> ```nano /etc/fstab```
> 
> 在最后增加以下内容：
> 
> ```/var/swapfile swap swap defaults 0 0```

- 删除Swap文件
> 首先将 Swap 文件取消激活：
> 
> ```swapoff /var/swapfile```
> 
> 然后删除我们设置的 Swap 文件：
> 
> ```rm /var/swapfile```
> 
> 最后再编辑 fstab 文件删除掉自动挂载 Swap 的设置即可：
> 
> ```nano /etc/fstab```

#### Linux 忘记密码解决方法
很多朋友经常会忘记Linux系统的root密码，linux系统忘记root密码的情况该怎么办呢？重新安装系统吗？当然不用！进入单用户模式更改一下root密码即可。
[方法](https://www.runoob.com/linux/linux-forget-password.html)

#### 开机挂载硬盘
- blkid命令查看设备uuid：```sudo blkid```
- 修改fstab文件：```sudo nano /etc/fstab```
- 在最后一行加上
> ```
> UUID=4d7ea1e1-eb1a-dc4f-9464-d1ff18f978cc /mnt/wd4t ext4 defaults,nofail,x-systemd.device-timeout=5,noatime,noauto 0     0
> 
> UUID=c5b344c6-0d15-f749-bf43-49b83c705774 /mnt/wd4t-plex ext4 defaults,nofail,x-systemd.device-timeout=5,noatime,noauto 0     0
> 
> UUID=1755d824-4458-4590-9068-f7fa86a53b6b /mnt/wd8t ext4 defaults,nofail,x-systemd.device-timeout=5,noatime, 0     0
> 
> UUID=23960efb-16f3-4fae-8ac6-c5aaacd3ace0 /mnt/wdc ext4 defaults,nofail,x-systemd.device-timeout=5,noatime 0     0
> 
> UUID=f04af0a1-e236-4618-84f4-004bdb0fced7 /mnt/wdc ext4 defaults,nofail,x-systemd.device-timeout=5,noatime 0     0（原来的500G，坏了）
> ```

如果想同时识别两个硬盘 ,可将UUID改成/dev/sda1 ,这样不管哪个插上 ,都可以挂载到同一个位置 ,但是不要同时插上

#### 授予普通用户 sudo 权限
授予 sudo 权限有三个方法：
- 第一个是把用户添加到 sudo 用户组
> 命令：```usermod -aG sudo pi```
- 第二个是修改 sudo 配置文件 (etc/sudoers)
> 打开 sudo 配置文件:  
> ```visudo```
> 
> 以授予 pi 这个用户 sudo 权限为例子，添加如下内容：  
> ```pi ALL=(ALL) ALL```
- 第三个是添加配置文件到 /etc/sudoers.d/ 目录中（**推荐**）
> 以授予 pi 用户 sudo 权限为例，在终端中输入以下命令直接添加配置文件：  
> ```tee /etc/sudoers.d/pi <<< 'pi ALL=(ALL) ALL'```
> 
> 如果你不想输入每次 sudo 都输入密码，可以设置免密。  
> ```tee /etc/sudoers.d/pi <<< 'pi ALL=(ALL) NOPASSWD: ALL'```
> 
> 最后赋予正确的权限：  
> ```chmod 440 /etc/sudoers.d/pi```

#### 限制用户不能访问某个目录
- 使用setfacl

- 修改sshd文件(建议) /etc/ssh/sshd_config，在最后添加如下内容：
```
Match User lu
     ChrootDirectory  /mnt/wd8t/data/11-Share2Lu
     ForceCommand internal-sftp
     AllowTcpForwarding no
     X11Forwarding no
```

#### SSH运行多条命令
- 每条命令使用";"隔开 ,则无论前边的命令执行成功与否都会继续执行下一条命令
- 若命令间使用"&&"隔开 ,则只有前边的命令执行成功了再会继续执行后边的命令
- 若命令间使用"||"隔开 ,则只有前边的命令执行失败了才回继续执行后边的命令

### 常用软件
#### screen软件
- 创建会话```screen -S youtube```
- 恢复创建的会话```screen -r youtube```
- 查看已经创建的对话```screen -ls```
- 有时在恢复screen时会出现There is no screen to be resumed matching \*\*\* ,输入命令```screen -d ***```
- 其它键盘命令
> Ctrl + a ,d 暂离当前会话  
> Ctrl + a ,c 在当前screen会话中创建一个子会话  
> Ctrl + a ,w 子会话列表  
> Ctrl + a ,p 上一个子会话  
> Ctrl + a ,n 下一个子会话  
> Ctrl + a ,0-9 在第0窗口至第9子会话间切换  
> ```screen -D  -r baidu``` 结束别的应用占用  
> ```screen -dmS temp ping baidu.com``` 创建一个后台会话 ,并运行命令 

#### rclone软件
- 初始化配置：```rclone config```
- 参数：
> --bwlimit 8M 限制带宽每秒钟8M传输  ,100Mbps就得限制在12.5M  
> -P实时显示传输速度
- 过滤规则
> 目录过滤需要在目录名称后面加上 /，否则会被当做文件进行匹配。以 / 开头只会匹配根目录（指定目录下），否则匹配所目录。这同样适用于文件。
> 
> ```--exclude ".git/" ``` 排除所有目录下的.git 目录。
> 
> ```--exclude "/.git/" ``` 只排除根目录下的.git 目录。
> 
> ```--exclude "{Video,Software}/"``` 排除所有目录下的 Video 和 Software 目录。
> 
> ```--exclude "/{Video,Software}/"``` 只排除根目录下的 Video 和 Software 目录。
> 
> ```--include "/{Video,Software}/**"``` 仅包含根目录下的 Video 和 Software 目录

- 示例：
> ```rclone sync blny:/data /home/pi/sharebyme/blny-server -P --exclude "/{00 软件 ,#recycle}/"```

#### youtube-dl软件
- 安装
> ```
> sudo curl -L https://yt-dl.org/downloads/latest/youtube-dl -o /usr/local/bin/youtube-dl
> sudo chmod a+rx /usr/local/bin/youtube-dl
> ```
- 查看格式
> ```youtube-dl -F https....```
- 下载想要的格式
> ```youtube-dl -f 138+140 https....```
- 下载最佳格式
> ```youtube-dl -f bestvideo+bestaudio https....```
- 下载时使用代理
> ```youtube-dl --proxy socks5://127.0.0.1:10808 https….```
- youtube-dl -U 更新程序
- youtube下载完成移动到网盘
> 在~/.config/youtube-dl/下新建config文件 
> ```
> --rate-limit 5M
> -o /home/pontos/youtube-dl/%(title)s.%(ext)s
> --exec "rclone move {} OneDrive:/Myvps/Download -P --bwlimit 5M"
> -f bestvideo+bestaudio/best
> --proxy socks5://127.0.0.1:10808
> ```

#### BBR加速
uname -r查看系统内核 ,BBR只能在4.9 以上版本 Linux 内核 ,不然需要升级内核
```
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf
echo "net.ipv4.tcp_congestion_control=bbr" >> /etc/sysctl.conf
sysctl -p
```
之后 ```lsmod | grep bbr```  如果显示BBR就说明已经开启了

#### FFmpeg格式工厂
转码:  
```ffmpeg -i input.flv output.mp4```

#### ufw防火墙
- ```sudo ufw allow ssh```（先进行这步再启动 ,免得登陆不上去）
- ```sudo ufw enable``` 开机启动
- ```sudo ufw disable``` 禁用
- ```sudo ufw allow 2290:2300/tcp``` 放行一行端口
- ```sudo ufw delete allow 80```
- ```sudo ufw allow 888``` 同时放行888端口的 tcp 和 udp
- ```sudo ufw status``` 查看防火墙状态

#### Docker容器
- ```docker ps -a``` 列出所有容器
- ```docker stop $(docker ps -a -q)``` 停止所有容器
- ```docker rm $(docker ps -a -q)``` 删除所有容器
- ```docker images``` 查看镜像
- ```docker rmi <image id>``` 删除镜像
- ```docker rmi $(docker images -q)``` 删除全部镜像
- ```docker rmi -f $(docker images -q)``` 强制删除全部镜像
- ```docker container prune``` 删除所有停止的容器
- docker-compose使用：
> docker-compose文件尽量不要放在root目录下 ,可能会出问题  
> ```docker-compose up -d``` 使用docker-compose运行 ,-d表示后台运行  
> ```docker-compose down``` 停止并删除容器
- volumes路径挂载:
> 使用绝对路径挂载数据卷  
> ```- /opt/data:/var/lib/mysql```
> 
> 以 Compose 配置文件为中心的相对路径作为数据卷挂载到容器
> ```- ./cache:/tmp/cache```
> 
> 使用用户的相对路径（~/ 表示的目录是 /home/<用户目录>/ 或者 /root/）
> ```- ~/configs:/etc/configs:ro```  
> ro表示权限为只读

#### Rsync同步软件
rsync（remote synchronize）是一个远程数据同步工具，可通过 LAN/WAN 快速同步多台主机之间的文件。也可以使用 rsync 同步本地硬盘中的不同目录。

常用参数：
- -a 归档模式，表示以递归方式传输文件，并保持所有文件属性
- -r 对子目录以递归模式处理
- -p 保持文件权限
- -g 保持文件属组信息
- -o 保持文件属主信息 (super-user only)
- -z 在传输文件时进行压缩处理
- ––exclude 指定排除一个不需要传输的文件匹配模式
- ––include 指定需要传输的文件匹配模式
- ––delete 删除那些接收端还有而发送端已经不存在的文件（分before默认、after、during三种）
- -P 在传输时显示传输过程
- -h 输出文件大小使用易读的单位（如，K，M等）
- -n 显示哪些文件将被传输（同––dry-run）

注意：
- 若使用普通用户身份运行 rsync 命令，同步后的文件的属主将改变为这个普通用户身份。
- 若使用超级用户身份运行 rsync 命令，同步后的文件的属主将保持原来的用户身份。

在本地磁盘同步数据  
```rsync -a --delete /home /backups```  
在指定复制源时，路径是否有最后的 “/” 有不同的含义，例如：  
/home ： 表示将整个 /home 目录复制到目标目录  
/home/ ： 表示将 /home 目录中的所有内容复制到目标目录

#### Samba文件共享
安装：```sudo apt install samba```   
修改配置文件：```sudo nano /etc/samba/smb.conf```
```
[seagate]
    comment = Samba on Seagate
    path = /mnt/seagate/data
    read only = no
    browsable = yes
```
之后重启服务：```sudo service smbd restart```  
防火墙配置：```sudo ufw allow samba```  
添加用户：```smbpasswd -a pi```再输入密码就可以了  
电脑端：添加网络位置\\RASPBERRYPI\seagate之后输用户名密码

#### v2ray软件
先修改时区  
配置文件在/etc/v2ray/config.json  
得放行上面给的端口号  
如果需要套CDN ,需要将cloudflare里面SSL里Flexible改成Full

#### Mariadb数据库
- apt-cache search mysql  查看有哪些软件可以安装
- apt-get install mariadb-server mariadb-client
- systemctl start mariadb 启动
- systemctl enable mariadb 开机启动
- mysql_secure_installation 设置root用户的密码dbpontos
- mysql -u root -p进入数据库
- create database wordpress;    创建新数据库
- drop database wordpress;  删除数据库
- SELECT User , Host , Password FROM mysql.user;  查看有几个用户
- show databases; 查看有几个数据库
- 之后创建用户名并授权
> ```
> CREATE USER 'wp_user'@'localhost' IDENTIFIED BY 'wp123456' ;
> GRANT ALL ON wordpress.* TO 'wp_user'@'localhost' ;
> FLUSH PRIVILEGES;
> EXIT;
> ```

#### Nginx网站环境
- systemctl 管理开机启动
- 网站目录一般在/var/www/html/下
- 配置文件可以单独设置.conf ,放在默认配置文件conf.d文件夹下面就行
-  测试nginx配置 ```nginx -t```
- 重新载入配置  ```/etc/init.d/nginx reload``` （或者```nginx -s reload```）

#### 雅黑探针
安装PHP ,将探针php文件放到/var/www/html/tanzhen/下面 ,并改名为index.php  
之后新建nginx配置文件 ,让nginx能解析php

#### typecho博客
注意装完之后先在cloudflare里面关掉always use https ,然后用http登陆 ,之后在在配置文件config.inc.php 中加入一行
```
/** 开启HTTPS */
define('__TYPECHO_SECURE__',true);
```
再在cloudflare开启always use https  
另外将nginx文件中的```enable-php.conf```改成```enable-php-pathinfo.conf```（有2处）  
Nginx一般在/usr/local/nginx/conf/vhost/你的域名.com.conf  
不然会出错

#### Cloudflare使用
Cloudflare可以对域名进行转发 ,进而保护真实IP。
- 对于http服务来说 ,支持80/8080/2052/2082/2086/2095端口
- 对于https服务来说 ,支持443/2053/2083/2087/2096/8443端口

#### mutt发送邮件
- 安装mutt和msmtp：sudo apt install mutt msmtp
- 创建~/.msmtprc文件，内容如下（**需要给600权限**）：
> ```
> account default
> host smtp.126.com
> from qianyu_jiang@126.com
> auth login
> port 25
> tls on
> user qianyu_jiang@126.com
> password EXPBHRXCDYHTOSCE
> ```
- 创建~/.muttrc文件如下：
> ```
> set sendmail="/usr/bin/msmtp"
> set from="qianyu_jiang@126.com"
> ```
- 发送邮件：
> ```echo "内容" | mutt -s "主题" 379998894@qq.com```
> 
> ```echo "内容" | mutt -s "主题" 379998894@qq.com  -a /mnt/wd8t/历史经验的决议.docx```

#### 树莓派相关
- 树莓派开启SSH登陆并自动联网
> 在根目录创建SSH空白文件  
> 在根目录创建wpa_supplicant.conf文件（数字越大优先级越高）
- raspi-config配置
> 需要扩展根分区 ,让所有容量可用  
> 需要开启VNC功能
- 修改树莓派交换分区 SWAP
> ```sudo nano /etc/dphys-swapfile```  
> 将 CONF_SWAPSIZE 的值修改成你想要的大小
> 
> ```sudo /etc/init.d/dphys-swapfile restart```  
> 最后查看是否有变更：```free -h```
- 树莓派监控
> 使用motion软件
- 树莓派换TF卡
> 方法1：  
> ```sudo fdisk -l```  查看挂载的磁盘信息 ,mmcblk0是系统盘 ,sda是挂载上去的新卡  
> ```dd bs=4M if=/dev/mmcblk0 of=/dev/sda status=progress```  
> 操作完成后换新卡raspi-config拓展卡空间
> 
> 方法2：  
> 直接在VNC里面附件里面有SD卡复制选项 ,exfat的卡也可以用 ,会自动再进行分区
- 硬盘自动休眠
> 使用hd-idle  
> 
> ```sudo nano /etc/default/hd-idle```  
> 修改下面内定来开启hd-idle  
> ```START_HD_IDLE=true```  
> 
> 调整空闲时间为10分钟 (60 秒 * 10)  ，可选多个盘  
> ```HD_IDLE_OPTS="-i 0 -a sda -i 600"```   
> ```HD_IDLE_OPTS="-i 0 -a sda -i 1200 -a sdb -i 1200"```  
> 
> 重启服务：```sudo service hd-idle restart```
