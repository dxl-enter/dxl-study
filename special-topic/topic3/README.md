# 免密登陆

## Linux系统配置SSH免密登录(多主机互通)

Linux系统镜像:CentOS-7-x86_64-minimal-1810.iso
虚拟机版本:VMware-workstation-full-12.1.0-3272444

操作成功后的效果:
每台主机可以本机SSH免密登录,也可以与其他主机之间实现SSH免密登录,也就是每台主机都可以一对多SSH免密登录.

现用虚拟机搭建三台主机,IP分别是:
192.168.0.102	master1
192.168.0.103	master2
192.168.0.104	master3
- 免密登录的原理

使用非对称加密，密码学这部分不多说，由于我自己研究的也不是很深，所以暂时不误导大家。就先简单举个形象的例子一笔带过：

​ 服务器上有把锁(公钥)，A口袋里有把钥匙(私钥)，B口袋里也有把钥匙(私钥)，一个锁可以配置多把钥匙，但是钥匙都是一样的，都放在自己的口袋里小心保管着，锁是公开的。有钥匙才能开锁，而且得是对应的钥匙。

- 开始操作
PS:
`authorized_keys`:存放远程免密登录的公钥,主要通过这个文件记录多台机器的公钥
`id_rsa `: 生成的私钥文件
`id_rsa.pub` ： 生成的公钥文件
`know_hosts` : 已知的主机公钥清单

> 方法一:

先选择其中一台主机,在该主机上生成公钥和私钥,再将公钥和私钥上传到其他主机上,具体操作如下:
在这里我就选择master1进行操作以下操作了:
- 1.登录Linux系统,根据自己实际情况选择登录用户,执行下面代码生成公钥私钥对:
```
ssh-keygen -t rsa -C "cola" -f "cola"
这里我们解释一下这几个参数的含义

-t：指定加密方式，一般我们使用rsa的加密方式，当然也可以使用其他加密方式，可以自行折腾。
-C：指定密钥的名称，这里的参数值cola，将会参与最终秘钥对的加密，即会在最终的加密字符串里有体现。
-f：指定秘钥对文件名
最终会在你当前目录下生成两个文件cola_rsa 和 cola_rsa.pub，前者是秘钥文件，后者是公钥。

```
会出现如下提示,一路回车就行
```
[root@master1 ~]# ssh-keygen -t rsa -C "cola" -f "cola"
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): //这里回车
Enter passphrase (empty for no passphrase): //这里回车
Enter same passphrase again: //这里回车
Your identification has been saved in /root/.ssh/id_rsa.
Your public key has been saved in /root/.ssh/id_rsa.pub.
The key fingerprint is:
df:71:f6:3e:bb:bb:6c:38:91:f4:bc:70:a1:dd:86:a9 root@master1
The key's randomart image is:
+--[ RSA 2048]----+
|                 |
|                 |
|                 |
|             . . |
|        S   o Ooo|
|         . . Oo*o|
|          . ..=.o|
|            Eo.= |
|              o*B|
+-----------------+
```
注意：在程序提示输入passphrase时直接输入回车，表示无证书密码(如果需要再输入)。

- 2.生成秘钥的默认目录为:~/.ssh,该目录下会生成下面两个文件:

id_rsa

id_rsa.pub

- 3.实现本地免密登录,将id_rsa.pub中的内容拷贝到authorized_keys
```
ssh-copy-id localhost
```
~/.ssh目录下会生成一个新的文件:authorized_keys

- 4.完成上述步骤后就可以本地SSH免密登录了,运行下面代码出现一行登录时间就代表本地SSH免密登录成功
```
ssh localhost
```
下面是本地SSH免密登录成功的标志:
```
[root@master1 ~]$ ssh localhost
Last login: Mon Aug 27 08:41:20 2018 from 192.168.33.2
```

- 5.如果本机能成功SSH免密登录,
先退出SSH登录:
```
exit
```
再执行以下代码将本机的~/.ssh文件夹复制到其他主机上:
```
scp -r ~/.ssh 192.168.0.102:~/

scp -r ~/.ssh 192.168.0.103:~/
```
提示输入密码时,输入远程主机密码回车即可

- 6.测试SSH免密登录,这里就不发测试了,大家自行测试

> 方法二:

将每台机器生成的id_rsa.pub追加添加到同一个authorized_keys内,然后再将该authorized_keys发送到其他远程主机上.

具体步骤如下:
- 1.在master1,master2,master3上分别执行:
```
ssh-keygen -t rsa
```

与"方法一"内所述一样,一路回车即可,生成秘钥的默认目录为~/.ssh
- 2.接着制作包含master1,master2,master3中所有id_rsa.pub的authorized_keys文件:
此处在master 1上生成authorized_keys文件,

将生成的公钥到服务器对应的home路径下的.ssh/中，输入一下命令，
这里的home就是服务器登录用户的根目录，例如我用root用户登录的，我的根目录就是~。

这里的坑注意⚠️，公钥名一定是个字符串要用引号框起来。

回车，提示输入密码，第一次上传公钥会有些提示。

在master1上执行:
```
ssh-copy-id -i 192.168.33.201
```

在master2上执行:
```
ssh-copy-id -i 192.168.33.201
```

在master3上执行:
```
ssh-copy-id -i 192.168.33.201
```
注意:此处代码中的"-i"千万不要忘记了!!!

配置公钥文件的访问权限为600
```
chmod 600 cola_rsa.pub
```

- 3.通过scp将master1上生成的authorized_keys文件发送给其他主机:
在master1上执行
```
scp -r ~/.ssh/authorized_keys 192.168.33.202:~/.ssh
```
```
scp -r ~/.ssh/authorized_keys 192.168.33.203:~/.ssh
```
提示输入密码时,输入远程主机密码回车即可

- 4.测试SSH免密登录,可先测试本机免密登录,再测试远程主机远程登录

本机登录可用:

ssh localhost

远程登录将localhost换成远程主机IP即可
比如在master1上登录master2,就在master1上执行:
```
ssh 192.168.33.202
```
相关故障处理:
部分人在配置完成后可能出现无法登录的情况,错误代码我不太记得了,欢迎各位读者在下面补充.
造成故障的原因是之前配置过程中配置失败,然后重新对SSH免密登录进行配置,配置完成后无法正常登录,解决方法如下:

删除各主机下~/.ssh目录中的known_hosts文件:
```
rm -rf ~/.ssh/known_hosts
```

## 免密登陆功能的本地配置文件

编辑自己home目录的.ssh/ 路径下的config文件 

配置config文件的访问权限为 644/700

- 配置本地私钥

上面几步都是在远程服务器上操作的，这步操作是在本地机器上操作。

把第二步生成的私钥复制到你的home目录下的.ssh/路径下，你可以通过vi打开cola_rsa私钥文件，复制里面的内容，粘贴到你本机的.ssh/下一个新建的文件里，比如我这里新建一个文件还叫cola_rsa，打开这个文件，将刚才复制的私钥的内容粘贴到这个文件里。

配置你的私钥文件访问权限为 600
```
chmod 600 cola_rsa
```
- 免密登陆功能的本地配置文件

编辑本地home目录下的.ssh/路径下的config文件，如果没有，新建一个即可，编辑config文件

```
Host cola
User root
HostName 192.168,0.103
IdentityFile ~/.ssh/cola_rsa

Host cola1
User root
HostName 192.168,0.104
IdentityFile ~/.ssh/cola_rsa
# -------如果需要多主机配置只要在这儿加就好了

# -------以下几行照抄就行，上面几个需要配置对应的参数
Protocol 2
Compression yes
ServerAliveInterval 60  #配置发送心跳包的频率
ServerAliveCountMax 20  #每次心跳包发送个数
LogLevel INFO #日志等级
```

配置config文件访问权限为700

```
chmod 700 config
```

都配置完了？恭喜你你已经可以进行免密登录啦，根据本文的步骤做的配置，可以在终端中输入

```
ssh cola
```
## 总结
当然，凡是涉及到登录远程服务器验证密码的地方，这个免密配置都生效，例如向远程服务器传文件
```
scp xxx.md cola:~/
```
也不需要验证密码了，就可以将本地的xxx.md文件传到远端的~路径下了。


# 安装插件
## 安装jenkins
1. 安装jdk

`yum install openjdk`
* 如果提示`没有可用软件包 openjdk`,需要使用`yum search openjdk`查询出来的openjdk服知道install后面

2. 安装jenkins

```
wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat/jenkins.repo
rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
yum install jenkins
```

3. 启动jenkins

`service jenkins start/stop/restart`

## 配置免密远程登录
1. 

## 安装PM2
* 安装前提：
	1. node环境
	2. npm
* 安装开始
	1. 全局安装 `npm install -g pm2`
	2. 保存当前进程状态 `pm2 save`
	3. 生成开机自启动服务 `pm2 startup`
	4. 查看启动项 `systemctl list-unit-files | grep enable`

	
	```
	$ pm2 start app.js -i 4 #后台运行pm2，启动4个app.js 
                           # 也可以把'max' 参数传递给 start
                           # 正确的进程数目依赖于Cpu的核心数目
$ pm2 start app.js --name my-api # 命名进程
$ pm2 list               # 显示所有进程状态
$ pm2 monit              # 监视所有进程
$ pm2 logs               #  显示所有进程日志
$ pm2 stop all           # 停止所有进程
$ pm2 restart all        # 重启所有进程
$ pm2 reload all         # 0秒停机重载进程 (用于 NETWORKED 进程)
$ pm2 stop 0             # 停止指定的进程
$ pm2 restart 0          # 重启指定的进程
$ pm2 startup            # 产生 init 脚本 保持进程活着
$ pm2 web                # 运行健壮的 computer API endpoint (http://localhost:9615)
$ pm2 delete 0           # 杀死指定的进程
$ pm2 delete all         # 杀死全部进程
```

	```
	运行进程的不同方式
	
	$ pm2 start app.js -i max  # 根据有效CPU数目启动最大进程数目
	$ pm2 start app.js -i 3      # 启动3个进程
	$ pm2 start app.js -x        #用fork模式启动 app.js 而不是使用 cluster
	$ pm2 start app.js -x -- -a 23   # 用fork模式启动 app.js 并且传递参数 (-a 23)
	$ pm2 start app.js --name serverone  # 启动一个进程并把它命名为 serverone
	$ pm2 stop serverone       # 停止 serverone 进程
	$ pm2 start app.json        # 启动进程, 在 app.json里设置选项
	$ pm2 start app.js -i max -- -a 23                   #在--之后给 app.js 传递参数
	$ pm2 start app.js -i max -e err.log -o out.log  # 启动 并 生成一个配置文件
	你也可以执行用其他语言编写的app  ( fork 模式):
	$ pm2 start my-bash-script.sh    -x --interpreter bash
	$ pm2 start my-python-script.py -x --interpreter python
	```
