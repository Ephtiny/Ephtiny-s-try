# 创建版本库

## 创建仓库

1.先通过下面代码创建一个空目录

```
$ mkdir learngit
$ cd learngit
$ pwd
```

​	这里的pwd用于显示当前目录

2.通过`git init`命令把这个目录变成Git可以管理的仓库

```
$ git init
```

​	在把仓库创建好后会有一个隐藏的.git目录，可以通过 `ls -ah`查看

​	`ls`为查看当前目录的文件

## 在仓库中添加文件

1.用`git add`把文件添加到仓库（下面的<>在输入时是不需要的）

```
$ git add <文件名.后缀>
```

2.用`git commit`把文件提交到仓库

```
$ git commit -m "说明"
```

​	-m后面输入的是本次提交的说明

​	可以通过`add`一次添加多个文件，然后用`commit`一次性提交，如：

```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```

​	可以使用`ls`或`dir`查看当前目录的文件

# 时光机穿梭

## 文件修改查询与仓库的当前状态

1.在文件修改后，后续如果要查看到上次提交前修改了什么可以通过下面的代码进行查询

```
$ git diff <文件名>
```

​	也可以直接通过`git diff`查询（不添加文件名），尝试后可以，但因只是修改了一个文件，出现的只是一个文件的修改，多个文件的修改暂未尝试

2. `git status` 可以让我们时刻掌握仓库当前的状态，如告诉我们哪个文件被修改了但还没准备提交修改、准备提交什么、还有什么文件没有提交

## 版本回退

1.可以通过 `git log` 获得从最近到最远的提交日志，其中 `commit` 后面的一串十六进制的数值是 `commit id` （版本号），日志如下：

```
$ git log
commit 45f1c55881db3755631c2bf4565b488e2916a5bd (HEAD -> main)
Author: Ephtiny <you@example.com>
Date:   Fri Apr 7 22:19:35 2023 +0800

    append GPL

commit fb179a134f34b67ef6d60679b2df34d214952b4e
Author: Ephtiny <you@example.com>
Date:   Fri Apr 7 22:17:24 2023 +0800

    未尝试修改多个文件后直接用git diff查询

commit 79081cab329009fb9a0800c7c22ef426f6117ecd
Author: Ephtiny <you@example.com>
Date:   Fri Apr 7 22:10:27 2023 +0800

    “

commit ec4b0942e2dd21f6712aab0b20ada52ff156b768
Author: Ephtiny <you@example.com>
Date:   Fri Apr 7 22:02:01 2023 +0800

    add distributed
```

​	上面的日志未显示完全，可以通过回车键往下翻	

​	如果觉得显示太多还可以用 `git log --pretty=oneline` 即加上后面这个参数，效果如下：

```
45f1c55881db3755631c2bf4565b488e2916a5bd (HEAD -> main) append GPL
fb179a134f34b67ef6d60679b2df34d214952b4e 未尝试修改多个文件后直接用git diff查询
79081cab329009fb9a0800c7c22ef426f6117ecd “
ec4b0942e2dd21f6712aab0b20ada52ff156b768 add distributed
3721d97507e4531a6706564ab3a35c455dd0fdd6 写了一个readme.txt
c21f50e5ea976f0ff86da1ed70c48d28a64e1cd4 (origin/main) add readme
```

未完待续...

# 远程仓库

GitHub提供Git仓库托管服务，只需注册一个GitHub账号就可以免费获得Git远程仓库

注册后由于本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以需要一点设置（创建过SSH Key的不需要再创建）：

1.创建SSH Key：

```shell
$ ssh-keygen -t rsa -C "youremail@example.com"
```

​	把上面的邮件地址换成自己的，然后一路回车使用默认值即可

​	一切顺利的话可以再用户主目录里找到`.ssh`目录，里面有 `id_rsa`和 `id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对， `id_rsa`是私钥，不能泄露出去， `id_rsa.pub`是公钥，可以放心地告诉他人

2.登录GitHub，点击右上角头像的settings里的SSH and GPG keys，点击New SSH key，填上任意Title，在Key文本框里粘贴 `id_rsa.pub`文件的内容后，点击Add Key

## 添加远程库

1.登录GitHub，然后New repository，创建远程仓库，其中仓库名称最好别是中文，如Digital Circuit

​	接下来GitHub会给出一些基础的帮助

![image-20230418174534770](https://gitee.com/ephtiny/image/raw/master/img/202304182149797.png)

2.在本地的Digital Circuit仓库下运行下面的命令

```
$ git remote add origin git@github.com:Ephtiny/Digital-Circuit.git
```

​	其中的`Ephtiny`为用户名，`Digital-Circuit`为仓库名

​	远程库的名字就是 `origin`，这是默认叫法，也可以改成别的

3.把本地库的所有内容推送到远程库上

```
$ git push -u origin master
```

​	`git push`实际就是把当前分支 `master`推送到远程

​	由于远程库是空的，第一次推送 `master`分支时加上了 `-u`参数，Git不但会吧本地的 `master`分支内容推送到远程心的 `master`分支，还会把本地的 `master`分支与远程的 `master`分支关联起来，在以后推送或者拉取时就可以简化命令

## 从远程库克隆

1.选择一个库点击Code中SSH下的复制键

2.自选一个位置git bash here，并输入

```
$ git clone git@github.com:Ephtiny/Ephtiny-s-try.git
```

​	`git clone`后面的为复制内容

## 同步远程仓库

1.将修改添加到暂存区

```
$ git add .
```

2.填写修改信息

```
$ git commit -m ""
```

3.将更新同步到远程仓库

```
$ git push origin main
```

​	这里最后的部分不一定是main，而是代码段上一行最后的括号里的内容，如图：

![image-20230425204846578](https://gitee.com/ephtiny/image/raw/master/img/202304252048653.png)
