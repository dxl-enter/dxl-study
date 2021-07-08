# flex
## 整个页面上中下布局
1. 首先在整个页面使用fc + hvh
2. 在header部分使用height多少
3. 在内容部分使用live-container + f1
4. 在footer部分使用height多少 + f




```
.hvh {
  height: 100vh;
}
  .live-container {
    box-sizing: border-box;
    overflow-x: hidden;
    overflow-y: scroll;
    -webkit-overflow-scrolling: touch;
  }
.fc {
  display: flex;
  flex-direction: column;
}
.f1 {
  flex: 1;
}
.f {
  display: flex;
}
```
