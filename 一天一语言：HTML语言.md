
# 简介

超文本标记语言，是一种用于创建网页的标准标记语言。由浏览器解析。

HTML对大小写不敏感

举个列子:

```
<!DOCTYPE html>    #声明为 HTML5 文档
<html>             #元素是 HTML 页面的根元素
<head>             #元素包含了文档的元（meta）数据
<meta charset="utf-8">  # 使得中文字符不是乱码
<title>test</title>     #元素描述了文档的标题
</head>
<body>
    <h1>我的第一个标题</h1>       #元素定义一个大标题
    <p>我的第一个段落。</p>       #元素定义一个段落
</body>
</html>
```

# 基础语法

## 标题

通过`<h1> - <h6>` 标签来定义的

```
<h1>这是一个标题</h1>
<h2>这是一个标题</h2>
```

## 段落

通过标签 `<p>` 来定义的.

```
<p>这是一个段落。</p>
```

浏览器会自动地在段落的前后添加空行

## 链接

链接是通过标签 <a> 来定义的

```
<a href="http://www.runoob.com">这是一个链接</a>
```

其中,`href="http://www.runoob.com"`为其"属性"

## 图像

是通过标签 <img> 来定义的

```
<img src="/images/logo.png" width="258" height="39" />
```

# 注释

类似如下格式,浏览器会将其忽略

```
<!-- 这是一个注释 -->
```

# 换行

`<br>`符号,注意其不需要开始结束匹配,即不需要`</br>`

# 文本格式

| 标题 | 含义 |
|---|---|
|`<b>...</b>`|	定义粗体文本 |
|`<em>` |	定义着重文字 |
|`<i>` |	定义斜体字 |
|`<small>` |	定义小号字 |
|`<strong>` |	定义加重语气 |
|`<sub>` |	定义下标字|
|`<sup>` |	定义上标字|
|`<ins>` |	定义插入字 |
|`<del>` |	定义删除字 |

# 元素

由开始标签(`<x>`)到结束标签(`</x>`)包裹起来的代码

```
<html>

<body>
<p>This is my first paragraph.</p>
</body>

</html>
```

上面代码包含了三个元素

元素含有属性,属性总是以名称/值对的形式出现，比如：name="value"

```
<h1 align="center">This is heading 1</h1>
```

以上就是说把h1居中排列
