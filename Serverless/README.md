# Serverless
## Serverless框架介绍
1. Serverless又名无服务器，所谓无服务器并非不需要依赖和依靠服务器等资源，而是开发者再也不用过多考虑服务器的问题，可以更专注在产品代码上，狭义的Serverless是faas和baas组成
2. Serverless是一种软件系统架构的思想和方法，它不是软件框架、类库或者工具。它与传统架构的不同之处在于，完全由第三方管理，由事件触发，存在于无状态（stateless）、暂存（可能只存在于一次调用的过程中）计算容器内。构建无服务器应用程序意味着开发者可以专注在产品代码上，而无需管理和操作云端或本地的服务器或运行时（运行时通俗的讲就是运行环境，比如nodejs环境，java环境，php环境）。Serverless真正做到了部署应用无需涉及基础设施的建设，自动构建、部署和启动服务。
3. 通俗的讲：Serverless是构建和运行软件时不需要关心服务器的一种架构思想。老程序员都用过虚拟主机，刚开始学Serverless你可以把它理解为虚拟主机的升级版本。虚拟主机已经是快被淘汰的上一代产物了，云计算涌现出很多改变传统it架构和运维方式的新技术，比如虚拟机、容器、微服务，无论这些技术应用在哪些场景，降低成本、提升效率是云服务永恒的主题。Serverless的出现真正的解决了降低成本、提升效率的问题。它真正做到了弹性伸缩、高并发、按需收费、备份容灾、日志监控等。
## 传统模式和Serverless模式下项目开发上线流程

## 支持Serverless的厂商
1. 亚马逊 AWS Lambda  https://aws.amazon.com/cn/lambda
2. 谷歌 Google Cloud Functions https://cloud.google.com/functions
3. 微软 Microsoft Azure https://www.azure.cn
4. 阿里云函数计算 https://www.aliyun.com/product/fc
5. 腾讯云 云函数SCF(Serverless cloud function) https://cloud.tencent.com/product/scf
6. 华为云 functionGraph https://www.huaweicloud.com/product/functiongraph.html

## 关于大家关心的几个问题？
1. 为什么不使用亚马逊、谷歌、微软、ibm和Serverless？
答：在国内阿里云、腾讯云使用的更多一些。就和大家购买域名、购买服务器一样，首先想到的坑定不是国外的运营商，当然如果你英文好也可以尝试
2. 阿里云、腾讯云、华为云我们为什么选择腾讯云？

```
答:
1、微信小程序的云开发就是基于腾讯云，选择腾讯云更方便和小程序对接
2、腾讯云在Serverless方面相比其他厂商支持更好一些
3、腾讯云的技术在线客服非常棒
4、腾讯云和Serverless合作在腾讯云中集成了Serverless Framework 让我们可以用我们喜欢的框架开发Serverless应用。也可以让我们快速部署老项目。
5、价格更便宜
```
3. 会使用腾讯云的Serverless以后，其他服务商的Serverless也会了吗？ 是的

## 三分钟搭建部署我们的Serverless应用
这里主要给大家介绍是如何通过Serverless Framework 提供的云函数SCF组件快速创建于部署一个云函数项目。
### 前提条件
Serverless Framework帮助您将项目快速部署到腾讯云Framework平台。因此在部署前，清确认您已经注册腾讯云账号并完成实名认证

```
1. 安装Serverless
npm install -g serverless
serverless -v

2. 创建项目 - 自己要创建项目的目录上面运行Serverless
serverless

3. 部署 - 在Serverless.yml文件所在的项目根目录，运行以下指令进行部署
serverless deploy
```




