为了统一团队Git规范，降低维护成本，制定团队Git操作规范。

● 必须关闭git autocrlf替换功能。 参考文档：https://www.cnblogs.com/sdgf/p/6237847.html
● 提交commit 必须准确提交commit记录表示当前commit的操作。
● 每个开发模块、功能、bug修复需分别提交commit，不要合并一起提交。
● commit 记录提交规范统一，参考文档：https://blog.csdn.net/weixin_43801564/article/details/116593685
● 在进行commit提交之前一定要进行 code  review,判断是否符合预期，禁止无关、错误代码提交到仓库。
● 当每次开发新的功能或者修复 Bug , 一定要从远程更新本地开发分支，保证本地开发分支获取最新代码！然后从开发分支迁出分支进行开发或者修改！

Git记录提交规范
feat : 开发了具体的需求功能
fix:修复了bug
docs :文档相关提交
style：代码格式，比如说新增了一个分号，去掉了一些空格之类（注意不是css的变动）
refactor:代码重构，比如对现有功能的重写
test: 测试相关，比如说新增了测试用例
chore：其他改动，不属于其他type的变动都可以用这个表示
revert：撤销之前的




type: subject
(空一行)
body

其中type是提交信息的类型，subject可以是对提交内容的概括，body作为具体的提交内容


具体type的值只能为以下几类：
feat : 开发了具体的需求功能
fix: 修复了bug
docs :文档相关提交
style：代码格式，比如说新增了一个分号，去掉了一些空格之类（注意不是css的变动）
refactor:代码重构，比如对现有功能的重写
test: 测试相关，比如说新增了测试用例
chore：其他改动，不属于其他type的变动都可以用这个表示
revert：撤销之前的commit


git 禁用crlf和lf自动转换功能设置：
git config --global core.autocrlf false
git config --global core.safecrlf true



IDE设置使用UNIX换行符:
IDEA的设置File -> Settings
Editor -> Code Style
Line separator (for new lines) ，选择：Unix and OS X (\n)
对已使用Windows换行符的文件，可以使用Sublime Text打开，
View->Line Endings，选Unix，保存；



分享：idea git提交规范插件：https://plugins.jetbrains.com/plugin/9861-git-commit-template
