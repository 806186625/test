初始化配置：
git config -- global user.name "806186625"
git config --global user.email "806186625@qq.com"

初始化仓库：
git init 
添加：
git add readme.txt
git add ……
提交：
git commit -m "message"

查看状态：
git status 
查看不同：
git diff readme.txt

查看历史记录：
git log
美化：
git log --pretty=online
只能看到 message 的信息

倒退：
git reset --hard HEAD^
几个^倒退几次 可以HEAD~100

读取：
cat readme.txt

返回上一层版本（命令行窗口不能关）：
git reset --hard 版本号前几位(1094a)

记录每次命令：
git reflog

查看工作区和版本库最新版本区别：
git diff HEAD --readme.txt

1
当你改乱了（删除也是）工作区某个文件的内容，想直接丢弃工作区的修改时，用命令
git checkout -- file

2
当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令
git reset HEAD <file>(readme.txt)
就回到了场景1，第二步按场景1操作。

删除文件：
git rm readme.txt

“1.如果你用的rm删除文件，那就相当于只删除了工作区的文件，如果想要恢复，直接用git checkout -- <file>就可以 2.如果你用的是git rm删除文件，那就相当于不仅删除了文件，而且还添加到了暂存区，需要先git reset HEAD <file>，然后再git checkout -- <file> 3.如果你想彻底把版本库的删除掉，先git rm，再git commit 就ok了”


要关联一个远程库，使用命令git remote add origin git@server-name:path/repo-name.git；
关联后，使用命令git push -u origin master第一次推送master分支的所有内容；
此后，每次本地提交后，只要有必要，就可以使用命令git push origin master推送最新修改；
分布式版本系统的最大好处之一是在本地工作完全不需要考虑远程库的存在，也就是有没有联网都可以正常工作，而SVN在没有联网的时候是拒绝干活的！当有网络的时候，再把本地提交推送一下就完成了同步，真是太方便了！

克隆到本地：
git clone git@github.com:用户名/仓库名字.git

Git鼓励大量使用分支：
查看分支：git branch
创建分支：git branch <name>
切换分支：git checkout <name>或者git switch <name>
创建+切换分支：git checkout -b <name>或者git switch -c <name>
合并某分支到当前分支：git merge <name>
删除分支：git branch -d <name>


当Git无法自动合并分支时，就必须首先解决冲突。解决冲突后，再提交，合并完成。
解决冲突就是把Git合并失败的文件手动编辑为我们希望的内容，再提交。
用git log --graph命令可以看到分支合并图。
即是多个分支各自提交commit 此时无法自动merge，需手动修改


合并分支时，加上--no-ff参数就可以用普通模式合并，合并后的历史有分支，能看出来曾经做过合并，而fast forward合并就看不出来曾经做过合并。



分支策略
在实际开发中，我们应该按照几个基本原则进行分支管理：
首先，master分支应该是非常稳定的，也就是仅用来发布新版本，平时不能在上面干活；
那在哪干活呢？干活都在dev分支上，也就是说，dev分支是不稳定的，到某个时候，比如1.0版本发布时，再把dev分支合并到master上，在master分支发布1.0版本；
你和你的小伙伴们每个人都在dev分支上干活，每个人都有自己的分支，时不时地往dev分支上合并就可以了。
【我感觉同一个任务不太可能多个人一起做，只是大家各自完成各自的，各自提交相互修改】


修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；
当手头工作没有完成时，先把工作现场git stash一下，然后去修复bug，修复后，再git stash pop，回到工作现场；
在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。


查看远程库信息，使用git remote -v；
本地新建的分支如果不推送到远程，对其他人就是不可见的；
从本地推送分支，使用git push origin branch-name，如果推送失败，先用git pull抓取远程的新提交；
在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name，本地和远程分支的名称最好一致；
建立本地分支和远程分支的关联，使用git branch --set-upstream-to=origin/分支名  本地分支名
从远程抓取分支，使用git pull，如果有冲突，要先处理冲突。


rebase操作可以把本地未push的分叉提交历史整理成直线；
rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。


敲命令git tag <name>就可以打一个新标签：
$ git tag v1.0

比方说要对add merge这次提交打标签，它对应的commit id是f52c633，敲入命令：
$ git tag v0.9 f52c633

还可以创建带有说明的标签，用-a指定标签名，-m指定说明文字：
$ git tag -a v0.1 -m "version 0.1 released" 1094adb

命令git push origin <tagname>可以推送一个本地标签；
命令git push origin --tags可以推送全部未推送过的本地标签；
命令git tag -d <tagname>可以删除一个本地标签；
命令git push origin :refs/tags/<tagname>可以删除一个远程标签。


忽略某些文件时，需要编写.gitignore；
.gitignore文件本身要放到版本库里，并且可以对.gitignore做版本管理！





















































