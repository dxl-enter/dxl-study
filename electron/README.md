# electron
## 创建项目
1. 安装electron

```
npm install -g electron
cnpm install -g electron
```

2. 克隆一个仓库、快速启动一个项目

```
克隆示例项目的仓库
git clone https://github.com/electron/electron-quick-start
进入这个仓库
cd electron-quick-start
安装依赖并运行
npm install && npm start
```

3. electron-forge 搭建一个electron项目
electron-forge相当于electron的一个脚手架，可以让我们更方便的创建、运行、打包electron项目。
github地址：https://github.com/electron-userland/electron-forge
官网地址：https://www.electronforge.io
note:electron forge requires node 10 or above,plus git installed.

```
1、如果你的电脑上面安装了最新版本的nodejs可以使用npx创建项目，如果你电脑上面安装了yarn也可以使用yarn创建项目
npx create-electron-app my-new-app
或者
yarn create electron-app my-new-app

2、运行项目
cd my-new-app
npm start

3、也可以使用以下方法创建项目
npm install -g @electron-forge/cli
electron-forge init my-new-app
cd my-new-app
npm start
```

4. 手动创建一个electron项目

```
1、新建一个项目目录，例如：electrondemo01
2、在electrondemo01目录下新建三个文件：index.html、main.js、package.json
3、index.html里面用css进行布局
4、在main.js中写以下代码
const { app, BrowserWindow } = require('electron');
const path = require('path');

const createWindow = () => {
  const mainWindow = new BrowserWindow({
    width: 800,
    height: 600,
  });

  // and load the index.html of the app.
  mainWindow.loadFile(path.join(__dirname, 'index.html'));
};
app.on('ready', createWindow);
app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') {
    app.quit();
  }
});

```

## electron主进程和渲染进程
1. package.json中定义的入口被称为主进程。在主进程中实例化browserWindow创建的web页面被称为渲染进程。一个electron应用只有一个主进程。但是可以又多个渲染进程，每个electron中的web页面运行在它自己的渲染进程中。
2. 主进程使用browserWindow示例创建页面。每个browserWindow实例都在自己的渲染进程里运行页面。当一个browserWindow实例被销毁后，相应的渲染进程也会被终止。

## electron主进程和渲染进程中使用nodejs以及nodejs第三方模块
electron5.x之前默认可以在主进程以及渲染进程中直接使用nodejs，但是在electron5.x之后默认没法在渲染进程中直接使用nodejs，如果我们想在渲染进程中使用nodejs的话需要进行如下配置

```
const mainWindow = new BrowserWindow({
  width: 800,
  height: 600,
  webPreference:{
    nodeIntegration:true,   // 开启渲染进程中使用的nodejs
    enableRemoteModule:true // electron10.x以后要使用remote模块的话必须得在browserWindow中开启此项
  }
});
```
渲染进程的报的错在浏览器console中，而主进程的报错在编辑器控制台
