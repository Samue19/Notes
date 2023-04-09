# js

JavaScript是一种运行在浏览器中的解释型的编程语言。

在Web世界里，只有JavaScript能跨平台、跨浏览器驱动网页，与用户交互。

js代码直接嵌入网页和单独的文件引入。

编写的js代码是纯文本文件，

浏览器的安全限制，`file://`开头的地址无法执行如联网等js代码



### Array

改变`Array`的`length`的值会导致`Array`大小的变化。

对原数组无影响：concat，slice（切片），reduce，filter， some，every，indexOf，join，includes，

对原数组有影响：push，unshift，splice（拼接），reverse，sort，

from，of，find，fill

flat，flatMap，

#### 数组去重

```js
let newArr = arr.filter((val, i, array) => {
    return array.indexof(val) === i;
})
// Set
let newArr = [...new Set(arr)];
let newArr = Array.from(new Set(arr));
```

#### 数组拍平

```js
let newArr = arr.toString().split(',').map(item => 0 + item);
let newArr = arr.flat(1);
```



### Set，Map

JavaScript的对象是键值对，但键必须是字符串

`Map` 是一组键值对的结构

初始化`Map`需要一个二维数组，或者直接初始化一个空`Map`。`Map`具有以下方法：

```js
var m = new Map([['Michael', 95], ['Bob', 75], ['Tracy', 85]]);
var m = new Map(); // 空Map
m.set('Adam', 67); // 添加新的key-value
m.has('Adam'); // 是否存在key 'Adam': true
m.get('Adam'); // 67
m.delete('Adam'); // 删除key 'Adam'
```

`Set` 是一组不重复key的集合，

要创建一个`Set`，需要提供一个`Array`作为输入，或者直接创建一个空`Set`：

```js
var s1 = new Set(); // 空Set
var s = new Set([1, 2, 3, 3, '3']);
var s2 = new Set([1, 2, 3]); // 含1, 2, 3
s.add(1);
s.delete(1);
```



### iterable

`Array`、`Map`和`Set`都属于`iterable`类型

具有`iterable`类型的集合可以通过新的`for ... of`循环来遍历。

`iterable`内置的`forEach`方法，它接收一个函数，每次迭代就自动回调该函数

### generator

生成器，generator和函数不同的是，generator由`function*`定义（注意多出的`*`号），并且，除了`return`语句，还可以用`yield`返回多次。

`next()` 调用`generator`对象

`for of` 循环迭代`generator`对象

因为generator可以在执行过程中多次返回，所以它看上去就像一个可以记住执行状态的函数，

异步回调代码变成“同步”代码(异步顺序执行，同步执行一次)



### String

字符串是不可变的

模板字符串`${name}`，

`toUpperCase()` 和 `toLowerCase()` 大小写

`indexOf`（） 搜索字符串出现的位置

`substring()` 截取字符串

charAt，charCodeAt，concat，fromCharCode，lastIndexOf，match，search，slice，split，substr，valueOf，toString，replace，trim，repeat，



### RegExp

`\d`可以匹配一个数字

`\w`可以匹配一个字母或数字

`.`可以匹配任意字符

`\s`可以匹配一个空格（也包括Tab等空白符）

匹配变长字符

`*`表示任意个字符（包括0个）

`+`表示至少一个字符

`?`表示0个或1个字符

`{n}`表示n个字符

`{n,m}`表示n-m个字符

进阶

`[]`表示范围

`^`表示行的开头

`$`表示行的结束

**RegExp**

```js
var re1 = /ABC\-001/;
var re2 = new RegExp('ABC\\-001');

re1; // /ABC\-001/
re2; // /ABC\-001/
```

`test()`方法用于测试给定的字符串是否符合条件

**分组**

正则表达式还有提取子串的强大功能。用`()`表示的就是要提取的分组

`exec()` 匹配成功后，会返回一个`Array`

**贪婪匹配**

匹配尽可能多的字符

非贪婪匹配，加`?`

**全局搜索**

`g`，表示全局匹配

`i`标志，表示忽略大小写

`m`标志，表示执行多行匹配



### Object

JavaScript的对象是一种无序的集合数据类型，它由若干键值对组成。

属性 是字符串值

`in` 检测是否存在某一属性

`hasOwnProperty()` : 判断该属性是否自身拥有

`setPrototypeOf()`: 

getOwnPropertyNames，getOwnPropertySymbols，ownKeys，getOwnPropertyDesciptor, defineProperty, 

for in，

浅拷贝：assign，

深拷贝：JSON.parse(JSON.stringify())

freeze

Configurable， Enumerable，Writable，Value





### 数据类型

基本数据类型：Undefined, Null, Boolean, Number, String，Symbol，BigInt。

parseInt，parseFloat，Math.floor，Math.ceil，Math.round，Math.abs，toFixed

Object，Date，Array，RegExp，

判断数据类型：

typeof：判断基本数据类型（非null）,  string，number，boolean，symbol，bigint，undefined，object， function

instanceof：判断⼀个对象的具体类型，⼀些基础 数据类型，数组等会被判断为object。 

constructor：能判断基本类型和引 ⽤类型，但是对于 null 和 undefined 是⽆效的，以及 constructor 不太稳定。 

Object.prototype.toString.call：是根据原 型对象上的 tostring ⽅法获取的，该⽅法默认返回其调⽤者的具体类型。



判断对象是否具有属性：in，Reflect.has，hasOwnProperty，hasOwn，

**解构赋值**

```js
var [x, y, z] = ['hello', 'JavaScript', 'ES6'];
// 可以嵌套使用
// 可以忽略元素
let [, , z] = ['hello', 'JavaScript', 'ES6']; // 忽略前两个元素，只对z赋值第三个元素
var person = {
    name: '小明',
    age: 20
};
// 如果person对象没有single属性，默认赋值为true:
var {name, age=18} = person;
```

对一个对象进行解构赋值时，同样可以直接对嵌套的对象属性进行赋值，只要保证对应的层次是一致的，如果对应的属性不存在，变量将被赋值为`undefined`

使用场景

```js
// 交换变量值
[x, y] = [y, x]
// 快速获取页面的域名和路径
var {hostname:domain, pathname:path} = location;
// 如果一个函数接收一个对象作为参数，那么，可以使用解构直接把对象的属性绑定到变量中。
function buildDate({year, month, day, hour=0, minute=0, second=0}) {
    return new Date(year + '-' + month + '-' + day + ' ' + hour + ':' + minute + ':' + second);
}
```





### 字符集

utf-8，utf-16，unicode，base64



### 内存管理



### 继承

参考：https://juejin.cn/post/6844903696111763470

#### 原型链

构造函数、原型和实例之间的关系：每个构造函数都有一个原型对象，原型对象都包含一个指向构造函数的指针，而实例都包含一个原型对象的指针。

继承的本质就是**复制，即重写原型对象，代之以一个新类型的实例**。

![img](https://p1-jj.byteimg.com/tos-cn-i-t2oaga2asx/gold-user-assets/2018/10/30/166c2c0107fd80c7~tplv-t2oaga2asx-zoom-in-crop-mark:1512:0:0:0.awebp)

```js
function Parent() {
 this.arr = [1, 2, 3];
}
Parent.prototype.getName = function () {
 console.log(this.arr);
}
function Child() {}
Child.prototype = new Parent();		// 共用一个Parent实例导致的

var child1 = new Child();
var child2 = new Child();
console.log(child1.getName()) // [1,2,3]
child1.arr.push(4)
console.log(child1.getName()) // [1,2,3,4]
```

缺点 

1. 引⽤类型的属性被所有实例共享 
2. 创建Child实例时，不能向Parent传参

#### 借⽤构造函数(经典继承)

```js
function Parent() {
    this.arr = [1, 2];
}
function Child() {
    Parent.call(this);
}
var child1 = new Child();
child1.arr.push(3);
console.log(child1.arr); // [1,2,3]
var child2 = new Child();
console.log(child2.arr); // [1,2]
```

缺点 

+ 只能继承父类的**实例**属性和方法，不能继承原型属性/方法

+ 无法实现复用，每个子类都有父类实例函数的副本，影响性能

#### 组合继承

原型链继承+经典继承

用原型链实现对**原型**属性和方法的继承，用借用构造函数技术来实现**实例**属性的继承。

```js
function Parent(name) {
 this.name = name;
 this.colors = ['red', 'blue', 'green'];
}
Parent.prototype.getName = function () {
 console.log(this.name)
}
function Child(name, age) {
 Parent.call(this, name);
 this.age = age;
}
Child.prototype = new Parent();
Child.prototype.constructor = Child;
var child1 = new Child('kevin', '18');
child1.colors.push('black');
console.log(child1.name); // kevin
console.log(child1.age); // 18
console.log(child1.colors); // ["red", "blue", "green", "black"]
var child2 = new Child('daisy', '20');
console.log(child2.name); // daisy
console.log(child2.age); // 20
console.log(child2.colors); // ["red", "blue", "green"]
```

融合 原型链 继承和构造函数的优点，JS最常⽤继承模式

缺点:  在使用子类创建实例对象时，其原型中会存在两份相同的属性/方法。

#### 原型式继承

利用一个空对象作为中介，将某个对象直接赋值给空对象构造函数的原型。

```js
function createObj(o) {
 function F() {}
 F.prototype = o;
 return new F();
}
var person = {
 name: 'kevin',
 friends: ['daisy', 'kelly']
}
var person1 = createObj(person);
var person2 = createObj(person);
person1.name = 'person1';
console.log(person2.name); // kevin
person1.friends.push('taylor');
console.log(person2.friends); // ["daisy", "kelly", "taylor"]
```

缺点：

- 原型链继承多个实例的引用类型属性指向相同，存在篡改的可能。
- 无法传递参数

另外，ES5中存在`Object.create()`的方法，能够代替上面的object方法。

#### 寄⽣式继承

核心：在原型式继承的基础上，增强对象，返回构造函数

```js
function createObj(o) {
 var clone = Object.create(o);
 clone.sayName = function () {
 console.log('hi');
 }
 return clone;
}
```

缺点（同原型式继承）：

- 原型链继承多个实例的引用类型属性指向相同，存在篡改的可能。
- 无法传递参数

#### 寄⽣组合式继承

```js
function Parent(name) {
    this.arr = [1, 2, 3]
    this.name = name;
}
Parent.prototype.printArr = function() {
    console.log(this.arr)
}
function Child(name, age) {
    Parent.call(this, name);
    this.age = age
}
function prototype(child, parent) {
 var prototype = Object.create(parent.prototype); //创建⽗类原型对象的副本
 prototype.constructor = child; //增强对象，补充因重写原型⽽失去的默认的constructor属性
 child.prototype = prototype; //将创建的新副本指定给⼦类的原型对象
}
// 当我们使⽤的时候：
prototype(Child, Parent);
let child1 = new Child('samuel', 11);
let child2 = new Child('tom', 13);
child1.arr.push(4);
console.log(child1);
console.log(child2);
```

它只调用了一次`Parent` 构造函数，避免了在`Child.prototype` 上创建不必要的、多余的属性, 同时，原型链还能保持不变；因此，还能够正常使用`instanceof` 和`isPrototypeOf()`

**这是最成熟的方法，也是现在库实现的方法**

#### 混入方式继承多个对象

```js
function MyClass() {
     SuperClass.call(this);
     OtherSuperClass.call(this);
}

// 继承一个类
MyClass.prototype = Object.create(SuperClass.prototype);
// 混合其它
Object.assign(MyClass.prototype, OtherSuperClass.prototype);
// 重新指定constructor
MyClass.prototype.constructor = MyClass;

MyClass.prototype.myMethod = function() {
     // do something
};
```

`Object.assign`会把 `OtherSuperClass`原型上的函数拷贝到 `MyClass`原型上，使 MyClass 的所有实例都可用 OtherSuperClass 的方法。

#### ES6类继承extends

`extends`关键字主要用于类声明或者类表达式中，以创建一个类，该类是另一个类的子类。其中`constructor`表示构造函数，一个类中只能有一个构造函数，有多个会报出`SyntaxError`错误,如果没有显式指定构造方法，则会添加默认的 `constructor`方法，使用例子如下。

```js
class Parent {
    constructor() {
        
    }
}
class Child extends Parent {
    constructor() {
        super();
        
    }
}
// 原理
function _inherits(subType, superType) {
  
    // 创建对象，创建父类原型的一个副本
    // 增强对象，弥补因重写原型而失去的默认的constructor 属性
    // 指定对象，将新创建的对象赋值给子类的原型
    subType.prototype = Object.create(superType && superType.prototype, {
        constructor: {
            value: subType,
            enumerable: false,
            writable: true,
            configurable: true
        }
    });
    
    if (superType) {
        Object.setPrototypeOf 
            ? Object.setPrototypeOf(subType, superType) 
            : subType.__proto__ = superType;
    }
}
```





### 页面生命周期

+ DOMContentLoaded ：DOM构建完成，外部资源可能尚未加载完成。 
+ load：加载完成了 HTML和外部资源 
+ beforeunload/unload：当⽤户正在离开页⾯时



### 函数

JavaScript的函数不但是“头等公民”，而且可以像变量一样使用，具有非常强大的抽象能力。

`apply(this, [args])` 

`call(this, args)`

`bind(this, args)`

**高阶函数**

一个函数就可以接收另一个函数作为参数

`map(func)` 单一数组元素计算，得到一个新数组

`reduce（func)` 累积数组元素计算

`filter(func)` 过滤数组元素

`sort(func)` 默认将元素转为String后排序，`x < y`  是 `-1` , 直接修改原数组

`every(func)` 判断所有元素是否满足

`find(func)` 查找符合条件的第一个元素

`findIndex(func)` 返回索引

`forEach(func)` 遍历数组



### 模块化

特点 

1. 解决命名污染，全局污染，变量冲突等 
2. 内聚私有，变量不能被外部访问 
3.  更好的分离，按需加载 
4. 引⼊其他模块可能存在循环引⽤问题 
5. 代码抽象，封装，复⽤和管理 
6. 避免通过script标签从上⾄下加载资源 
7. ⼤型项⽬资源难以维护，特别是多⼈合作的情况

CommonJS：同步加载，require，服务器编程，导出时都是值拷贝，模块在⾸次执⾏后会缓存

AMD：浏览器使用，异步加载，会编译成 require/exports 来执⾏

CMD：于浏览器端，异步加载模块，使⽤模块时才会加载执⾏。

ES6： import 和 export 的形式来导⼊导出模块，异步导⼊，导⼊导出的值都指向同⼀个内存地址



### ajax

```js
const ajax = new XMLHttpRequest();
ajax.open('GET', url, true);
ajax.setRequestHeader("Content-type", "application/x-www-formurlencoded");
ajax.send(null);
ajax.onreadystatechange = function () {
 if (ajax.readyState == 4 && (ajax.status == 200 || ajax.status == 304)) {
     
 }
};
```



### 变量

var，let，const
`var`：没用块作用域{}
`const`：常量，同一个作用域不能改

`Object.freeze()`：冻结变量



正则表达式：| ，[] , () , \ , ^ , $ , \d , \D , \s , \S , \w ,\W , . , ? , ?: , + , * , {} , $` , $' , $& , ?<> , ?= , ?<= , ?! ,
test(),match(),exec(),search(),replace(),
匹配模式：g , i , m , u , y ,



### Promise

微任务 , 宏任务 ，
Promise().then().catch().finally()
Promise.reject(), Promise.all() , Promise.allSettled(), Promise.race() ,
async , await ,



### DOM



### BOM





变量,

数据类型,

类型转换,

运算符,

条件判断,

循环,

函数,

作用域,

对象,

数组,

字符串,

时间,

BOM,

DOM,

事件,

原型链,

构造函数,
es6,

定义变量,

箭头函数,

解构赋值,

模板字符串,

展开运算符,

类语法
get,post,