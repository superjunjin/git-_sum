# git 命令行总结

------

## 下载

Git: https://git-scm.com/download 

TortoiseGit: https://tortoisegit.org/download/

## 图

![cmd-markdown-logo](http://static.open-open.com/lib/uploadImg/20140614/20140614202514_819.png)


## 配置
- 查看配置信息：git config [--global | system | local] --list
- 设置用户名：git config [--global | system | local] user.name <yourname>
- 设置用户邮箱：git config [--global | system | local] user.email <youremail@xxx.com>
- 设置git命令别名：git config [--global | system | local] alias.<newCommand> <originalCommand>
- 生成公钥：
  cd ~/.ssh
  ssh-keygen -t rsa -C "youremail@xxx.com" 两次回车
- 设置用户名密码授权：git config --global credential.helper osxkeychain
经过上面的设置，下次克隆 `HTTPS` 地址时会询问用户名和密码，并授权给osxkeychain，完成之后用户名和密码就会存储到keychain中，此后再也不会在 Git 中询问了。

## 通用简化命令
**`大写字母一般代表强制执行`**

**-r**：remote，操作远端命令 

**-a**：all，所有命令 

**-d**：delete，删除命令 

**-D**：强制删除命令 

**-b**：分支命令 

**-m**：重命名命令

## 基本命令
**git init**：对本地项目添加git管理

**git clone projectaddress newname**：克隆项目 
默认克隆项目到项目名字的文件夹，添加newname后，克隆到newname文件夹

**git add**：跟踪所有文件且暂存文件（新文件）或暂存文件（注意有点号）

**git commit -a -m 'added new marks'**： 
自动把所有已经跟踪过的文件暂存起来一并提交并添加注释（跳过 git add步骤）

**git status**：查看文件状态

**git pull**: 下拉远端代码到本地

**git push**: 提交本地代码到远端

## 分支
**git branch branchname**：新建分支

**git branch**：查询本地分支 

**git branch -r**：查询远端分支 

**git branch -a**：查询所有分支

**git branch -m | -M oldbranch newbranch**: 重命名分支，如果newbranch名字分支已经存在，则需要使用-M强制重命名，否则，使用-m进行重命名。

**git checkout branchname**：切换分支

**git checkout -b branchname**：新建并切换分支

**git branch -d | -D branchname**: 删除本地分支(注意不要再要删除的分支执行，切换到其他分支，再删除想删除的分支) 

**git push origin --delete branchname**: 删除远程分支

**git merge branchname**：合并分支 

eg：合并branchname到主分支： 

git checkout master 

git merge branchname

**git push --set-upstream origin branchname**：第一次push分支会报错，需用此命令提交

**git branch –merged**：查询已经合并分支 
一般来说，列表中没有 * 的分支通常都可以用 git branch -d 来删掉。原因很简单，既然已经把它们所包含的工作整合到了其他分支，删掉也不会损失什么。

**git branch –no-merged**：查询尚未合并分支 
由于这些分支中还包含着尚未合并进来的工作成果，所以简单地用 git branch -d 删除该分支会提示错误。 
不过，如果你确实想要删除该分支上的改动，可以用大写的删除选项 -D 强制执行。

## 通常使用步骤
### 从服务端获取项目
1. **git clone** 克隆项目到本地

2. **git checkout branchname** 切换到需要的分支

3. 增删改代码或文件（尽量在改之前，pull代码，保持本地代码最新状态，避免冲突）

4. 借助TortoiseGit工具，右键git commit，选好要commit文件，写好注释，然后commit，然后push（如果有要恢复到修改之前的文件，右键`revert`恢复）

5. 有时push不成功，需要先pull代码（远程主机的版本比本地版本更新，要先在本地做`git pull`合并差异，然后再推送到远程主机）

6. 有时pull之后有冲突，不想改或没有必要改，想恢复到pull之前状态。
  - 方法一：
     - **git reflog branchname**：会查看分支历史变动记录 

     - **git reset –hard branchname@{id}**：可以恢复到对应id的历史状态 

  - 方法二：

     - **git log**：查看之前提交记录 
     
         - **git log --pretty=oneline**：只查看commitid的方法
     - **git reset –hard commitId**：通过commit的id回退到那个状态

### 从本地新建项目
1. **git init**
2. **git add .** 跟踪所有文件且暂存文件（`注意有点号`）
3. **git commit -a -m 'init'**：(`执行此命令后，才有master主分支，才可以新建分支，否则会报错`)
4. **git branch branchname**：新建分支

## 其他命令使用

1. 从原项目获取所有的提交信息和完整项目，提交到新地址
 
 - **git clone –bare** 原项目地址 

 - **git push –mirror** 新项目地址

2. **git fetch**：与git pull相比git fetch相当于是从远程获取最新版本到本地，但不会自动merge。如果需要有选择的合并git fetch是更好的选择。效果相同时git pull将更为快捷。

## tortoisegit常用
1. git history 
选中文件，右键选择git history，可以查看文件修改历史

## tip
1. git log如何退出
英文状态下按Q

2. git 在pull或者合并分支的时候有时会遇到这个界面。可以不管(直接下面3,4步)，如果要输入解释的话就需要:

(1).按键盘字母 i 进入insert模式

(2).修改最上面那行黄色合并信息,可以不修改

(3).按键盘左上角"Esc"

(4).输入":wq",注意是冒号+wq,按回车键即可

## 参考
http://www.open-open.com/lib/view/open1402748724087.html


