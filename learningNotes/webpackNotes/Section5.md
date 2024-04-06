# Section5-WebPack(Part1)

## 快速上手

- yarn init --yes 初始化
- yarn add webpack webpack-cli --dev 安装 webpack 包
- yarn webpack 启动打包
  - 从 index.js 开始打包
  - 存放在 dist 文件中
  - 打包后引入不需要 type="module"
- 简化指令
  - 为了不每次都输入 yarn，在 package.json 中配置 scripts

## 配置文件

- 默认行为 'src/index.js' -> 'dist/index.js'
- webpack.config.js
  - 运行在 node 环境，用 CommonJS 来编写

```js
const path = require('path')

module.exports = {
  entry: './src/main'm
  output: {
    filename: 'bundle.js'
    path: path.join(__dirname, 'output')
  }
}

```

## 工作模式

- webpack --mode xxx

  - production 优化打包结果
  - development 优化打包速度
  - none 不进行额外的处理

> 可以在配置文件直接设置

## 打包结果运行原理
