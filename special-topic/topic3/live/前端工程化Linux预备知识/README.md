# 前端工程化linux预备知识
## 常用的linux
* systemctl enable
* systemctl disable
## linux进程管理
* top命令详解
* ps命令详解：当前用户不是root身份，要加sudo
* sed
* kill（+进程id）、pkill（+进程名）命令及使用注意事项 -9是强制退出
* w命令
## linux网络管理
* 查看和配置的网络基本信息
* 重启网卡
* 查看路由配置router
* 排查网络故障 tracerout
* 怎么找到占用网络端口的进程
## 进程、线程与协程
* 进程的目的就是担当分配系统资源（cpu时间、内存）的实体，进程是动态的，操作系统是对硬件资源的调度，操作系统说了算，像一个部门
* 线程是操作系统能够进行运算调度的最小单位（内存管理、任务调度）：会共享进程的内存空间和部分代码空间，瘦身了。linux（pthread线程库，linux信号系统）和window的线程的管理机制不同（windows流氓软件：dll注入到servise上，永远杀不死），操作系统说了算，部门必须有一个以上的人，公司可以管理多个部门
* 协程是一种用户态（和它相对的是内核态）的轻量级线程，无法利用多核资源，消耗的资源更少，核心数越多，它的速度越快，节省了操作系统调度的时间（线程或进程平均分配核心），可以自己控制，不经过操作系统，你想怎么做公司都不管你
* io密集型（数据转发；nginx，最大io消耗：网络、外存，10k、100k并发）应用的发展：多进程 -> 多线程 -> 事件驱动 -> 协程
* cpu密集型（人多力量大；桌面应用、运算量比较大，长时间占用cpu进行运算，浮点数运算分给了GPU）应用的发展：多进程 -> 多线程
* 调度和切换的时间：进程 > 线程 > 协程
## 进程与线程
* 操作系统的设计，可以归结为三点：
	- 1. 以多进程形式，允许多个任务同时运行
	- 2. 以多线程形式，允许单个任务分成不同的部分运行
	- 3. 提供协调机制，一方面防止进程之间和线程之间产生冲突，另一方面允许进程之间和线程之间共享资源（锁机制：同步任务），操作系统协调
## 进程与线程的资源共享
* 文件句柄（不是指针，是在操作系统层面抽象出来的），关闭文件后，会回收文件句柄
* 寄存器
* 栈：函数调用栈
* 单线程进程：fork一个线程时，会原封不动复制线程的所有文件，会对内存照成重复使用
## linux免密远程登录
* 免密登录的原理 （ssh 用户名 ip地址会人工干预输入密码）：写完的脚本，会定时执行，
* 配置免密登录的步骤
	- 1. 生成密钥对：不对称加密（加密用公钥-开着的锁，解密用私钥）

	`ssh-keygen -t rsa -C “你自己的名字” -f “你自己的名字_rsa”`
	-t：加密方式
	rsa：不对称加密，长度达到4k已经到军用级别
	-C：要写到密钥中的名字，必须要加双引号
	-f：生成密钥文件的文件名，会产生默认的密钥名，但是可能会混淆
	直接敲回车到最后，但是中间会提示：
	要不要对密钥加密码：不要（当你在使用密钥的时候，还要手动输入密码，不能自动化测试）
	_rsa:是私钥
	_rsa.pub:是公钥
	- 2. 上传配置公钥

	`上传公钥到服务器对应账号的home路径下的.ssh/中（是隐藏文件），（ssh-copy-id -i "公钥文件名" 用户名@服务器ip或域名）`
	`配置公钥文件访问权限为 600`
	- 3. 配置本地私钥

	`把第一步生成的私钥复制到你的home目录下的.ssh/路径下`
	`配置你的私钥文件访问权限为600`
	`chmod 600 你的私钥文件名`
	- 4. 免密登录功能的本地配置文件

	`编辑自己home目录的.ssh/路径下的config文件`
	`配置config文件的访问权限为644`
	如果没有config文件，你可以自己创建一份
	host：服务器的别名
	user：加了之后，不用再写user名
	port：改了默认端口号，必须写
	hostname：ip或者绑定的域名
	identityFile：私钥路径
	protocal：协议版本号
	serverAliveInterval：远程连接到服务器，一段时间不工作的时候，会踢你下线，防止被踢掉
	serverAliveCountMax：并发登录的
	logLevel：日志记录的等级
	lastb -n 10:最近10次的爆破
