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

 

\---

 

**操作顺序：**

>   `git add test.txt`

>   `git commit`

或

>   `git commit -a -m 注释`

删除文件同理，要将版本库中的同时删除

 

\---

 

 
