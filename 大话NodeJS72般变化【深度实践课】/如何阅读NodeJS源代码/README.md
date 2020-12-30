### 一个错误堆栈信息优化的故事
1. node中出现非逻辑业务的错误，因为是nodejs异步机制。
### 如何运行
1. make test
2. 源文件分三类
* 纯javascript写的核心模块（lib、src）
* 带NativeBinding的javascript核心模块
* C++文件
* v8实现c++到javascript的转化
* nodejs实现事件循环机制：异步请求通过loop回丢掉队列里面，这个队列最后再发请求，走回调
