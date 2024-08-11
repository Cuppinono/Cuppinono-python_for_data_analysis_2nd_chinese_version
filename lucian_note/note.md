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

20240811
数据分析针对的数据主要是结构化数据 - structured data，比如：
	a. 表格型数据
	b. 多为数组（矩阵）
	c. 通过关键列相互联系的多个表 - SQL
	d. 时间序列数据
Python有一个叫做全局解释器锁（Global Interpreter Lock，GIL）的组件，这是一种防止解释器同时执行多条Python字节码指令的机制。
	a. 全局解释器锁（Global Interpreter Lock，简称 GIL）是 Python 解释器中的一种机制，主要用于管理多线程环境下	 的内存和数据安全。
	b. GIL 是一种互斥锁，用于确保在任意时刻只有一个线程能够执行 Python 字节码。这意味着即使在多核CPU上Python解释器也只能同时执行一个线程的 Python 代码。
	c. GIL工作原理
		1、互斥锁机制：当一个线程持有GIL时，其他线程必须等待，直到该线程释放GIL。
		2、时间片：持有GIL的线程会在执行一段时间后释放GIL，允许其他线程获取GIL。
		3、释放和竞争：当一个线程释放GIL后，其它等待的线程会竞争获取GIL。
	d. GIL的影响
		1、CPU 密集型任务：由于 GIL 的存在，多线程无法充分利用多核 CPU，导致 CPU 密集型任务的性能受限。
		2、IO 密集型任务：在 IO 密集型任务中，线程在等待 IO 操作时会释放 GIL，允许其他线程执行 Python 字节码，因此多线程在这种情况下能发挥一定作用。
	e. 如何应对 GIL 的限制
		1、使用多进程：通过 multiprocessing 模块创建多个进程，每个进程有自己的 GIL，从而绕过 GIL 的限制
		2、使用 C 扩展：将关键部分的代码编写为 C 扩展，这些部分在执行时不受 GIL 的影响
		3、异步编程：使用异步编程模型（如 asyncio 库）可以减少对线程的依赖，避免 GIL 对程序性能的影响
	f. 并不是说Python不能执行真正的多线程并行代码。例如，Python的C插件使用原生的C或C++的多线程，可以并行运行而不被GIL影响，只要它们不频繁地与Python对象交互。

数据规整（Munge/Munging/Wrangling） 指的是将非结构化和（或）散乱数据处理为结构化或整洁形式的整个过程。

Python 中的简单赋值永远不会复制数据。将列表分配给变量时，该变量引用现有列表。您通过一个变量对列表所做的任何更改都将通过引用该变量的所有其他变量看到。
	a. id() 函数返回对象的唯一标识符，这通常是对象在内存中的地址。如果两个变量指向同一个对象，它们的 id() 值将相同，表示它们是对同一块内存的引用。
	b. 所有切片操作都会返回一个包含所请求元素的新列表。  
		rgb = ["Red", "Green", "Blue"]   --- id(rgb) = 数字1(139955995081024)
		rgba = rgb                       --- id(rgba) = 数字1(139955995081024)
		correct_rgba = rgb[:]            --- id(correct_rgba) = 数字2(139955995081216)
		
