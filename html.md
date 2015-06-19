#HTML编码规范

## [1.书写规范](#guide)

* 只使用小写，包括标签名、属性名、属性值(一些可以自定义的字符串属性值除外)

```html
<!-- 不推荐 -->
<A HREF="/">Home</A>

<!-- 推荐 -->
<img src="google.png" alt="Google">
```

* 为每个块级元素或表格元素标签新起一行，并且对每个子元素进行缩进

* 确保你的IDE使用的是UTF-8编码来保存文件的，在定义页面的编码时使用 `<meta charset="utf-8">`就好了。在样式表文件里不用去声明UTF-8编码什么的。

* 文档类型: `<! DOCTYPE html>`

* 使用规范化的html

* 使用语义化的html标签，根据用途来选择标签

* 把多媒体元素可知化。像图片、视频、动画等多媒体元素，要有相关的文字来体现其内容，比如<img>可以使用`alt`属性来说明其图片内容

```html
<!-- 不推荐 -->
<img src="sheet.png">

<!-- 推荐 -->
<img src="sheet.png" alt="screenshot".>

```

* 确保页面的结构、样式、行为三者相分离。确保文档或模板中只包含`html`, 把用到的样式都写到样式表文件中，把脚本文件都写到`js`文件中。这在多人协作时非常重要

```html
<!DOCTYPE html>
<html>
<head lang="en">
    <meta charset="UTF-8">
    <title></title>
    <link rel="stylesheet" href="http://fonts.googleapis.com/css?family=Open+Sans:300,400,700"/>
</head>
<body>
    <span href="#" class="button" id="toggle-login">Log in</span>
</div>
    <script src="http://code.jquery.com/jquery-2.1.3.js"></script>
</body>
</html>
```

## [2.最佳实践](#practice)

### 保持标签闭合

```html
<!-- bad -->
<li>Some text here
<li>Some new text

<!-- good -->
<ul>
    <li>Some text here</li>
</ul>

### 尽量不要使用内联样式

```html
<!-- bad -->
<p style="color:#ccc">An example to illustrate inline style in html</p>

<!-- good -->
<p class="html_bp">An example to illustrate inline style in html</p>

### 使用连续的标题

```html
<!-- bad -->
<h1>This is the topmost heading</h1>
<h3>This is a sub_heading underneath the topmost heading</h3>

<!-- good -->
<h1>This is the topmost heading</h1>
<h2>This is a sub_heading underneath the topmost heading</h2>
```

### 在合适的地方使用合适的标签
HTML标签是构造规范内容结构的关键。例如 `<em>` 标签用来强调重点内容。 `<p>`标签适用于突出文章段落。如果想要在段落间加空行,就不要使用`<br/>`

```html
<!-- bad -->
<p>段落1<br/>
段落2</p>

<!-- good -->
<p>段落1</p>
<p>段落2</p>
```

### 为图片标签添加alt属性

```html
<!-- bad -->
<img id="logo" src="images/bgr_logo.png"/>

<!-- good -->
<img id="logo" src="images/bgr_logo.png" alt="Tom - Web Development"/>
```

### 添加适当的title属性
```html
<!-- bad -->
<a href="javascript:;">go away</a>

<!-- good -->
<a href="javascript:;" title="go away">go away</a>
```


### 不要滥用`<br/>`

```html
<!-- bad -->
<span>abcde</span>
<br/>
<em>def</em>

<!-- good -->
<p>
Here's an interesting fact about corn
</p>
```

## [3.参考文档](#reference)
- [dyygtfx/FeCodeGuide](https://github.com/dyygtfx/FeCodeGuide)
- [tsq/front-end-principles](https://github.com/tsq/front-end-principles/)