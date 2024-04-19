# Section0-React 介绍

React 由 Meta 公司开发，可以开发普通的网页，也可以开发原生应用，

## React 的优势

相较于传统基于 DOM 开发的优势

1. 组件化的开发方式
2. 不错的性能

相较于其它前端框架的优势

1. 丰富的生态
2. 跨平台支持

## 开发环境创建

create-react-app 是一个快速创建 React 开发环境的工具，底层由 Webpack 构件，封装了配置细节，开箱即用
执行命令：

```bash
npx create-react-app react-basic
```

1. npx - Node.js 工具命令，查找并执行后续的包命令
2. create-react-app - 核心包（固定写法），用于创建 React 项目
3. react-basic React 项目的名称（可以自定义）
   :::warning
   创建 React 项目的更多方式
   [React 文档](https://zh-hans.react.dev/learn/start-a-new-react-project)
   :::

## 什么是 JSX

JSX 是 Javascript 和 XML（HTML）的缩写，表示在 JS 代码中编写 HTML 模板结构

JSX 是 JS 的语言拓展，浏览器无法识别，需要解析工具（BABEL）来做解析后才可以运行

在 JSX 中用 大括号语法 `{}` 识别 Javascript 的**表达式**

1. 使用引号传递字符串
2. 使用 JavaScript 变量
3. 函数调用和方法调用
4. 使用 JavaScript 对象

## 列表循环

在 JSX 中原生 map 方法来渲染列表，同时要给每个元素加一个 key

```js
const list = [
  { id: 1001, name: "Vue" },
  { id: 1002, name: "React" },
];

<ul>
  {list.map(item => <li key={item.id}>{item.name}</li>)}
<ul>
```

## 条件渲染

可以通过逻辑与运算符&&，三元表达式实现基础的条件渲染

> && 是只要为 True 就一直前进，直到 False 或者最后

自定义函数 + if 语句

## 事件绑定

on + 事件名称 = { 事件处理程序 }

使用事件对象参数

可以在回调函数中设置形参 e

传递自定义函数，使用箭头函数，然后再调用

同时传递事件和对象和自定义参数，保持顺序一致

## 组件

用户界面的一部分，它可以有自己的逻辑和外观，可以互相嵌套，也可以复用

> 在 React 中，一个组件就是**首字母大写的函数**，内部存放了组件的逻辑和视图 UI, 渲染组件只需要把组件当成标签书写即可

## usestate 基础使用

是一个 React Hook （函数），我们可以加一个状态变量

状态变量一旦变化，整个视图 UI 都会变化

1. 修改状态的规则

   状态不可变。我们应该替换它而不是修改它

2. 修改对象状态

   用 set 方法，先展开字符，再赋值新的

基础样式处理

需求：点击 Tab，做高亮处理

点击谁就把谁的 type 记录下来，然后和遍历时的每一项匹配

## classnames 优化类名

[Github 链接](https://github.com/JedWatson/classnames)
