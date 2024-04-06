# Section2-“头”里有什么——HTML 元信息

## 1. 什么是 HTML 头部

HTML 头部包含 HTML `<head>` 元素的内容，与 `<body>` 元素内容不同，页面在浏览器加载后它的内容不会在浏览器中显示，它的作用是保存页面的一些元数据。

## 2. 添加标题

`<title>` 元素也被以其他的方式使用着。比如说，如果你尝试为某个页面添加书签（在 Firefox 浏览器中，点击书签 > 将当前标签页添加到书签，或点击地址栏末尾的星标），你会看到 `<title>` 的内容被作为建议的书签名。

> 注意区分 `<h1>` 用来标记页面内容的标题（故事名称、新闻摘要等等）。

## 3. 元数据：<meta> 元素

- 指定文档中的字符编码

```html
<meta charset="utf-8" />
```

`utf-8` 是一个通用的字符集，它包含了任何人类语言中的大部分的字符，意味着该 web 页面可以显示任意的语言；

- 添加作者和描述
  - `name` 指定了 meta 元素的类型
  - `content` 指定了实际元数据内容
  - 有利于获取信息和 SEO

```html
<meta name="author" content="Chris Mills" />
<meta
  name="description"
  content="The MDN Web Docs Learning Area aims to provide
complete beginners to the Web with all they need to know to get
started with developing web sites and applications."
```

- 其他类型的元数据
  - 向某些网站（如社交网站）提供可使用的特定信息。
  - 当网站的 URL 显示在 网站 上时，它具有特殊的效果。
  - Facebook 编写的元数据协议 Open Graph Data 为网站提供了更丰富的元数据。
  - Twitter 还拥有自己的类型的专有元数据协议（称为 Twitter Cards）

## 4. 在你的站点增加自定义图标

title 旁边的图标,也会保存在书签

```html
<link rel="icon" href="favicon.ico" type="image/x-icon" />
```

## 5. 在 HTML 中应用 CSS 和 JavaScript

`<link>` 元素经常位于文档的头部，它有 2 个属性，rel="stylesheet" 表明这是文档的样式表，而 href 包含了样式表文件的路径：

```html
<link rel="stylesheet" href="my-css-file.css" />
```

`<script>` 元素也应当放在文档的头部，并包含 src 属性来指向需要加载的 JavaScript 文件路径，同时最好加上 defer 以告诉浏览器在解析完成 HTML 后再加载 JavaScript

```html
<script src="my-js-file.js" defer></script>
```

## 6. 为文档设定主语言

HTML 文档会被搜索引擎更有效地索引（例如，允许它在特定于语言的结果中正确显示），对于那些使用屏幕阅读器的视障人士也很有用（例如，法语和英语中都有“six”这个单词，但是发音却完全不同）。

```html
<html lang="zh-CN">
  …
</html>
```

你还可以将文档的分段设置为不同的语言。例如，我们可以把日语部分设置为日语，如下所示：

```html
<p>Japanese example: <span lang="ja">ご飯が熱い。</span>.</p>
```
