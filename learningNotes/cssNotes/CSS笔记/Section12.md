# Emmet 和结构伪类

## 1. 认识 emmet 语法

- Emmet (前身为 Zen Coding) 是一个能大幅度提高前端开发效率的一个工具.
  - 在前端开发的过程中，一大部分的工作是写 HTML、CSS 代码, 如果手动来编写效果会非常低.
  - VsCode 内置了 Emmet 语法,在后缀为.html/.css 中输入缩写后按 Tab/Enter 键即会自动生成相应代码
  - !和 html:5 可以快速生成完整结构的 html5 代码，这就是 emmet 的使用
- `>`（子代）和`+`（兄弟）
- `*`（多个）和`^`（上一级）
- ()（分组）
- 属性(id 属性、class 属性、普通属性) {}（内容）
  - div#header+div#main>.container>a[href]
  - a[href="http://www.baidu.com"]{百度一下}
- $（数字）
- 隐式标签 .item 默认 div
- CSS Emmet
  - w100
  - h100
  - 等等

## 2. 结构伪类

### nth-child

- :nth-child(1)
  - 是父元素中的第 1 个子元素
- :nth-child(2n)
  - n 代表任意正整数和 0
  - 是父元素中的第偶数个子元素（第 2、4、6、8......个）
  - 跟:nth-child(even)同义
- :nth-child(2n + 1)
  - n 代表任意正整数和 0
  - 是父元素中的第奇数个子元素（第 1、3、5、7......个）
  - 跟:nth-child(odd)同义
- nth-child(-n + 2)
  - 代表前 2 个子元素

### nth-last-child()

- :nth-last-child()的语法跟:nth-child()类似，不同点是:nth-last-child()从最后一个子元素开始往前计数
- :nth-last-child(1)，代表倒数第一个子元素
- :nth-last-child(-n + 2)，代表最后 2 个子元素

### nth-of-type( )、nth-last-of-type( )

- :nth-of-type()用法跟:nth-child()类似
  - 不同点是:nth-of-type()计数时只计算同种类型的元素
- :nth-last-of-type()用法跟:nth-of-type()类似
  - 不同点是:nth-last-of-type()从最后一个这种类型的子元素开始往前计数

### 否定伪类（negation pseudo-class）

- :not()的格式是:not(x)
  - x 是一个简单选择器
  - 元素选择器、通用选择器、属性选择器、类选择器、id 选择器、伪类（除否定伪类）
- :not(x)表示除 x 以外的元素

### 其他伪类

- 其他常见的伪类(了解):
  - :first-child，等同于:nth-child(1)
  - :last-child，等同于:nth-last-child(1)
  - :first-of-type，等同于:nth-of-type(1)
  - :last-of-type，等同于:nth-last-of-type(1)
  - :only-child，是父元素中唯一的子元素
  - :only-of-type，是父元素中唯一的这种类型的子元素
- 下面的伪类偶尔会使用:
  - :root，根元素，就是 HTML 元素
  - :empty 代表里面完全空白的元素
