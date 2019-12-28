环境变量
命令行添加，set PATH=%PATH%;C:\Program Files\Git\bin         
 或者
计算机系统——单击“高级系统设置”选项。
系统属性里单击选择——环境变量；
git 目录下的 bin（如 C:\Program Files\Git\bin ）添加到 PATH 环境变量。
选择 PATH——编辑，将 bin 的路径（ C:\Program Files \Git\bin ）添加到变量值后面  ！！！之間是分號
可以在 cmd 和 Git Bash 中使用 git 命令了。
//注意 以前C:\Program Files (x86)\Git\bin

          
输入帐号用户名和Email地址
$ git config --global user.name "yemengweixing"           //Your Name 用戶名
$ git config --global user.email "yemengzi@Outlook.com"   //Your Email 註冊郵箱
--global参数，表示你这台机器上所有的Git仓库都会使用这个配置


创建SSH Key
$ ssh-keygen -t rsa -C "yemengzi@Outlook.com"
C:\Users\MENGFUZI\.ssh     //C:\Users\用户名字目录\.ssh 

打开id_rsa.pub公钥文件，拷贝里面公钥文本       在SSH and GPG keys设置公钥



用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，
id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人

输入ssh git@github.com     测试是否连接上github
Warning: Permanently added the RSA host key for IP address 'ip地址' to the list of known hosts.

 //连接后的显示
PTY allocation request failed on channel 0
Hi yemengweixing! You've successfully authenticated, but GitHub does not provide shell access.
Connection to github.com closed.  

不同的电脑 都添加Key到GitHub     


////////////////////////////////////////////////////////////////////////////////////////////////////////////
命令

 $ mkdir learngit          建立文件夹
$ cd learngit             进入文件夹
$ pwd                     查看目录结构
/Users/文件夹             显示目录结构

 $ git init                    當前目录变成Git可以管理的仓库
Initialized empty Git repository in /Users/michael/learngit/.git/         当前目录下多了一个.git的目录

////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////

添加    （本地git库）将想要快照的内容写入缓存区   
 
git add . 命令来添加当前项目的所有文件
$ git add 文件名字带后缀名               git add告诉Git，把文件添加到仓库
//更某个文件
$ git add 文件名
 //更某个目录
$ git add 目录名/

执行 git reset HEAD 以取消之前 git add 添加，但不希望包含在下一提交快照中的缓存


提交（本地修改过的文件提交到本地库中）缓存区内容添加到仓库中
$ git commit -m "提交说明"              git commit把添加的文件提交
//1 file changed：1个文件被改动（我们新添加的readme.txt文件）；
2 insertions：插入了两行内容（readme.txt有两行内容）


关联到远程仓库（推送前要指定仓库）

 	
$ git remote add origin git@github.com:yourname/yourgit.git


推送（本地仓库的代码推送到远程主机的某个远程分支）本地库中的最新信息发送给远程库
git push <远程主机名> <远程分支名>
git push     命令，实际上是把当前分支master推送到远程
git push-u      加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起

git push -u origin master第一次推送master分支的所有内容
git push origin master推送最新修改

再次更新到仓库，使用 add>>commit>>push origin master 即可

//////////////////////////////////////////////////////////////////////////////////////////////////////////////////
提交后，用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别

git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”


git status命令可以让我们时刻掌握仓库当前的状态

git diff顾名思义就是查看difference（具体修改）查看执行 git status 的结果的详细信息，显示的格式正是Unix通用的diff格式

尚未缓存的改动：git diff
查看已缓存的改动： git diff --cached
查看已缓存的与未缓存的所有改动：git diff HEAD
显示摘要而非整个 diff：git diff --stat

$ git status
On branch master
nothing to commit, working tree clean
当前没有需要提交的修改，工作目录是干净（working tree clean）的


git log命令 查看历史记录
显示从最近到最远的提交日志（上到下）

$ git log --pretty=oneline       简化的记录
1commit id（版本号）2 提交信息          内容12

git reflog       查看命令历史            回到以前版本的 回到未来的哪个版本

HEAD表示当前版本  分支
(HEAD -> master)

git reset命令    
退到上一个版本     git reset --hard HEAD^
回退版本的时候，Git仅仅是把HEAD从指向以前版本

git reset --hard 版本号（git reset --hard commit_id）
版本号没必要写全，前几位就可以了  7位
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////.
把远程更新到本地仓库

　　　下载远程到本地 ：git fetch origin master

　　　合并远程到本地：git merge origin/master



克隆 拷贝
git clone <repo>      git clone [url]     指定目录    git clone <repo> <directory> 


拉取
git pull <远程主机名> <远程分支名> 

分支
master是指向提交的，HEAD指向的就是当前分支     (HEAD -> master)
列出分支： 查看分支数量

git branch               有*为当前分支

创建分支命令：

git branch (branchname)


切换分支命令:

git checkout (branchname)

合并分支命令:     任何分支合并到当前分支中去

git merge 

删除分支命令：

git branch -d (branchname)




检查已有的配置信息，可以使用 git config --list 命令：


rm命令 删除文件
rm  文件名字

git mv 修改名字

git mv 原名字 新名字




# tortoisegit 小乌龟

设置 网络
C:\Program Files\Git\usr\bin\ssh.exe