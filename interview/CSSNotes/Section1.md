# CSS 面试题

## 盒模型

题目：简述 CSS 的盒模型

CSS 的盒模型主要包括以下两种，可通过 box-sizing 属性进行配置：

- content-box：默认属性。width 只包含 content
- border-box：width 包含 (content、padding、border)

## CSS specificity (权重)

题目：css 选择器有哪些？优先级？哪些属性可以继承？

1. 常用选择器：

   - id 选择器（#box），选择 id 为 box 的元素

   - 类选择器（.one），选择类名为 one 的所有元素

   - 标签选择器（div），选择标签为 div 的所有元素

   - 后代选择器（#box div），选择 id 为 box 元素内部所有的 div 元素

   - 子选择器（.one>one_1），选择父元素为.one 的所有.one_1 的元素

   - 相邻同胞选择器（.one+.two），选择紧接在.one 之后的所有.two 元素

   - 群组选择器（div,p），选择 div、p 的所有元素

   - 伪类选择器

   - 伪元素选择器

   - 属性选择器

   - 层次选择器（p~ul），选择前面有 p 元素的每个 ul 元素

2. 优先级

   **内联/!important > ID 选择器 > 类/属性选择器 > 标签选择器**
   到具体的计算层⾯，优先级是由 A 、B、C、D 的值来决定的

   规则：

   - 从左往右依次进行比较 ，较大者优先级更高

   - 如果 4 位全部相等，则后面的会覆盖前面的

   - 其中通配符选择器 `*`，组合选择器 `+ ~ >`，否定伪类选择器 `:not()` 对优先级无影响

## z-index

- 层叠上下文可以包含在其他层叠上下文中，并且一起创建一个层叠上下文的层级。
- 每个层叠上下文都完全独立于它的兄弟元素：当处理层叠时只考虑子元素。
- 每个层叠上下文都是自包含的：当一个元素的内容发生层叠后，该元素将被作为整体在父级层叠上下文中按顺序进行层叠。

[MDN 参考链接](https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_positioned_layout/Understanding_z-index/Stacking_context)

## 水平垂直居中

题目：如何实现一个元素的水平垂直居中

- flex:

  - `justify-content: center`
  - `align-content: center`

- grid:

  - `place-items: center`

- absolute/translate:
  - `position: absolute`
  - `left/top: 50%`
  - `transform: translate(50%)`

## 左侧固定、右侧自适应

题目: css 如何实现左侧固定 300px，右侧自适应的布局

使用 flex 布局，左侧 300px，右侧 flex-grow: 1。pug 代码及 css 代码示例如下

```css
.container {
  display: flex;
}
.left {
  flex-basis: 300px;
  flex-shrink: 0;
}
.main {
  flex-grow: 1;
}
```

如果只使用 Grid 布局，则代码会更加简单，只需要控制容器的 CSS 属性

```css
.container {
  display: grid;
  grid-template-columns: 300px 1fr;
}
```

## 三列均分布局

题目: 如何实现三列均分布局

- flex:  
  方案一: `flex: 1`;  
  方案二: `flex-basis: calc(100% / 3)`

- grid:  
  父容器: `grid-template-columns: 1fr 1fr 1fr`

进一步问题：如何实现十六列均分布局？  
`grid-template-columns: repeat(16, 1fr)`

## 如何画一个正方形/长宽固定的长方形

现代化的解决方案是使用长宽比的 CSS 属性: `aspect-ratio`

## CSS 如何避免样式冲突

## CSS 变量

## CSS 黑暗模式
