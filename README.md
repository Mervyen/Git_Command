本地库，暂存区的操作指令
====

1.初始化本地库
-----
**1.1 初始化命令**
> * 命令：`git init`
> * 注意不要随意改动当前目录下`.git`文件内的东西

**1.2设置签名(标识个人)**
> * 命令（项目级别>系统级别)<br>

>项目级别：仅在当前项目有用（信息保存在`.git/config`）<br>
    git config user.name your_project_name <br>
    git config user.email your_project_emailAddr <br>
    
>系统级别：对存在于当前系统下的所有项目有用(信息保存在`~/.gitconfig`）<br>
        git config --global user.name your_system_name <br>
        git config --global user.email your_system_emaiAddr <br>
        
> * 用户名：andy<br>
    Email地址：tomato@gamail.com<br>
    用户名和Email可以不一样，只是同时用来标识和确认某一个自然人<br>

PS:如果之前已经配置过系统级别的签名了，那么以上两步可以直接用`git add`进行初始化<br>

2.基本操作
-----
**2.1 查看当前状态(工作区，暂存区)**<br>
> * 命令：`git status`
    
    
*在本地库的任何一个子目录（非新建子目录）内使用`git status`命令会查看到整个本地库的当前状态*。<br>
    
**2.2 加入暂存区**<br>
> * 命令：`git add`<br>

>如果想删除暂存区内的文件的话，可以使用命令`git rm --cached <file>`去删除暂存区内的这个文件。<br>

**2.3 加入本地库**<br>
> * 命令：`git commit -m "your_commitNote"`<br>

**2.4 查看本地库log**<br>
> * 命令：`git log`<br>

>在log后面还有添加一些参数，如`git log --oneline`,每条记录显示为一行<br>
`git log --pretty=oneline`每条记录显示为一行，比上一条命名会更加详细的显示`hash值`<br>

> * 命令：`git reflog`（推荐）<br>

>会显示指针，更加方便版本指针的操作<br>

**2.5 版本选择**
> * 命令：`git reset --hard TheVersionThatYouWantToGo(the hash value)`（推荐）
eg.`git reset --hard 0cbb3bc`

> * `git reset`的参数对比<br>
    --soft参数(较少使用)：①在本地库移动HEAD指针<br>
    --mixed参数(较少使用)：①在本地库移动HEAD指针②重置暂存区<br>
    --hard参数：①在本地库移动HEAD指针②重置暂存区③重置工作区<br>
    
> * 删除并找回（文件必须添加到本地库后才可以删除找回）<br>
    第一种情况：<br>
    在工作区删除之后，①执行了`git add`②执行了`git commit`。那么也可以通过HEAD指针将文件找回<br>
    第二种情况:<br>
    在工作区删除之后，①执行了`git add`并**没有**执行`git commit`。那么也可以通过HEAD指针将文件找回<br>
    
    
**2.6 文件比较**
> * 命令：`git diff`
> * `git diff`参数比较<br>
    --`git diff`：不指定文件名，将**暂存区**的所有文件与工作区的所有文件进行比较<br>
    --`git diff fileName`：指定文件名，将**暂存区**的该文件与工作区的该文件比较<br>
    --`git diff HEAD`:不指定版本和文件名，将**本地库**的最新版本的所有文件与工作区的所有文件进行比较<br>
    --`git diff HEAD fileName`：指定版本和文件名，将**本地库**的该版本文件与工作区该文件比较<br>

>**ps：** HEAD的一些操作：<br>
    HEAD^：表示上一个版本，有几个`^`就代表上几个版本。<br>
    HEAD~n：表示上`n`个版本，`n`是个常数。<br>
    

**2.7 分支操作**
> * 命令：
`git branch [branchNmae]`:创建名为“branchName”的分支。<br>
`git branch -v`:查看分支。<br>
`git checkout [branchName]`:切换到名为“branchName”的分支。<br>
 `git merge [branchName]`:合并分支**此处的branchname是有新内容的分支**<br>
 >>①先切换到接受修改的分支上`git checkout 接受修改的分支`<br>
 ②执行merge操作`git merge 有新内容的分支` <br>
 
> * 合并出现冲突<br>
    <<<<<<< HEAD<br>              
    apple   revise in hot_fix<br>
    =======                     <br>    
    apple revise in master branch``<br>
    >>>>>>> master<br>
如上文本显示：<br>
①**<<<<<<< HEAD**和***=======***之间显示的是当前分支的内容。<br>
②***=======***和**>>>>>>> master**之间显示的是另外一分支内容。<br>
手动选择需要留下那个部分，之后再add和commit就ok了。<br>
**注意此处的commit是不可以带文件名的！！！**<br>

---
远程库的操作指令
====
---
**·**`master`代表本地的master分支。<br>
**·**`origin master`前面的origin代表的是远程库的别名（在下面的1.2 有说明），后面的master代表的是远程的master分支名。<br> 
**·**`origin/master`代表一个概念，是远程的分支名。是将远程的代码通过`git fetch`拉取到本地后建立的一份拷贝。<br>
1.初始化远程库操作
-----
**1.1 创建远程库**
> * 选择github当做我们的远程库

**1.2 将本地库和远程库连接**
> * 命令`git remote add origin hhtps://xxxxxxxxxxxxx`。这样之后，我们每次提交都不需要输入hhtps：//xxxxx这一长串网络地址来了。这里的**origin**相当于我们hhtps这个地址的别名。（此处也可以使用ssh_key，形式如：git@github.com:yourName/yourRespositoriesName.git）

2.基本操作
-----
**2.1 拉取操作**
> * pull = fetch + merge
> * 命令:
`git pull [远程库别名][远程分支名]`：从远程库fetch并merge。<br>
`git fetch [远程库别名] [远程分支名]`：从远程库将最新的文件拉到本地，创建一个“[远程库别名/远程分支名]”的分支名。可以在使用*git checkout 分支名*切换到该分支查看。<br>
`git merge [远程库别名/远程分支名]`：在当前分支，将分支“[远程库别名/远程分支名]”合并到当前分支。<br>

> **注意事项**： <br>
①如果**本地库**的文件不是基于**远程库**最新版本进行的修改，是不可以先推送的，必须先拉取。<br>
②使用拉取命令之后，如果进入了冲突状态，则按照“本地操作的2.7 分支操作”进行处理。**处理完成后的commit是不可以带文件名的**<br>


