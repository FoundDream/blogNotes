# CSS 常见选择器

## 1. 选择器

- 选择器来选出符合条件的元素
- 分类
  - 通用选择器
    - 选择所有元素，不推荐使用，会遍历所有元素，不利于性能优化
  - 简单选择器
    - 元素选择器
    - 类选择器
    - id 选择器
  - 属性选择器
    - [title]：选中有 title 的属性
    - [title=div]：div 有 title 的属性
    - 还有需要其他用法，但是实际开发不会使用，需要可以查 MDN 文档
  - 后代选择器
    - 所有的后代
      - .home span {}
    - 直接子代选择器
      - .home > span {}
  - 兄弟选择器
    - 兄弟指的是有同样的父元素
    - 相邻兄弟选择器
      - 使用+号链接 .home + span
    - 普通兄弟选择器
      - 使用~号链接 .home ~ span
  - 选择器组 - 交集选择器
    - 如果 div 和 p 都有 box 类，但是我只想要 div 被选择，此时就可以使用
    - div.box
  - 选择器组 - 并集选择器
    - 加逗号就行
    - body, p, div

## 2. 伪类

- 伪类也是选择器的一种，它用于选择处于特定状态的元素
- 常见的伪类
  - 动态伪类
    - :link :visited :hover :active :focus
  - 目标伪类
    - :target
  - 语言伪类
    - :lang
  - 元素状态伪类
    - :enable :disabled :checked
  - 结构伪类
    - 后续再补充学习
  - 否定伪类
    - :not
- [MDN 伪类文档](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes)

- 动态伪类

  - a:link 未访问过
  - a:visited 已访问过
  - a:hover 悬浮在上面
  - a:active 点上了还没松手
  - a:focus a/input 聚焦的时候可以使用
  - 建议顺序 LVHA LVFHA
  - 如果只设置 a，相当于全部状态都一样

- 伪元素

  - :first-line、::first-line
  - :first-letter、::first-letter
  - :before、::before
  - :after、::after
  - 为了区分伪元素和伪类，建议伪元素使用 2 个冒号，比如::first-line

- ::before 和::after 用来在一个元素的内容之前或之后插入其他内容（可以是文字、图片）
  - 通过 content 属性来添加内容，如果 content 不设置，则不会显示
  - 默认是 inline level，如果想设置宽度要先调整为 inline-block
