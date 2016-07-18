# gitskills
#0.0 Git 分布式版本控制系统
* 1.Git与其他版本控制系统的差异
	* Git 和其它版本控制系统（包括 Subversion 和近似工具）的主要差别在于 Git 对待数据的方法。
	* 提交更新，或在 Git 中保存项目状态时，它主要对当时的全部文件制作一个快照并保存这个快照的索引。 为了高效，如果文件没有修改，Git 不再重新存储该文件，而是只保留一个链接指向之前存储的文件。 Git 对待数据更像是一个 快照流。
	* 近乎所有操作都是本地执行,在 Git 中的绝大多数操作都只需要访问本地文件和资源.
	* Git 保证完整性
	* Git 一般只添加数据

* 2.三种状态
	Git 有三种状态，你的文件可能处于其中之一：已提交（committed）、已修改（modified）和已暂存（staged）。
	由此引入 Git 项目的三个工作区域的概念：Git 仓库、工作目录以及暂存区域。
	基本的 Git 工作流程如下：
	* 在工作目录中修改文件。
	* 暂存文件，将文件的快照放入暂存区域。
	* 提交更新，找到暂存区域的文件，将快照永久性存储到 Git 仓库目录。
* 没有'中央服务器', 每一台电脑都是一个完整的版本库, 与集中式版本控制系统最大区别是没有联网就可以操作.

#1.0 Git基础
##1.1 Git基础_安装
* 1 安装 ---> git bash
* 2 全局配置username和email:
	* git config命令的--global参数为全局配置, 但是可以通过对某个仓库	指定不同的用户名和Email地址.
##2.0 Git基础_创建版本库
* 1 版本库 repository 目录中的文件由Git管理, 修改删除由Git跟踪
* 2 创建版本库:
	* mkdir 路径  创建空目录
	* cd  路径    转到路径
	* pwd 		显示当前目录
	* git init  初始化仓库-->创建仓库
	* git add	添加
	* git commit -m'message' 提交
* 3 修改并提交
	* 修改 ---> 修改 ---> 提交
##3.0 Git基础_时空穿梭机
* 1 查看状态
	* 查看工作区的状态:	git status 
	* 查看文件是否被修改以及修改内容:	git diff + 文件
	
###3.1 Git基础_时空穿梭机 _版本退回
* 1 HEAD指针
	* Git内部有个指向当前版本的HEAD指针,退回某个版本时,Git仅仅是将HEAD调整了指向, 并更新了工作区文件
* 2 回到过去  HEAD 版本操作
	* 1 版本日志显示:git log 
		* 查看简洁信息: git log --pretty=oneline 参数
	* 2 版本表示: 
		* HEAD^ 上一个版本 HEAD^^ 上上个版本  HEAD~100 前100个版本
	* 3 版本退回操作:
		* git reset --hard HEAD^ 退回上一个版本 
		* git reset --hard 版本号 退回到该版本号版本
	* 4 查看当前文件内容: cat + 文件名
	* 5 退回上一个版本 wrote a 文件名 file
* 3 回到未来  commit id 进行版本操作
	* 1 git reflog 记录每次命令, 可以查看到commit id
	* 2 回到未来: git reset --hard commit_id

###3.2 Git基础_时空穿梭机 _工作区和暂存区
* 工作区 working directory
	* pc中的工作目录   learngit文件夹
* 版本库 repository
	* 版本库隐藏目录".git" 
		* 暂存区 stage
		* master分支: git自动创建的第一个分支
		* 指针HEAD
* 向Git版本库中添加的步骤:
	* 1 git add, 将文件添加到暂存区 stage
	* 2 git commit, 将暂存区文件提交到当前分支

###3.3 Git基础_时空穿梭机 _管理修改概念
* Git管理修改, 每次修改如果不add到stage, 就不会被commit

###3.3 Git基础_时空穿梭机 _撤销修改
* 场景1: 仅仅修改了工作区文件，撤销: git checkout -- file
* 场景2: 修改了工作区文件并add, 撤销: git reset HEAD file 回到场景1 ---> git checkout -- file
* 场景3: 已经提交, 撤销: 版本退回  git reset --hard 版本id/HEAD^

###3.3 Git基础_时空穿梭机 _删除文件
* 删除操作: rm test.txt  并 commit
* 删错之后恢复: 将误删文件恢复到最新版本: git checkout -- test.txt


##4.0 远程仓库 GitHub

##4.1 远程仓库 GitHub_添加远程库
* 1 关联远程库: git remote add origin git@server-name:path/repo-name.git
* 2 关联之后第一次推送master分支内容: git push -u origin master
* 3 此后提交执行: git push origin master

##4.2 远程仓库 GitHub_从远程仓库克隆
* 从远程仓库克隆一个仓库到本地, 需要直到仓库的的地址: git clone git@github.com:GitHub用户名/repo-name.git
* Git支持多种协议, 包括https, 通过ssh支持的原生git协议速度最快

##5.0 分支管理

##5.1 分支管理_创建与合并分支
* 应用场景: 分支需要完全完成后合并到主分支
* 原理:HEAD指向的就是当前分⽀支。
⼀一开始的时候，master分支是⼀条线，Git⽤master指向最新的提交，再用HEAD指向master，就能确定当前分⽀，以及当前分支的提交点
每次提交，master分支都会向前移动⼀一步，这样，随着你不断提交，master分⽀支的线也越来越长。
当我们创建新的分支，例如dev时，Git新建了⼀一个指针叫dev，指向master相同的提交，再把HEAD指向dev，就表示当前分支在dev上
假如我们在dev上的⼯工作完成了，就可以把dev合并到master上。Git怎么合并呢？最简单的方法，就是直接把master指向dev的当前提交，就完成了合并
* 操作:
	* 查看分支: git branch
	* 创建分支: git branch name
	* 切换分支: git checkout name
	* 创建并切换: git checkout -b name
	* 合并某分支到当前分支: git merge name
	* 删除分支: git branch -d name

##5.2 分支管理_解决冲突
* 当Git无法自动合并分支时, 必须先解决冲突, 然后再提交, 合并完成.
* 合并冲突时, Git标记出不同分支的内容:  需要修改后保存
	  <<<<<< HEAD
	  ======
	  <<<<<< feature1
* 查看合并图: git log --graph --pretty=oneline --abbrev-commit

##5.3 分支管理_分支管理策略
* 分支管理原则
	* 1 master分支稳定, 仅仅用来发布新版本, 不应该经常修改
	* 2 dev分支进行修改操作, dev分支不稳定, 如果到需要版本发布时将dev分支合并到master上, 并发布版本
* --no-ff参数, 在合并分支时添加就可以使用普通模式合并, 合并后有历史分支,能对历史进行查看. 而fast forward合并并看不出曾经做出的合并.

##5.4 分支管理_Bug分支
* 修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；当⼿头⼯作没有完成时，先把⼯作现场 git stash ⼀一下，然后去修复bug，修复后，再 git stash pop ，回到⼯作现场。
* 操作命令:
	* 工作区暂时储藏: git stash
	* 确定分支修复bug, checkout 分支
	* 修复bug, 提交, 回到主分支, checkout master
	* 查看工作现场存储, git stash list
	* 恢复并删除: git stash apply  git stash drop  或者直接 git stash pop	

##5.5 分支管理_Feature分支
* git branch -D 分支name  强行删除分支
##5.3 分支管理_多人协作
* 多人协作工作模式:
	* 1. ⾸先，可以试图⽤ git push origin branch-name 推送自己的修改；
	* 2. 如果推送失败，则因为远程分⽀支⽐比你的本地更新，需要先用 git pull 试图合并；
	* 3. 如果合并有冲突，则解决冲突，并在本地提交；
 	* 4. 没有冲突或者解决掉冲突后，再⽤用 git push origin branch-name 推送就能成功！
 	* 5 如果 git pull 提⽰“no tracking information”，则说明本地分支和远程分⽀支的链接关系没有创建，用命令 git branch --set-upstream branch-name origin/branch-name 。
* 为了避免冲突, push到远程之前先pull

##6.0 标签管理
• 命令 git tag name ⽤用于新建⼀一个标签，默认为HEAD，也可以指定⼀一个commit id；
• -a tagname -m "blablabla..." 可以指定标签信息；
• -s tagname -m "blablabla..." 可以⽤用PGP签名标签；
• 命令 git tag 可以查看所有标签；

##6.1 操作标签
• 命令 git push origin tagname 可以推送⼀一个本地标签；
• 命令 git push origin --tags 可以推送全部未推送过的本地标签；
• 命令 git tag -d tagname 可以删除⼀一个本地标签；
• 命令 git push origin :refs/tags/tagname 可以删除⼀一个远程标签。

##7.0 使用GitHub
• 在GitHub上，可以任意Fork开源仓库；
• ⾃自⼰己拥有Fork后的仓库的读写权限；
• 可以推送pull request给官⽅方仓库来贡献代码。

##8.0 自定义Git
* 1. 忽略某些⽂文件时，需要编写.gitignore。
* 2. gitignore⽂文件本⾝身要放到版本库⾥里，并且可以对.gitignore做版本管理

* 配置别名
	* $ git config --global alias.st status  ---> git status 更改为 git st
	* $ git config --global alias.别名 原命令

						--------------2016/7/13 10:50