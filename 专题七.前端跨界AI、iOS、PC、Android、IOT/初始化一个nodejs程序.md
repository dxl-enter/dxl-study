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


浏览器打开localhost:3000


# 创建Dockerfile文件
1. Dockerfile是由一系列命令和参数构成的脚本，一个Dockerfile里面包含了构建整个image的完整命令。Docker通过docker build执行Dockerfile中的一系列命令自动构建image。在.dockerignore文件里面写入代码。表示过滤改类型的文件。类似git的.gitignore

```
# 忽略以下文件
# logs 
logs
*.log
npm-debug.log*

# Runtime data
pids
*.pid
*.seed

# Directory for instrumented libs generated by jscoverage/jscover
lib-cov

# covarage Directory used by tools like istanbul
covarage

# dependency directories
node_modules
jspm_packages

# optional npm cache directory
.npm

# optional repl history
./node_repl_history
.idea
.node_modules
node_modules
.vscode
```

2. 在Dockerfile文件中写入一下代码

```
# 定制node镜像版本
FROM node:8.9-alpine
# 声明作者
MAINTAINER evilboy
# 移动当前目录下面的文件到app目录下
ADD . /app/
# 进入到app目录下，类似cd
WORKDIR /app
# 安装依赖
RUN npm install
# 对外暴露的端口
EXPOSE 3000
# 程序启动脚本
CMD ["npm","start"]

```

# 构建镜像
1. 使用build命令构造镜像，注意后面那个"."不能少，表示当前路径，如果在其他路径这儿要写全路径

```
docker build -t docker_demo .
```

2. 等待镜像构造完成，然后使用images命令查看镜像 docker images
3. 此时可以看到images已经构建完成。现在已经启动images，并测试

```
# 启动镜像 -d表示后台执行， -p 9000:3000表示指定本地的9000端口映射到容器内的3000端口，docker_demo为镜像名称
# 第一次启动执行用下面的
docker run -d -p 9000:3000 docker_demo
# 第二次启动执行用下面的
docker start docker_demo
# 查看容器
docker ps
```

4. 此时浏览器打开http://localhost:9000，表示容器运行正常
5. 如果此时本地无法打开，可以使用log 命令查看日志。根据日志修改对应出现的对方。docker log
