# Learn_git

---

## git 是什么

---

分布式   版本控制   系统

来历：linus  花了两周时间用C写的用来管理 linux 源代码  （牛！！！）

发展：08年 GitHub 上线  免费为开源项目提供 git 储存

版本控制：你对你的代码进行多次修改  （多个版本）  想看到前后修改的区别 或者想  恢复先前的项目

分布式&集中式

集中式：从图书馆借书  改了后  还给图书馆  版本库在中央服务器  必须联网才能工作 从中央服务器下载任务

修改  上传至中央服务器

分布式：版本库在每个人的电脑上	工作时不需要联网  多人协作时将各自修改部分互相推送

通常有一台电脑来充当“中央服务器” 但仅仅是用来交换大家的修改内容 没有他照样用

版本控制系统只能追踪文本文件的改动 不能追踪二进制文件的变化  不能控制word word是二进制文件

---

## 安装 Git

---

---



## 创建版本库

---

在一个目录下  git init  命令

会生成一个隐藏的  .git 目录 用ls -ah 命令可以看见（追踪管理版本库）

---

## 添加文件进版本库

---

被添加文件一定在在git 仓库（版本库 repository)目录下

git add readme.md

git commit -m"提交说明"

git add 文件1

git add 文件2

git add 文件3

git commit -m"提交三个文件"

add添加需要提交的文件

commit -m""提交这些文件并附带说明

---

## 查看仓库状态

---

git status

---

## 查看文件修改状态

---

git diff 文件名

查看哪些被修改的地方

---

## 查看历史日志

git log 

git log --pretty=oneline  输出更简单一点

git reflog  记录操作日志

---

## 版本表示

---

HEAD 表示当前版本

HEAD^ 表示向前退一个版本

HEAD^^ 

HEAD~100 退100个版本

---

## 版本退回

---

### git reset --hard HEAD^  (hard留在后面讲？)

### 注意：在 cmd 中 ^ 被认为是换行符  会报错

git reset --hard commit_number版本穿梭

##工作区和暂存区

---

## 工作区

创建 放置文件的目录

## 版本库 （repository）

隐藏目录 .git 

版本库里有  stage master HEAD

## stage (暂存区)

git add 将工作区的文件提交到暂存区

暂存区 可以放置多个文件

多个文件（同一批次 一次任务）可以使用 git commit -m 命令 一次提交到 master 		

## 管理修改

git diff HEAD --readme.md

可以查看工作区和版本库修改的区别

第一次 修改 

git add

第二次修改

git commit

提交无效

git add

git commit

才有效

---

##撤销修改

git checkout -- 文件名

 a. 没有git add 在工作区修改 后 想撤销

 b. git add 后  在工作区  又修改  撤销后 成 git add 内容

git reset HEAD file

将 stage 中的 文件退回 工作区 然后用  git checkout -- 文件名 撤销修改



## 删除文件

rm test.txt

test.txt 是已提交到 repository 中 的文件

则 可以

git rm 文件名  删除改文件

git commit -m"删除信息"

或者

git checkout -- 文件名 恢复文件  只能恢复到删除前状态

---

## 远程仓库（第一个特性）

---

​	

github 与git  之间是  SSH 加密的

用户主目录  .ssh  id_rsa id_rsa.pub(后缀可能被系统隐藏  publisher  xx 文件)

在git bash  创建 SSH

ssh-keygen -t rsa -C "youremail@example.com"

一路回车

在git hub 中 找到 SSH key  添加  id_rsa.pub （公钥）

---

## 添加远程库

---

关联远程库

git remote add origin git@github.com:yourname(path)/learngit(repo-name).git

第一次推送git push -u origin master

以后：git push origin master

---

##从远程库克隆

---

git clone git@github.com:richardlmy\gitskills.git

---

## 分支管理

---

#### 创建和合并分支

---

git branch 查看分支

git branch <branch name> 创建分支

git checkout  <branch name>切换分支

git checkout -b <branch name> 创建并切换分支

·git merge <branch name > 将某分支合并到当前分支

git branch -d <branch name> 删除分支

---

### 冲突处理

---

合并分支时当两个分支内容有冲突  合并时会报冲突错误  此时需要修改 冲突内容

---

### 分支管理策略

---

git merge --no--ff -m"说明“ branch name

可以保留分支的信息

用 git log --graph --pretty=oneline

实际管理，master 应该是主线内容  dev 应该是我们干活的那一部分

---

### BUG分支

---

BUG 分支 讲的是 当前正在工作  突然发现其他部分有BUG 

此时用 git stash (将手上工作保存)

再去其他分支 去 新建一个分支 处理BUG

处理后 删除 分支 git branch -d  branch name

回到 原分支  git checkout 分支

git stash pop 回到现场 删除 stash

git stash list 可以查看stash

---

### Feature 分支  管理

---

用于新特性的开发

需要新开发一个新功能  则 再开一个新分支处理  git checkout -b feature-test

git add test1 

git commit -m"test1"

开发好了后 准备提交

此时需要舍弃新功能

git branch -D feature-test  删除分支

---

### 多人协作

---

 git remote 用来查看远程库的信息

git remote -v  显示更详细的信息

 git push origin master 将master 分支推送到远程库对应的 master分支上

mater分支 是主分支必须时刻同步

dev分支 是工作分支 也需要时刻同步

feature分支 取决于是否合作开发

bug分支 一般不推送除非BOSS要看你修复的BUG

因此，多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin branch-name`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin branch-name`推送就能成功！

如果`git pull`提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream branch-name origin/branch-name`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

### 标签

git tag <tagname>  给当前HEAD指向的操作打标签

git tag 可以查看所有的标签

git show <tagname> 可以查看tag 标签信息

git tag -a <tagname> -m"说明信息"  commit id

git tag -s<tagname> -m"说明信息"  commit id  PGP签名的标签

#### 操作标签

删除：git tag -d tagname

推送到远程库：git push origin <tagname>

git push origin --tags所有标签

删除远程标签

1. 先删除本地 git tag -d name

2. ```
   git push origin :refs/tags/v0.9
   ```



配置别名

git config --global alias.st status







​	























​	



