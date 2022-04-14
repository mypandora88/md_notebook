## Github使用
#### 安装  
```
apt install git
```

#### 查看配置  
```
git config --list
```

#### 添加用户名邮箱
```
git config --global user.name "mypandora88"
git config --global user.email mypandora@protonmail.com
```

#### 配置ssh
```
ssh-keygen -t rsa -C "mypandora@protonmail.com" #首先在本地创建ssh key；
```
之后会要求确认路径和输入密码，我们这使用默认的一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key。

回到github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key,title随便填，粘贴你电脑上生成的key。

为了验证是否成功，在git bash下输入：
```
ssh -T git@github.com
```
如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。

#### 本地建库
```
cd /mnt/wdc/data/05-Using/Github/md_notebook #定位到要创建库的文件夹
git init #初始化
echo "this is a test file" > README.md #创建一个readme的文件
git add README.md #或者git add --all 往仓库里添加文件，把文件送到缓冲区
git commit -m "first commit" #将缓存区里的改动给提交到本地的版本库， first commit 是本次提交的信息
git branch -M main #选择哪个分支
```

#### 推送到github
```
git remote add origin git@github.com:mypandora88/md_notebook.git #只第一次的时候用
git push -u origin main
```

#### 创建分支
```
git branch new #新建分支new
git checkout new #切换到分支new
```
