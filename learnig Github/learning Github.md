
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

		$ git reset --hard HEAD^
		HEAD is now at ea34578 add distributed
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