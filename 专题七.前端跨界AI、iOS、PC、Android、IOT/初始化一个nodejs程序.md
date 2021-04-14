# 初始化一个nodejs程序
## 以下操作必须已经安装了nodejs
1. 首先创建一个空文件夹。并创建一下文件
* server.js
* package.json
* Dockerfile
* .dockerignore
```
mkdir docker_demo
cd docker_demo
touch server.js
touch package.json
touch Dockerfile
touch .dockerignore
```
2. 然后在server.js写入

```
const koa = require('koa');
const app = new koa();

app.use(async ctx => {
  ctx.body = "Hello decker";
});
app.listen(3000);
```
3. 在package.json中写入

```
{
  "name":"docker_demo",
  "version":"0.1.0",
  "private":true,
  "script":{
    "start": "node server.js"
  },
  "dependencies":{
    "koa": "^2.5.0"
  }
}
```

4. 测试程序，控制台输入

```
npm start
```
