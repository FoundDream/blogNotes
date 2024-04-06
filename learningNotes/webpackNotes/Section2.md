# Section2-ES Module(Part1)

## ES Module 特性

### 特性

- 使用 ES Module 标准  
  通过给 script 添加 type = "module" 的属性，就可以以 ES Module 的标准来执行 JS 代码

  ```js
  <script type="module"></script>
  ```

- 特性

  - 自动采用严格模式，不用添加'use strict'
  - 每个 ES Module 都是运行在单独的私有作用域中（变量不能公用），解决了污染作用域的问题
  - ESM 是通过 CORS 的方式请求外部 JS 模块的
  - ESM 的 scripte 标签会延迟执行脚本，类似 defer 属性，这样就不会阻拦加载其他内容了

  > 跨源资源共享（CORS，或通俗地译为跨域资源共享）是一种基于 HTTP 头的机制，该机制通过允许服务器标示除了它自己以外的其他源（域、协议或端口），使得浏览器允许这些源访问加载自己的资源。跨源资源共享还通过一种机制来检查服务器是否会允许要发送的真实请求，该机制通过浏览器发起一个到服务器托管的跨源资源的“预检”请求。在预检中，浏览器发送的头中标示有 HTTP 方法和真实请求中会用到的头。

## ES Module 导入和导出

### 导入和导出的简单用法

- export 导出代码

  ```js
  export const name = "foo module";
  export { name }; // 更常见
  export { name as fooName }; // 重命名
  export { name as default }; // 默认导出，需要重命名
  export default name; // 默认导出
  ```

- import 导入代码

  ```js
  import { name } from "./module.js";
  import { default as fooName } from "./module.js";
  import abc from "./module.js"; // 随便取名字，会直接重命名，因为我们默认导出了
  ```

### 导入和导出的注意事项

- 对 {} 的理解

  这是一个固定的语法，不要错误的理解为解构  
  这是导出对 name 的引用，并不是复制，仅仅是告诉了地址

  ```js
  export { name };
  ```

  这样就是导出一个对象，JS 对于这两个 {} 的理解是不一样的

  ```js
  export default { name };
  ```

- 不能在模块的外部修改成员，在外部状态为只读

### 导入用法

- 规则用法

  - 不能省略拓展名.js
  - 相对路径，必须要以./开头
  - 绝对路径，用/开头，或用完整 URL
  - import 只能出现在最顶层，不能嵌套在函数之中

- 特性

  - 直接 {}，不会提取成员，而只是执行模块
  - 直接 import 同理
  - 用 \* 提取所有成员，会提取 2 成一个 object
  - 动态加载模块，调用 import 会返回一个 promise
  - 同时导出 export 和 export default

  ```js
  import {} from "/module.js";
  import "./module.js";
  import * as mod from "/module.js";
  import("/module.js").then((module) => console.log(module));
  import abc, { name } from "/module.js"; // 同时导出的情况
  ```

### 直接导出所导入的成员

直接把 import 改成 export
我们导入的成员，将会成为导出成员，所以在当前作用域下，我们不能访问当前成员了
如果是 default 的话，要先进行重命名，不然无法识别是那个文件的 default
