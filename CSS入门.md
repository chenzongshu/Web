
# 插入样式表

当读到一个样式表时，浏览器会根据它来格式化 HTML 文档。插入样式表的方法有三种

## 外部样式表

当样式需要应用于很多页面时，外部样式表将是理想的选择。在使用外部样式表的情况下，你可以通过改变一个文件来改变整个站点的外观。每个页面使用<link>标签链接到样式表。<link> 标签在（文档的）头部：

```
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css" />
</head>
```

浏览器会从文件 mystyle.css中读到样式声明，并根据它来格式文档。外部样式表可以在任何文本编辑器中进行编辑。文件不能包含任何的html标签。样式表应该以.css扩展名进行保存。下面是一个样式表文件的例子：

```
hr {color: sienna;}
p {margin-left: 20px;}
body {background-image: url("images/back40.gif");}
```

不要在属性值与单位之间留有空格。假如你使用 “margin-left: 20 px” 而不是 “margin-left: 20px” ，它仅在 IE 6 中有效，但是在 Mozilla/Firefox 或 Netscape 中却无法正常工作。

## 内部样式表

当单个文档需要特殊的样式时，就应该使用内部样式表。你可以使用<style>标签在文档头部定义内部样式表，就像这样:

```
<head>
<style type="text/css">
  hr {color: sienna;}
  p {margin-left: 20px;}
  body {background-image: url("images/back40.gif");}
</style>
</head>
```

内联样式

需要在相关的标签内使用样式（style）属性。Style 属性可以包含任何 CSS 属性。本例展示如何改变段落的颜色和左外边距：

```
<p style="color: sienna; margin-left: 20px">
This is a paragraph
</p>
```

## 多重样式

同时有内部和外部样式的时候,相同的项,内部覆盖外部





# 基础语法

CSS 对大小写不敏感。不过存在一个例外：如果涉及到与 HTML 文档一起工作的话，class 和 id 名称对大小写是敏感的。

语法
```
selector {declaration1; declaration2; ... declarationN }
```

其中,每个declaration为属性+值得组合

```
selector {property: value}
```

## id选择器

id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。,以 "#" 来定义

下面的两个 id 选择器，第一个可以定义元素的颜色为红色，第二个定义元素的颜色为绿色：

```
#red {color:red;}
#green {color:green;}
```

下面的 HTML 代码中，id 属性为 red 的 p 元素显示为红色，而 id 属性为 green 的 p 元素显示为绿色。

```
<p id="red">这个段落是红色。</p>
<p id="green">这个段落是绿色。</p>
```

注意：id 属性只能在每个 HTML 文档中出现一次。


## 类选择器

在 CSS 中，类选择器以一个点号显示：

```
.center {text-align: center}
```

在上面的例子中，所有拥有 center 类的 HTML 元素均为居中。
在下面的 HTML 代码中，h1 和 p 元素都有 center 类。这意味着两者都将遵守 ".center" 选择器中的规则。

```
<h1 class="center">
This heading will be center-aligned
</h1>

<p class="center">
This paragraph will also be center-aligned.
</p>
```

注意：类名的第一个字符不能使用数字！它无法在 Mozilla 或 Firefox 中起作用。

## 属性选择器

对带有指定属性的 HTML 元素设置样式

下面的例子为带有 title 属性的所有元素设置样式：

```
[title]
{
color:red;
}
```

还可以指定属性的值, `title="W3School"` 设置所有元素设置样式：


# CSS伪类

常用的有 `:hover` , `:active` , `active`

## hover

就是鼠标停在上面,改变显示样式时候,可以用

html
```
<tr class="backrecord" v-for="(item, index) in records" tabindex="1">
```

css

```
.backrecord:hover{
   background: #dcf2fe;
}
```

上面即可实现,在鼠标悬浮在表格某一行时,背景色改变的效果

顺便说一句,:hover的好搭档cursor属性，当属性值为pointer时，如下，光标覆盖目标时会变成手型。cursor还有url属性，其为设置图片地址。

```
cursor: pointer;
cursor: url("/image/mousemove.png")
```


## active/focus

`:active` : 元素被点击时变色，但颜色在点击后消失
`:focus`  : 元素被点击后变色，且颜色在点击后不消失

```
<div class="col-sm-12" id="">
    <button type="submit" class="btn btn-warning" id="one">Button1</button>
    <button type="submit" class="btn btn-warning" id="two">Button2</button>
</div>
```

```
button#one:active
{
    background:olive;
}
button#two:focus
{
    background:red;
}
```

** 由于div等元素无法接受键盘或其他用户事件，即不支持`:focus`伪类，可通过增加tabIndex属性使其支持`:focus` **

```
<div tabindex="1">
Section 1
</div>

<div tabindex="2">
Section 2
</div>

<div tabindex="3">
Section 3
</div>

div:focus {
    background-color:red;
}
```

## 扩展:

能够响应键盘事件的元素是有限的，它们是：form元素、a标签元素，window、document这样的元素；

但其它元素如果想响应键盘事件则必须具备两个基本要素：

1、 具有tabindex属性
2、 获取焦点；
