## 1. SVN ##
1. [链接1](https://www.jianshu.com/p/6b3b7b915332 "链接1")
2. [链接2](http://keenwon.com/1072.html "链接2") 
3. [链接3](http://blog.sina.com.cn/s/blog_13cc013b50102wk5m.html "链接3")
## 2. git（在git bash中操作)
- [git 教程- 廖雪峰讲git](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000 "git 教程")
- [git 命令大全](https://blog.csdn.net/jtracydy/article/details/70402663 "git 命令大全")
- [git fetch 与 git pull](https://www.cnblogs.com/chenlogin/p/6592228.html "git fetch")

- 查看用户名和邮箱地址：

		$ git config user.name
		
		$ git config user.email  

- 设置、修改用户名和邮箱地址（如果你要修改当前全局的用户名和邮箱时，需要在上面的两条命令中添加一个参数，`--global`，代表的是全局。）

		$ git config --global user.name "username"
		
		$ git config --global user.email "email"

- pwd
	
		pwd 显示当前目录

- cd /f/gitStore

		cd /f/gitStore 进入盘符及文件夹（与cmd不一样）

- git init

		git init 初始化git仓库

- git add 

		`git add '文件名'` 将工作区修改的文件添加到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)
		`git add .` 将工作去所有的修改文件添加到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)
		`git add -u` 表示添加编辑或者删除的文件，不包括新添加的文件

- git rm filename  
	**git rm filename 指的是直接将删除文件放进暂存区(如果想撤销就是git reset HEAD -- filename, 撤销暂存区区，放回工作区。然后git checkout -- filename, 撤销工作区的修改)， 所以必须git commit 提交到版本库。**   

	**如果时rm filename, 是在工作区将filename删除(如果想撤销，直接git checkout -- filename,撤销工作区的修改)，接下来是git add 提交到暂存区， 最后是git commit 提交到版本库**   
 

		`git rm '文件名'` 从版本库里面删除文件  

		
- git commit
	
		git commit -m "备注提交信息" 将暂存区的文件提交到仓库

- git diff

		git diff 比较的是工作区文件与暂存区文件的区别（上次git add 的内容）

		git diff --cached 比较的是暂存区的文件与仓库分支里（上次git commit 后的内容）的区别
		
		git diff HEAD -- filename 比较的是工作区中的文件与版本库中文件的差异

- git log

		git log 查看显示从最近到最远的提交日志

		git log --pretty=oneline 查看显示从最近到最远的提交日志简单日志

		git log -1 显示最近一次的提交信息

- git status

		git status 查看显示工作区和暂存区有没有变化（可以让我们时刻掌握仓库当前的状态）
		git status 还可以在分支合并冲突的时候提示我们哪个文件冲突

- git reset --hard HEAD

		git reset --hard HEAD~2 
		用HEAD表示当前版本，上一个版本就是HEAD^，上上一个版本就是HEAD^^，
		当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100

- git reset --hard commitID

		git reset --hard commitID 回退到某个版本（commitID是版本号）

- git reflog

		git reflog 查看命令历史，以便确定要回到未来的哪个版本


- git checkout -- filename(撤销工作区的修改)

	 	git checkout -- filename 把工作区的修改全部撤销
		一种是文件自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
		一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
		总之，就是让这个文件回到最近一次git commit或git add时的状态。	

- git reset HEAD -- filename（撤销暂存区，重新放回工作区）


		git reset HEAD -- filename 把暂存区的修改撤销掉（unstage），重新放回工作区

- git clone（默认 ： 只能看到本地的master分支）

		git clone git@github.com:yanqiangsjz/website.git 将远程仓库克隆到本地开发（多人协作开发）

- git branch 分支名称

		git branch dev 创建dev分支  

		git branch 列出所有本地分支

		git branch -a 列出所有本地分支和远程分支

		git branch -d 分支名称 : 删除分支

		git branch -r 列出所有远程分支

- git checkout 分支名称

		git checkout dev 切换到dev分支

- git checkout -b 分支名称
	
		git checkout -b dev 创建并切换到dev分支

- git merge 分支名称（现在是在master分支上) -m '备注提交信息'（**合并之前必须都先commit，即工作区和暂存区使用git status 应该是没有文件，即是已经是最新的commit**）

		1. git merge dev 合并指定分支(dev)到当前分支(master)
		2. git merge --no-ff -m "备注提交信息" 分支名称   （--no-ff）强制禁用Fast forward模式，
		   Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。上边的方法也可以
		3. 合并冲突以后解决冲突以后必须：1、git add 2、git commit
		4. git merge的冲突判定机制如下：先寻找两个commit的公共祖先  
		   比较同一个文件分别在ours和theirs下对于公共祖先的差异，然后合并这两组差异
		   如果双方同时修改了一处地方且修改内容不同，就判定为合并冲突，依次输出双方修改的内容。
		5. 如果在dev分支上正在开发一个功能，但是这是master上需要解决一个bug，这时需要切换回master在开发出一个bug分支  
		   来解决这个bug，但是在dev分支上功能还没有开发完，不能commit。这时解决办法是：第一步、将dev分支上的工作现场  
		   ‘封存’起来，使用git stash。 第二步、 切换到新的bug分支将bug修改完然后切换回主分支将bug分支合并。  
		   第三部、 切换回dev分支，将bug分支同时也合并到dev分支（原因是 ： 避免是如果bug分支上修改的东西太多，在最后  
		   dev开发完成以后，master合并dev分支的时候出现大面积的冲突） 

    参考 ： **[git合并分支冲突原因](https://zhidao.baidu.com/question/1607297872270021147.html?qbl=relate_question_0&word=%B7%D6%D6%A7%D4%DA%CA%B2%C3%B4%C7%E9%BF%F6%CF%C2%BB%E1%BA%CF%B2%A2%D3%D0%B3%E5%CD%BB "git合并分支冲突原因")**

- git stash
		
		git stash 把当前工作现场“储藏”起来(如果在一个分支上修改了文件但是因为还没有修改完不能提交的时候，  
				  如果要开发出一个新的分支解决一个问题，如果不使用git stash， 那么在另一个分支上也是可  
				  以看到这个分支上修改的内容。  
				  主要是在不使用git stash的情况下，切换分支是失败的)
		结论 ： 1.工作区和暂存区是共用的，在各个分支里都可以看到没被stash的文件。
    		   2.在工作区和暂存区的文件都可以stash，pop之后都会出现在工作区
		
		git stash list 查看使用git stash 储藏起来的工作现场

		git stash apply 恢复工作现场（但是stash内容并不删除）

		git stash drop  删除stash内容

		git stash pop 恢复工作现场并删除stash内容

- git branch -D 分支名称

		git branch -D 分支名称  强制删除一个还没有合并的分支
		说明：如果一个分支在开发完成以后待合并，如果出于某种原因这个分支废弃了，但是这个分支必须删除。
			 如果一个分支还没有commit， 是可以使用 git branch -d 分支名称 删除的

- git remote

		git remote -v 查看远程库的信息

- git push origin master
		
		git remote -v master  将本地master分支推送到远程库

- git push origin dev

		git push origin dev  将本地分支dev推送到远程库

- git checkout -b dev origin/dev

     	git checkout -b dev origin/dev  多人协作时，如果同事从远程库clone时，默认情况下，
		你的同事只能看到本地的master分支。如果，你的同事要在dev分支上开发，就必须创建远程
		origin的dev分支到本地，就是这个命令

- git pull origin 分支名称 （取回远程仓库的变化，并与本地分支合并）

	 	git pull 在向远程库推送某个分支的时候，需要先"Git pull"更新本地的代码
	 	即 ： 如果你的同事先想dev分支或者master分支推送了他的提交，接下来你去推送很有可能会失败
		     因为你的同事最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，
		     先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送
		如果git pull  也失败了 ： 
					$ git pull
					remote: Counting objects: 8, done.
					remote: Compressing objects: 100% (6/6), done.
					remote: Total 8 (delta 2), reused 8 (delta 2), pack-reused 0
					Unpacking objects: 100% (8/8), done.
					From github.com:yanqiangsjz/rhjt
					   6876a33..e2516f8  oneline    -> origin/oneline
					There is no tracking information for the current branch.
					Please specify which branch you want to merge with.
					See git-pull(1) for details.
					
					    git pull <remote> <branch>
					
					If you wish to set tracking information for this branch you can do so with:
					
					    git branch --set-upstream-to=origin/<branch> oneline
		
		原因是 ： 没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
				 git branch --set-upstream-to=origin/dev dev


-  git branch --set-upstream-to=origin/dev dev

			git branch --set-upstream-to=origin/dev dev 设置dev和origin/dev的链接。成功以后就可以git pull

- git tag <tagname>（存储在本地）

		git tag <tagname>用于新建一个标签，默认为HEAD，也可以指定一个commit id

- git tag -a <tagname> -m "描述信息"

		git tag -a <tagname> -m "blablabla...

- git tag

		git tag 可以查看所有标签信息

- git show [tag]

		 git show [tag] 查看tag信息

- git tag -d <tagname>

		git tag -d <tagname> 删除本地标签

- git push origin <tagname>

		git push origin <tagname> 推送某个标签到远程

- git push origin --tags
		
		git push origin --tags 一次性推送全部尚未推送到远程的本地标签

- `git tag -d <tagname>` 然后  `git push origin :refs/tags/v0.9`

		git tag -d <tagname> 然后  git push origin :refs/tags/v0.9 删除远程标签

- git checkout -b[branch] [tag]

		git checkout -b[branch] [tag] 新建一个分支，指向某个tag

- git fetch (取回远程仓库的变化，但并不会主动与本地分支合并。这个比git pull 更安全)

		//方法一
		$ git fetch origin master //从远程的origin仓库的master分支下载代码到本地的origin master

		$ git log -p master.. origin/master//比较本地的仓库和远程参考的区别

		$ git merge origin/master//把远程下载下来的代码合并到本地仓库，远程的和本地的合并

		//方法二
		$ git fetch origin master:temp //从远程的origin仓库的master分支下载到本地并新建一个分支temp

		$ git diff temp//比较master分支和temp分支的不同

		$ git merge temp//合并temp分支到master分支

		$ git branch -d temp//删除temp

	 ***
 	**注意**： 命令执行以后出现"**:**"时，证明git bash 下边还有内容。可以点击回车查看  
	**注意**： 命令执行以后，若是 git bash 里面不能编辑新的命令，可以点击"**q**"键，即可继续输入命令  
	**注意**： `--global`参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。 如果不加，那只针对当前的仓库起作用。


- git config --global color.ui true

		git config --global color.ui true 让Git显示颜色

- git config --global alias.st status

		git config --global alias.st status 为git命令配置简单别名
		git config --global alias.last 'log -1'

## 3. gitHub ##

- 将本地git仓库同步到github上
	
		1. git remote add origin git@github.com:yanqiangsjz/newSite.git
		2. git push -u origin master
		3. 以后修改提交到远程库直接git push origin master就可以了

##4 webpack

- [webpack中文教程](https://www.webpackjs.com/)
- [入门教程](https://www.jianshu.com/p/42e11515c10f)
- [体积优化](https://www.jeffjade.com/2017/08/06/124-webpack-packge-optimization-for-volume/)
- [CommonsChunkPlugin-1](https://www.cnblogs.com/dong93/p/7655171.html)
- [CommonsChunkPlugin-2](https://segmentfault.com/a/1190000012828879)
- [webpack.DllPlugin-1](webpack.DllPlugin)
- [webpack.DllPlugin-2](https://www.douban.com/note/587230087/)
- [path与publicPath-1](https://www.jb51.net/article/116443.htm)
- [path与publicPath-2](https://www.jb51.net/article/139333.htm)