# Section3-ES Module(Part2)

## ES Module in Browsers

### Polyfill 兼容方案

很多国产浏览器或者老 IE 还是不支持这个 ES Module 特性，我们可以用转译器来解决这个问题，也可以用 Polyfilll

- ES Module Loader

  - 直接引用就好
  - 将不识别的代码交给 Babel 转换
  - chrome 会执行两次，所以我们在 script 标签上加上 no module
  - 只适合本地测试，效率很差

  > 提供 Github 链接  
  > [ModuleLoader] (https://github.com/ModuleLoader/browser-es-module-loader )  
  > [promise-polyfill] (https://github.com/taylorhakes/promise-polyfill)  
  > 但是对于 npm 文件来说，我们可以直接用 UNPKG 去下载文件目录，这样更方便简单

## ES Module in Node.js

### 支持情况

- 准备工作

  - 将文件名改成.mjs
  - 输入指令 node index.mjs
  - nodemon 会识别代码修改自动重启动

- 内置模块兼容了 ESM 的提取成员方式
- 第三方模块都是导出默认成员，不能单独导出，只能全部导出一个 object

### 与 CommonJS 模块交互

- ES Module 中可以导入 CommonJS 模块
- 不能再 CommonJS 模块中通过 require 载入 ES Module
- CommonJS 始终只会导出一个默认成员

### 与 CommonJS 模块的差异

- ESM 中没有 CommonJS 中的那些模块全局对象

  ```js
  // 加载模块函数
  console.log(require);

  // 模块对象
  console.log(module);

  // 导出对象别名
  console.log(exports);

  // 当前文件的绝对路径
  console.log(__filename);

  // 当前文件所在目录
  console.log(__dirname);
  ```

- 若在 ESM 中想获取路径，可以使用下面的方法

  ```js
  import { fileURLToPath } from "url";
  import { dirname } from "path";
  const __filename = fileURLToPath(import.meta.url);
  const __dirname = dirname(__filename);
  ```

### 新版本进一步支持 ESM

在 package.json 中加一个 "type" : "module"，也会以 ESM 工作，不需要改拓展名。如果你真的闲的没事干，想在改 type 之后继续用 commonJS，你可以把文件名改成 .cjs，但是你为什么？？

### Babel 兼容方案

- 将新特性转换成旧代码
- yarn babel-node index.js
- 其实是一个个预设插件来转换代码，所以每次需要重新输入代码
- 为了避免重新输入代码，可以新建一个 .babelrc 配置文件来配置

![Babel 原理](../img/babel.jpg "图片title")
