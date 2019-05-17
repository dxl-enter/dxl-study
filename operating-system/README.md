# 操作系统
### 操作系统：
* 哪些古老的系统
* 更适合工作和娱乐的windows(闭源，加linux子系统 - 兼容操作系统的程序)c#
	putty（不推荐）、xshell、在cmder终端环境下使用ssh命令
	shift+ins：粘贴
* 适合开发的linux（规范-工业标准posix，非常节省资源）
	- 行编辑器：vi/vim（键位图）
	- 服务管理命令：systemctl（比kill安全）
	- 网络管理命令（最新版ip addr）
	- 命令行下载route（检测网络端口）（新命令ip route）
	- an（机器名称解析-会很慢）
	- |：是管道命令
	- ss -anp | grep 80：80端口被谁占用的
	- kill -9:给发了强制退出信号（9是优先级最高的手段，导致工作只做一半）
	- 判断主进程：pid谁小
	- 命令行的下载：wget+下载的url（服务器时间）、curl+下载地址+-o+名字名称（本地时间、封装高）
	- 怎么查看linux命令的帮助（内置命令：70%）：--help、-h、man（非常有用，更详细的文档、linux的api setsid）
	- yum install wget
	- 在终端不小心ctrl+s了怎么办？终端不动了，锁住终端的。ctrl+q解除锁
* 非常好用的macos（对参数位置很严格） item2
	以上用ssh命令
* ubuntu、centos、redhat、fedors、debian哪个好用？
ubuntu：服务器其次选择，图形界面经常奔溃<br/>
| centos：服务器首选<br/>
| redhat：<br/>
| fedors：国外，桌面首选<br/>
debian：国外
steam：国外

### linux进程管理相关命令
* top命令：任务管理器，隔几秒刷新一次，退去q
* ps：看当前系统中进程 aux所有进程。 看特定|grep 哪个用户启动的，pid分辨进程的唯一标识，【】归系统（内核）管 不能动，路径或参数的可以自己管理。1号进程是协助其他的进程的
* kill、pkill（用文件名nginx）
* w：哪些用户登录进来
* last：登录历史（什么时候谁登录进去的）
* last -n：只显示10条
* lastb：登录失败的记录，这个账号密码不能太简单
