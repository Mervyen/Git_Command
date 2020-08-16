本地库，暂存区的操作指令
= = = =

1.初始化本地库<br>

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
##2.基本操作<br>
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


