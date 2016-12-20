
1. 创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录
2. `git init`把这个目录变成git可以管理的仓库
3. `git add`添加文件
4. `git commit`备注文件 
	- `-a`跳过`git add`这一步
	- `-m`直接在一行备注，不打开编辑器
5. `git status`让我们时刻掌握仓库当前的状态
6. `git diff`如果能看看具体修改了什么内容
	`git diff readme.txt`
7. `git log`命令显示从最近到最远的提交日志
	- 如果嫌输出信息太多，看得眼花缭乱的，可以试试加上`—pretty=oneline`参数

			$ git log --pretty=oneline
			3628164fb26d48395383f8f31179f24e0882e1e0 append GPL

8. 将版本返回去之前的版本用`git reset`
	- 用`HEAD`表示当前版本，`HEAD^`表示上一个版本，`HEAD^^`表示上上个版本，往上一百个版本就是`HEAD~100`  
		`$ git reset --hard HEAD^  `  
		`HEAD is now at ea34578 add distributed`	
		- 如果后悔了，想要已经被删除的那个版本，也可以使用这个办法，将HEAD改成那个的版本号前面几位

9. `git reflog`就可以查询以前的版本号了，查看命令历史，以便确定要回到未来的哪个版本
10. 每次修改，如果不`add`到暂存区，那就不会加入到`commit`中。
11. 命令`git checkout -- readme.txt`意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
	- 一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
	- 一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
		总之，就是让这个文件回到最近一次git commit或git add时的状态。
12. 如果已经`git add`了，但还没有`git commit`，用命令`git reset HEAD file`可以把暂存区的修改撤销掉（unstage），重新放回工作区, 然后再用`git checkout`修改

	- 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令`git checkout -- file`。
	- 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令`git reset HEAD file`，就回到了场景1，第二步按场景1操作。
	- 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，用`git reset --hard HEAD^ `那个办法，不过前提是没有推送到远程库。

13. 删除文件：
	例子：
	1. 添加一个新文件test.txt,并且已经commit
	2. 本地删除这个文件 `rm test.txt`
	3. `git status`立刻告诉你哪些文件被删除了
	4. 现在有两个选择：
		1. 确实要从版本库中删除该文件，用`git rm`删除再`commit`.
		2. 删错了，但版本库还有了，所以从版本库恢复。用`git checkout -- test.txt`
		`git checkout`其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
	5. 如果最后发现从版本库也删除错了，可以先用`git reflog`查询版本号，然后用`git reset --hard 版本号`恢复，这时工作区和版本库都恢复了

14. 设置远程仓库：
	1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id\_rsa`和`id\_rsa.pub`这两个文件 ，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：`ssh-keygen -t rsa -C "youremail@example.com"`

		你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可.  
		如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有`id\_rsa`和`id\_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id\_rsa`是私钥，不能泄露出去，`id\_rsa.pub`是公钥，可以放心地告诉任何人。  
		 
	2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面, 然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id\_rsa.pub`文件的内容

15. 添加远程库：已经在本地创建了一个Git仓库后，又想在GitHub创建一个Git仓库，并且让这两个仓库进行远程同步

	- 登陆GitHub，然后，在右上角找到“Create a new repo”按钮，创建一个新的仓库：

		- 可以从这个仓库克隆出新的仓库

			`echo "# testrepository" \>\> README.md  `  
			`git init  `  
			`git add README.md  `  
			`git commit -m "first commit" `   
			`git remote add origin https://github.com/yangyzhang/tesrepositoryt.git `   
			`git push -u origin master`


		- 也可以把一个已有的本地仓库与之关联，然后，把本地仓库的内容推送到GitHub仓库。在本地的test文件夹里
	
			`git remote add origin https://github.com/yangyzhang/test.git
	git push -u origin master`

	**注意！第一次用`git push -u origin master `,之后都用`git push origin master `**

16. 克隆远程库 `git clone git@github.com:michaelliao/gitskills.git`
17. 创建与合并分支

	- `git branch newbranch`创建分支
	- `git checkout newbranch`切换分支 
	- 或者可以一次性创建和转换`git checkout -b newbranch`
	- `git branch`查看当前分支
	- `git merge <name>`合并某分支到当前分支
	- `git branch -d <name>`删除分支

18. 解决冲突 
	1. 当我们`git merge`在不同branch的文件有两个版本时，发生冲突
	2. `git status`帮助我们查看出现问题的文件。
	3.  打开这个文件，Git用\<\<\<\<\<\<\<，=======，\>\>\>\>\>\>\>标记出不同分支的内容。把文件进行和修改成我们要的版本。
	4. 照常add、commit文件
	5. 可以使用`git log --graph`查看分支的情况，
			`git log --graph --pretty=oneline --abbrev-commit`更简洁
	6. 删除分支\`git branch -d <name>
			`
19. 分支管理策略  
	    通常，合并分支时，如果可能，Git会用Fast forward模式，但这种模式下，删除分支后，会丢掉分支信息。  
	如果要强制禁用Fast forward模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。  

	merge的时候使用`--no-ff`  
	    `git merge --no-ff -m "merge with no-ff" dev`

	在实际开发中，我们应该按照几个基本原则进行分支管理：

		1. 首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
		2. 那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
		3. 你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。

20. Bug分支 
	当你接到一个修复一个代号101的bug的任务时，很自然地，你想创建一个分支issue-101来修复它，但是，等等，当前正在dev上进行的工作还没有提交.并不是不想提交，而是工作只进行到一半，还没法提交.
	**Git还提供了一个stash功能，可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作**
	1. `git stash`
	2. 修复Bug
	3. 回到dev分支继续工作
	4. `git stash list`查看保存的工作现场
	5. 工作现场还在，Git把stash内容存在某个地方了，但是需要恢复一下，有两个办法：

		- 一是用`git stash apply`恢复，但是恢复后，stash内容并不删除，你需要用`git stash drop`来删除；
		- 另一种方式是用`git stash pop`，恢复的同时把stash内容也删了：

	6. 可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令:`git stash apply stash@{0}`
		 
21. Feature分支

	- 开发一个新feature，最好新建一个分支；
	- 如果要丢弃一个没有被合并过的分支，可以通过`git branch -D <name>`强行删除。

22. 多人协助

	- 当你从远程仓库克隆时，实际上Git自动把本地的master分支和远程的master分支对应起来了，并且，远程仓库的默认名称是origin。要查看远程库的信息，用`git remote`
	- 推送分支：就是把该分支上的所有本地提交推送到远程库。推送时，要指定本地分支，这样，Git就会把该分支推送到远程库对应的远程分支上：
	`git push origin master`
	推送其他分支比如dev:
	`git push origin dev` 
	 
	并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
		- master分支是主分支，因此要时刻与远程同步；
		- dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
		- bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
		- feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。

	- 抓取分支：如果小伙伴在另一台电脑或者另一个目录里克隆，默认情况下只能看到本地的master分支，如果要在dev分支上开发，就必须创建origin的dev分支到本地
		 
		`git checkout -b dev origin/dev`  
		现在，他就可以在dev上继续修改，然后，时不时地把dev分支push到远程
			 
```
$ git commit -m "add /usr/bin/env"
    [dev 291bea8] add /usr/bin/env
    1 file changed, 1 insertion(+)
    $ git push origin dev
        Counting objects: 5, done.
        Delta compression using up to 4 threads.
        Compressing objects: 100% (2/2), done.
        Writing objects: 100% (3/3), 349 bytes, done.
        Total 3 (delta 0), reused 0 (delta 0)
        To git@github.com:michaelliao/learngit.git
           fc38031..291bea8  dev -> dev···
```
    你的小伙伴已经向origin/dev分支推送了他的提交，而碰巧你也对同样的文件作了修改，并试图推送:  
	1.  推送失败，因为你的小伙伴的最新提交和你试图推送的提交有冲突，解决办法也很简单，Git已经提示我们，先用git pull把最新的提交从origin/dev抓下来，然后，在本地合并，解决冲突，再推送  
	2.  git pull也失败了，原因是没有指定本地dev分支与远程origin/dev分支的链接，根据提示，设置dev和origin/dev的链接：
	 `$ git branch --set-upstream dev origin/dev`  
	3. 再次`git pull`  
	4.  如果有冲突，手动解决冲突，再提交，再push

**多人协作的工作模式通常是这样:**

	s1. 首先，可以试图用git push origin branch-name推送自己的修改；
	2. 如果推送失败，则因为远程分支比你的本地更新，需要先用git pull试图合并；
	3.  如果合并有冲突，则解决冲突，并在本地提交；
	4. 没有冲突或者解决掉冲突后，再用git push origin branch-name推送就能成功！
	
	    如果git pull提示“no tracking information”，
	    则说明本地分支和远程分支的链接关系没有创建，
	    用命令git branch --set-upstream branch-name origin/branch-name


23. 标签管理

	1. 首先，切换到需要打标签的分支上
	2. 敲命令`git tag <name>`就可以打一个新标签
	3. 用命令`git tag`查看所有标签
	4. 默认标签是打在最新提交的commit上的。如果要给以前的打上标签,找到历史提交的commit id，然后打上就可以了。
		` git tag v0.9 6224937`
	5. 标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：

		`$ git show v0.9`  
		`commit 622493706ab447b6bb37e4e2a2f276a20fed2ab4`  
		`Author: Michael Liao [askxuefeng@gmail.com][1]`  
		`Date:   Thu Aug 22 11:22:08 2013 +0800`  
		`add merge`

	6. 还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
	`git tag -a v0.1 -m "version 0.1 released" 3628164`

	7. `git tag -s <tagname> -m "blablabla..." `可以用PGP签名标签；
	8. 如果标签打错了，也可以删除：`git tag -d v0.1`
	9. 因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。
	10. 如果要推送某个标签到远程，使用命令`git push origin <tagname>`
	11. 一次性推送全部尚未推送到远程的本地标签：`git push origin --tags`
	12. 命令`git push origin :refs/tags/<tagname>`可以删除一个远程标签。
