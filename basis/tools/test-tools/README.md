# JavaScript于QA测试工程师
### 单元测试
* 为什么？
	现在ci和cd需要这个做铺垫 devops自动化运维 nodevops不要运维 
	保证代码质量都靠自动化测试（测试qa 前端fe 后端rd 运维op 数据库db 项目主管pm）
	- 正确性：测试可以验证代码的正确性，在上线前做到心理有底
	- 自动化：当然手工也可以测试，通过console可以打印出内部的信息，但是这是一次性的事情，下次测试还需要从头来过，效率不能得到保证。通过编写测试用例，可以做到一次编写，多次运行。
	- 解释性：测试用例用于测试接口、模块的重要性，那么在测试用例中就会涉及如何使用这些api。其他开发人员如果要使用这些api，那就阅读测试用例是一种很好的途径，有时比文档说明更清晰。
	- 驱动开发：知道设计：代码被测试的前提是代码本身的可测试性，那么要保证代码的可测试性，就需要在开发中注意api的设计，tdd将测试前移就是起到这么一个作用。
	- 保证重构：互联网行业产品迭代速度很快，迭代后必然存在代码重构的过程，那怎么才能保证重构后代码的质量呢？有测试用例做后盾，就可以大胆的进行重构
* 单元测试简介：
	- 目的：单元测试能够让开发者明确知道代码结果
	- 原则：单一职责、接口抽象、层次分离
	- 断言库：保证最小单元是否正常运行监测方法
	- 测试风格：测试驱动开发（test-driver development：tdd）：提前把测试用例写好，再写项目（这个在国内很难推动）、（behavior-driver development：bdd）行为驱动开发均是敏捷开发方法论：先把代码写完再测试（大部分公司用这个）。
		+ tdd：关注所有的功能是否被实现（每一个功能都必须有对应的测试用例），suite配合test利用assert（‘tobe’==user.name）；
		+ bdd：关注整体行为是否符合整体预期，编写的每一行代码都有目的提供一个全面的测试用例集。expect/should,describe配合it利用自然语言expect(1).toEqual(fn())执行结果
* 单元测试框架：
	- better-assert（tdd断言库）
	- should.js（bdd断言库）
	- expect.js（bdd断言库）
	- chai.js（tdd bdd双模）
	- jasmine.js（bdd断言库）
	- node.js本身继承require("assert")
	- intern 更是一个大而全的单元测试框架
	- qunit 一个游离在jquery左右的测试框架
	- macaca 一套完整的自动化测试解决方案 国产神器来自阿里巴巴
* 单元测试运行流程（图片）
* 自动化单元测试
	- karma 自动化runner集成phantomjs无刷新
	- npm install -g karma
	- karma init（会在项目下生成karma.conf.js文件：配置files、singleRun：true）
	- npm install karma-cli --save-dev
	- npm install karma-jasmine jasmine-core --save-dev（安装断言库）
	- npm install karma-chrome-launcher --save-dev
	- npm install karma-phantomjs-launcher --save-dev
	- npm install karma-mocha --save-dev
	- npm install karma-chai --save-dev
* 搭建环境
	- 安装：`sudo npm i -g yarn（有缓存）`,`sudo npm install -g cnpm --registry=https://registry.npm.taobao.org`，区别：yarn有离线缓存，比npm要快
	- npm init -y:直接确定本地这个包
	- 最早的npm 在本地装了一个包，这个包的版本发生了变化，就会造成原来的文件报错，后来解决这个问题，在本地加了个锁package.json.lock
	-  save和save-dev是有区别的，save：上线阶段用的包save-dev：开发阶段用的包，npm的包并不一定都会用到你的项目里，有些包在开发阶段用，但是编译完了就不用了（远程部署只装save不装dev）。
* 测试代码
	- 分支测试：必须在spec里面建立两个分支的测试，但是建立一个也测试通过，这个少了一个分支没有测试到，此时应该装代码测试覆盖率检查
	- 测试覆盖率检查：`npm install phantom --save-dev`必须装phantom否则报错：`Cannot load browser "PhantomJS": it is not registered! Perhaps you are missing some plugin?`,`npm install karma-coverage --save-dev`，并且配置如下 

	```preprocessors: {
      'unit/**/*.js': ['coverage']
    },
    // coverage生成的报表 放哪里去
    coverageReporter: {
      type: 'html',
      dir: './docs/coverage/'
    },


    // test results reporter to use
    // possible values: 'dots', 'progress'
    // available reporters: https://npmjs.org/browse/keyword/karma-reporter
    reporters: ['progress', 'coverage']
    ```
    
    - 一小段代码是单元，一小段插件也是单元
    	+ 别碰这种单元册，会被搞疯
		+ `npm install --save-dev react-testing-library`
		+ `npm install --save-dev react-dom`
		+ jest 专门测试

			```
			npm install --save-dev jest-dom ject
			这时候运行npm run unit会默认执行tests里面的代码，这时需要把tests文件移走。这时候再运行npm run unit，这时代码提示不认识const {getByTestId} = render(<App/>);中的<App/>，需要继续安装以下包
			npm install --save-dev react-scripts
			npm install --save-dev react
			// 需要卸载`"jest": "^24.8.0",`否则会报错
			```
*  e2e:端对端（平时再去写对应文件的时候，都要人肉的点,但是这个是自动化脚本，写程序去自己执行， 任何项目都必须用e2e）
	- selenium-webdriver
		+ `npm install selenium-webdriver --save-dev`
		+ 安装驱动（https://github.com/mozilla/geckodriver/releases+firefox浏览器）
	- Nightwatch.js
		+ 更加纯粹化
		+ 非常专业
	- rize.js
		+ `npm install --save-dev puppeteer rize`
		+ 跑在后台的进程，更适合写爬虫
		+ 没有报错则可以跑通
	- f2etest （阿里巴巴的测试框架）
		+ 原理：代码提交到svn，有一台git机器能从svn上拉去代码，这个机器就是测试的头（带着一帮小弟->不同版本的浏览器windows云 进行录制（一处生成，处处运行）测试）这个环境需要会的知识特别多（iis、linux等 ）
		+ UI Recorder

* service测试：
	- 主要作用：用来测试异步脚本（提供：it、done）
	- 安装`npm install --save-dev mocha `
* 

### UI测试
* ui走查环节：
* PhantomCSS：PhantomJS的孪生妹妹，比较两个图像对不对
* backstop：要比PhantomCSS强大
	- `npm install -g backstopjs`
	- 测试图片放在
	- `backstop init`
	- `backstop test`
* 
### 性能测试
### 安全测试
### 功能测试
### 总结
1. 单元测试 小的函数
2. 单元测试 小的组件
3. 接口测试 确保数据
4. e2e测试 确保功能
5. UI测试 确保样式
6. f2etest 确保多浏览器下的实际环境 【冒烟测试】：就是只测改的功能，【回归测试】：所有的都测试一遍

### 遇到的问题
* 报错：TypeError: undefined is not a constructor (evaluating 'window.add(1)') in tests/unit/index.spec.js (line 3)
	- 解决1: 使用function(a)
	- 解决2: phantomJS这边对ES6支持的不好，还的配置karma-webpack
* 
