# Node.js

## Node.js 是什么

> Node.js is a JavaScript runtime built on V8 engine.

- Node.js 基于 V8 引擎来执行 JavaScript 代码，但是不仅仅只有 V8 引擎
  - V8 可以嵌入到任何 C++程序中，包括 Chrome 和 Node.js
  - 在 Chrome 中，需要解析 HTML 和 CSS 等，所以要提供支持浏览器操作的 API，浏览器的事件循环等
  - 在 Node.js 中，也需要提供其他支持，比如文件系统的读写，压缩解压文件等操作
- 架构图
  - js 代码会先经过 V8 引擎，在经过 bindings，将任务放到 libuv 的事件循环中
  - libuv 是用 C 语言编写的库
  - 提供了上述所需要提供支持的操作

![nodejs](../../../img/feProject/node.js-architecture.png ":size=70%")

## Node 多版本管理 - nvm

- nvm 本身是原生 mac 软件，但是有人做了 nvm-windows
- 常见命令

  - `nvm install latest` 安装最新版本
  - `nvm list` 查看所有版本
  - `nvm use` 切换版本

## Node 常见命令

- `node file.js` 直接运行
- `node file.js num1=20` 带参数运行
  - 会存放在`process`中，用`process.argv`获取参数，argv 本质上是一个数组
  - argv (argument vector)，在 JavaScript 是代指数组，在 C++代指一种数据结构
  - 可以用 forEach 遍历
- Node 内置命令

  - `console.clear()` 清理命令行
  - `console.trace()` 查看调用栈

> cls 是 windows 终端清空的方式，linux，mac，git bash 是 clear

## REPL 的使用

- Read-Eval-Print-Loop 读取-求值-输出循环
- 是一个交互式的编程环境，类似浏览器的控制台
- 直接输入`node`就可以进入，`Ctrl+C`退出

## 常见的全局对象

- 全局对象类似浏览器中的 window，node 中也有自己的全局对象
- 有许多内置的全局对象，Global objects
- module，exports，require() 在模块化中很重要
- 也包括和 window 中一样的定时器方法，其实一模一样，只不过是由 node 提供
- global 和 window 都可以用 globalThis 来表示

> 用 var 来声明变量时，会加到 window，但不会加在 global，这是个微小的区别

### 特殊的全局对象

- 本质上并不是全局对象，但是每个程序都会内置，因此表现地像是全局变量
- 包括：\_\_dirname、\_\_filename 等
- \_\_dirname
  - 展示当前文件所在的目录结构
- \_\_filename
  - 当前目录+文件名
