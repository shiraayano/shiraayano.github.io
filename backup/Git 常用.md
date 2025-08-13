# git工作流


![](https://cdn.nlark.com/yuque/0/2025/png/49455411/1754926453749-6542ce21-ad30-4bb7-ac7d-3be5def6c5a8.png)



工作区

平时写代码的地方

暂存区

git add 会把文件提交到暂存区

本地仓库

git commit 会把暂存区的文件提交到本地仓库

远程仓库

git push 会把文件push到远程仓库

git pull 从远程仓库拉取文件



1.git init 初始化仓库

这会在项目文件夹下创建一个.git 目录

2.git add . 将文件添加至暂存区

3.git commit -m "" 将暂存区的文件提交到本地仓库

git remote 将本地仓库与远程仓库关联

<font style="color:rgb(0, 0, 0);">git remote add origin https://github.com/user/repo.git</font>

4.git push

<font style="color:rgb(0, 0, 0);">git push -u origin master 第一次推送使用-u 将本地分支与远程分支关联起来</font>

<font style="color:rgb(0, 0, 0);">git push -u origin master:main 将本地的 master 分支关联远程 main 分支</font>

> 改名
>
> git branch -m main
>
> git push -u origin main
>



修改文件后工作区的文件状态会变为已修改

我们提交前先从远程拉取仓库git pull

git add .

git commit -m 

git push





```plain
#集中式工作流-经典的SVN式协作模式
#=开始工作前：同步最新代码=
git clone https://github.com/team/project.git
git pull origin main #获取团队最新更改
#=开发新功能=
#直接在main分支上开发
git add .
git commit-m"feat:添加用户认证功能"
#=推送更改
git push origin main
#==如果推送失败（有冲突）
git pull origin main
#拉取冲突的更改
#手动解决冲突·.
git add .
git commit-m"resolve:合并冲突"
git push origin main
#重新推送
```



> 遇到_<font style="color:rgba(0, 0, 0, 0.75);">non-fast-forward</font>_
>
> <font style="color:rgb(0, 0, 0);">git pull --rebase origin master</font>
>
> <font style="color:rgb(0, 0, 0);">git push -u origin master</font>
>



> 设置用户名/邮箱（用户签名）首次安装需要设置 （和远程仓库无关）
>
> $ git config --global user.name shiraayano
>
> $ git config --global user.email shiraayano@adouzi.eu.org
>



[https://www.runoob.com/git/git-create-repository.html](https://www.runoob.com/git/git-create-repository.html)

