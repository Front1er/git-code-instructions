# git code makes instructions

useful instructions links

[基于 VScode 的 git 详细使用指南【保姆级！建议收藏！】_vscode git-CSDN博客](https://blog.csdn.net/weixin_48024605/article/details/136037857)

[看完这篇还不会用Git，那我就哭了！ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/94008510)

[血泪教训之请不要再轻视Git —— 我在工作中是如何使用 Git 的 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/250493093)

[似懂非懂的Git —— 你也只会三招吗？ - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/107686455)


## 1 git native code versioning

### 1.1 git user name and email

```cmd
git config --global user.name "Your Name"
git config --global user.email "youremail@yourdomain.com"
```

confirm information:

```cmd
git config --list
user.name=Your Name
user.email=youreamil@yourdomain.com
```

### 1.2 set git alias

```cmd
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.logl 'log --oneline'
```

```cmd
~/.gitconfig
```

###  Initialize the repository

### manipulate

View the status of the current project:  `git st`

#### 初始化 Git

cd 命令导航到要在终端中设置版本控制的目录，初始化 Git：`git init`

#### 添加并提交

```cmd
git add <file>
git commit -m 'first commit'
```

#### 远程备份

```cmd
# 示例
git remote add origin \
https://github.com/wupeixuan/repo.git 
# 以我的一个仓库为例
git remote add origin \
https://github.com/wupeixuan/JDKSourceCode1.8.git
```

#### 代码推送

```cmd
git push origin master
```

#### 高级文件添加

```cmd
# 逐个添加文件
git add filename

# 添加当前目录中的所有文件
git add -A

# 添加当前目录中的所有文件更改
git add .

# 选择要添加的更改（你可以 Y 或 N 完成所有更改）
git add -p
```

#### 高级提交

```cmd
### 提交暂存文件，通常用于较短的提交消息
git commit -m 'commit message'

### 添加文件并提交一次
git commit filename -m 'commit message'

### 添加文件并提交暂存文件
git commit -am 'insert commit message'

### 更改你的最新提交消息
git commit --amend 'new commit message' 

# 将一系列提交合并为一个提交，你可能会用它来组织混乱的提交历史记录
git rebase -i
### 这将为你提供核心编辑器上的界面：
# Commands:
#  p, pick = use commit
#  r, reword = use commit, but edit the commit message
#  e, edit = use commit, but stop for amending
#  s, squash = use commit, but meld into previous commit
#  f, fixup = like "squash", but discard this commit's log message
#  x, exec = run command (the rest of the line) using shell
```

### 分支与合并

#### 分支

```cmd
### 创建一个本地分支
git checkout -b branchname

### 在2个分支之间切换
git checkout prc/dev-wupx
git checkout master

### 将新的本地分支作为备份
git push -u origin branch_2

### 删除本地分支，这不会让你删除尚未合并的分支
git branch -d branch_2

### 删除本地分支，即使尚未合并，这也会删除该分支！
git branch -D branch_2

### Viewing all current branches for the repository, including both ### local and remote branches. Great to see if you already have a ### branch for a particular feature addition, especially on bigger ### projects
### 查看存储库的所有当前分支，包括本地和远程分支。
git branch -a

### 查看已合并到您当前分支中的所有分支，包括本地和远程。 非常适合查看所有代码的来源！
git branch -a --merged

### 查看尚未合并到当前分支中的所有分支，包括本地和远程
git branch -a --no-merged

### 查看所有本地分支
git branch

### 查看所有远程分支
git branch -r

# 将主分支重新设置为本地分支
$ git rebase origin/master

# 将分支推送到远程存储库源并对其进行跟踪
$ git push origin branchname
```

#### 合并

```cmd
### 首先确保你正在查看 master 分支
git checkout master

### 现在将你的分支合并到 master 
git merge prc/dev-wupx
```

### 修复错误和回溯

```cmd
### 切换到最新提交的代码版本
git reset HEAD 
git reset HEAD -- filename # for a specific file
### 切换到最新提交之前的代码版本
git reset HEAD^ -- filename
git reset HEAD^ -- filename # for a specific file
### 切换回3或5次提交
git reset HEAD~3 -- filename
git reset HEAD~3 -- filename # for a specific file
git reset HEAD~5 -- filename
git reset HEAD~5 -- filename # for a specific file
### 切换回特定的提交，其中 0766c053 为提交 ID
git reset 0766c053 -- filename
git reset 0766c053 -- filename # for a specific file
### 先前的命令是所谓的软重置。 你的代码已重置，但是git仍会保留其他代码的副本，以备你需要时使用。 另一方面，--hard 标志告诉Git覆盖工作目录中的所有更改。
git reset --hard 0766c053
```

### 搜索

```cmd
### 搜索目录中的字符串部分
git grep 'project'

### 在目录中搜索部分字符串，-n 打印出 git 找到匹配项的行号
git grep -n 'project'

### git grep -C <行数> 'something' 搜索带有某些上下文的字符串部分（某些行在我们正在寻找的字符串之前和之后）
git grep -C<number of lines> 'project'

### 搜索字符串的一部分，并在字符串之前显示行
git grep -B<number of lines> 'project'

### 搜索字符串的一部分，并在字符串之后显示行
git grep -A<number of lines> 'something'
```

### 看谁写了什么

```cmd
### 显示带有作者姓名的文件的更改历史记录
git blame 'filename'

### 显示带有作者姓名和 git commit ID 的文件的更改历史记录
git blame 'filename' -l
```

### 日志

```cmd
### 显示存储库中所有提交的列表 该命令显示有关提交的所有信息，例如提交ID，作者，日期和提交消息
git log

### 提交列表仅显示提交消息和更改
git log -p

### 包含您要查找的特定字符串的提交列表
git log -S 'project'

### 作者提交的清单
git log --author 'wupx'

### 显示存储库中提交列表的摘要。显示提交ID和提交消息的较短版本。
git log --oneline

### 显示昨天以来仓库中的提交列表
git log --since=yesterday

### 显示作者日志，并在提交消息中搜索特定术语
git log --grep "project" --author "wupx"
```

![img](https://pic2.zhimg.com/v2-31a3f3d822e9c7cd2264054b0808ab61_r.jpg)

<img src="C:\Users\admin\AppData\Roaming\Typora\typora-user-images\image-20240630015530257.png" alt="image-20240630015530257" />
