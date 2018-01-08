# 数字与字符串相互转换

## 数字转字符串

1 用String函数,或者toString方法

```
var i = 10;
var s1 = i.toString();
var s2 = String(i);
```
2 要给它添加一个空的字符串即可

```
var n = 100; 
var n_as_string = n + ""; 
```


## 字符串转数字

1 使用函数`parseInt(string)`,注意该函数只截取整数

2 使用Number函数

```
var number = Number(string_value); 
```

# js数组与字符串的互换

## 数组转字符串

可以用`.tostring`或者`.join`来转,不过join需要指定分割符 

```
var a, b;
a = new Array(0,1,2,3,4);
b = a.join("-");

b = a.toString();
```

## 字符串转数组

将字符串按某个字符切割成若干个字符串，并以数组形式返回

```
var s = "abc,abcd,aaa";
ss = s.split(",");// 在每个逗号(,)处进行分解。
```

# 浅拷贝和深拷贝

```
var a = 30;
var b = a;
a = 20;
console.log( b )   // 30
 
var a = [1,2];
var b = a;
a[0] = 5;
console.log( b )  // [5,2]  
```

number,string类型都是基本类型，而基本类型存放在栈区，访问时按值访问，赋值是按照普通方式赋值；

**对象和数组是通过引用来赋值的**，所以改变a的同时b也会跟着改变。**这种拷贝就是浅拷贝**

引用对象存放的方式是：在栈中存放对象变量标示名称和该对象在堆中的存放地址，在堆中存放数据。

对象使用的是引用赋值。当我们把一个对象赋值给一个新的变量时，赋的其实是该对象的在堆中的地址，而不是堆中的数据。也就是两个对象指向的是同一个存储空间，无论哪个对象发生改变，其实都是改变的存储空间的内容，因此，两个对象是联动的。

```
var a = [1,2,3];
var b = a;
a = [4,5,6];
alert(b); //[1,2,3]

var a = [1,2,3];
var b = a;
a.pop();
alert(b); //[1,2]
```

但是,看了上面程序,是不是有点懵,原因如下

> a = [4,5,6];//改变的是a引用本身，没有改变数组对象，a和b没有了关系。
a.pop();//改变的是数组对象，a引用没有改变。
b = a;//该操作后，b直接指向数组对象，不是b指向a，a再指向数组。
//所以改变a引用并不会对b引用造成影响，改变数组对象可以。

## 浅拷贝

简单的赋值就是浅拷贝,注意**对象和数组在赋值的时候都是引用传递。所以赋值的时候只是传递一个指针**

## 深拷贝

### 数组深拷贝

```
//深拷贝
var a = [1,2,3];
var deepArry = [];

function deepCopy(arry1, arry2){
    for(var i = 0,l= arry1.length;i<l;i++){
        arry2[i] = arry1[i];
    }
}

deepCopy(a,deepArry);
```

**或者使用JS提供的b =a.slice(0);   b = a.concat([]);**

如果是多维数组需要循环对每个值进行拷贝

### 对象深拷贝

- 1、用递归的方式来做，

```
function deepCopy(o,c){
	    var c = c || {}
	    for(var i in o){
	    if(typeof o[i] === 'object'){
	  	   	   	  //要考虑深复制问题了
                      if(o[i].constructor === Array){
                    	//这是数组
                    	c[i] =[]
                    }else{
                    	//这是对象
                    	c[i] = {}
                    }
                    deepCopy(o[i],c[i])
	  	   	   }else{
	  	   	   	 c[i] = o[i]
	  	   	   }
	  	   }
	  	   return c
	  }
```

- 2、利用JSON.stringify和JSON.parse来做

```
var newObj = JSON.parse( JSON.stringigy( someObj ) );
```

该方法对于JSON安全的对象有用.
> JSON安全:可以序列化为一个JSON字符串并且可以根据这个字符串解析出一个结构和值完全一样的对象

缺点:

- 无法复制函数
- 原型链没了，对象就是object，所属的类没了。
