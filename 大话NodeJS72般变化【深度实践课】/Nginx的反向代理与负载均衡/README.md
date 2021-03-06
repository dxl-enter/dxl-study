### Nginx的反向代理与负载均衡
1. 什么是反向代理与负载均衡
* 我们有时候，用自己的计算机A想访问国外的某个网站B，但是访问不了，此时，有一台中间服务器C可以访问国外的网站B，那么，我们可以用自己的电脑访问服务器C，通过C来访问B的这个网站。那么这个时候，服务器C称为代理服务器，这种访问方式叫做正向代理。正向代理有一个特点，就是我们明确知道要访问哪个网站。
* 再如，当我们有一个服务器集中，并且服务器集群中的每台服务器的内容一样的时候，同样我们要直接从个人电脑访问到服务器集中的服务器的时候无法访问，且此时第三服务器能访问集群，这个时候，我们通过第三方服务器访问服务器集群的内容，但是此时我们并不知道是哪一台服务器提供的内容，此时的代理方式称之为反向代理。
* 当一台服务器的单位时间内的访问量越大的时候，服务器的压力会越大。当一台服务器压力大得超过自身得承受压力能力得时候，服务器会崩溃。为了避免服务器奔溃，让用户有更好地体验，我们通常同各国负载均衡得方式分担服务器压力。那么什么时候负载均衡呢？是这样，我们可以建立很多很多个服务器，这些服务器组成一个服务器集群，然后，当用户访问我们网站得时候，先访问一个中间服务器，再让这个中间服务器再服务器集群中选择一个压力较小得服务器，然后将该访问请求引入该选择得服务器。这样，用户得每次访问，都会保证服务器集群中的每个服务器的压力趋于平衡，分担了服务器压力，避免了服务器奔溃的情况。
2. nginx负载均衡的实现
* nginx是一款可以通过反向代理实现负载均衡的服务器，使用nginx服务实现负载均衡的时候，用户的访问受限会访问到nginx服务器，然后nginx服务器再从服务器集群表中选择压力较小的服务器，然后将改访问请求引向该服务器。若服务器集群中的某个服务器奔溃，那么从待选服务器中将该服务器删除，也就是说一个服务器加入奔溃了，那么nginx就肯定不会将访问请求引入该服务器了，
3. http upstream模块
* 什么是http upstream：是nginx服务器的一个重要模块。upstream模块实现在轮询和客户端ip之间实现后端的负载均衡。
* ip_hash指令：如何让同一个用户落在同一台服务器上
* server指令：
4. 其他负载均衡的方法

![服务器集群文件](https://github.com/dxl-enter/dxl-study/blob/master/%E5%A4%A7%E8%AF%9DNodeJS72%E8%88%AC%E5%8F%98%E5%8C%96%E3%80%90%E6%B7%B1%E5%BA%A6%E5%AE%9E%E8%B7%B5%E8%AF%BE%E3%80%91/Nginx%E7%9A%84%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E4%B8%8E%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1/Dingtalk_20201229141545.jpg?raw=true)

### 部署nodejs上线步骤
1. 打开https://brew.sh/index_zh-cn.html
2. brew search nginx  brew install nginx
3. brew info nginx
4. nginx -v 查看nginx信息
5. 启动sudo brew services start nginx(默认端口8080)
  * 备注：如果你安装过jenkins的话这里会失败
  * sudo launchctl unload/Library/LaunchDaemons/org.jenkins-ci.plist
  * systemctl start jenkins
6. 关闭sudo brew services stop nginx/nginx
7. nginx -s reload 、nginx -s stop
8. 打开nginx具体安装目录 查看配置文件 /usr/local/etc/nginx/
9. 验证配置文件nginx -t -c 自己的配置文件地址
10. 拷贝配置文件至node项目目录 重新修改
11. 服务器端的nginx地址
### 腾讯地图H5 NodeJS架构搭建
1. 摆在眼前的现实
* 业务的烂尾楼：可做可不做
* 纯前端项目开发无代理中间层
* gulp完成整站的业务
* 对静态资源的版本控制不足 无md5等：更新版本后因为缓存之前版本代码，现在代码无用
* 利用ajax对后端解救解耦：后端返回的数据过于庞大
2. 架构升级
* php是最好的语言
* 寻找合适的脚手架支持node以及前端资源
* 基于fis的yogurt预发布版本 坑！
* 跌跌撞撞第一个controller（路由）：这条路是controller，到哪个弯拐是action
* 准备完备的中间层（request：用户输入的对象、response：给用户输出的对象、next：传输数据）：错误处理、配置、报告、用户信息、客户端判断是都是微信QQ、地理定位同通过next挂载到request对象全局可用。
3. 逐步完备
* 抽象的接口层，必须通过继承实现对应方法
* 可容错可重试http请求模块
* 不停更新提取壮大的帮助类文件夹（微信定位、数据距离处理计算公式、服务出错短信、用户ip等等）
* controller义军突起疯狂的正则验证
* model发力，异步model同步model，责任链模式。所有协议Unix Domain Socket(内存见交换数据)走IPC（进程间交换数据）同时搭载L5动态分配集群IP（维护内部服务器ip的列表）
4. 预备上线
* 前端工程化的搭载动态文件的map分析压缩打包并至CDN
* 单测、压测性能分析工具发现Bug
* 编写nginx-conf实现负载均衡和反向代理
* PM2启动应用程序小流量灰度上线，修复Bug：bug不会都修复完就要上线
* 上线前的不眠夜
5. 服务器集群

![服务器集群文件](https://github.com/dxl-enter/dxl-study/blob/master/%E5%A4%A7%E8%AF%9DNodeJS72%E8%88%AC%E5%8F%98%E5%8C%96%E3%80%90%E6%B7%B1%E5%BA%A6%E5%AE%9E%E8%B7%B5%E8%AF%BE%E3%80%91/Nginx%E7%9A%84%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E4%B8%8E%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1/Dingtalk_20201229150007.jpg)

![服务器集群文件](https://github.com/dxl-enter/dxl-study/blob/master/%E5%A4%A7%E8%AF%9DNodeJS72%E8%88%AC%E5%8F%98%E5%8C%96%E3%80%90%E6%B7%B1%E5%BA%A6%E5%AE%9E%E8%B7%B5%E8%AF%BE%E3%80%91/Nginx%E7%9A%84%E5%8F%8D%E5%90%91%E4%BB%A3%E7%90%86%E4%B8%8E%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1/Dingtalk_20201229150121.jpg)

6. 经典代码

```
// 动态匹配职责链
router.get(/^\/(\d+)_(\d+)/,cModel.A,cModel.B,cModel.C);

// 加密模块
var shaObj = new jsSHA(string, 'TEXT');
var hash = shaObj.getHash('SHA-1', 'HEX');

// 做一些特殊的请求报头
var forPound = req.headers['x-forwarded-for-pound'];

// 在抛出异常的地方做处理
callback(new Error('Fail to parse http response to json,url:'+reqOptions.url),res,body);

// 在路由没有加载进来之前把middleware加载进来
require('./middleware')(app);
```

