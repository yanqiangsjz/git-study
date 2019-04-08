### SVN常用操作
----------
1. ##### 安装 : 安装SVN客户端，windows一般选择乌龟客户端 &nbsp;&nbsp; [https://tortoisesvn.net/downloads.html](https://tortoisesvn.net/downloads.html "客户端下载")
 
2.  ##### 如果你不习惯英文，可以下载中文语言包&nbsp;&nbsp; [https://tortoisesvn.net/downloads.html](https://tortoisesvn.net/downloads.html "客户端下载")

3. ##### 检出版本库文件到本地:
		

		创建一个空文件夹。在空文件夹内右键 -> TortoiseSVN -> SVN Checkout(检出) -> 选择repository的正确路径 -> 点击OK(确定)
		即可。如果需要确定你的身份，可能会弹出一个对话框输入你的账号密码点击OK(确定)即可

4. ##### 项目导入：你已经在本地建立好了项目，需要把你项目推到SVN上

	
	
		-）方法1、右键 -> TortoiseSVN -> Repo-browser -> 填写正确路径 (进入到版本库) -> 在相应目录下，右键，加入文件/加入文件夹，选择相应目录即可

		-）方法2、右键要导入到版本库的本地文件夹 -> TortoiseSVN -> Import(导入) -> 选择repository的正确路径 -> 点击OK(确定)
		即可 **注意 : 此方法会将本地文件夹中的文件导入到版本库里面，但是文件夹本身是不会被导入的**

5. ##### 导入成功以后，你还得重新检出，重新检出的项目才是受SVN控制的。

6. #####  检出的文件经过修改，需要重新提交到版本库。右键单击检出的文件夹 -> SVN Commit -> 点击Ok(最好输入提交信息，方便后续管理及回滚) 提交之前先 SVN Update(更新)

7. ##### 将新增文件添加到版本库：
	
	
		如果在本地检出的文件中新添加了文件，如果没有任何操作，在你右键单击检出的文件夹 -> SVN Commit时，添加的文件并不会出现在提
	    交的列表中，这是因为添加的新文件并不属于版本库管理，不属于版本库管理的文件时不能提交到版本库的。所以在有新文件时必须将它添
		加到版本库中

		操作：右键检出的文件夹或者是新添加的文件 -> TortoiseSVN -> Add 就可以选择将新文件添加到版本库的管理中。最后 SVN Commit

8. ##### 如果是想删除某个文件，也应该通知版本库：右键要删除的文件 -> TortoiseSVN -> Delete

9. ##### 如何多人协作：


		-）1、假如你和B在协作。B写完代码提交到了SVN，你想获取最新修改，就需要选择更新：右键本地检出的文件夹 -> SVN Update
	
		-) 2、如果版本库上已经有别人提交过的新的commit，你是提交不上去的，必须先更新(SVN Update)再提交

		-) 3、如何确定版本库有没有更新：

			 &1.直接右击 `SVN Update` 更新；
			 &2.右键检出的文件夹 -> TortoiseSVN -> Check For Modifacations -> Check repository  检查版本库，
			   就可以看到版本库是否修改了文件及修改了哪些文件。右键单击修改的文件 -> Compare With HEAD AND BASE
		       可以比较本地和版本库中文件的差异 
	
		-）4、 如果B提交到版本库后，A 没有更新并且修改了同一个文件（B已经修改并commit）,则更新的时候会发生冲突，它会提示你哪个文件冲突，
		你只需打开那个文件，按照需求解决冲突即可。解决冲突以后 -> 右击本地已经解决的冲突文件 -> TortoiseSVN -> Resolve(解决) 即可 

10. ##### 修改但是未提交还原为初始未修改状态: 


		如果你改了代码，但是还没有提交，可以使用还原功能: 右键单击检出的文件夹 -> TortoiseSVN -> Revert...(还原)

11. ##### 修改并提交如何回滚到指定版本：（并不会生成新的版本）
		
		 右键单击检出的文件夹 -> TortoiseSVN -> Updatae to revision -> show log（选择版本）-> 点击Ok。 
		 注意:这个回滚并不会在svn库中并不会生成新的版本，这个时候再commit的话还是在之前最新版本的基础上进行commit、
		 下次SVN Update之后，还是会回到当前的版本。 如果你只是想临时恢复到以前的某个版本查看代码，那么就用update to revision

12. ##### 修改并提交如何回滚到指定版本：（会生成新的版本， 回滚完必须commit）
		 

		右键单击检出的文件夹 -> TortoiseSVN –> Show Log，右击你想要回滚到的版本。可以看到两个选项：“Revert to this revision”和“Revert changes from this revision”。
		首先看“Revert to this revision”，这个比较好理解，也比较常用。就是把文件恢复到某个版本，然后SVN Commit，文件就回滚成功了。
	 	回滚成功后，所有的历史还存在。例如回滚到版本n，commit之后，会出现新的版本m，但是他的内容和版本n是一样的。

13. ##### 创建分支

	
	  	右键单击检出的文件夹 -> TortoiseSVN –> Branch/tag,弹出框的to path输入新的分支名称,建议/branch/xxx,
		点击OK就创建出xxx分支.(建议创建前先svn update)； （勾选 Switch working copy to new branch/tag， 可以直接切换到新分支）

14. ##### 切换分支

		
		右键单击检出的文件夹 -> TortoiseSVN –> switch,弹出框的to path输入或选择分支名称，点击OK

15. ##### 合并分支


		-方法1 ： 右键单击检出的文件夹 -> TortoiseSVN –> merge-> merge a range of revisions-> URL to merge from 选择需要合并的代码分
		支,specific range输入框选择show log选择需要合并的版本号区间,然后一路next完成合并 -> 最后需要svn commit才能完成合并。
		如果有冲突解决冲突;如果合并以后还未提交的时候又想撤回合并前的状态，直接右键单击检出的文件夹 -> SVN -> Revert...(还原)放弃本次合并即可
		
		-方法2 ：右键单击检出的文件夹 -> TortoiseSVN –> merge -> merge two different trees(可以理解为合并两个树;) -> 在From中选择的目标
		文件夹，即需要“合并到”的svn目录（即master），To：选择包含所做修改的svn目录（即分支）点击Next，下一个页面使用默认项，
		点击Merge;-> 这时候的合并操作是在本地完成的，并没有提交到SVN；-> 最后需要需要svn commit才能完成合并。如果你在本次合
		并中发现问题，直接右键单击检出的文件夹 -> SVN -> Revert...(还原)放弃本次合并即可

		-方法2说明：选择该选项，会把两个目录的“不一样”合并到目标文件夹目录，这里“不一样”,是以非目标文件夹为基准的，比如branch
		的修改合并到master，将以branch为基准，按指定版本，把branch和master的不一样合并到master目录，这样的话可能会把master
		中增加的文件给删除，或者把master对某个文件做的修改覆盖掉，最终使得master和branch一模一样。

16. ##### 删除分支


		右键单击检出的文件夹 -> TortoiseSVN –> repo browser(进入版本库),弹出框的左边选择需要删除的分支右击 -> delete


17. ##### 检查版本库提交记录

	
		右键单击检出的文件夹 -> TortoiseSVN –> Show Log



18. ##### tag与branch 是一样的操作


19. ##### 配置SVN服务器的步骤

	
		