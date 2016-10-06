# Git教程

www.liaoxuefeng.com

`sudo apt-get install git` Linux上安装git

安装完成后的配置:

```git
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

`git init` 初始化一个Git仓库(Repository)

添加文件到Git仓库:

```git
git add xxx
git commit -m "xxx"
```

`git status` 仓库当前的状态

`git diff <file>` 查看修改

`git diff HEAD -- <file>` 查看修改

`git log` 查看提交日志

`git log --pretty=oneline` 一行显示日志

`commit id` 版本号

`HEAD` 当前版本，`HEAD^` 上一个版本，`HEAD^^` 上上个版本…… 100个`HEAD~100`

`git reset --hard HEAD^` 退到上一个版本

`git reset --hard commit_id` 退到指定版本（不必写全）

`git reflog` 查看历史命令（可查询commit_id重返未来)

`master` 主分支

`modified` 被修改了

`Untracked` 未被添加

```
         add                    commit
工作区     →       暂存区stage     →     分支branch（如master、dev）
          ←                       ←
          rm                     reset
```

`git checkout -- file` 撤销工作区的修改，回到最近一次`git commit`或`git add`时的状态。

`git checkout <name>` 切换分支

`git reset HEAD file` 把提交到暂存区的重新放回工作区

## 撤销修改：

场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考[版本回退](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013744142037508cf42e51debf49668810645e02887691000)一节，不过前提是没有推送到远程库。

## 删除：

`rm xxx` 从工作区中删除

`git rm` + `git commit` 从分支中删去

## 关联github

`$ ssh-keygen -t rsa -C "youremail@example.com"` 创建ssh key，用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

登陆GitHub，打开“Account settings”，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容

## 添加远程库

需要先在github上新建一个库

`git remote add origin git@server-name:path/repo-name.git` 关联一个远程库。例如：

`git remote add origin git@github.com:michaelliao/learngit.git` 关联github.com的远程库learngit

`git push -u origin master` 关联后一次性推送master分支的所有内容

`git push origin master` 向远程库提交修改

## 从远程库克隆

`git clone git@github.com:michaelliao/gitskills.git` 使用SSH

`git clone https://github.com/michaelliao/gitskills.git` 使用HTTPS（要输密码）

## 分支

查看分支：`git branch`

创建分支：`git branch <name> `

切换分支：`git checkout <name>` 

创建+切换分支：`git checkout -b <name> `

合并某分支到当前分支：`git merge <name> `

删除分支：`git branch -d <name> `

merge时冲突，改冲突文件，改完`git add` `git commit` 

`git log --graph` 分支合并图

`git log --graph --pretty=oneline --abbrev-commit` 同上，好看一点

`$ git merge --no-ff -m "merge with no-ff" dev` --no-ff模式合并

合并分支时，加上`--no-ff`参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而`fast forward`合并就看不出来曾经做过合并。



- 忽略某些文件时，需要编写`.gitignore`；
- `.gitignore`文件本身要放到版本库里，并且可以对`.gitignore`做版本管理！



配置别名示例：`git config --global alias.st status`

配置Git的时候，加上`--global`是针对当前用户起作用的，如果不加，那只针对当前的仓库起作用。

每个仓库的Git配置文件都放在`.git/config`文件中

## 标签

- 命令`git tag `用于新建一个标签，默认为`HEAD`，也可以指定一个commit id；
- `git tag -a  -m "blablabla..."`可以指定标签信息；
- `git tag -s  -m "blablabla..."`可以用PGP签名标签；
- 命令`git tag`可以查看所有标签。