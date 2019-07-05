兼容：1/window.devicepixelratio.   压缩viewport
# 从0到大论前端持续集成
## 什么是持续集成（CI）
* 在持续集成环境中，开发人员将会频繁的提交代码到主干。这些新提交在最终合并到主线之前，都需要通过编译 提交-自动化测试-qa-运维-工单-上线（各地区）-内网测试
* 持续交付（continlious delivery）
* 持续化部署（continlious deployment）：conmit-自动化测试-上线（devops：qa+op+软件工程师）
* 持续集成需求
	- 持续集成
	- 线上代码和代码

* 立项 - 仓库（喜欢什么）- 保管好文档 - UI/UE - 动画设计师 - 开发（版本库）- jenkins自动化测试 - 测试 - 上线 - 运维（眼动仪）

## 121齐步走
* 统一代码仓库通过分支管理合并主干道svn
* 自动化构建工具，编译、部署、测试、监控、本机开发上线环境。fis3/webpack/jdists/package.json/chai/supertest/mocha/selenium-webdriver
* 持续集成平台。jenkins、travis cli
* 部署工具。rsync、shelljs、yargs
* 运营同学有权限操作运营页面保存即可上线

## svn开发阶段图示
trunk - branch（先把主干的拉去下来再提交，防止覆盖别人的代码） - tags（回滚机制）

# 前端工程化
## 自动化编译流程 
从外向里 ，再由里向外
## 前端模块化
* 1. 前端模块化框架肩负着 模块管理、资源加载两项重要的功能，这两项功能与工具、性能、业务、部署等工程环节都有着非常紧密的联系

amd：依赖提前声明
cmd：用之前才加载，和nodejs比较像

* 2. 为什么使用webpack？
	- webpack执行commonjs标准，解决了依赖配置和请求流量

## 静态资源定位
* omi
* san.js
* js直接调用汇编

## 自动化部署
* http://www.bootschool.net：ascii
* lolcatjs：渐变色
* emojipe：小表情
* inquirer：用户交互
* js2ts：
* 容错

## 前端工程化与架构
1.awk查 sed改
