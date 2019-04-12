## 1、 git（在git bash中操作)

- 明确一些git中的概念
		
		-） git版本管理工具中四个区域概念：

			(1)Workspace：工作区

			(2)Stage：暂存区

			(3)Repository：仓库区（或本地仓库）

			(4)Remote：远程仓库
	
			其中工作区和暂存区在各个不同的分支中是共享的（方便理解stash操作）

		-）git中一些单词的大概意思

			(1) HEAD   表示当前版本，上一个版本就是HEAD^(可以写为HEAD~1)，上上一个版本就是HEAD^^^^^(可以写为HEAD~5),
 
		-) git中文件状态

			(1) untracked：新建的文件，没有git add [filename] 的都属于未被git追踪到文件
			
			(2) 未加入到暂存区的文件: 指的是已经被追踪（tracked）过，但是没有加入到暂存区(已经执行过git add的但是这次修改后还没有git add)	
			
		-）远程库

			(1) origin : git给远程库起的默认名称是origin

- git init

		git init 初始化git仓库

		git init [program-name] 新建一个目录，将其初始化为Git代码库

- git clone（默认 ： clone下来的版本只能看到master分支， 如果，想要在dev分支上开发，就必须创建远程
origin的dev分支到本地）

		git clone git@github.com:yanqiangsjz/website.git 将远程仓库克隆到本地开发（多人协作开发）

		git checkout -b [branch] [remote]/[branch] （创建远程[remote]的[branch]分支到本地。  一般远程仓库和本地仓库分支命名一样）
		
- git config （--global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用。  如果不加，那只针对当前的仓库起作用。）

		git config --list 显示当前的Git配置

		git config user.name 查看用户名

		git config user.email  

		git config --global user.name [username] 设置全局用户名

		git config --global user.email [email]

		git config --global color.ui true 配置Git显示颜色

- git add 

		git add [filename]  添加指定文件到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)

		git add [dir]  添加指定目录到暂存区，包括子目录    

		git add .  添加当前目录的所有文件到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)

		git add -u  表示添加编辑或者删除的文件，不包括新添加的文件

- git rm filename  
	
		git rm [filename] 删除工作区文件并放进暂存区
		如果想从暂存区撤销：git reset HEAD -- [filename]
		如果想撤销工作区的修改：git checkout -- [filename]

		注意区别 : rm [filename]  删除工作区文件, 并没有放进暂存区
		如果想撤销工作区的修改：git checkout -- [filename]

		git rm --cached [filename]	停止追踪文件，但该文件会保留在工作区(untracked状态)
 

- git diff

		git diff [filename] 比较的是工作区文件与暂存区文件的差异

		git diff --cached [filenam] 比较的是暂存区的文件与上一个commit的差异
		
		git diff HEAD -- [filename] 比较的是工作区与当前分支最新commit之间的差异

- git status

		git status 查看文件状态; 还可以在分支合并冲突的时候提示哪个文件冲突

- git commit
	
		git commit -m [message]  暂存区提交到仓库区

		git commit [filename1] [filename2] ... -m [message]  暂存区的指定文件提交到仓库区

		git commit -a -m [message]  工作区中修改后，还未使用git add . 命令添加到暂存区中的文件也一并提交上去 
		相当于git add . 与git commit –m [message] 两句操作合并为一句进行使用。commit完成过后，git status,
		下方的工作区是干净的

- git log

		git log 查看当前分支的版本历史
		
		git log --stat 查看commit历史，以及每次commit发生变更的文件

		git log --pretty=oneline 查看从最近到最远的提交日志简单日志（--pretty=oneline：单行模式）

		git log -1 查看最近一次的提交信息

		git log -n 查看最近n次的提交信息

		git log --graph  查看分支合并图

		git log --graph --pretty=oneline  查看分支合并图；简单日志

		git reflog 查看命令历史，以便确定要回到未来的哪个版本

- git blame

		git blame [filename]  查看指定文件是什么人在什么时间修改过

- git shortlog

		git shortlog -sn 查看所有提交过的用户，按提交次数排序

- git show
		
		git show [commit] 显示某次提交时，文件变化
		
		git show [commit]:[filename]  显示某次提交时，某个文件的内容(注意[commit]:[filename]冒号之间没有空格)

- git checkout (1)

	 	git checkout -- [filename]  工作区filename的修改撤销

		git checkout . 撤销工作区的全部修改

		解释 ：一种是文件修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
		一种是文件已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
		总之，就是让这个文件回到最近一次git commit或git add时的状态。	

- git checkout (2)

		git checkout [branch] 切换分支

		git checkout -b [branch] 创建并切换到该分支(如果在切换分支的时候，未commit, 有可能会报错)

- git checkout (3) 

		git checkout -b [branch] [remote]/[branch]
		说明：
	 	多人协作时，如果同事从远程库clone时，默认情况下，你的同事只能看到本地的master分支。如果，你的同事要在（[branch]）分支上开发，
		就必须创建远程([remote])的([branch])到本地
		
		
- git reset (1)

		git reset [filename] 重置暂存区的指定文件，与上一次commit保持一致，工作区不变

		git reset --hard  重置暂存区与工作区，与上一次commit保持一致

		git reset --hard HEAD~2  回退到某个版本(这里是从当前版本回退两个版本)

		git reset --hard commitID 回退到某个版本（commitID是版本号）

- git reset (2)

		git reset HEAD -- [filename] 把暂存区的修改撤销（unstage），重新放回工作区
		

- git branch 分支名称

		git branch [branch] 创建分支  

		git branch 列出所有本地分支

		git branch -a 列出所有本地分支和远程分支

		git branch -r 列出所有远程分支

		git branch -d [branch] 删除分支

		git branch -D [branch]  强制删除一个还没有合并（已经commit）的分支

		说明：
		1、如果一个分支在开发完成以后（分支已经commit）待合并，如果出于某种原因这个分支废弃了，但是这个分支必须删除。git branch -D [branch]
		2、如果一个分支还没有commit， 是可以使用 git branch -d [branch]


- git merge (merge之前必须都先commit，即工作区和暂存区使用git status 应该是干净的工作区域，即是已经是最新的commit)

		git merge [branch] 合并指定分支([branch])到当前分支

		git merge --no-ff -m [message] [branch] 合并指定分支([branch])到当前分支,禁用Fast forward模式

		解释 : 禁用Fast forward模式,Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

		必要 : 如果merge出现冲突， 则解决冲突以后必须：1、git add 2、git commit。

		建议 :
		(1 解决完成冲突以后，最好直接将分支删除，如果需要，再新建一条分支。原因是在解决冲突了以后，如果还切换回之前的分支继续开发，
		分支还是冲突发生前的内容（解决冲突只解决的主分支master的（而且冲突解决不是全部按照分支内容解决的）所以再次提交会报错。
		(2 如果合并冲突完全放弃原来主分支的冲突采用dev分支的内容，则合并后主分支的内容和现存在dev分支是一样的内容，不删除原来的分
		支继续在上面开发也是可以的

		冲突判定机制 : 先寻找两个commit的公共祖先，比较同一个文件分别在ours和theirs下对于公共祖先的差异，然后合并这两组差异如果
		双方同时修改了一处地方且修改内容不同，就判定为合并冲突，依次输出双方修改的内容

		分支策略 : 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；那在哪干活呢？干活都在dev分支上,
		也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；每个人
		都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

		补充建议 : 如果在dev分支上正在开发一个功能，但是这是master上需要解决一个bug，这时需要切换回master在开发出一个bug分支  来解决
		这个bug，但是在dev分支上功能还没有开发完，不能commit。这时解决办法是：第一步、将dev分支上的工作现场  ‘封存’起来(git stash)
		第二步、 切换到主分支，新建主分支的bug分支，将bug修改完然后切换回主分支将bug分支合并。 第三部、 切换回dev分支，将bug分支同时
		合并到dev分支（原因是 ： 避免是如果bug分支上修改的东西太多，在最后  dev开发完成以后，master合并dev分支的时候出现大面积的冲突）

- git stash
		
		git stash list 查看使用储藏起来的工作现场

		git stash apply 恢复工作现场（但是stash内容并不删除）

		git stash drop  删除stash内容

		git stash pop  恢复工作现场并删除stash内容
		

		说明：
		git stash 只能“储藏”已被追踪过的文件。意思就是说如果是新添加的文件还没有执行过`git add`的文件，在使用git stash后还是会在工作区中出现，
		并不会别“储藏”。所以要使用git stash, 请将untrack状态的文件执行git add, 使其可被git追踪

		git stash 把当前工作现场“储藏”起来(如果在一个分支上修改了文件但是因为还没有修改完不能提交的时候，  如果要开发出一个新的分支解决一个问题，
		如果不使用git stash， 那么在另一个分支上也是可以看到这个分支上修改的内容。)

		结论 ： 
		1.工作区和暂存区是共用的，在各个分支里都可以看到没被stash的文件。
    	2.在工作区和暂存区的文件都可以stash，pop之后都会出现在工作区
		
		
		说明 : 假设在dev分支上正在开发，忽然程序出现bug,需要即刻修复，但是dev分支上的任务还没有完成，无法提交合并到master。
		但是现在就需要在master上创建一个分支bugs去修复这个问题。因为工作区和暂存区对所有分支默认都是共用的，所以在bugs分支
	    上会执行dev分支上未完成的修改。这样是不允许的。所以我们可以在dev分支中git stash 将dev分支
		中的工作区和暂存区隐藏起来，这样在别的分支中就看不到dev分支工作区中和暂存区中的已有的工作，这意味着工作区是干净的。我们可以在
		bugs分支中可以看到工作区是干净的，可以执行任意我们的任务。等待bugs分支开发完成，再切换到master分支，接着将bugs分支merge
		到master。但是现在我们思考一下，现在主分支是最新的（修复了bugs并且merge上去的)，但是我们的dev分支却还是和未修复bugs的
		master主分支同步的版本。如果这样的话，在我们开发完dev分支并且合并到master分支上时，就有可鞥会出现问题（除非是增加文件，否则就
		会出现合并冲突）。如果我们的dev分支版本现在不存在master中存在的bug,则我们完全可以放心。但是如果dev中也会出现像master
		中出现的bug,则当我们将dev合并到master中时，还是会出现同样的bug。主要是在这种情况下，还会发生合并时候冲突。所以在将bugs
		合并到master以后，我们也可以选择将bugs分支合并到dev分支中，合并完成之后，现在master和dev中的代码是一样的。但是我们之前
		在dev中执行了git stash, 还有“储藏”的工作区中已经开发但未提交的内容，当我们执行git stash pop 恢复之前的工作现场并删除
		stash内容，会发现有冲突发生了（因为现在dev分支和master分支是一样的，现在该文件是已经修复完成的， 但是我们释放的工作区中之前就对
		该文件做了修改：同一个文件不同的内容，这样就会明显的出现冲突）。这是我们就需要解决这些冲突（其实就是将之前修改的删掉，保留和现在
		master主分支中的文件一样的信息）。解决完成以后。我们就完全解决了以后dev合并到master中可能存在的冲突，并且在合并以后不会再出现同样
		的错误		


- git remote (git给远程库起的默认名称是origin)

		git remote -v 查看远程库的信息

		git remote show [remote] 显示某个远程仓库的信息

		git remote add [remote] [url] 增加一个新的远程仓库，并命名 (一般是origin)

		git remote rm [remote]  删除远程库
		

- git push 
		
		git push [remote] master  将主分支推送到远程库
		
		git push [remote] [branch] 将([branch])分支推送到远程库

		git push [remote] --delete [branch] 删除远程分支

		git push [remote] [tagname] 推送某个标签到远程

		git push [remote] --tags 一次性推送全部尚未推送到远程的本地标签

     	
- git pull origin 分支名称 （取回远程仓库的变化，并与本地分支合并）

	 	git pull [remote] [branch]  取回远程仓库的变化，并与本地分支合并

		说明 : 在向远程库推送某个分支的时候，需要先"Git pull"更新本地的代码

	 	即 ： 如果你的同事先在dev分支推送他的提交，接下来你去推送很有可能会失败。因为你的同事最新提交和你试图推送的提交有冲突，
		解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，
		git add -> git commit -> 再推送

		如果: git pull 也失败了 ： 
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
		
		原因 ： 没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：git branch --set-upstream-to=origin/dev dev

		git pull --rebase origin master 远程库同步到本地库  （解决的问题：error: failed to push some refs to ‘git@gitee.com:name/project.git’）


-  git branch --set-upstream-to=origin/dev dev

			git branch --set-upstream-to=origin/dev dev 设置dev和origin/dev的链接。成功以后就可以git pull

- git tag 

		git tag [tagname] 为当前HEAD打标签（本地tag）
		
		git tag [tagname] commitId（commitId 默认未HEAD; 本地tag）

		git tag -a [tagname] -m [message] commitId 为本地tag添加说明

		git tag 查看所有标签信息

		git show [tagname] 查看某个tag信息

		git tag -d [tagname] 删除本地标签


- 删除远程标签

		git tag -d [tagname] -> git push [remote] :refs/tags/[tagname]

		说明：git tag -d [tagname]（先从本地删除）;  git push [remote] :refs/tags/[tagname]（然后，从远程删除）


- git checkout -b [branch] [tag]

		git checkout -b[branch] [tagname] 新建一个分支，指向某个tag


- git fetch (取回远程仓库的变化，但并不会主动与本地分支合并。这个比git pull 更安git全)

		//方法一 例子
		git fetch origin master //从远程的origin仓库的master分支下载代码到本地的origin master

		git log -p master.. origin/master//比较本地的仓库和远程参考的区别

		git merge origin/master//把远程下载下来的代码合并到本地仓库，远程的和本地的合并

		//方法二
		git fetch origin master:temp //从远程的origin仓库的master分支下载到本地并新建一个分支temp

		git diff temp//比较master分支和temp分支的不同

		git merge temp//合并temp分支到master分支

		git branch -d temp//删除temp


## 2. gitHub ##

- 将本地git仓库同步到github上
	
		1. git remote add [remote] [url]
		
		2. git push -u [remote] [branch] （指定[remote]为默认主机）
		
		3. 以后修改提交到远程库直接git push [remote] [branch]就可以了  (不带任何参数的git push，默认只推送当前分支)

## 3、 git自定义

- 忽略特殊文件

		有些时候，你必须把某些文件放到Git工作目录中，但又不能提交它们，比如保存了数据库密码的配置文件啦，等等，
		每次git status都会显示Untracked files ...，有强迫症的童鞋心里肯定不爽。好在Git考虑到了大家的感受，
		这个问题解决起来也很简单，在Git工作区的根目录下创建一个特殊的.gitignore文件，然后把要忽略的文件名填
		进去，Git就会自动忽略这些文件不需要从头写.gitignore文件，GitHub已经为我们准备了各种配置文件，
		只需要组合一下就可以使用了。所有配置文件可以直接在线浏览. 查看请点击下面的链接 

	 [https://github.com/github/gitignore](https://github.com/github/gitignore "github")


- 配置别名（--global参数是全局参数，也就是这些命令在这台电脑的所有Git仓库下都有用,针对当前用户。如果不加，那只针对当前的仓库起作用。）

		git config --global alias.st status （为查看状态配置别名）
		git config --global alias.last 'log -1' （为显示最后一次提交信息配置别名）
		git config --global alias.unstage 'reset HEAD' (为暂存区的修改撤销回工作区配置别名)
		git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
		
		那么配置文件放在哪里呢：

		(1) 每个仓库的Git配置文件都放在.git/config文件中
		(2) 当前用户的Git配置文件放在用户主目录下的一个隐藏文件.gitconfig中 
		(3) 我们可以直接在配置文件中进行配置
		



	
		


- git 上传项目到github一般流程
		

		1、本地项目git init -> git add . -> git commit -m '注释'
		2、在github上创建项目
		3、git remote add [remote] [url]
		4、如果在github上创建的项目不包含README.md（即使一个空文件夹），则
		git push -u origin master 直接就可以了
		5、如果在github上创建的项目包含README.md，但是在本地的文件夹中
		没有这个文件， 首先 git pull --rebase origin master（依照远程库README.md内容为准）
		将远程库同步到本地库，然后 git push -u origin master 就可以了
		6、如果在github上创建的项目包含README.md, 本地文件夹中也包含这个文件，则
		git pull origin master --allow-unrelated-histories，然后如果发现有
		冲突则解决冲突（也可以使用git fetch origin master --allow-unrelated-histories, 
		然后手动 git merge origin/master）， 然后git add README.md, git commit -m '注释',
		最后 git push -u origin master

- pwd（linux命令）
		

		pwd 显示当前目录