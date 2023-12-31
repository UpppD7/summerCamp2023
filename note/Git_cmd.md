Git命令
=======

初始化、新建、删除、配置
------------------------

`git -v` 查看当前git版本号

`git init` 创建git仓库（初始化）

`git clone https`  将远程仓库内容下载到本地

`git config xxx xxx` 本地配置

`git config --global xxx xxx` 全局配置

`git config -l` 获取软件的配置信息

`git status` 查看暂存区文件状态

`git add filename` 把文件放入暂存区

`git rm --cached filename` 把暂存区的文件放入工作区

`git commit -m 注释` 暂存区文件存入仓库中



---



**操作顺序：**

>   `git add test.txt`

>   `git commit`

或

>   `git commit -a -m 注释`

删除文件同理，要将版本库中的同时删除

 

---



## 日志、恢复

`git log` 查看版本库信息

`git log --oneline` 一行显示（仅显示前七位版本号）

`git log --graph` 查看操作日志（列表）

`git restore filename` 恢复误删除文件（未删除历史版本）

`git reset --hard 版本号` 恢复误删文件（可能丢失历史提交）

`git revert 版本号`  将当前版本库还原到所给版本号提交之前的操作



---



## 新建、切换、合并分支

`git branch XXXX` 创建分支（基于已有的提交）

`git branch -v` 查看所有分支（星号*为当前所在分支）

`git checkout xxx` 切换到xxx分支

`git checkout -b xxx` 创建并切换到xxx分支（两步合成一步）

`git branch -d xxx` 删除某分支

`git merge new_branch` 将新分支合并到当前分支（若有冲突，自行修改文件再重新提交到主干分支中）



---



## 标签，拉取、推送远程库

`git tag`  显示目前所有标签

`git tag xxx 版本号` 给已知版本号的历史记录添加标签xxx（不能重复）

`git tag -d xxx` 删除标签xxx

`git log 标签名` 查找所给标签名之前的所有历史记录

`git push 远程仓库名 分支名` 推送到远程仓库（第一次push要在push后面加`-u`）

`git pull 远程仓库名 分支名` 拉取远程仓库到本地



 

 
