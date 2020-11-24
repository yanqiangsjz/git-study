## 1、 git（在git bash中操作) 

- 明确一些git中的概念

		-)  此文档是基于git1.0版本
		
		-) git版本管理工具中四个区域概念：

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

- git add (v1.0)

		git add [filename]  添加指定文件到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)

		git add [dir]  添加指定目录到暂存区，包括子目录 

		git add -A    是git add . 和 git add -u 的并集   

		git add .  添加当前目录的所有文件到暂存区(表示添加新文件和编辑过的文件不包括删除的文件)

		git add -u  表示添加编辑或者删除的文件，不包括新添加的文件

- git add (v2.0)

		"git add <path>" is the same as "git add -A <path>" now, so that
		"git add dir/" will notice paths you removed from the directory and
		record the removal.  In older versions of Git, "git add <path>" used
		to ignore removals.  You can say "git add --ignore-removal <path>" to
		add only added or modified paths in <path>, if you really want to.

- git rm filename  
	
		git rm [filename] 删除工作区文件并放进暂存区
		如果想从暂存区撤销：git reset HEAD -- [filename]
		如果想撤销工作区的修改：git checkout -- [filename]

		注意区别 : rm [filename]  删除工作区文件, 并没有放进暂存区
		如果想撤销工作区的修改：git checkout -- [filename]

		git rm --cached [filename]	停止追踪文件，但该文件会保留在工作区(untracked状态)
 

- git 



		git diff --stat 仅仅比较统计信息即文件列表

		git diff [filename] 比较的是工作区文件与暂存区文件的差异

		git diff --cached(--staged) [filename] 比较的是暂存区的文件与上一个commit的差异
		
		git diff HEAD -- [filename] 比较的是工作区与当前分支最新commit之间的差异

		git diff [commitId1] [commitId2] 比较两次提交之间的差异

		git diff <branch1> <branch2> 在两个分支之间比较


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
		
		git log --stat 查看commit历史，以及每次commit发生变更的文件列表

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

		git show [commit] --stat 显示某次提交时，提交的文件列表

		git show 显示最后一次的文件改变的具体内容
		
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

		git checkout -b [branch] [remote]/[branch]  切换到branch分支上,接着跟远程的origin地址上的branch分支关联起来

		说明：多人协作时，如果同事从远程库clone时，默认情况下，你的同事只能看到本地的master分支。如果，你的同事要在（[branch]）分支上开发，
		就必须创建远程([remote])的([branch])到本地

- git restore(--staged 简写 -s  --worktree(默认) 简写 -w )

		git restore [filename...] 工作区filename的修改撤销 (同"git checkout(1)"作用一样)
		
		git restore --staged [filename...] 将文件从暂存区撤出，但不会撤销文件的更改 (同"git reset [filename]"作用一样)
		
		
- git reset (回退)

		git reset [filename] 重置暂存区的指定文件，与上一次commit保持一致，重新放回工作区

		git reset HEAD -- [filename] 把暂存区的修改撤销（unstage），重新放回工作区  与上面一样

		git reset --hard  重置暂存区与工作区，与上一次commit保持一致

		git reset --hard HEAD~2  回退到某个版本(这里是从当前版本回退两个版本)

		git reset --hard [commitID] 回退到某个版本（commitID是版本号）

- git reset 模式详解
	
		1、reset --hard：重置stage区和工作目录:reset --hard 会在重置 HEAD 和branch的同时，重置stage区和工作目录里的内容。当你在 reset 后面加了 
		--hard 参数时，你的stage区和工作目录里的内容会被完全重置为和HEAD的新位置相同的内容。换句话说，就是你的没有commit的修改会被全部擦掉。
		**简单的看，--hard就是完全替换为reset的版本信息，你工作区和暂存区也全部同步为reset版本相同的内容**

		2、reset --soft：保留工作目录，并把重置 HEAD 所带来的新的差异放进暂存区。reset --soft 会在重置 HEAD 和 branch 时，
		保留工作目录和暂存区中的内容，并把重置 HEAD 所带来的新的差异放进暂存区。
		**简单来看，也就是说--soft命令是撤销指定版本内容的那一次commit（并放进stage/暂存区），其他的东西都不改变。**

		3、reset 不加参数(--mixed)：保留工作目录，并清空暂存区。reset 如果不加参数，那么默认使用 --mixed 参数。
		它的行为是：保留工作目录，并且清空暂存区。也就是说，工作目录的修改、暂存区的内容以及由 reset 所导致的新的文件差异，都会被放进工作目录。
		简而言之，就是「把所有差异都混合（mixed）放在工作目录中」。工作目录的内容和 --soft 一样会被保留，但和 --soft 的区别在于，它会把暂存区清空,
		并把原节点和reset节点的差异的文件放在工作目录，总而言之就是，工作目录的修改、暂存区的内容以及由 reset 所导致的新的文件差异，
		都会被放进工作目录
		**简单的看，也就是说--mixed命令是撤销指定版本内容的那一次commit（并放进work/工作区），暂存区的修改也会清空，同时放到工作区。**


- get revert (反做)

		说明1：git revert是用于“反做”某一个版本，以达到撤销该版本的修改的目的。比如，我们
		commit了三个版本（版本一、版本二、 版本三），突然发现版本二不行（如：有bug），想
		要撤销版本二，但又不想影响撤销版本三的提交，就可以用 git revert 命令来反做版本
		二，生成新的版本四，这个版本四里会保留版本三的东西，但撤销了版本二的东西.

		说明2： `git revert commitId`之后并不会回滚到该id的内容，而是将该id的内容给逆
		向操作一遍，比如说，a操作添加了“haha”，commit了a，b操作添加了“xixi”，commit b。
		现在想回滚到只添加了“haha”，需要的是删除“xixi”，也就是逆向操作b，所以应该`git
		 revert b的commitId`。 `git revert` 应该翻译成“反转、逆转”比较好理解，而不是回
		退。
		
		git revert -n [commitId] 注意：反做可能会发生冲突，解决冲突后add-commit,会生成一个新的版本。(-n是--no-commit如果不带这个参数会自动提交一条commit)
		
		git revert -n commit1..commit2 反做多个commit(左开右闭，即不包括 commit1，但包括 commit2 )

		git revert --abort 取消本次反做

- git revert (merge commit)

		merge commit 和普通 commit 的不同之处在于 merge commit 包含两个 parent commit，代表该 merge commit 是从哪两个 commit 合并过来的。 查看log 如下：

		commit b40e266a3e446e92d8cb00227b703c4f18894bf3
		Merge: c1a1c33 87b6cb0

		这代表该 merge commit 是从 c1a1c33 和 87b6cb0 两个 commit 合并过来的

		revert merge commit 有一些不同，这时需要添加 -m 选项以代表这次 revert 的是一个 merge commit。
		**需要指定一个 parent number 标识出"主线"，主线的内容将会保留，而另一条分支的内容将被 revert。**如下

		git revert -m 1 b40e266a3e446e92d8cb00227b703c4f18894bf3  保留主分支
		git revert -m 2 b40e266a3e446e92d8cb00227b703c4f18894bf3  保留被merge的分支

		**坑： 注意下方图片revert 反坐重新上线问题**


	![](https://s1.ax1x.com/2020/09/10/wJDN7R.png)


		

- git branch 分支名称

		git branch [branch] 创建分支  

		git branch 列出所有本地分支

		git branch -r 列出所有远程分支

		git branch -a 列出所有本地分支和远程分支

		git branch -vv 查看本地分支对应的远程分支(注意：是-vv)

		git branch -d [branch] 删除分支

		git branch -D [branch]  强制删除一个还没有合并（已经commit）的分支

		git branch -m [oldName] [newName] 重命名分支

		git branch -a --contains commitID 根据commitId 查询关联分支

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

- git rebase 

		git pull --rebase (对应场景：本地与远端同一分支提交历史不一致)

		多个人在同一个分支上协作时，出现冲突是很正常的，比如现在有一个项目由我和A一同开发。我在修复了一个bug以后准备提交，发现git push失败，
		发现是远端版本更新，说明A在我之前已经提交了，我本地master分支的提交历史已经落后远端了，需要先pull一下，与远端同步后才能push。pull成功，
		现在使用git log看下一提交历史，发现分叉了！由于我本地master的提交历史和远端的master分支的提交历史不一致，所以git为我进行了自动合并，
		然后生成了一个新的提交历史。不想看到分叉。这个时候用git rebase就可以解决（简单方案：直接git pull --rebase）
		
		git rebase [branch] (branch 可以理解为基分支。 对应场景：不同分支之间的合并)
		
		这句命令的意识是：以master为基础，将feature分支上的修改增加到master分支上，并生成新的版本。 如果发生冲突，解决完成后 直接git add . 然后
		继续执行 git rebase --continue. rebase 完成后切回到主分支，执行 git merge [branch] (当然是先git pull --rebase 再执行merge) 
		就会出现一条完美的直线
		思考：

		git rebase -i [commitId|branch] (多个commit，合并为一个完整的commit提交。 再执行git rebase branch )
		
		好处：1、易于管理，2、git rebase branch 不用为每个commit都解决一次冲突(如果有冲突的话)
		
		解释：如果执行 git rebase -i [commitId], 最终不包括选中的commitId。 是合并commitId之后的所有commit

		解释：如果执行 git rebase -i branch, 其实就是将所在分支的所有commit全部合并。 branch 就是基分支的最后一次commitID。 
		其实和 git rebase -i [commitId] 是一个意思。 一般这样写，就不用去找commitId了。

		解释： 在一个基本的迭代周期里，你会有很多次commit，有跟配置文件相关的，有跟代码相关的，甚至有跟下次发布fixbug相关的。这些都是
		你在完成本地开发的时候一个变化记录而已。但是当你需要将你的迭代项目作为一次发布提交时就需要整合所有之前提交的那些很零碎的commit。
		很多commit这样提交上去之后就很难管理和跟踪，所以我们需要将这些commit 合并为一个总的commit

		再合并的过程中，只需要保留一个commit就可以了，剩下的commitId 将前面的pick 改为 squash 保存退出vim;
		在继续弹出的vim编辑器中删掉旧的提交信息，在对应位置填写总的log 保存退出即成功。

		
		一般操作流程： 
			1、 git pull --rebase, 
			2、 新建切换分支branch-one、 
			3、 branch-one 开发 提交、 测试通过、  
			4、 git rebase -i master(假设master是基分支) 将 branch-one的所有commit 整合为一个commit、 
			5、 git checkout master、 git pull --rebase 将master 分支更新、 
			6、 git checkout branch-one、 git rebase master(有冲突解决冲突 git add .   git rebase --continue )、 
			7、 git checkout master、 git merge branch-one。

- git merge 与 git rebase

		
		git merge 操作合并分支会让两个分支的每一次提交都按照提交时间（并不是push时间）排序，并且会将两个分支的最新一次commit点
		进行合并成一个新的commit，最终的分支树呈现非整条线性直线的形式

		git rebase 操作实际上是将当前执行rebase分支的所有基于原分支提交点之后的commit打散成一个一个的patch，并重新生成一个
		新的commit hash值，再次基于原分支目前最新的commit点上进行提交，并不根据两个分支上实际的每次提交的时间点排序，rebase完成后，
		切到基分支进行合并另一个分支时也不会生成一个新的commit点，可以保持整个分支树的完美线性

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
		该文件做了修改：同一个文件不同的内容，这样就会明显的出现冲突）。这时我们就需要解决这些冲突（其实就是将之前修改的删掉，保留和现在
		master主分支中的文件一样的信息）。解决完成以后。我们就完全解决了以后dev合并到master中可能存在的冲突，并且在合并以后不会再出现同样
		的错误		


- git fsck

		git fsck --lost-found   找到最近的一些删除的提交
		
		git show [commitId] 查看删除文件内容

		git merge [commitId] 本地合并误删的文件内容

		说明: stash 之后的内容没有应用到代码上就手欠直接给删除了,上述方法可以恢复数据

- git remote (git给远程库起的默认名称是origin)

		git remote -v 查看远程库的信息

		git remote show [remote] 显示某个远程仓库的信息

		git remote add [remote] [url] 增加一个新的远程仓库，并命名 (一般是origin)

		git remote rm [remote]  删除远程库
		

- git 
		
		git push [remote] master  将主分支推送到远程库
		
		git push [remote] [branch] 将([branch])分支推送到远程库

		git push [remote] --delete [branch] 删除远程分支

		git push [remote] [tagname] 推送某个标签到远程

		git push [remote] --tags 一次性推送全部尚未推送到远程的本地标签

		git push -f 强推(一般用于reset后 本地库HEAD指向的版本比远程库的要旧)

     	
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

		git pull --rebase [remote] [branch] rebase模式 多人合作不了解的慎用


-  git branch --set-upstream-to=origin/dev dev

			git branch --set-upstream-to=origin/dev dev 设置dev和origin/dev的链接。成功以后就可以git pull

- git tag 

		git tag [tagname] 为当前HEAD打标签（本地tag）
		
		git tag [tagname] [commitId]（commitId 默认未HEAD; 本地tag）

		git tag -a [tagname] -m [message] [commitId] 为本地tag添加说明

		git tag 查看所有标签信息

		git show [tagname] 查看某个tag信息

		git tag -d [tagname] 删除本地标签


- 删除远程标签

		git tag -d [tagname] -> git push [remote] :refs/tags/[tagname]

		说明：git tag -d [tagname]（先从本地删除）;  git push [remote] :refs/tags/[tagname]（然后，从远程删除）


- git checkout -b [branch] [tag]

		git checkout -b[branch] [tagname] 新建一个分支，指向某个tag


- git fetch (取回远程仓库的变化，但并不会主动与本地分支合并。这个比git pull 更安全)

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
		
		2. git push -u [remote] [branch]（相当于git push [remote] [branch] + git branch --set-upstream-to=origin/[brnach] [origin]）
		
		3. 以后修改提交到远程库直接git push [remote] [branch]就可以了  (不带任何参数的git push，默认只推送当前分支)

		4. -u 也就是--set-upstream, 代表的是更新默认推送的地方，这里就是默认以后git pull和git push时，都是推送和拉自origin。

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


## 4、 gitFlow（代码管理流程和规范）[点击--->gitflow](https://github.com/nvie/gitflow "gitflow")


	Git Flow常用的分支

	Production 分支 (所有在Master分支上的Commit应该Tag)
	也就是我们经常使用的Master分支，这个分支是最近发布到生产环境的代码，最近发布的Release， 这个分支只能从其他分支合并，不能在这个分支直接修改
	
	Develop 分支
	这个分支是我们是我们的主开发分支，包含所有要发布到下一个Release的代码，这个主要合并与其他分支，比如Feature分支
	
	Feature 分支
	这个分支主要是用来开发一个新的功能，一旦开发完成，我们合并回Develop分支进入下一个Release
	
	Release分支
	当你需要一个发布一个新Release的时候，我们基于Develop分支创建一个Release分支，完成Release后，我们合并到Master和Develop分支
	
	Hotfix分支
	当我们在Production发现新的Bug时候，我们需要创建一个Hotfix, 完成Hotfix后，我们合并回Master和Develop分支，所以Hotfix的改动会进入下一个Release




windows 下载：

1、下载getopt.exe
getopt.exe的下载链接：[http://downloads.sourceforge.net/gnuwin32/util-linux-ng-2.14.1-bin.zip](http://downloads.sourceforge.net/gnuwin32/util-linux-ng-2.14.1-bin.zip)
解压，进入bin目录，复制其中的getopt.exe文件到你的git安装目录，例如，D:\Program Files (x86)\Git\bin

2、下载libintl3.dll
libintl3.dll下载链接：[http://gnuwin32.sourceforge.net/downlinks/libintl-bin-zip.php](http://gnuwin32.sourceforge.net/downlinks/libintl-bin-zip.php)
解压，进入bin目录，复制libintl3.dll文件到你的git安装目录。

3、下载libiconv2.dll
libiconv2.dll下载链接：[http://gnuwin32.sourceforge.net/downlinks/libiconv-bin-zip.php](http://gnuwin32.sourceforge.net/downlinks/libiconv-bin-zip.php)
解压，进入bin目录，复制libiconv2.dll文件到你的git安装目录。

4、获取git flow的代码，打开git bash，输入以下命令：

`git clone -–recursive git://github.com/nvie/gitflow.git`

5、运行git flow的安装脚本

打开windows的cmd（可能需要管理员权限），进入上面的git flow代码目录，键入以下命令：

cd gitflow

cd contrib

msysgit-install.cmd [git的安装目录]

例如，

msysgit-install.cmd “D:\Program Files (x86)\Git”

耐心等待执行完毕。

6、 验证安装

打开git bash，输入 `git flow`



	
