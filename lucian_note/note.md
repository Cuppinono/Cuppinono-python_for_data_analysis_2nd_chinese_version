20240810
vim显示行号：set nu / number;
使用touch命令可以创建文本文件，比如txt，或者md;
git clone <remote-url> -b <分支名称> 命令可以将指定的某一个远程分支拉取到我们本地，而且拉取的本地分支自动和远程同名分支建立追踪关系;
	当从远程仓库拉取代码的时候一般都是使用git clone <url>命令来获取，这样我们是将项目整个都克隆到我们本地仓库，并且还是主分支。
git fetch <url> 也可以实现拉去远程仓库的某个特定分支，区别是,本地除了拉去主分支还有特定分支。
	<默认情况下，git fetch下载的分支和远程的分支名相同。>
	a. 拉取整个远程代码库 $ git clone https://github.com/521/springboot-rabbitmq.git
	b. 进入项目目录，也就是进入master主分支 $ cd springboot-rabbitmq/
	c. 执行git fetch命令，将远程仓库的所有分支拷贝到本地仓库 $ git fetch
	d. 执行git checkout <分支名称>命令，切换到我们想要拉取的指定某一个分支的本地分支 $ git checkout dev开发分支
git checkout -b 命令获取远程仓库特定分支 -- 执行git checkout -b <本地分支名称> origin/<远程分支名称>
	a. 拉取整个仓库 $ git clone https://github.com/521/springboot-rabbitmq.git
	b. 进入项目目录，也就是进入master主分支 $ cd springboot-rabbitmq/
	c. 执行git branch -a查看所有分支名称，* 号表示当前分支
	d. 执行git checkout -b <本地分支名称> origin/<远程分支名称>，拉取指定的某一个分支 $ git checkout -b dev开发分支 origin/dev开发分支
	e. 拉取该分支的最新代码 $ git pull origin dev开发分支
在本地分支 <main_local> 做了改动，push到仓库的新建分支<dev1>上，用来区分远程仓库主分支的版本
	a. git pull origin main_local:dev1
本地版本回退,会使工作目录，暂存区和本地仓库都回退到指定版本
	a. git log 查询需要回退版本的commit id
	b. git reset --hard <commit_id>
	c. 回退后想强制push到远程分支<HEAD> $ git push origin HEAD -f
 
