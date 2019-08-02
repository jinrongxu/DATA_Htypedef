[toc]
# gitHub
gitHub是一个==网站==，==开源==及==私有软件项目==的==托管平台==，因为只支持==git== 。
### 本地项目推送远程仓库
仓库内部无文件
```
git init //初始化本地仓库
git add .//工作区提交暂存区
git commit -m "描述" //提交仓库
git remote add origin GitHub仓库地址（远程仓库地地址ssh）
git remote -v //查看关联远程仓库
git push origin master（仓库名）//推送到远程仓库
```
### 远程仓库克隆到本地
远程仓库内存在文件（readme.md）

```
git clone 仓库地址//在远程仓库上克隆
git add . //工作区提交暂存区
git commit -m "描述"//提交仓库
git pull origin master//远程代码拉取到本地工作区
git push origin master//提交到远程仓库
```
### 分支管理
实际开发中，应该按照几个基本原则进行管理：<br/>
首先，==master分支是非常稳定的==，仅用来发布新版本，==平时不能在上面干活==；干活都在dev分支上，
==dev分支是不稳定==的，你和你的小伙伴们每个人都在dev分支上干活，==每个人都有自己的分支==，都往dev分支上合并。比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本
