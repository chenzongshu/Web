

# 调用

## 1 直接调用

JavaScript代码可以直接嵌在网页的任何地方，不过通常我们都把JavaScript代码放到`<head>`中：

```
<html>
<head>
  <script>
    alert('Hello, world');
  </script>
</head>
<body>
  ...
</body>
</html>
```

由`<script>...</script>`包含的代码就是JavaScript代码，它将直接被浏览器执行。

## 2 通过js文件

把JavaScript代码放到一个单独的.js文件，然后在HTML中通过`<script src="..."></script>`引入这个文件：

```
<html>
<head>
  <script src="/static/js/abc.js"></script>
</head>
<body>
  ...
</body>
</html>
```

# 输出

JavaScript 可以通过不同的方式来输出数据：

- 使用 window.alert() 弹出警告框。
- 使用 document.write() 方法将内容写到 HTML 文档中。

   如果在文档已完成加载后执行 document.write，整个 HTML 页面将被覆盖。

- 使用 innerHTML 写入到 HTML 元素。
如需从 JavaScript 访问某个 HTML 元素，您可以使用 document.getElementById(id) 方法。
请使用 "id" 属性来标识 HTML 元素，并 innerHTML 来获取或插入元素内容：

```
<!DOCTYPE html>
<html>
<body>

<h1>我的第一个 Web 页面</h1>

<p id="demo">我的第一个段落</p>

<script>
document.getElementById("demo").innerHTML = "段落已修改。";
</script>

</body>
</html>
```

- 使用 console.log() 写入到浏览器的控制台。


# 基本语法

JavaScript的语法和Java语言类似，每个语句以;结束，语句块用{...},对大小写敏感

## 注释

// 或者 /*   */

## 数据类型

### 数字

不区分整形和浮点,都是Number

### 字符串

以单引号'或双引号"括起来

### 数组

和Java区别在于数组可以包含任意类型,也可以通过Array来创建tongguo

```
[1, 2, 3.14, 'Hello', null, true];   #合法

new Array(1, 2, 3); // 创建了数组[1, 2, 3]
```

### 对象

对象

JavaScript的对象是一组由键-值组成的无序集合，例如：

```
var person = {
    name: 'Bob',
    age: 20,
    tags: ['js', 'web', 'mobile'],
    city: 'Beijing',
    hasCar: true,
    zipcode: null
};
```

要获取一个对象的属性，我们用对象变量.属性名的方式：

```
person.name; // 'Bob'
person.zipcode; // null
```

如果属性名包含特殊字符，就必须用''括起来：

```
var xiaohong = {
    name: '小红',
    'middle-school': 'No.1 Middle School'
};
```

xiaohong的属性名middle-school不是一个有效的变量，就需要用`''`括起来。访问这个属性也无法使用`.`操作符，必须用['xxx']来访问：

```
xiaohong['middle-school']; // 'No.1 Middle School'
xiaohong['name']; // '小红'
xiaohong.name; // '小红'
```

### 条件判断和循环

和C/Java语言一样


### 变量

通过var声明

### 函数

```
function myFunction(var1,var2)
{
代码
return xx;
}
```

如果变量在函数内没有声明（没有使用 var 关键字），该变量为全局变量。

```
function myFunction() {
    carName = "Volvo";
    // 此处可调用 carName 变量,但是为全局变 量
}
```

### 函数参数

与其他语言不同，ECMAStript函数不介意传递进来的参数个数和类型吗，也就是说，即使你定义的函数只接受2个参数，但是你可以传1个，三个，甚至不传递。

是因为在函数体内所有参数都被丢到了一个数组arguments中，编译器不关心该数组中有多少数据。

可以在函数体内使用 arguments[0]、arguments[1] ······之类来访问参数数组

# 事件

在事件触发时 JavaScript 可以执行一些代码。
HTML 元素中可以添加事件属性，使用 JavaScript 代码来添加 HTML 元素。

```
<button onclick="this.innerHTML=Date()">现在的时间是?</button>
```

常见事件

|事件|描述|
|----|------|
|onchange   |HTML 元素改变|
|onclick   |用户点击 HTML 元素|
|onmouseover |用户在一个HTML元素上移动鼠标|
|onmouseout |用户从一个HTML元素上移开鼠标|
|onkeydown |用户按下键盘按键|
|onload	|浏览器已完成页面的加载|

更多事件见手册

# 全局变量

JavaScript通过函数管理作用域，在函数内部声明的变量只在这个函数内部，函数外面不可用。另一方面，全局变量就是在任何函数外面声明的或是未声明直接简单使用的，在浏览器中，window即指向了全局对象本身。

由于JS的特性：1、你可以甚至不需要声明就可以使用变量；2、JavaScript有隐含的全局概念，意味着你不声明的任何变量都会成为一个全局对象属性

非常容易生成全局变量，全局变量易冲突特别是和第三方插件，所以尽量少用全局变量。

# DOM

DOM： Browser Object Document，即浏览器对象模型，处理网页内容的方法和接口，其核心对象为window
