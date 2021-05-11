# Git简要笔记

**Git结构**

工作区-暂存区-仓库

## 基本操作

**本地库初始化**

`git init`

**设置签名**

- 项目级别/仓库级别

  ```git
  cd 项目目录
  git config user.name test
  git config user.email test@test.com
  ```

- 系统用户级别

  ```
  git config --global user.name test2
  git config --global user.email test2@test.com
  ```

**查看工作区和暂存区状态**

`git status`

**把工作区中新建/修改的文件放入暂存区**

`git add 文件名`将某个文件放入暂存区

`git add .`将所有文件放入暂存区

**从暂存区移除文件**

`git rm --cached 文件名`

**从暂存区的内容提交到本地库**

`git commit -m "提交说明" 文件名`

**查看版本记录**

`git log` 显示完整的版本记录

`git log --pretty=oneline` 每行一个版本记录，且记录完整的版本hash值

`git log --oneline` 每行一个版本记录，且记录部分版本hash值

`git reflog`  每行一个版本记录，且记录部分版本hash值和HEAD信息

**基于索引指定版本**

`git reset --hard 索引值` 推荐的方式，索引值的部分值，通过reflog查看的hash值

`git reset --hard HEAD^1` 只能回退，其中符号^代表回退的步数，一个为一步，即上一个版本

`git reset --hard HEAD~2` 只能回退，其中数字2代表回退的步数

**比较文件**

`git diff 文件名` 将工作区的文件与暂存区文件比较

`git diff HEAD 文件名` 将工作区的文件与本地库历史记录比较

`git diff` 比较多个文件

## 分支管理

**创建分支**

`git branch 分支名`

**查看分支**

`git branch -v`

**切换分支**

`git checkout 分支名`

**合并分支**

`git checkout 分支名` 切换到要接受修改的分支 

`git merge 分支名` 执行合并命令，该分支名为有修改的分支 

## Github操作

**注册和新建仓库**

https://www.github.com

**创建远程仓库别名**（创建者）

`git remote add origin https://github.com/test/test.git`  将远程仓库地址改为别名`origin`

`git remote -v` 查看远程仓库的别名信息

**本地仓库推送到远程仓库**（创建者）

`git push origin master` 其中`origin`为远程仓库地址，`master`为本地仓库需要推送的分支

**克隆操作**（参与者A，需要创建者邀请）

`git clone https://github.com/test/test.git`

克隆操作完成以下三个动作：

- 完整下载远程库到本地
- 创建远程地址别名
- 初始化本地库

**拉取操作**（创建者）

pull=fetch+merge

`git fetch origin master` 下载远程库信息，不会修改本地文件信息，`origin`为远程仓库地址，`master`为远程仓库分支

`git merge origin/master` 合并远程库和本地库文件

`git pull origin master` 拉取远程仓库文件

**协同开发时的冲突**

- 如果不是基于远程仓库最新版进行修改，不能推送，必须先拉取文件
- 拉取后如果进入冲突状态，按照“分支冲突解决”操作解决（参考界面提示）

**跨团队协作**

* 参与者B要fork一份，再clone到本地修改，之后push到远程仓库
* pull request到创建者，创建者审核之后merge