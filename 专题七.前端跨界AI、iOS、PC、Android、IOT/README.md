# 大前端之Kubernetes与Docker
## Docker
1. 微服务的核心思想
 * 微服务属于架构层面的设计模式
  + 之前的做法是单体应用：把页面、逻辑、持久层放在一起
    优点：简单方便
    缺点：压力大，要做负载（页面、逻辑复制同一份的东西，持久层使用同一哥，造成数据库压力变大）；在同一个进程；
    逻辑层服务有的繁忙有的闲，需要根据具体的业务情况，复制繁忙的服务：eg：京东双十一
  + 微服务：加了一个网关统一对外；
           有自己业务的数据库，这样业务就独立出开来了（逻辑和持久层绑在一块复制），服务与服务之间调用内部轻量级的通信方式(为了性能一般不用http，用文本json、消息队列、rtc)
    优点：不同团队操作、压力变小、多进程
    场景：业务迭代快、团队规模大、业务复杂度高、业务需要长期演进
 * 微服务的设计概念以业务功能为主
 * 微服务独立提供对应的业务功能
 * 微服务不拘泥于具体的实现语言
 * 微服务架构 ≈ 模块化开发 + 分布式计算
 * 微服务继承和部署
  + 持续集成 - jenkins
  + 虚拟化 - 虚拟机
  + 容器 - docker，提供基本的运行环境
2. Docker vs vm
  * vm
    + 运行在宿主主机之上的完整的操作系统
    + 运行自身操作系统会占用较多的资源
  * docker
    + docker更加轻量高效
    + 对系统资源的利用率很高
    + 比虚拟机技术更为轻便、快捷
    + 隔离效果不如vm
3. docker的相关概念
  * apache 是web容器
  * tomcat是java容器
  * 通常用于如下场景：
    + web应用的自动化打包和发布：jenkins中加入docker命令打包完push
    + 自动化测试和持续集成、发布：打包的程序放在服务器中，另一边的无头浏览器开始跑
    + 在服务器环境中部署和调整数据库或其他后台应用：把服务包装起来：微信小程序（无服务器）
    + 从头编译或者扩展现有的openShift或cloud Foundry平台来搭建自己的PaaP环境
  * docker是cs架构，主要有两个概念：
    + docker daemon：运行在宿主机上；docker守护进程；用户通过docker client（docker命令）与docker daemon交互
    + docker client：docker命令行，是用户使用docker的主要方式；docker client与docker daemon通信将结果返回给用户；docker client页可以通过socket或者restful api访问远程的docker daemon
  * Dockerfile
    + Dockerfile概念
    + Dockerfile文件格式
    + 构建镜像
    + 镜像标签
    + 修改容器内容

```
FROM centos
MAINTAINER Dxler <823221088@qq.com>

RUN yum install gcc automake autoconf libtool make -y
RUN yum install zlib zlib-devel libffi-devel -y
```

4. 安装与hello world
5. 常用命令与docker
6. docker hub
7. 实战：打包一个web服务器
## Kubernetes
1. 什么是k8s
2. k8s的特性
  * 源码编译安装方式
4. k8s的安装与配置
  * 安装
  * 配置文件结构
  * 常用配置方法
6. 搭建一个nodejs集群
