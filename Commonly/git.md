[toc]
# git <br/>
git 是一种==开源==的==分布式==版本控制系统，快速，高效的处理从小型到大型项目的所有==事物管==理。

### git与svn的区别
git |svn
---|---
分布式 | 集中式
历史版本可以存储完整的文件，便于恢复 | 存储差异文件，历史版本不可恢复 
可以离线完成，自动记录每一次修改，并可以方便切换版本 | 不可以离线完成大部分操作

==git最强大的优点是分支管理==


### 常用的命令

命令 | 说明
---|---
git config --list  | 获取git的配置项
git config 配置项名 | 获取具体的配置项名
git config --gobal 配置项名 新名字 | 修改新配置项
git init | 初始化本地版本库
git status  |把工作区的所有修改提交到暂存区
git add 文件路径 | 把工作区指定文件提交到暂存区
git commit -m "描述" |把暂存区的修改提交本地版本库（master分支）
git diff | 查看工作区具体修改
git diff -cached | 查看暂存区具体修改
git log | 查看历史记录（在英文状态下Q退出当前状态）
git reflog | 可以查看所有分支的所有操作记录（包括包括已经被删除的 commit 记录和 reset 的操作）
#### 撤销
###### 第一种情况 撤销工作区的修改

```
git checkout 文件路径
git checkout . 所有文件
```
###### 第二种情况 撤销暂存区的修改

```
git reset 文件路径 //把暂存区的修改撤回工作区
git checkout 文件路径
```
###### 第三种情况

```
git reset --hard HEAD^//退回上一个版本
git reset --hard HEAD^^//上上个版本
HEAD^^//回到n个版本上
```
###### 回到指定版本

```
git reset --hard commitId

如何获取所有版本的commit_id呢？
针对这个需求，需要分两种情况：
*	第一，git bash窗口没有关闭，使用前面查过的commit_id
*	第二，git bash窗口关闭。比如，昨天做的操作，今天后悔了。 使用 git reflog

```
### git 分支管理

命令 | 说明
---|---
git branch 分支名 | 创建分支
git branch |查看本地所有分支
git branch -r|查看远程所有分支
git branch -a|查看本地和远程所有分支
git checkout 分支名 |切换分支
git checkout -b 分支名 |创建并切换分支
git branch -d|删除本地分支
### 命令窗口退出（英文状态下）

```
:wq  //强制退出当前
q    //退出git log 描述
```









