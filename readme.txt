初始化配置：
git config -- global user.name "806186625"
git config --global user.email "806186625@qq.com"
git 
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



git what you dont want
















