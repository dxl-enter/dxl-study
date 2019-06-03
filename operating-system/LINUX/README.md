## 03 Linux基础入门
### 3.1 linux操作系统介绍
    linux发行版本：ubuntu、redhat、centos、debain、fedora等
    虚拟机：是通过软件模拟的具有完整硬件系统功能的，运行在一个完全隔离环境中的完整计算机系统。流行的虚拟机软件有vmware（商业化）、virtualbox（开源）和virtual pc（微软 免费）
### 3.2 linux和虚拟机基本安装
### 3.3 linux基本命令入门
    当前短目录：ls dir
    长格式目录：ls -l（访问权限 数量 属于用户组 大小 创建时间 名称）
    显示隐藏文件：ls -a
    创建目录：mkdir 目录名称
    复制文件：cp 复制文件 复制到aaa/复制之后文件名称
    复制目录：cp -R 复制目录 复制到aaa/复制之后目录名称
    显示用户全部目录：pwd
    删除文件命令：rm 文件名
    删除目录命令：rm -r 目录名称
    
### 前端必会的linux知识
* linux官方网站：www.kernel.org
* linux和windows有什么区别
	- linux：用于服务器，内核是unix
	- unix：制定业界的规范
	- mac：是基于BSD
		+ https://www.vmware.com/cn.html
		+ flution
		+ 终端：putty（不推荐）、xshell 6.0（推荐）
		+ iterm2
	- windows：主要用于个人的桌面（图形界面-对系统资源的消耗）
		+ vmware虚拟机
		+ centos: dvd-centos
		+ cmder终端运行：ssh root@服务器地址 exit退出服务器
	- 发型的cpu - 多核心方向发展
* 认识linux环境
	- 目录 内容
	- bin：命令
	- etc：放置配置文件和重要的脚本
	- mount(mnt)
	- shell:linux是内核，发行版是在此基础上加了外壳
	- home: 普通用户的家
	- root:超级管理员的家（～）
	- boot：linux的核心文件
* 命令
	- 上传文件命令： scp 文件名 root@服务器地址:/root
	- ssh root@服务器地址 
	- exit：退出服务器
	- vi：文本编辑器（再输入i进行编辑）退出编辑：esc -> :wq(!表示强制退出，顺序不能错，必须先进行写再退出)
	- ifdown ens33（网卡名称）: 关闭网卡
	- ifup ens33（网卡名称）: 启动网卡
	- nano：仿照图形界面
	- yum：安装（linux发行版命令中的）
	- 如果密码忘记了：centos进入单用户模式
* 前端开发必须要懂的知识
	- 网络端口
		+ 什么是端口
			给门编号
		+ 端口冲突时怎么回事
			一个端口在同一时间内只能为一个进程使用（服务和服务自建发生）
	- 什么时服务
		+ 服务管理：
		+ 查看系统服务状态命令：systemctl status nginx（服务名）
		+ 启动服务：systemctl/le start nginx（服务名）
		+ 停止服务：systemctl stop nginx（服务名）
		+ 重启服务：systemctl restart nginx（服务名）
		+ 热更新配置：systemctl reload nginx（服务名）

	- 什么时终端
* 安装nodejs

## [前端必会的Linux知识](https://github.com/dxl-enter/dxl-study/blob/master/Linux%20%E5%BC%80%E5%8F%91%E7%8E%AF%E5%A2%83%E5%88%9D%E5%87%86%E5%A4%87%E8%AE%B2%E4%B9%89.pdf)
