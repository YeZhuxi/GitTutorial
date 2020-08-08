注: [] 表示此处内容根据用户实际情况替换



## 用户配置

-   git config --global user.name "[username]" 配置用户名
-   git config --global user.email "[user@example.com\]" 配置邮箱
-   git config user.name 查看当前用户名
-   git config user.email 查看当前用户邮箱



## 基本文件操作和命令

-   cd E: 进入E盘
-   mkdir [directoryname] 创建目录, 如testgit
-   cd [directoryname] 进入目录
-   pwd 显示当前目录
-   touch [filename] 创建文件, 如readme.txt
-   cat [filename] 显示文件内容
-   rm [filename] 删除文件
-   ls\dir 查看当前目录内容
-   clear 清屏
-   reset 重置



## 修改提交

-   git init 把目录变成可管理仓库(添加.git目录)
-   git add [filename] 添加到暂存区
-   git commit -m "[注释]" 提交到工作区
-   git commit --amend 对当前提交节点再次提交, 不产生新的子节点
-   git status 查看是否有文件未提交
-   git restore [filename] 提交之前丢弃修改
-   git diff [filename] 查看被修改的内容



## 版本管理

-   git log 查看历史记录
-   git reset --hard [ref] ref是某个提交记录的引用, 对远程分支无效
-   git reset --hard HEAD^ 相对引用, 退回到上个版本
-   git reset --hard HEAD^^ 退回到上上个版本,依此类推
-   git reset --hard HEAD~[number] 回退到前number个版本
-   git reset --hard [hash] 直接引用, 退回到hash对应的提交
-   git revert HEAD 通过再提交一次上个版本回退到上个版本, 对远程分支有效
-   git reflog 获取version
-   git reset --hard [version] 退回到指定版本
-   git checkout -- [filename] 丢弃工作区的修改





## 分支管理

-   分支

    ​	在版本回退里，每次提交，Git都把它们串成一条时间线，这条时间线就是一个分支。截止到目前，只有一条时间线，在Git里，这个分支叫主分支，即master分支。HEAD严格来说不是指向提交，而是指向master，master才是指向提交的，所以，HEAD指向的就是当前分支, 不同分支上的修改互不影响

-   git branch 查看分支, 当前分支前会添加一个 * 号

-   git branch [branchname] [ref] 在ref创建分支, ref默认为当前位置

-   git checkout [branchname] 切换分支

-   git checkout [ref] 分离HEAD, 使其指向指定的提交, commit可以用相对\绝对引用表示

-   git checkout -b [branchname] 创建并切换分支

-   git merge [branchname] 合并到当前分支

-   git branch -d [branchname] 删除分支

-   git branch -f master [ref] 强制使master指向某个提交

-   git rebase [dstbranchname] [srcbranchname] 把src分支复制到dst位置, src默认为当前分支

-   git cherry-pick [ref1 ref2...] 把提交记录复制到当前位置

-   git rebase -i HEAD~[number] 交互式rebase

-   git tag [tagname] [ref] 给指定提交添加tag

-   git describe [ref] 查看距离ref最近的标签

-   bug分支

    -   在开发中，会经常碰到bug问题，每个bug都可以通过一个临时分支来修复，修复完成后，合并分支，然后将临时的分支删除掉
    -   比如在开发中接到一个404 bug时候，可以创建一个404分支来修复它，但是，当前分支上的工作还没有提交
    -   并不是不想提交，而是工作进行到一半时候，还无法提交，比如当前分支(假设分支名是dev)要2天完成，但是bug需要5个小时内完成。怎么办呢？Git提供了一个stash功能，可以把当前工作现场 "隐藏起来"，等以后恢复现场后继续工作
        -   git stash 隐藏dev未提交的修改
        -   git stash list 查看历史stash
    -   创建issue-404分支来修复bug, 首先确定在哪个分支上修复bug, 比如master
        -   git checkout master 切换到分支master
    -   在master上创建一个临时分支
        -   git checkout -b issue-404 创建并切换到分支issue-404
    -   修复完成后, 切换到分支master, 合并分支issue-404, 然后删除
        -   git checkout master
        -   git merge issue-404
        -   git branch -d issue-404
    -   回到dev分支, 恢复stash内容
        -   git checkout dev 切换到分支dev
        -   恢复法一
            -   git apply 恢复stash内容到dev
            -   git stash drop 删除stash
        -   恢复法二
            -   git stash pop 恢复并删除stash



## 远程仓库

-   创建SSH Key 

    -   打开cmd
        -   ssh-keygen -t rsa -C "[user@example.com]"
        -   id_rsa是私钥,id_rsa.pub是公钥
    -   登录GitHub --> 点击头像 --> settings --> SSH and GPG keys --> new SSH key
        -   Title随便填
        -   把公钥内容复制粘贴到Key, 点击Add SSH key
    -   完成, 可以看到自己添加的SSH了

    

-   添加远程仓库

    -   登录GitHub --> 点击右上角"+"图标 --> New repository, 创建一个新的仓库
    -   Repository name填写本地仓库名称
    -   默认是Public, 可以修改为Private, 这样只有自己可以看到
    -   点击Create repository, 创建成功

-   链接

    -   在本地仓库运行如下命令, 关联本地库
        -   git remote add origin [url]
    -   在本地仓库运行如下命令, 把master分支内容推送到远程仓库
        -   git push -u origin master
        -   第一次需要 -u 参数, 把本地master分支和远程master分支关联
    -   成功, 在GitHub页面可以看到远程仓库内容和本地一致
    -   从现在起, 只要本地做了提交, 就可以通过如下命令把新修改推送到远程仓库
        -   git push origin master
    -   通过如下命令, 可以把远程仓库克隆到本地
        -   git clone [url]



## 多人协作

-   从远程库克隆时，Git自动把本地的master分支和远程的master分支对应，并且远程库的默认名称是origin
-   git remote 查看远程库信息, 增加参数 -v查看详细信息
-   推送分支
    -   要指定本地分支名
        -   git push origin master
        -   git push origin dev
    -   master是主分支, 要时刻与远程同步
    -   一些bug分支不需要推送到远程, 可以先合并到master, 然后把master推送到远程
-   抓取分支
    -   多人协作时，大家都会往master分支上推送各自的修改。现在模拟另外一个同事，在另一台电脑上(要把SSH key添加到GitHub上)或者同一台电脑上另外一个目录克隆，新建一个目录名字叫testgit2
    -   首先把dev分支推送到远程
    -   接着进入testgit2, 把远程库克隆到本地
    -   把远程origin的dev分支到本地来
        -   git checkout -b dev origin/dev
    -   开发完推送到远程
    -   伙伴已经向origin/dev分支上推送了提交，而我在我的目录文件下也对同样的文件同个地方作了修改，也试图推送到远程库时, 推送失败，因为伙伴最新提交的和我试图推送的有冲突
    -   先用把最新的提交抓取下来, 然后再本地合并
        -   git branch --set-upstream dev origin/dev 指定本地dev分支与远程origin/dev分支的链接
        -   git pull 抓取成功, 但是有冲突
        -   解决冲突方法和分支管理解决冲突方法一样, 解决后再push