# CSS 盒子模型

## 1. 认识盒子模型

一般具有四个属性

- 属性（content）
  - 元素内容 width/height
- 内边距（padding）
  - 元素和内容之间的间距
- 边框（border）
  - 元素自己的边框
- 外边距（margin）
  - 元素和其他元素之间的间距
- 每个属性有四个边

![CSS-Model](../../../img/cssNotes/box-model.png ":size=50%")

- 设置内容是通过宽度和高度设置的
  - 移动端适配时, 可以设置最大宽度和最小宽度
  - min-width：最小宽度，无论内容多少，宽度都大于或等于 min-width
  - max-width：最大宽度，无论内容多少，宽度都小于或等于 max-width
  - min-height max-height 不常用

> 水平居中补充:
> `text-align` 用于 inline level;
> `margin: 0 auto` 用于 block level  
> margin 的实际原理是，盒子元素会占据一整行，给一个盒子设置了宽度，还有剩余空间没有占用，默认会把右边填满，这样设置可以让左右去平方空白，做到居中效果

!> 注意: 对于行内级非替换元素来说, 设置宽高是无效的!

## 2. 盒子模型属性

### 内边距 - padding

- padding 缩写属性
  - 从上开始，顺时针转动
  - 如果有三个值，left = right
  - 如果两个值，就是上下左右一样
  - 如果一个值，全部都一样

### 边框 - border

- 用于设置盒子的边框
  - 边框有宽度 width
    - border-width 是 4 个属性的简写属性
  - 宽度有样式 style
    - border-style 是上面 4 个属性的简写属性
    - 有很多种类，具体可以去看看文档
  - 边框有颜色 color
    - border-color 是上面 4 个属性的简写属性
- 可以用 border 直接缩写三个大属性，任意顺序

![border-style](../../../img/cssNotes/boder-style.png ":size=50%")

- border-radius 圆角
  - 属性：
    - 数值
    - 百分比，在水平和垂直方向会分别计算
  - 如果一个元素是正方形, 设置 border-radius 大于或等于 50%时，就会变成一个圆

### 外边距 - margin

- margin 属性用于设置盒子的外边距, 通常用于元素和元素之间的间距
- margin 包括四个方向，margin 是缩写属性
- margin 也并非必须是四个值, 也可以有其他值

> 建议是父子关系之间用 padding，兄弟关系之间用 margin

- margin 的上下传递问题
  - 要清楚，左右是不会传递的
  - margin-top: 如果块级元素的顶部线和父元素的顶部线重叠，那么这个块级元素的 margin-top 值会传递给父元素
  - margin-bottom: 如果块级元素的底部线和父元素的底部线重写，并且父元素的高度是 auto，那么这个块级元素的 margin-bottom 值会传递给父元素
  - 如何防止出现传递问题
    - 给父元素设置 padding-top\padding-bottom
    - 给父元素设置 border
    - 触发 BFC: 设置 overflow 为 auto
- margin 的上下折叠问题
  - 垂直方向上相邻的 2 个 margin（margin-top、margin-bottom）有可能会合并为 1 个 margin，这种现象叫做 collapse（折叠）
  - 水平方向上的 margin（margin-left、margin-right）永远不会 collapse
  - 折叠后最终值的计算规则
    - 两个值进行比较，取较大的值
  - 为了防止折叠，最好只设置一个 margin
  - 两种可能
    - 两个兄弟块级元素之间上下 margin 的折叠
    - 两个兄弟块级元素之间上下 margin 的折叠

![collapse](../../../img/cssNotes/collapse.png ":size=80%")

### 外轮廓 - outline

- outline 表示元素的外轮廓
  - 不占用空间
  - 默认显示在 border 的外面
- 属性：
  - outline-width: 外轮廓的宽度
  - outline-style：取值跟 border 的样式一样，比如 solid、dotted 等
  - outline-color: 外轮廓的颜色
  - outline：outline-width、outline-style、outline-color 的简写属性，跟 border 用法类似
- 实际应用：
  - 去除 a 元素、input 元素的 focus 轮廓效果

### 盒子阴影 - box-shadow

- 属性 `<shadow> = inset? && <length>{2,4} && <color>?`
  - 第 1 个`<length>`：offset-x, 水平方向的偏移，正数往右偏移
  - 第 2 个`<length>`：offset-y, 垂直方向的偏移，正数往下偏移
  - 第 3 个`<length>`：blur-radius, 模糊半径
  - 第 4 个`<length>`：spread-radius, 延伸半径
  - `<color>`：阴影的颜色，如果没有设置，就跟随 color 属性的颜色
  - inset：外框阴影变成内框阴影
- 盒子阴影 – [在线查看](https://html-css-js.com/css/generator/box-shadow/)

### 文字阴影 - text-shadow

- text-shadow 用法类似于 box-shadow，用于给文字添加阴影效果
- 属性 `<length>{2,3} && <color>?`
  - 相当于 box-shadow, 它没有 spread-radius 的值
- [在线查看效果](https://html-css-js.com/css/generator/box-shadow/)

## 3. 注意事项

### 行内非替换元素的注意事项

- 以下属性对行内级非替换元素不起作用
  - width、height 直接不会生效
  - margin-top、margin-bottom 直接不会生效
- 以下属性对行内级非替换元素的效果比较特殊
  - padding-top、padding-bottom 会生效，但是不占用空间
  - border-top、border-bottom 会生效，但是不占用空间

### 盒子尺寸计算 - box-sizing

- 用来设置盒子模型中宽高的行为
- content-box（W3C 标准盒子模型）
  - padding，border 都布置在 width，height 的外边
- border-box（IE 盒子模型（IE8 以下浏览器））
  - pading，border 都布置在 width，height 的里面

### 一些思考题

- 背景色有没有设置到 border 下面？
  - 有设置，会给盒子模型所有属性都设置
- border 如果没有设置颜色，会使用什么颜色？
  - 如果设置了前景色（color 属性），会使用 color
