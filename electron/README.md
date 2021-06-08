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
