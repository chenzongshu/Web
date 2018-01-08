
# 入门简介

Vue是一个小巧轻便的JavaScript库。它有一个简单易懂的API，能够让开发者在开发web应用的时候更加简易便捷。实际上，一直让Vue引以为豪的是它的便捷性、执行力、灵活性。

http://www.cnblogs.com/keepfool/p/5619070.html 

## 创建实例

我们可以先初始化一个html页面，然后我们需要引入Vue 的js文件。
引入的方式有很多

- 可以在script中引入Vue的cdn
- 去官网上下载Vue的min.js，
- 用 npm 安装一个Vue的依赖

```
<!DOCTYPE html>
      <html>
            <head>
                  <title>从零开始学Vue</title>
            </head>
      <body>
            <!-- 从cdn导入 -->
            <script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>
      </body>
</html>
```
> 当你在开发过程中，确保你使用的是没有压缩过的版本，因为没有压缩的版本会提供有用的详细的警告，将会给你的代码书写节省很多时间。

我们先在body里面写入一个div，并且创建一个Vue实例，然后将实例和div绑定起来。 当你创建一个新的Vue实例的时候要使用Vue()构造器，然后在你的实例中指出你的挂载点。这个挂载点就是你想要划分出来的Vue实例的边界。挂载点和实例边界是一一对应的，你只能在挂载点上处理你实例边界内的事务，而不能在你的挂载点上处理实例边界外的事务。 在Vue实例中设置挂载点的参数是 “ el ”，el 的值可以用dom元素定义。

```
<!DOCTYPE html>
      <html>
            <head>
                  <title>从零开始学Vue</title>
            </head>
      <body>
            <div id="vueInstance">这中间就是实例挂载点的实例边界</div>

            <script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>

            <script>
                  // 创建一个新的Vue实例，并设置挂载点
                  var V = new Vue({
                        el : '#vueInstance'
                  });
            </script>
      </body>
</html>
```

就像你在上面看到的那样，new一个Vue()就能创建一个新的实例，然后指定一个DOM元素作为实例的挂载点。定义挂载点的时候，我们用到了css选择器的id来定义。实例化的名字也可以自己来定义，以便之后调用。

## 所谓MVC

```
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title></title>
    </head>

    <body>
        <!--这是我们的View-->
        <div id="app">
            {{ message }}
        </div>
    </body>
    <script src="js/vue.js"></script>
    <script>
        // 这是我们的Model
        var exampleData = {
            message: 'Hello World!'
        }

        // 创建一个 Vue 实例或 "ViewModel"
        // 它连接 View 与 Model
        new Vue({
            el: '#app',
            data: exampleData
        })
    </script>
</html>
```
在创建Vue实例时，需要传入一个选项对象，选项对象可以包含数据、挂载元素、方法、模生命周期钩子等等。

在这个示例中，选项对象的el属性指向View，`el: '#app'`表示该Vue实例将挂载到`<div id="app">...</div>`这个元素；data属性指向Model，`data:exampleData`表示我们的Model是exampleData对象。
Vue.js有多种数据绑定的语法，最基础的形式是文本插值，使用一对大括号语法，在运行时{{ message }}会被数据对象的message属性替换，所以页面上会输出"Hello World!"。

## 利用v-model进行双向数据绑定

我们可以用v-model对input输入框进行绑定，从而我们可以使用动态的获取数据对象的值。你可以认为v-model是一个指定的属性，就像html元素的属性。这里的双向数据绑定可以用在很多表单元素上，比如input、textarea、select。 Vue利用v-model这个指令绑定了一个数据，而这个数据是我们希望能够通过用户输入操作而更新的数据。 比如我们下面这个例子，我们要在input标签上绑定数据name，我们需要在Vue实例中的data对象中实现声明。

```
<div id="vueInstance">
      输入您的姓名: <input type="text" v-model="name">
      <p>{{ $data | json }}</p> 
      <p>{{ name }}</p>     
</div>

<script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>//之后这行会省略
<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                  name : '_Appian'
            }
      });
</script>
```

无论用户输入多少次，这个name都会被自动更新。并且，如果name的值被改变了，其他有映射name的地方的值也会被修改。这种input框和映射的同步修改的原因，就是利用v-model这个指令，让数据通过底层的数据流进行绑定后直接修改。这就是数据的双向绑定的概念。

> \$data是Vue实例观察的数据对象，本质类型是一个对象，所以可以转成json。可以用一个新的对象替换。实例代理了它的数据对象的属性。{{}}，利用两个花括号进行插值。这里插入的值是$data实时变化的值。|json，只是一个更直观的能让数据展示出来的方法。也可以看做是一个过滤器，就像JSON.stringify()的效果一样。

> {{ name }}，就是直接在插值表达式，两个花括号中间插入数据变量，直接映射name的值。

## 利用v-on进行事件绑定

Vue是利用v-on指令进行事件监听和事件分发的。你可以在Vue的实例中创建一个方法来绑定监听事件，可以创建一个方法来分派一个点击事件。

下面的例子中，我们将创建一个say方法，这个方法绑定在一个button上。点击产生的效果就是弹出一个带有用户name的欢迎框。为了将这个方法指派给button，我们需要用v-on:click来进行事件绑定。

```
<div id="vueInstance">
      输入您的姓名: <input type="text" v-model="name">
      <button v-on:click="say">欢迎点击</button> // #1
      <button @click="say">欢迎点击</button>     // #2
</div>

<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                  name : '_Appian'
            },
            methods : {
                  say : function(){
                       alert('欢迎' + this.name);
                 }
            }
      });
</script>
```

当然了，不仅是可以绑定click点击事件，还可以绑定其他鼠标事件，键盘输入事件等一些js的事件类型。比如v-on:mouseover，v-on:keydown，v-on:submit，v-on:keypress，v-on:keyup.13等等，或者是一些其他的自定义事件。

> 在开发过程中，你可能会频繁的用到事件绑定，v-on写起来有点麻烦，所以上例中提供了两种写法，#2就是对#1写法的缩写。利用@代替v-on，这里不多说。

## 利用v-if或者v-show进行条件判定

如果我们希望用户在登录之后才能看到欢迎弹窗，而如果没有登录则给它一个登录界面。Vue会提供给我们v-if指令和v-show指令用来控制不同登录状态下的显示内容。

利用先前的例子，我们可以用loginStatus的值来控制是否登录，如果是true则显示输入框和按钮让他能够看到欢迎弹窗，但如果是false（即未登录），则只能看到输入账号、密码的输入框和提交按钮（暂时不进行身份验证，只改变登录状态）。

```
<div id="vueInstance">
      //loginStatus为true时会显示的section
     <section v-if="loginStatus">
         输入您的姓名: <input type="text" v-model="name">
         <button v-on:click="say">欢迎点击</button>
         <button @click="switchLoginStatus">退出登录</button>
     </section>

      //loginStatus为false时会显示的section
     <section v-if="!loginStatus">
           登录用户: <input type="text">
           登录密码: <input type="password">
           <button @click="switchLoginStatus">登录</button>
     </section>
</div>

<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                  name : '_Appian',
                  loginStatus :　false
            },
            methods : {
                  say : function(){
                       alert('欢迎' + this.name);
                  },
                   switchLoginStatus : function(){
                       this.loginStatus = !this.loginStatus;
                   }
            }
      });
</script>
```

> this的执行就是实例V。this的指向是一个需要自己去搞懂的问题，这里不多说。 在上述例子中，只要把V-if换成v-show，一样可以获得等同的效果。同时v-if和v-show他们都支持v-else，但是绑定v-else命令的标签的前一兄弟元素必须有 v-if 或 v-show。

在上面的例子中，只要点击“登录”或者“退出登录”按钮都会触发switchLoginStatus方法，只要触发了这个方法就会导致loginStatus的状态变化（在true和false中进行切换），从而改变了html中的v-if的判断条件结果的变化，基于当前的loginStatus的布尔值的状态，使得显示的section是不同状态下的section。

> v-show和v-if之间有什么区别呢? 在切换 v-if 块时，Vue有一个局部编译/卸载过程，因为 v-if 之中的模板也可能包括数据绑定或子组件。v-if 是真实的条件渲染，因为它会确保条件块在切换当中合适地销毁与重建条件块内的事件监听器和子组件。 v-if 也是惰性的：如果在初始渲染时条件为假，则什么也不做——在条件第一次变为真时才开始局部编译（编译会被缓存起来）。 相比之下，v-show 简单得多——元素始终被编译并保留，只是简单地基于 CSS 切换。 一般来说，v-if 有更高的切换消耗而 v-show 有更高的初始渲染消耗。因此，如果需要频繁切换 v-show 较好，如果在运行时条件不大可能改变 v-if 较好。

## 利用v-for输出列表

如果你是经营一个电商平台的商人的话，你一定有很多页面都需要渲染商品列表的输出。v-for指令允许循环我们的数组对象，用 “element in arrayObj”的方式，念作“循环arrayObj这个数据对象里的每一个element”。

下面的例子中，我们将会利用v-for指令循环输出一个商品列表。每一个商品都会在一个li中，li中输出商品的名称、价格和商品类型。

```
<div id="vueInstance">
     <ul>
         <li v-for="el in products">
            {{ el.name }} - ￥ {{ el. price }} - {{ el. category }}
         </li>
     </ul>
</div>

<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                   products : [
                         {name: 'microphone', price: 25, category: 'electronics'},
                         {name: 'laptop case', price: 15, category: 'accessories'},
                         {name: 'screen cleaner', price: 17, category: 'accessories'},
                         {name: 'laptop charger', price: 70, category: 'electronics'},
                         {name: 'mouse', price: 40, category: 'electronics'},
                         {name: 'earphones', price: 20, category: 'electronics'},
                         {name: 'monitor', price: 120, category: 'electronics'}
                   ]
            }
      });
</script>
```

> 当然了，data中的数组对象，可以不用像上面这样定义也可以，我们可以从数据库导入，或者是利用ajax请求得到。这里只是为了演示v-for。

有时候我们可能会需要拿到商品在数组对象里的对应下标。我们可以用$index来获得。

```
//#1
<li v-for="el in products">
    {{ $index }} - {{ el.name }} - ￥ {{ el. price }} - {{ el. category }}
</li>

//#2
<li v-for="(index,el) in products">
   {{ index }} - {{ el.name }} - ￥ {{ el. price }} - {{ el. category }}
</li>
```

## 计算属性Computed

计算属性的应用场景，一般是在有一个变量的值需要其他变量计算得到的时候，会用到。

比如，例如用户在输入框输入一个数 x，则自动返回给用户这个数的平方 x²。你需要对输入框进行数据绑定，然后当数据修改的时候，就马上计算它的平方。

```
<div id="vueInstance">
         输入一个数字: <input type="text" v-model="value">
         <p>计算结果：{{ square }}</p>
</div>

<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                  value : 1
            },
            computed : {
                  square : function(){
                       return this.value * this.value;
                  }
            }
      });
</script>
```

> 计算属性定义数值是通过定义一系列的function，就像我们先前定义methods对象的时候是一样的。比如square方法是用来计算变量“square”的，其方法的返回值是两个this.value的乘积。

接下来可以用computed做一个复杂一点例子。系统会随机取一个110以内的数字，用户可以在输入框随机输入一个110之内的数字，如果刚好用户的输入和系统的随机数刚好匹配，则游戏成功，反之失败。

```
<div id="vueInstance">
         输入1~10内的数字: <input type="text" v-model="value">
         <p>计算结果：{{ resultMsg }}</p>
</div>

<script>
      var V = new Vue({
            el : '#vueInstance',
            data : {
                  value : null,
                  randNum : 5//第一次随机数为5
            },
            methods : {
                  getRandNum: function(min, max){
                      return Math.floor(Math.random() * (max - min + 1)) + min;
                  }
            },
            computed : {
                  resultMsg : function(){
                       if (this.value == this.randNum) {
                            this.randNum = this.getRandNum(1, 10);
                            return '你猜对了!';
                       } else {
                            this.randNum = this.getRandNum(1, 10);
                            return '猜错了，再来!';
                       }
                  }
            }
      });
</script>
```

# 过滤器

过滤器是一个通过输入数据，能够及时对数据进行处理并返回一个数据结果的简单函数。Vue有很多很便利的过滤器，可以参考官方文档，http://cn.vuejs.org/api/#过滤器，过滤器通常会使用管道标志 “ | ”， 比如：

```
 {{ msg | uppercase  }}     // 'abc' => 'ABC'
```

> uppercase过滤器 : 将输入的字符串转换成大写字母的过滤器。

## 链式过滤

VueJs允许你链式调用过滤器，简单的来说，就是一个过滤器的输出成为下一个过滤器的输入，然后再次过滤。接下来，我们可以想象一个比较简答的例子，使用了Vue的 filterBy + orderBy 过滤器来过滤所有商品products。过滤出来的产品是属于电器类商品，并且按电器字母排序。

> filterBy过滤器 : 过滤器的值必须是一个数组，filterBy + 过滤条件。 过滤条件是：‘string || function’ + in ‘optionKeyName’

> orderBy过滤器 : 过滤器的值必须是一个数组，orderBy + 过滤条件。 过滤条件是：‘string || array ||function’ + ‘order ≥ 0 为升序 || order < 0 为降序’

接下来，我们可以看下第二个例子：我们有一个商品数组products，我们希望遍历这个数组，并把他们打印成一张清单，这个用v-for很容易实现。

```
<li v-for="product in products">
      {{ product.name | capitalize }} - {{ product.price | currency }}
</li>
```

> capitalize过滤器 : 将输入的字符串首字母转换成大写字母的过滤器。 currency过滤器 : 将输入的数字转换成现金的过滤器。可以跟上货币符号（默认$）和保留的小数位（默认2）。

利用上面的两个过滤器，能够很好的把一个json数组的商品清单格式化成通熟易懂的商品价格清单。

如果只想要电器类商品，可以在v-for上加过滤条件：

```
<li v-for="product in products | filterBy 'electronics' in 'category' 'name' ">
      {{ product.name | capitalize }} - {{ product.price | currency }}
</li>
```

上面的例子，就是用filterBy 过滤在 'category' 和 'name' 中含有'electronics' 关键字的列表。

最后我们还需要将这个列表用字母进行排序。我们可以在 filterBy 过滤器的基础上，链式调用orderBy 过滤器。

```
<ul>
       <li v-for="product in products
                   | filterBy 'electronics' in 'category'
                   | orderBy  'name' "
       >
            {{ product.name | capitalize }} - {{ product.price | currency }}
      </li>
</ul>
```

orderBy 的排序方式默认是升序，如果想要降序，只需要加一个小于0的参数：`orderBy  'name'  -1`

## 自定义过滤器

定义一个全局的自定义过滤器，需要使用Vue.filter()构造器。这个构造器需要两个参数。

> Vue.filter() Constructor Parameters: 1.filterId: 过滤器ID，用来做为你的过滤器的唯一标识； 2.filter function: 过滤器函数，用一个function来接收一个参数，之后再将接收到的参数格式化为想要的数据结果。

回到之前的例子： 现在设想我们有一个网上商城，并给我们的所有商品打五折。

为了完成这个例子，我们需要完成的是

- 使用Vue.filter()构造器创建一个过滤器叫做discount
- 输入商品的原价，能够返回其打五折之后的折扣价

```
  Vue.filter( 'discount' , function(value) {
        return value  * .5 ;
  });
  
  <ul>
      <li v-for="product in products">
           {{ product.name | capitalize }} - {{ product.price | discount | currency }}
      </li>
</ul>
```

那如果我们想要的是任意折扣呢？我们应该在discount过滤器里增加一个折扣数值参数，改造一下我们的过滤器。

```
  Vue.filter( 'discount' , function(value,discount) {
        return value  * ( discount / 100 ) ;
  });
```

```
<ul>
      <li v-for="product in products">
           {{ product.name | capitalize }} - {{ product.price | discount 25 | currency }}
      </li>
</ul>
```

我们也可以在我们Vue实例里构造我们的过滤器，这样构造的好处是，这样就不会影响到其他不需要用到这个过滤器的Vue实例。

```
  new Vue({
        el : 'body',
        data : {
              products : [
                    {name: 'microphone', price: 25, category: 'electronics'},
                    {name: 'laptop case', price: 15, category: 'accessories'},
                    {name: 'screen cleaner', price: 17, category: 'accessories'}
              ]
        },
        filters: {
              discount : function(value, discount){
                    return value * ( discount / 100 );
              }
        }
  });
```

定义在全局就能在所有的实例中调用过滤器，如果定义在了实例里就在实例里调用过滤器。


# 组件

## 简单用法

利用组件能够很好的把一个你正在构建的具有复杂接口的应用拆分开来，同时，组件也具有很高的复用性，即使是在你正在开发的是不同的项目也能封装复用。

先创建一个简单的html页面，并将Vue实例化后挂载在我们的DOM元素上。

```
<!DOCTYPE html>
      <html>
            <head>
                  <title>揭开Vue组件的神秘面纱</title>
            </head>
      <body>
            //这中间就是实例挂载点的实例边界
            <div id="vueInstance"></div>

            //Vue的CDN，之后会省略不写
            <script src="http://cdn.jsdelivr.net/vue/1.0.16/vue.js"></script>

            <script>
                  // 创建一个新的Vue实例，并设置挂载点
                  var V = new Vue({
                        el : '#vueInstance'
                  });
            </script>
      </body>
</html>
```

然后我们将创建我们的第一个简单的，可复用的组件。在Vue中你，可以使用Vue.component()来创建和注册你的组件，这个构造器有两个参数：

> - 组件的名字
- 包含组件参数的对象

这个对象有点像Vue()构造器里的对象，它也有类似于Vue()里的el属性和data属性，但是又有点不一样。

Vue()构造器的el和data可以是对象。 Vue.component()构造器的el和data只能是函数。

现在来看看第一个组件是如何运作的。我想要注册一个组件，用p标签输出一行我的自我介绍。所以我创建了一个组件，并填入两个参数：

> - 组件的名字:'mine'
- 包含组件参数的对象:这个对象包含一个属性'template'

```
Vue.component('mine',{
    template : '<p>My name is Appian.</p>'
})
```

现在你已经有了自己的一个组件了，你可以在你的应用的任何地方使用它。只要你调用它的唯一标识(就是组件名字)，并用普通html标签的格式来书写，比如，组件上注册的内容就会在你的自定义标签的地方插入。

```
 <div id="vueInstance">
    <mine></mine>   //标识注册的内容会在这里插入
    <mine></mine>
    <mine></mine>   //重复插入注册内容
 </div>

 <script>
       Vue.component('mine',{   //这里就是注册的内容
           template : '<p>My name is Appian.</p>'
       });

       var V = new Vue({
             el : '#vueInstance'
       });
 </script>
```

Vue使用模板Template来代替组件，并使自定义的唯一标识用html标签插入到DOM结构中去，使得html更加简洁、整齐和直观。

## 利用template标签处理复杂组件

现在你可能会想，我写的组件怎么可能只有一行p标签？一行p标签还有必要组件这么麻烦吗？是的，组件是为了更复杂的封装复用而生的。所以，如果你只会Vue.component()构造器中的template属性定义html代码，利用字符串拼接拼出所有的代码，这样只会让你比用jq更加疲惫不堪。

为了避免上面的这种情况，所以我们可以用template标签（注意属性和标签是不一样的）来达到我们的目的。我们可以在页面的任何地方，定义template标签，并在template标签内，写好我们的模板。因为template标签在页面加载的时候不会渲染出来，只有在我们需要它的时候，这个标签内的内容才会被渲染出来。所以，你可以把template标签放在任何地方，并给它一个id，以便在组件注册的时候能够找到模板。

```
 <div id="vueInstance">
    <mine></mine>   //标识注册的内容会在这里插入
 </div>

 <template id="mineTpl">
         <p>My name is Appian.</p>
         <button>点击没有任何事件</button>
 </template>

 <script>
       Vue.component('mine',{   //这里就是注册的内容
           template : '#mineTpl'
       });

       var V = new Vue({
             el : '#vueInstance'
       });
 </script>
```

我们现在已经可以利用这样的方法创建一个复杂的组件了。这样我们可能将复杂的代码进行功能分区之后组件化，用组件的思想避免代码一坨一坨的。组件化能够帮你更清晰的组织好你的模块，使你的组件更加vue化。

## 通过props向组件中传递数据

每次创建组件实例的时候，这个实例都划分了自己的组件范围，这个范围导致了在这个组件区域内无法获得其父组件的数据。所以，Vue是如何处理父组件向子组件中传递数据的呢？答案是，通过props。

先看一个最简单，从父组件向子组件中传递data的例子。注册的mine组件是子组件，他希望从父组件那里得到‘city’这个数据的信息，所以在mine的构造器里增加了一个参数props，用来接收父组件传递过来的city的值。

```
Vue.component('mine',{
    template : '<p>Appian is from {{ city }}.</p>',
    props : ['city']
});
```

上面的例子中，我们定义了props作为一个数组，所以props可以用来接收多个字段，而这些字段就是子组件期望从父组件那里得到的。

props不一定要是数组，也可以是对象。可以在对象中详细的定义很多props的限制条件。

```
Vue.component('mine',{
    template : '<p>Appian is from {{ city }}.</p>',
    props : {
        city : {
            type : String,//定义字符串类型
            required : true,//该字段是必须的
            default : 'China'//设置默认值
        }
    }
});
```

> 我们不需要每次都将props的限制条件都写出来，因为在这个例子中的数据是一个很简单的字段，上例中只是为了完整展示props的对象表示方法，所以才展开来写的。

那父组件那里又是怎么指派字段给子组件的呢？

```
<mine city="FuJian-YongAn"></mine>
```

这样直接在mine标签里面定义‘city’字段，就是父组件指派字段的方式之一。但是这样直接指派是很瞎的，我们需要的是动态变化的city，这个一会我们会说到的。

先简单介绍一下我们接下来要做的事。我们要假装我们正在搭一个博客，博客需要展示作者的基本信息，此时，我们可能会需要一些数据对象，可能是从数据库获得的，或者ajax请求到的，总之就是请求到了之后，将这个数据对象定义在父级的data中。并在html的template标签中准备渲染。

```
<div id="vueInstance">
    <mine></mine> //标识注册的内容会在这里插入，之后也要展开来说！！！
</div>

<template id="mineTpl">
     <h1>{{ name }}</h1>
     <h2>{{ title }}</h2>
     <h3>{{ city }}</h3>
     <p>{{ content }}</p>
</template>

<script>
    //Vue.component()的构造在下文中展开来说！！！

    var V = new Vue({
         el : '#vueInstance',
         data : {
            name : 'Appian',
            title : 'This is a title',
            city : 'FuJian-XiaMen',
            content : 'There are some desc about Appians Blog'
         }
    });
</script>
```

准备好模板渲染之后，当然也要注册mine的构造器Vue.component()。除了基本的绑定模板id（#mineTpl）之外，还需要指定这个子组件想要的数据的字段名，并把期望得到的4个字段写在props中。

```
Vue.component('mine',{
   template : '#mineTpl',
   props : ['name','title','city','content']
});
```

这样我们就能告诉父级，子组件需要的字段是哪些。接下来父级就可以指派字段的值给子组件了。前面的city字段是写死的，现在这里绑定的字段就是动态绑定的。

```
<mine :name='name'
      :title='title'
      :city='city'
      :content='content'
  ></mine>
```

> 等号左右两边的字段名称可以不一样。 等号左边的字段名，是指在子组件的props中声明的名字。在html写成肉串式，但是在props中写成驼峰式。 等号右边的字段名，是指在父级里定义的字段的名字。

> ‘:’是‘v-bind’的缩写

这样就能把父组件的4个字段绑定到子组件上。现在，只要父组件指派的字段的值一发生改变，子组件的值也会发生相应的改变。

## $emit事件 (把子组件的数据传给父组件)
我们知道，父组件是使用props传递数据给子组件，但如果子组件要把数据传递回去，应该怎样做？那就是自定义事件！

每个 Vue 实例都实现了事件接口(Events interface)，即：

- 使用 `$on(eventName)` 监听事件
- 使用 `$emit(eventName)`触发事件

```
ps:App.vue 父组件
　 Hello.vue 子组件
 

<!--App.vue  :-->

<template>
　　<div id="app">
　　　　<hello @newNodeEvent="parentLisen" />
　　</div>
</template>

<script>
    import hello from './components/Hello'
    export default {
        name: 'app',
        'components': {
            hello
        },
        methods: {
            parentLisen(evtValue) {    
                //evtValue 是子组件传过来的值
                alert(evtValue)
            }
        }
    }
</script>


<!--Hello.vue  :-->

<template>
　　<div class="hello">
　　　　<input type="button" name="" id="" @click="chilCall()" value="子调父" /> 
　　</div>
</template>

<script>
    export default {
        name: 'hello',
        'methods': {
            chilCall(pars) {
                this.$emit('newNodeEvent', '我是子元素传过来的')
            }
        }
    }
</script>
```

## 构建一个简易评论社区系统

现在就可以利用前面学到的内容，搭建一个简易的评论社区系统，样式什么的先不管，只讲究js的具体实现。

- 创建一个新的Vue实例
- 给实例挂载一个div（#vueInstance）
- 定义数据，然后渲染。

```
<div id="vueInstance">
    <div class="container">
        <ul>
           //这里即将渲染出评论的投票列表
        </ul>
    </div>
</div>

<template id="postTpl">
     <li>
         <i class="up">我支持</i>
         <span>票数： {{ post.votes }}</span>
         <i class="down">我反对</i>
         <a>话题： {{ post.title }}</a>
       </li>
</template>


<script>
    //Vue.component()的构造在下文中展开来说！！！

    var V = new Vue({
         el : '#vueInstance',
         data : {
             posts: [{
                title: '请大大多多为我投票，我给大家发红包',
                votes: 15
             },{
                title: '投我准没错',
                votes: 53
             },{
                title: '不要投给我楼上的',
                votes: 10
             }]
         }
    });
</script>
```

现在先构造好数据，有投票的话题和投票人数。然后再构造好模板（template标签），这个模板值用来渲染单个话题。模板里有除了渲染话题和投票人数，还有两个按钮，用来投赞成票或者反对票。之后我们只需要在html循环模板，然后就能多次插入模板，渲染成列表。当然也可以在模板里渲染好列表再一次插入。我们先用前一种方法。

不管css的样式问题，现在就可以开始注册Vue.component()构造器了，以便我们渲染页面。我们在注册的时候要明确，我注册的子组件需要的props是父级的posts数组中的一个元素对象post。所以我们应该这样注册：

```
Vue.component('post',{
    template : '#postTpl',
    props : ['post']
});
```

然后我们使用自定义的标签插入在html中去。

```
<div id="vueInstance">
    <div class="container">
        <ul>
           <post v-for="post in posts" :post="post"></post>
        </ul>
    </div>
</div>
```

这样我们就已经完成了循环输出posts数组了。因为我们把数组的元素指派给了子组件，所以子组件就可以渲染title和vote。接下来要做的就是增加“赞成”和“反对”按钮的逻辑代码，并我们需要对投票状态进行锁定，就是如果我们投了某个话题的赞成票就不能再投该话题的反对票，反之亦然。 所以让我们开始在模板里面定义点击事件吧，投赞成票的事件叫做“upvote”，投反对票的事件叫做“downvote”。

```
<template id="postTpl">
     <li>
         <i class="up" @click="upvote">我支持</i>
         <span>票数： {{ post.votes }}</span>
         <i class="down" @click="downvote">我反对</i>
         <a>话题： {{ post.title }}</a>
       </li>
</template>
```

```
Vue.component('post',{
    template : '#postTpl',
    props : ['post'],
    data : function (){
        return {  //data必须为function，定义投票状态
            upvoted: false,
            downvoted: false
        }
    },
    methods : {
        upvote : function() { //点击赞成的事件
            this.upvoted = !this.upvoted;
            this.downvoted = false;
        },
        downvote: function() { //点击反对的事件
            this.downvoted = !this.downvoted;
            this.upvoted = false;
        }
    }
});
```

> 注意，data里面的两个布尔值的定义是作为一个函数的返回值定义的。那是因为我们想要给每一个组件都设置一个是否投票的状态。 （还记得之前我说过，这次的列表渲染是循环渲染多个模板，每个模板都只是一个话题的相关信息，而现在在组件中定义的data：upvoted和downvoted，也是专属于某个模板的。） 这样我们如果投了某个话题的赞成票，并不会影响剩下话题的投票情况。

接下来已经完成了点击事件的状态控制，那么点击“赞成”和“反对”会导致话题的票数发生变化。这个时候我们可以利用之前的教程中学过的computed属性进行计算。

> 组件也有computed属性哦~

```
Vue.component('post',{
    template : '#postTpl',
    props : ['post'],
    data : function (){ //同上，略 },
    methods : {  //同上，略 },
    computed: {  //重点部分
        votes: function () {
            if (this.upvoted) {
                return this.post.votes + 1;
            } else if (this.downvoted) {
                return this.post.votes - 1;
            } else {
                return this.post.votes;
            }
        }
    }
});
```

到此为止，应该组件中的逻辑处理差不多完成了，现在要做的就是让我们在组件中修改的投票人数，能够在模板中渲染出来。因为我们现在的votes的值是在子组件中修改的，而一开始渲染的时候，我们的votes只是一味的接受父级传过来的值，所以，现在要把修改的值显示在模板上。 所以模板变成了这样:

```
<template id="postTpl">
     <li>
         <i class="up" @click="upvote">我支持</i>
         <span>票数： {{ votes }}</span>
         <i class="down" @click="downvote">我反对</i>
         <a>话题： {{ post.title }}</a>
       </li>
</template>
```

现在我们的投票系统已经基本完成了。我们可能会希望我们的投票系统好看一点，直观一点。所以我们可以在按钮上绑定一些样式。比如当用户已经投了某个话题的赞成票或者反对票，就让这个按钮变成橙色。

```
.disabled {
    color : orange;
}
```

Vue是利用v-bind:class来进行样式绑定的，可以简写成一个‘:’。其绑定的内容是一个对象，对象里面是class的名字和class对应的状态。

```
<template id="postTpl">
     <li>
         <i class="up" @click="upvote" :class="{disabled: upvoted}">我支持</i>
         <span>票数： {{ votes }}</span>
         <i class="down" @click="downvote" :class="{disabled: downvoted}">我反对</i>
         <a>话题： {{ post.title }}</a>
       </li>
</template>
```

如果我们点击了某个话题的赞成按钮，则它的upvoted就会变成true，则disabled的样式就绑定到赞成按钮上去。如果点了该话题的反对按钮，则它的upvoted就会变成false，则disabled就不会绑定到赞成按钮上。以上就是模板最终的样子。

## 组件的复用性的利用

我们已经利用了我们对Vue的基本语法还有一些组件的基本操作，建立起了一个基本的话题投票系统。在教程的最后一部分，我们将看看，我们应该如何将这个投票系统组件进行复用。

复用的关键在于组件的命名，让你的命名能够复用。至少你在构建你的组件的时候，你要问自己，“是否其他地方也能用到这个组件？”

比如，在上面的例子中，posts的意思是，这个数据是从ajax的post请求过来的数据，为了便于理解，才取名为posts，为了让自己的组件名字一看就知道关联，所以把模板的id定义为#postTpl，tpl是template的简写，自定义标签的命名也是post。总之，就是这样的细节，不仅方便自己阅读，也方便其他人阅读你的代码。

现在我们的评论系统需要增加一个功能，就是增加一个发布评论的功能。就是增加了一个发布评论的区域（#commentBox）。

```
<div id="vueInstance">
    <div class="container">
        <ul>
           <post v-for="post in posts" :post="post"></post>
        </ul>

        <div id="commentBox">
            请输入评论内容并提交：
            <input type="text" v-model="comment" @keyup.enter="postComment">
            <button @click="postComment">提交评论</button>
        </div>
    </div>
</div>

//模板渲染不变

<script>
//Vue.component()的注册不变。

var V = new Vue({
     el : '#vueInstance',
     data : {
         posts: [{
            title: '请大大多多为我投票，我给大家发红包',
            votes: 15
         },{
            title: '投我准没错',
            votes: 53
         },{
            title: '不要投给我楼上的',
            votes: 10
         }],
          comment: ''
     },
     methods: {
         postComment: function() {
             this.posts.push({
               title: this.comment,
               votes: 0
             })
             this.comment = '';
         }
     }
});
</script>
```

输入框用v-model绑定了comment字段，为了无论用户输入什么，在提交的时候都能获得他输入的值。当用户按回车或者点击提交按钮的时候都会触发postComment方法。这里的事件绑定一个是用的回车事件 @keyup.enter，还有一个点击事件@click。postComment方法就是把话题和投票为0的对象push进posts数组中去，Vue会将新的模板自动渲染出来。

这样一个可复用的组件就构造完成了，组件化会节省开发者的很多时间。组件是否复用，也要结合开发的实际需求而定。
