#CSS编码规范

## [1.格式](#format)
### 最终选择的代码风格必须保证: 易于阅读，易于清晰的注释

1. 在多个选择器的规则集中，每个单独的选择器独占一行。
2. 在规则集的左大括号前保留一个空格。
3. 在声明块中，每个声明独占一行。
4. 每个声明前保留一级缩进。
5. 每个声明的冒号后保留一个空格。
6. 对于声明块的最后一个声明，始终保留结束的分号。
7. 规则集的右大括号保持与该规则集的第一个字符在同一列。
8. 每个规则集之间保留一个空行。

```css
.selector-1,
.selector-2,
.selector-3[type="text"] {
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
    box-sizing: border-box;
    display: block;
    font-family: helvetica, arial, sans-serif;
    color: #333;
    background: #fff;
    background: linear-gradient(#fff, rgba(0, 0, 0, 0.8));
}

.selector-a,
.selector-b {
    padding: 10px;
}
```

### 声明顺序[非严格要求]
样式声明的顺序尽量遵守一个单一的原则。我的倾向是将相关的属性组合在一起，并且将对结构来说比较重要的属性(比如定位或者盒子模型)放在前面，先于排版、背景及颜色等属性。

参考规范代码：
```css
.selector {
    /* Positioning*/
    position: absolute;
    z-index: 10;
    top: 0;
    right: 0;
    bottom: 0;
    left: 0;
    
    /* Display & Box Model */
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    width: 100px;
    height: 100px;
    padding: 10px;
    border: 10px solid #333;
    margin: 10px;
    
    /* Other */
    background: #000;
    color: #fff;
    font-family: sans-serif;
    font-size: 16px;
    text-align: right;
}
```

### 例外及细微偏移原则的情况
对于大量仅包含单条声明的声明块，可以使用一种略微不同的单行格式。在这种情况下，在左大括号之后右大括号之前都应该保留一个空格。

```css
.selector-1 {width: 10%;}
.selector-2 {width: 20%;}
.selector-3 {width: 30%;}
```
对于以逗号分隔并且非常长的属性值 -- 例如一堆渐变或者阴影的声明  -- 可以放在多行中，这有助于提高可读性。

```css
.selector {
    box-shadow:
        1px 1px 1px #000,
        2px 2px 1px 1px #ccc inset;
    background-image:
        linear-gradient(#fff, #ccc),
        linear-gradient(#f3c, #4ec);
```

### 杂项
* 在十六进制值中，使用小写，如 `#aaa`。
* 单引号或双引号的选择保持一致。推荐使用双引号，如 `content:""`。
* 对于选择器中的属性值也加上引号，如`input[type="checkbox"]`。
* *如果可以的话*，不要给0加上单位，如`margin: 0`。

### 预处理：格式方面额外的考虑

不同的CSS预处理有着不同的特性、功能以及语法。编码习惯应当根据使用的预处理程序进行扩展，以适应其特有的功能。推荐在使用SCSS时遵守以下指导。

* 将嵌套深度限制在1级。对于超过2级的嵌套，给予重新评估。这可以避免出现过于详实的CSS选择器。
* 避免大量的嵌套规则。当可读性受到影响时，将之打断。推荐避免出现多于20行的嵌套规则出现。
* 始终将`@extend`语句放在声明块的第一行。
* 如果可以的话，将`@include`语句放在声明块的顶部，紧接着`@extend`语句的位置。
* 考虑在自定义函数的名字前加上`x-`或其它形式的前缀。这有助于避免将自己的函数和CSS的原生函数混淆，或函数命名与库函数冲突。

```scss
.selector-1 {
    @extend .other-rule;
    @include clearfix();
    @include box-sizing(border-box);
    width: x-grid-unit(1);
    // other declarations
}
```

## [2.命名](#naming)
- 全小写 中划线-连接
- 不要使用下划线和驼峰命名CSS
- 因此命名的时候尽量采用清晰的、有意义的名字
- 对于html文件和css文件中的代码，尽量采用一致的命名规则

```css
/* 没有意义的命名  */
.s-scr {
    overflow: auto;
}
.cb {
    background: #000;
}

/* 比较有意义的命名方式 */
.is-scrollable {
    overflow: auto;
}
.column-body {
    background: #000;
}
```


## [3.实例](#example)
下面是含有上述约定的示例代码：

```css
/* ==========================================================================
   Grid layout
   ========================================================================== */

/**
 * Column layout with horizontal scroll.
 *
 * This creates a single row of full-height, non-wrapping columns that can
 * be browsed horizontally within their parent.
 *
 * Example HTML:
 *
 * <div class="grid">
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 *     <div class="cell cell-3"></div>
 * </div>
 */

/**
 * Grid container
 *
 * Must only contain `.cell` children.
 *
 * 1. Remove inter-cell whitespace
 * 2. Prevent inline-block cells wrapping
 */

.grid {
    height: 100%;
    font-size: 0; /* 1 */
    white-space: nowrap; /* 2 */
}

/**
 * Grid cells
 *
 * No explicit width by default. Extend with `.cell-n` classes.
 *
 * 1. Set the inter-cell spacing
 * 2. Reset white-space inherited from `.grid`
 * 3. Reset font-size inherited from `.grid`
 */

.cell {
    position: relative;
    display: inline-block;
    overflow: hidden;
    box-sizing: border-box;
    height: 100%;
    padding: 0 10px; /* 1 */
    border: 2px solid #333;
    vertical-align: top;
    white-space: normal; /* 2 */
    font-size: 16px; /* 3 */
}

/* Cell states */

.cell.is-animating {
    background-color: #fffdec;
}

/* Cell dimensions
   ========================================================================== */

.cell-1 { width: 10%; }
.cell-2 { width: 20%; }
.cell-3 { width: 30%; }
.cell-4 { width: 40%; }
.cell-5 { width: 50%; }

/* Cell modifiers
   ========================================================================== */

.cell--detail,
.cell--important {
    border-width: 4px;
}
```

## [4.代码组织](#organization)

对于css代码库来说，如何组织代码文件是很重要的，尤其对于那些很大的代码库显得更加重要。这里介绍
几个组织代码的建议：

* 逻辑上对不同的代码进行分离。
* 不同的组件(component)的css尽量用不同的css文件（可以在build阶段用工具合并到一起）
* 如果用到了预处理器（比如less），把一些公共的样式代码抽象成变量，例如颜色，字体等等

## [5.构建及部署](#build-and-deployment)
任何一个项目，都应该有一个build的过程，在这个阶段我们可以通过工具对代码进行检测，测试，压缩等等

## [6.最佳实践](#practice)

### css选择器
不同的标签类型尽可能不用相同的css类名；尽可能不用标签类型选择器，用css类名和ID足够定义css，因为ID是可以唯一确定Dom元素的，而css类是不推荐用于不同的标签的；另外应该少用ID选择器定义，因为ID的唯一性使得定义的css无法重用。
```css
/*bad*/
ul#menus{
}
div.info{
}
/*good*/
.main-menus{
}
.info{
}
```


### 属性名称和值的定义精简
css的某些属性定义可以可以分拆为各个独立项，比如padding，border, margin, background, font等，虽然分拆定义的可读性会好一些，但是就目前的经验来看，前端工程师们对这些常用的css理解程度足够好，合并后的定义不会对可读性带来影响，反而代码更简洁；此外对属性值为0的单位可以省略，在0后面添加入px em cm等单位是毫无意义的；对小数值可以省略小数点前的0；url值两端的引号可以省略。

```css
    /*bad*/
    border-top-style: none;
    font-family: palatino, georgia, serif;
    font-size: 100%;
    line-height: 1.6;
    padding-bottom: 2em;
    padding-left: 1em;
    padding-right: 1em;
    padding-top: 0;
    margin: 0.8em;
    background: #00FF00 url('bgimage.gif') no-repeat fixed top;
    /*good*/
    border-top: 0;
    font: 100%/1.6 palatino, georgia, serif;
    padding: 0 1em 2em;
    margin: 0.8em;
    background: #00FF00 url(bgimage.gif) no-repeat fixed top;
```

### 重设(reset)
全局重设可以确保一个网站在所有浏览器保持统一的外观。完全不一样的浏览器会在一个网站上应用自己的默认设置，这可能导致一个网站在不同的浏览器有不同的界面表现.


```css
/*bad*/
*{
    margin: 0;
    padding: 0;
}
p{
  margin: 0;
  padding: 0;
}
/*good*/
body,div,dl,dt,dd,ul,ol,li,h1,h2,h3,h4,h5,h6,pre, 
form,fieldset,input,textarea,p,blockquote,th,td { 
    padding: 0; 
    margin: 0; 
} 
table { 
    border-collapse: collapse; 
    border-spacing: 0; 
} 
fieldset,img { 
    border: 0; 
} 
address,caption,cite,code,dfn,em,strong,th,var { 
    font-weight: normal; 
    font-style: normal; 
} 
ol,ul { 
    list-style: none; 
} 
caption,th { 
    text-align: left; 
} 
h1,h2,h3,h4,h5,h6 { 
    font-weight: normal; 
    font-size: 100%; 
} 
q:before,q:after { 
    content:”; 
} 
abbr,acronym { 
    border: 0; 
}
```

### 避免写兼容某个浏览器的css代码[仅作参考，非强制]
避免写特定浏览器兼容代码，这里说的特定浏览器主要指的是万恶的IE系列浏览器，IE6，7尤为严重。碰到浏览器兼容问题，首先考虑的是能否换一种其它的解决方案，如果没有合适的解决方案，记得单独写一个css文件给这些特定的浏览器，不要把兼容代码和常规代码混合，这样方便代码的维护，如果后期不支持这些老旧浏览器，可以直接删除这些单独的css文件即可。
```css
/*bad*/
.bb{
height:32px;
  background-color:#f1ee18;/*所有识别*/
  .background-color:#00deff9; /*IE6、7、8识别*/
  +background-color:#a200ff;/*IE6、7识别*/
  _background-color:#1e0bd1;/*IE6识别*/
}
```
```html
<!--good-->
<!--[if IE 6]>
<link rel="stylesheet" type="text/css" href="css/ie6.css" />
<![endif]-->
<!--[if IE 7]>
<link rel="stylesheet" type="text/css" href="css/ie7.css" />
<![endif]-->
```

### 块元素和行内元素的区别，避免写无用的css代码
块级元素显示会独占一行，而行内元素不会独占一行。常见的块级元素有：div p ul ol table h1~h6 等；行内元素有：a em label span strong 等。块级元素的display默认样式是block，而行内元素是inline，可以通过重新定义display来互转块级元素和行内元素。但是记住以下的css样式对行内元素是无效的：width height 和垂直方向设置的margin padding，所以避免给行内元素定义这些无用的样式。
```css
/*bad*/
span{
  height: 100px;
  margin-top: 20px;
  margin-bottom: 10px;
  padding:15px 0;
  width:200px;
}
/*good*/
div{
  height: 100px;
  margin-top: 20px;
  margin-bottom: 10px;
  padding:15px 0;
  width:200px;
}
```

### CSS定义的权重
css的选择器是有权重的，当有多个样式时，权重高的样式会起作用。如果权重相同，则最后定义的样式会起作用，但是应该避免这种情况出现，因为光是靠前后的样式定义来影响最终的样式是不靠谱的，也会给后期的维护埋下一个雷区；另外为了代码的重用性，应尽可能定义小的权重，这和不推荐使用id来定义样式是一样的道理。
```css
/*权重为1*/
div{
}
/*权重为10*/
.class1{
}
/*权重为100*/
#id1{
}
/*权重为100+1=101*/
#id1 div{
}
/*权重为10+1=11*/
.class1 div{
}
/*权重为10+10+1=21*/
.class1 .class2 div{
}
```
```html
<div id="id" class="class_1 class_2"></div>
<!--bad-->
<style>
  #id{
    font-size: 12px;
  }
  .class_1{
    font-size: 14px;
  }
  .class_1 .class_2{
    font-size: 16px;
  }
</style>
<!--good-->
<style>
  .class_1{
    font-size: 14px;
  }
</style>
```


### 多组合少继承
把css定义中的固定部分和可变部分分开定义，使得代码达到最大程度的重用，这样的结果是增加了元素上添加的css类个数，但是提高了代码的维护性和可读性。
```css
.btn {
  display: inline-block;
  *display: inline;
  padding: 4px 10px 4px;
  margin-bottom: 0;
  *margin-left: .3em;
  font-size: 13px;
  line-height: 18px;
  *line-height: 20px;
  color: #333333;
  ...
  *zoom: 1;
  -webkit-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
     -moz-box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
          box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
}
/*在此基础上定义各种按钮的特定样式*/

.btn.disabled,
.btn[disabled] {
  cursor: default;
  background-color: #e6e6e6;
  background-image: none;
  opacity: 0.65;
  filter: alpha(opacity=65);
  -webkit-box-shadow: none;
     -moz-box-shadow: none;
          box-shadow: none;
}

.btn-large {
  padding: 9px 14px;
  font-size: 15px;
  line-height: normal;
  -webkit-border-radius: 5px;
     -moz-border-radius: 5px;
          border-radius: 5px;
}

.btn-small {
  padding: 5px 9px;
  font-size: 11px;
  line-height: 16px;
}
.btn-mini {
  padding: 2px 6px;
  font-size: 11px;
  line-height: 14px;
}
```

## [5.参考文档](#reference)
- [dyygtfx/FeCodeGuide](https://github.com/dyygtfx/FeCodeGuide)
- [tsq/front-end-principles](https://github.com/tsq/front-end-principles/)
- [imweb/code-guide](https://github.com/imweb/code-guide/blob/master/md/css.md)