# GIT和BASH操作

#### 在指定目录创建GIT仓库
```
cd d:
mkdir gitspace
cd gitspace/
git init
```

#### 检查当前目录路径和文件
```
pwd
ls
```

#### 增加文件或者文件夹，提交并附带说明，需要先配置EMAIL和名字以知道是谁提交的更改
```
git add filename
git config --global user.email "fte@foxmail.com"
git config --global user.name "R2BP"
git commit -m "尝试提交GIT和BASH的MARKDOWN笔记"
```

#### 检查是否有文件有更改，查询更改内容，确认后ADD和提交commit更改
```
git status
git diff filename
git commit -a filename -m "-a类似ADD，-m添加说明"
```

> Q：如果避免每次ADD，如何一次添加大量文件/文件夹？

#### 查询改动历史，确定版本号,跳转到指定版本git reset --hard commit_id
```
git log
git log --pretty=oneline
git reflog
```

> commit id可以是log中形如837ea565ae445fe4ea4430d2c8b9431c2cf3e9af或者837ea56的HASH值，
也可以用代表上一个版本的HEAD^，
上上一个版本就是HEAD^^，往上100个版本写100个^比较容易数不过来，可写成HEAD~100.

> 每次修改，如果不用git add到暂存区，那就不会加入到commit中

> 命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
总之，就是让这个文件回到最近一次git commit或git add时的状态。

> git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令

> git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。

>[关于ADD,commit,diff，暂存区和工作区的讨论，注意评论](https://www.liaoxuefeng.com/wiki/896043488029600/897271968352576)

#### 从硬盘和版本库中删除文件
```
rm filename
git rm filename
git commit
```

#### 创建SSH Key，设置好GITHUB的SSHKEY后，在GITHUB创建REPO，提交本地项目到远程
```
ssh-keygen -t rsa -C "fte@foxmail.com"
git remote add origin https://github.com/softe/hellogit.git
或者
git remote add origin git@github.com:softe/hellogit.git
git push -u origin master
```
> Git支持多种协议，包括https，但通过ssh支持的原生git协议速度最快。

> URL可以通过修改.git目录下的config文件修改

> 使用https除了速度慢以外，还有个最大的麻烦是每次推送都必须输入口令，但是在某些只开放http端口的公司内部就无法使用ssh协议而只能用https。

#### 过多尝试导致版本过多，强制重启版本
```
git checkout --orphan latest_branch
git add -A
git commit -am "清除所有历史版本以减少仓库大小，请重新从远程拷贝此仓库"
git branch -D master
git branch -m master
git push -f origin master
```
>[重启版本BAT](https://blog.csdn.net/COCO56/article/details/95109142)

#### 增加需要push的远程库
```
git remote set-url --add origin git@gitee.com:r2bp/leetcode-cn.git
```

[两个连接多远程库的方法](https://blog.csdn.net/mengzuchao/article/details/80489864)