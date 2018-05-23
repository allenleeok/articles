## JavaScript

1.  +'3.14' = 3.14 将字符串转化为数字
1.  jquery：
    bind() 是直接绑定在元素上，而 live() 是通过冒泡的方式来绑定到 document 元素上，delegrate 是可以设置委托对象的，不限于 document 元素，但是不能直接绑定在元素上，on()结合了以上所有方法
    end 方法
1.  foreach 和 map 的区别，
1.  圆括号运算符也叫分组运算符，它有两种用法：如果表达式放在圆括号中，作用是求值；如果跟在函数后面，作用是调用函数。圆括号运算符不能为空，否则会报错。由于圆括号的作用是求值，如果将语句放在圆括号之中，就会报错，因为语句没有返回值

1.  jsonp 的原理:
    允许用户传递一个 callback 参数给服务端，然后服务端返回数据时会将这个 callback 参数作为函数名来包裹住 JSON 数据，这样客户端就可以随意定制自己的函数来自动处理返回数据了。

1.  它只支持 GET 请求而不支持 POST 等其它类型的 HTTP 请求；它只支持跨域 HTTP 请求这种情况，不能解决不同域的两个页面之间如何进行 JavaScript 调用的问题

1.  基本数据类型和引用类型的区别：
    ECMAScript 包含两个不同类型的值：基本类型值和引用类型值。基本类型值指的是简单的数据段；引用类型值指由多个值构成的对象。当我们把变量赋值给一个变量时，解析器首先要做的就是确认这个值是基本类型值还是引用类型值。基本数据类型可以直接操作保存在变量中的实际值引用数据类型是保存在堆内存中的对象，与其它语言不同的是，你不可以直接访问堆内存空间中的位置和操作堆内存空间。只能通过操作对象的在栈内存中的引用地址。所以引用类型的数据，在栈内存中保存的实际上是对象在堆内存中的引用地址。通过这个引用地址可以快速查找到保存在堆内存中的对象。

1. redux三大原则: 单一数据源,State 是只读的,使用纯函数来执行修改，react和其他开发模式的区别，react的生命周期，
1. webpack等打包工具的原理
1. es6 symbol 新的数据类型
1. 继承的各种方式:

    ```javascript
    // 构造函数只继承属性
    var superType = function() {
      this.name = "asa";
    };

    superType.prototype.sayName = function() {
      console.log(this.name);
    };

    var subType = function() {
      superType.call(this);
    };

    var instance = new subType();
    console.log(instance); //subType {name: "asa”}
    ```

    ```javascript
    //组合继承
    var superType = function(name) {
      this.name = name;
    };

    superType.prototype.sayName = function() {
      console.log(this.name);
    };

    var subType = function() {
      superType.call(this, "allen");
      this.color = ["red", "blue", "yellow"];
    };

    subType.prototype = new superType();
    subType.prototype.constructor = subType;
    subType.prototype.sayColor = function() {
      console.log(this.color);
    };
    ```


    var instance1 = new superType();
    // instance1.sayColor();

    var instance = new subType();
    console.log(instance);
    instance.sayColor();
    ```

    ```javascript
    //原型式继承  需要对象字面量
    function object(o){
        function F(){}
        F.prototype = o;
        return new F();
    }

    //寄生式继承
    function createAnother(original){
        var clone = object(original); //通过调用函数创建一个新对象
        clone.sayHi = function(){
        //以某种方式来增强这个对象
            alert("hi");
        };
        return clone; //返回这个对象
    }

    //寄生组合式继承
    function inheritPrototype(subType, superType){
        var prototype = object(superType.prototype); //创建对象
        prototype.constructor = subType; //增强对象
        subType.prototype = prototype; //指定对象
    }
    ```

1.  闭包
1.  变量作用域:

    ```javascript
    var objects = {};
    var events = { fn1: "clicked", fn2: "changed" };
    for (var x in events) {
      objects[x] = function() {
        console.log(events[x]);
      };
    }
    objects.fn1(); //changed
    objects.fn2(); //changed

    // 变量x是var声明的，在全局作用域内都有效，所以全局只有一个变量x，每一次循环，变量x的值都会发生改变，而循环内被赋给对象objects的function在运行时，会通过闭包读到这同一个变量x，导致最后输出的是最后一轮的x的值。如果想保留每个值，就要用let，声明的变量仅在块级作用域内有效。
    ```

1.  url 解析:

    ```javascript
    function getQueryObject(url) {
      url = url == null ? window.location.href : url;
      var search = url.substring(url.lastIndexOf("?") + 1);
      var obj = {};
      var reg = /([^?&=]+)=([^?&=]*)/g;
      search.replace(reg, function(rs, $1, $2) {
        var name = decodeURIComponent($1);
        var val = decodeURIComponent($2);
        val = String(val);
        obj[name] = val;
        return rs;
      });
      return obj;
    }
    ```

1.  bind 函数:

    ```javascript
    function bind(fn, context) {
      return function() {
        return fn.apply(context, arguments);
      };
    }

    function curry(fn) {
      var args = Array.prototype.slice.call(arguments, 1);
      return function() {
        var innerArgs = Array.prototype.slice.call(arguments);
        var finalArgs = args.concat(innerArgs);
        return fn.apply(null, finalArgs);
      };
    }

    function bind(fn, context) {
      var args = Array.prototype.slice.call(arguments, 1);
      return function() {
        var innerArgs = Array.prototype.slice.call(arguments);
        var finalArgs = args.concat(innerArgs);
        return fn.apply(context, finalArgs);
      };
    }
    ```

1.  react differ 算法, react 的数据绑定, virtual dom, jsx, 高阶组件, 中间件, redux 
1.  es6
1.  ES6 Class 的实现原理：

    ```javascript
    "use strict";
    var _createClass = (function() {
      function defineProperties(target, props) {
        for (var i = 0; i < props.length; i++) {
          var descriptor = props[i];
          descriptor.enumerable = descriptor.enumerable || false;
          descriptor.configurable = true;
          if ("value" in descriptor) descriptor.writable = true;
          Object.defineProperty(target, descriptor.key, descriptor);
        }
      }

      return function(Constructor, protoProps, staticProps) {
        if (protoProps) defineProperties(Constructor.prototype, protoProps);
        if (staticProps) defineProperties(Constructor, staticProps);
        return Constructor;
      };
    })();
    function _classCallCheck(instance, Constructor) {
      if (!(instance instanceof Constructor)) {
        throw new TypeError("Cannot call a class as a function");
      }
    }

    var Parents = (function() {
      function Parents(name) {
        _classCallCheck(this, Parents);
        this.name = name;
      }

      _createClass(Parents, [
        {
          key: "sayName",
          value: function sayName() {
            console.log(this.name);
          }
        }
      ]);
      return Parents;
    })();
    ```

## HTML/CSS

1.  css3 动画属性
1.  清除浮动
1.  居中布局
1.  rem

## Algorithm
* 0-10000有几个0:
把10000看成0000,还是4个0,没区别吧
把所有1位数,前面补3个0变成0001/0002/0003…… 0009,这样多补了3*9=27个0对吧
把所有2位数,前面补2个0变成0010/0011/0012…… 0099,这样多补了2*90=180个0
把所有3位数,前面补1个0变成0100/0101/0102…… 0999,这样多补了1*900=900个0
现在这1万个数变成了0000-9999,对吧,这就是四位数,每位可以是0-9任选一个,可以重复对吗
这样一共多少4万个数字,而且0-9这10个数出现的机会是一样的,也就是说大家分别出现了4000次
用4000-27-180-900=2893,这就是0出现的次数

* 数组arr 求sum的两位组合
* 步骤条设置
* 深拷贝浅拷贝
* 查找数组交集
* 遍历dom节点
* 将两个有序数组合并为一个数组:

```javascript
function merge(left, right) {
  var result = [],
    il = 0,
    ir = 0;

  while (il < left.length && ir < right.length) {
    if (left[il] < right[ir]) {
      result.push(left[il++]);
    } else {
      result.push(right[ir++]);
    }
  }
  //这里注意
  result = result.concat(left[il] ? left.slice(il) : right.slice(ir));
  return result;
}
var left = [1, 4, 7, 8, 9, 10];
var right = [2, 5];
console.log(merge(left, right));
```

* BFS:

```javascript
const traverse = ndRoot => {
  const queue = [ndRoot];

  while (queue.length) {
    const node = queue.shift();
    printInfo(node);
    if (!node.children.length) {
      continue;
    }
    Array.from(node.children).forEach(x => queue.push(x));
  }
};

const printInfo = node => {
  console.log(node.tagName, `.${node.className}`);
};

// kickoff
traverse(document.querySelector(".root"));
```
