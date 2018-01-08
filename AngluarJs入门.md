
# 下载安装

- 1：NPM（npm install angular）
- 2：下载angular.js包（https://github.com/angular/angular.js/releases）
- 3：使用CDN上的angular.js（http://apps.bdimg.com/libs/angular.js/1.4.6/angular.min.js）

# 入门引导

看下面的例子

```
<!doctype html>
<html lang="en" ng-app>
<head>
    <meta charset="utf-8">
    <title>My HTML File</title>
    <link rel="stylesheet" href="css/app.css">
    <link rel="stylesheet" href="css/bootstrap.css">
    <script src="lib/angular/angular.js"></script>
</head>
<body>
<p>Nothing here {{'yet' + '!'}}</p>
</body>
</html>
```
`ng-app`标记了AngularJS脚本的作用域，在`<html>`中添加`ng-app`属性即说明整个`<html>`都是AngularJS脚本作用域。开发者也可以在局部使用`ng-app`指令，如`<div ng-app>`，则AngularJS脚本仅在该`<div>`中运行。



# 基础语法

## 常量

AngularJs的数字,字符串,数组,对象和JS的一样

## 

## 常用指令

- na-app:
声明angularjs所管辖的区域，一般写在body或者HTML上原则一个一面只写一个

```
<body ng-app=""> </body>
```

- ng-model 
1.把元素值（比如输入域的值）绑定到应用程序。

```
<div ng-app="" ng-init="firstName='John'">
     <p>在输入框中尝试输入：</p>
     <p>姓名：<input type="text" ng-model="firstName"></p>
     <p>你输入的为： {{ firstName }}</p>
</div>
```

2.验证用户输入

```
<form ng-app="" name="myForm">
    Email:
    <input type="email" name="myAddress" ng-model="text">
    <span ng-show="myForm.myAddress.$error.email">不是一个合法的邮箱地址</span>
</form>
```
最后一个span的提示信息会在 ng-show 属性返回 true 的情况下显示。

3.提供应用数据的状态

```
<form ng-app="" name="myForm" ng-init="myText = 'test@runoob.com'">
    Email:
    <input type="email" name="myAddress" ng-model="myText" required></p>
    <h1>状态</h1>
    {{myForm.myAddress.$valid}}  #如果输入的值是合法的则为 true
    {{myForm.myAddress.$dirty}}  #如果值改变则为 true
    {{myForm.myAddress.$touched}}#如果通过触屏点击则为 true
</form>
```

4.基于它们的状态为 HTML 元素提供了 CSS 类：

```
<style>
input.ng-invalid {
    background-color: lightblue;
}
</style>
<body>

<form ng-app="" name="myForm">
    输入你的名字:
    <input name="myAddress" ng-model="text" required>
</form>
```
显示效果是如果编辑文本域，不同状态背景颜色会发送变化
文本域添加了 required 属性，该值是必须的，如果为空则是不合法的。

- ng-bind 
指令把应用程序数据绑定到 HTML 视图。

```
<div id="div" ng-bind="name"></div>   # 等效于下面的语句
<div>{{name}}</div>
```

- ng-init 
指令初始化 AngularJS 应用程序变量。

```
<div ng-app="" ng-init="firstName='John'">

<p>姓名为 <span ng-bind="firstName"></span></p>

</div>
```

- 表达式：{{}}绑定表达式，可以包含数字、运算符和变量。但表达式在网页加载瞬间会看到{{}},所以可以用ng-bind=”代替

```
{{5+""+5+',Angular'}}
```

- ng-repeat
指令对于集合中（数组中）的每个项会 克隆一次 HTML 元素。

```
<div ng-app="" ng-init="names=['Jani','Hege','Kai']">
  <p>使用 ng-repeat 来循环数组</p>
  <ul>
    <li ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>
```

## 作用域scope

Scope(作用域) 是应用在 HTML (视图) 和 JavaScript (控制器)之间的纽带。
Scope 是一个对象，有可用的方法和属性。
Scope 可应用在视图和控制器上。

```
<div ng-app="myApp" ng-controller="myCtrl">
    <input ng-model="name">
    <h1>{{greeting}}</h1>
    <button ng-click='sayHello()'>点我</button>    
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.name = "Runoob";
    $scope.sayHello = function() {
        $scope.greeting = 'Hello ' + $scope.name + '!';
    };
});
</script>
```

## 过滤器

过滤器可以使用一个管道字符（|）添加到表达式和指令中。

- currency:格式化数字为货币格式。
- filter:从数组项中选择一个子集。
- lowercase:格式化字符串为小写。
- orderBy:根据某个表达式排列数组。
- uppercase:格式化字符串为大写。

```
<div ng-app="myApp" ng-controller="namesCtrl">

<ul>
  <li ng-repeat="x in names | orderBy:'country'">
    {{ x.name + ', ' + x.country }}
  </li>
</ul>

</div>
```

filter可以用来设置过滤项

```
<div ng-app="myApp" ng-controller="namesCtrl">

<p><input type="text" ng-model="test"></p>

<ul>
  <li ng-repeat="x in names | filter:test | orderBy:'country'">
    {{ (x.name | uppercase) + ', ' + x.country }}
  </li>
</ul>

</div>
```

还可以自定义过滤器

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.msg = "Runoob";
});
app.filter('reverse', function() { //可以注入依赖
    return function(text) {
        return text.split("").reverse().join("");
    }
});
```

# 进阶用法

## 服务(Service)

在 AngularJS 中，服务是一个函数或对象，可在你的 AngularJS 应用中使用。
AngularJS 内建了30 多个服务。

### $location 
它可以返回当前页面的 URL 地址

```
<div ng-app="myApp" ng-controller="myCtrl">
<p> 当前页面的url:</p>
<h3>{{myUrl}}</h3>
</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $location) {
    $scope.myUrl = $location.absUrl();
});
</script>
```

### $http

POST 与 GET 简写方法格式：

```
$http.get('/someUrl', config).then(successCallback, errorCallback);
$http.post('/someUrl', data, config).then(successCallback, errorCallback);
```

v1.5 中$http 的 success 和 error 方法已废弃。使用 then 方法替代。

此外还有如下方法

```
$http.get
$http.head
$http.post
$http.put
$http.delete
$http.jsonp
$http.patch
```

### $timeout
服务对应了 JS window.setTimeout 函数

```
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $timeout) {
    $scope.myHeader = "Hello World!";
    $timeout(function () {
        $scope.myHeader = "How are you today?";
    }, 2000);
});
```
两秒之后显示"How are you today?"

### $interval 
使得一个函数每隔固定时间被调用一次

```
<div ng-app="myApp" ng-controller="myCtrl"> 

<p>现在时间是:</p>

<h1>{{theTime}}</h1>

</div>

<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope, $interval) {
  $scope.theTime = new Date().toLocaleTimeString();
  $interval(function () {
      $scope.theTime = new Date().toLocaleTimeString();
  }, 1000);
});
</script>
```

访问在指定的周期(以毫秒计)来调用函数或计算表达式

### 自定义服务

```
<div ng-app="myApp" ng-controller="myCtrl">

<p>255 的16进制是:</p>

<h1>{{hex}}</h1>

</div>

<script>
var app = angular.module('myApp', []);

app.service('hexafy', function() {
	this.myFunc = function (x) {
        return x.toString(16);
    }
});
app.controller('myCtrl', function($scope, hexafy) {
  $scope.hex = hexafy.myFunc(255);
});
</script>
```

要使用访问自定义服务，需要在定义控制器的时候独立添加，设置依赖关系:

## Select(选择框)

使用`ng-option`

```
<div ng-app="myApp" ng-controller="myCtrl">
 
<select ng-init="selectedName = names[0]" ng-model="selectedName" ng-options="x for x in names">
</select>
 
</div>
 
<script>
var app = angular.module('myApp', []);
app.controller('myCtrl', function($scope) {
    $scope.names = ["Google", "Runoob", "Taobao"];
});
</script>
```

也可以使用ng-repeat 指令来创建下拉列表：

```
<select>
<option ng-repeat="x in names">{{x}}</option>
</select>
```

## 表格

使用html的`<table>`配合`ng-repeat`

## 事件

### 点击事件
常见的点击事件`ng-click`

```
<div ng-app="" ng-controller="myCtrl">

<button ng-click="count = count + 1">点我！</button>

<p>{{ count }}</p>

</div>
```

### 隐藏
ng-hide 指令用于设置应用部分是否可见。
ng-hide="true" 设置 HTML 元素不可见。
ng-hide="false" 设置 HTML 元素可见。

### 显示元素
ng-show="false" 可以设置 HTML 元素 不可见。
ng-show="true" 可以以设置 HTML 元素可见。

## Bootstrap

AngularJS 的首选样式表是 Twitter Bootstrap， Twitter Bootstrap 是目前最受欢迎的前端框架。

你可以在你的 AngularJS 应用中加入 Twitter Bootstrap，你可以在你的 `<head>`元素中添加如下代码:
`<link rel="stylesheet" href="//maxcdn.bootstrapcdn.com/bootstrap/3.3.4/css/bootstrap.min.css">`
如果站点在国内，建议使用百度静态资源库的Bootstrap，代码如下：
`<link rel="stylesheet" href="//apps.bdimg.com/libs/bootstrap/3.3.4/css/bootstrap.min.css">`
