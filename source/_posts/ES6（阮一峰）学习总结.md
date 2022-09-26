---
title:ES6（阮一峰）学习总结
categories:  #设置分类
- js
---
# ES6（阮一峰）学习总结（转载）

**1.块级作用域的引入**

在ES6之前，js只有全局作用域和函数作用域，ES6中let关键字为其引入了块级作用域。

```js
{
var a = 5;
let  b = 6;
}
console.log(a);     //5
console.log(b);     //b is undefined
```

let声明的变量只能在其所在的代码块内才能访问，var声明的变量由于是全局变量，因此可以在代码块外访问

**2.暂时性死区**

var声明的变量可以在声明之前使用，相当于默认为其声明其值为undefined了；

但是，let声明的变量一旦用let声明，那么在声明之前，此变量都是不可用的，术语称为“暂时性死区”。

```js
console.log(a);                     //undefined
var a=8;
console.log("----------");
console.log(b);                     //控制台报错
let b=9;
```

所以我们要养成变量先声明再使用的好习惯。

**3.const命令**

const用来定义常量，相当于java中的final关键字。

并且const声明常量之后就必须立即初始化！

**4.解构赋值**

```js
let [a,b,c] = [1,2,3];
let{x1,x2} = {x2:5,x1:6};
const [a,b,c,d,e]= "hello";
function  add([i,j]) {}---add([5,6]);
```

可以理解为“模式匹配”。

**5.字符串**

Unicode表示法

```js
"\u{码点}"
"\u{41}\u{42}\u{43}"                 //"ABC"
```

```js
let str = "書剑恩仇录";
str.codePointAt(0).toString(16);    //返回字符的码点并由十进制转到16进制---66f8
String.fromCodePoint(0x66f8);       //返回码点对应的字符---書
for (let a of str){
   console.log(a);
}                                   //for...of循环遍历字符串中每个字符挨个输出字符
str.at(0);                          //返回指定位置的字符，目前只是提案
str.startsWith('書',0);             //从指定位置往后开始检查，是否以“書”开始，位置参数可省略，默认为0
str.endsWith('剑',1);               //从指定位置向前检查，是否以“剑”结束
str.includes('恩',1);               //同上，不再啰嗦
str.repeat(2);                      //字符串重复指定次数“書剑恩仇录書剑恩仇录”，小数取整，Infinity和负数报错
str.padStart(8,'ab');               //指定字符从前开始补直到字符串长度符合要求，"aba書剑恩仇录"
str.padEnd(8,'ab');                 //指定字符从后开始补直到字符串长度符合要求，"書剑恩仇录aba"，若长度小于原长度，返回原字符串，上同
```

**6.模板字符串**

模板字符串采用反引号（`）标识，并且模板字符串中的空格、换行将在输出时有所保留。

```js
// 普通字符串
`In JavaScript '\n' is a line-feed.`

// 多行字符串
`In JavaScript this is
 not legal.`

console.log(`string text line 1
string text line 2`);

// 字符串中嵌入变量
let name = "Bob", time = "today";
`Hello ${name}, how are you ${time}?`
```

${主体}，其中主体可以是表达式、运算、对象属性还可以是函数，若是字符串将直接输出该字符串。

**7.含参函数的调用**

```js
function say(something){
    console.log("she say"+" '"+something+"'" );
}
say`hello`;                             //she say 'hello'
```

等同于say('hello')。

**8.数值拓展**

和字符串对象类似的，ES6也为数值类对象例如Number、Math添加了新的方法以及属性（常量），在这里就不多作记录。

**9.函数function**

```js
function show(name="jack",sex="boy"){
    console.log(name+" is a "+sex+"!");
}
show();                                  //jack is a boy!
show('judy');                            //judy is a boy!
show('judy','girl');                     //judy is a girl!
```

为函数的参数添加默认值，执行函数时如果不传该参数，那么就用默认值代替。

箭头函数：

var 变量名/函数名 = （参数，参数）=>{代码块}

```js
var f = v => v;
//等同于
var f = function(v) {
  return v;
};

var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = (num1, num2) => num1 + num2;
// 等同于
var sum = function(num1, num2) {
  return num1 + num2;
};
```

注意：如果return的是一个对象{id:id,age:age},那么箭头右边要用括号包起来().

**10.数组的扩展**

扩展运算符为三个点（...）,将一个数组转化为参数序列，通常与函数一起使用，show(...['judy','girl'])。

数组合并：[...arr1,...arr2,...arr3]

字符串转字符数组：[..."hello"]--------------["h","e","l","l","o"]

将实现Iterator接口的对象转化为真正的数组：[...nodelist]，这里的nodelist是一个类似于数组的nodelist对象

Generator 函数：该函数执行后返回一个遍历器对象，拓展运算符也可将其转化为数组。

```js
let a =function*(){
    yield 3;
    yield 4;
    yield 5;
    return 6;
};
console.log([...a()]);              //[3,4,5]
```

**11.数组的方法**

Array.from(对象，对新数组各项的改动规则)

这里的对象只适合①类数组对象②实现Iterator接口的对象；后面的规则可选

e.g:

Array.from([1, 2, 3], (x) => x * x)     //这里将数组每项按一定规则改变生成新数组[1,4,9]``

Array.of(数据1，数据2，数据3)

将一组数据转化为数组

e.g：

Array.of(1,2,3,4,5)                //[1,2,3,4,5]

copyWithin(被覆盖起始位置，选取的数据起始位置，选取额数据结束位置)

截取数组的一段数据，并覆盖到指定位置

e.g：

[1,2,3,4,5].copyWithin(0,2,4)        //被截取数据位置为[2,4）---[3,4],替换起始位置是0，所以结果是[3,4,3,4,5]

find(规则)、findIndex(规则)

这里的规则是一个回调函数，找到了就返回这个数组项/索引，找不到返回undefined/-1

e.g：

[9,8,7,6,5,4,3].find(n=>n<5)        //返回4

还可以添加第二个参数，如下

```js
function f(v){
    return v > this.age;
}
let  c =function(v){
    return v > this.age;
}
let person = {name: 'John', age: 20};
let a  =[10, 12, 26, 15].find(c, person);            //c、f都可以  
console.log(a);                                      //26
```

fill(被填充数据，起始位置，结束位置)

如果起始位置、结束位置不写，那么就默认全部填充

e.g：

[2,2,2,2,2,2].fill(8,2,4)                //将8覆盖原[2,4)位置上的数据，[2,2,8,8,2,2]

注意，如果给每项赋值的是一个对象，那么实际上只是一个指针，若改变一个位置的对象内容，那么所有项

的对象内容都会改变。

```js
let b = {name:'jack'};
let a =[2,2,2,2,2,2].fill(b,1,4) ;
console.log(a);               //[ 2, { name: 'jack' }, { name: 'jack' }, { name: 'jack' }, 2, 2 ]
a[1].name = "echo";
console.log(a);               //[ 2, { name: 'echo' }, { name: 'echo' }, { name: 'echo' }, 2, 2 ]
```

for...of遍历数组的键、值、以及各项键值对信息

```js
for (let index of ['a', 'b'].keys()) {
    console.log(index);
}
// 0
// 1

for (let elem of ['a', 'b'].values()) {
    console.log(elem);
}
// 'a'
// 'b'

for (let [index, elem] of ['a', 'b'].entries()) {
    console.log(index, elem);
}
// 0 "a"
// 1 "b"
```

备注：有的浏览器没有实现数组的values()方法，比如：Chrome！

**12：对象的拓展**

对象里面可以直接写入变量和函数

```js
//before：
var person = {
    name:'eco',
    age:18,
    say:function(something){
        console.log("hello "+something);
    }
};
person.say('world');

//now:
var firstname='jack';
var man = {
    firstname,
    say(something){
        console.log(this.firstname);
        console.log("hello "+something);
    }
};
man.say('world');
```

属性名/方法名：可以用中括号里面加上表达式的方式

e.g：

var a = 'age';

person.age=person['age']=person[a]

方法的name属性返回方法名

person.say.name                  //"say"

Object.is(值1，值2)用于比较两个值是否相等，返回布尔值

Object.assign(targetobject,sourceobject1,sourceobject2)

用于对象的合并，将源对象合并到目标对象，若有相同属性源对象属性覆盖目标对象属性

如果源对象是其他数据类型，只有字符串会以字符数组形式拷到目标对象，其他类型不会有效果。

```js
const v1 = 'abc';
const v2 = true;
const v3 = 10;

const obj = Object.assign({}, v1, v2, v3);
console.log(obj);           // { "0": "a", "1": "b", "2": "c" }
```

对象的属性描述：Object.getOwnPropertyDescriptors(obj)

对象的继承相关：

Object,setPrototypeOf(obj,proto)          //为obj对象设置一个原型对象，那么obj继承了proto对象的所有属性

Object.getPrototypeOf(obj)               //不难看出，这是读取一个对象的原型对象

super                                //指向当前对象的原型对象，相当于java中的超类

**13.Symbol函数**

为了防止不同人员书写代码造成变量名/方法名的冲突

```js
let a = Symbol();
let b = Symbol();
//函数可以添加带有描述性语言的字符串参数
a === b ;          
//false
```

**14.Set和Map数据结构**

Set：成员不重复的类数组结构

Set属性：size---返回成员总数

Set操作方法：add(value)---返回Set、delete(value)---返回布尔、has(value)---返回布尔、clear()---无返回值

Set遍历方法：keys()---返回键（索引）的遍历器、values()---返回值的遍历器、

  entries---返回键值对的遍历器、forEach(callback())---遍历每个成员，并通过回调函数基于数据做点什么

WeakSet：类似于Set，只是它的成员只能是对象，没有size，不能遍历

Map：广义上的键值对集合，键的范围不局限于字符串，对象也可以当作键

Map操作方法：set(key,value)---设置成员、get(key)---读取指定键的值，若无返回undefined



```js
const set = new Set([1, 2, 3, 4, 4]);
//[...set]---[1,2,3,4]

const map = new Map([
    ['name', '张三'],
    ['title', 'Author']
]);
```

 **15.Proxy代理**

```js
var handler = {
    get: function(target, name) {
        if (name === 'prototype') {
            return Object.prototype;
        }
        return 'Hello, ' + name;
    },

    apply: function(target, thisBinding, args) {
        return args[0];
    },

    construct: function(target, args) {
        return {value: args[1]};
    }
};

var fproxy = new Proxy(function(x, y) {
    return x + y;
}, handler);

fproxy(1, 2)                                      // 1
new fproxy(1, 2)                                  // {value: 2}
fproxy.prototype === Object.prototype             // true
fproxy.foo === "Hello, foo"                       // true
```



我们可以看出，上面声明了一个变量/函数fproxy，并且为其添加了一个拦截器对象handler，

那么对fproxy进行一些操作行为的时候，会优先被这个拦截器捕获，进行特定处理后输出结果

var fproxy = new Proxy(target,handler);      //一个Proxy实例

construct：构造一个新的fproxy时会触发拦截器的该方法，new fproxy(1,2)===>return {value : args[1]}===>{value : 2}

apply：函数执行时会触发拦截器的该方法，fproxy(1,2)===>return args[0]===>1

get：读取属性值的时候会触发拦截器的该方法，fproxy.foo===>foo对应该方法的参数name，return 'Hello, '+name;===>"Hello, foo"

set：设置属性值的时候会触发拦截器的该方法。

备注：

let obj = Object.create(fproxy);

这里为obj设置了原型fproxy，那么obj继承了fproxy的所有属性，obj.foo===>fproxy.foo===>"Hello, foo"

Proxy支持的拦截操作除了上面的4中之外还有9中，有兴趣的请点击 **[Proxy](http://es6.ruanyifeng.com/#docs/proxy)**。

**16.Reflect反射**

类似于java的反射，在跳过编译、不加载类的前提下，动态地调用类中的方法。

和Proxy相对应的，Reflect也有13个静态方法，详情请点击 **[Reflect](http://es6.ruanyifeng.com/#docs/reflect)**。

Reflect.get(target,name,receiver)------------读取target对象（必须是对象）的name属性值，若无返回undefined，

 若name属性有get声明，那么name函数中的this指向receiver对象。

Reflect.set(target,name,value,receiver)----设置target对象（必须是对象）的name属性值为value，

 若name属性有set声明，那么name函数中的this指向receiver对象。

注意：当Proxy和Reflect同时使用时，为一个Proxy实例赋值时，触发set拦截，若set拦截方法体内又有

 Reflect.set(target,name,value,receiver)，那么这又会触发拦截器的defineProperty拦截，前提是反射操作

​     传入了receiver参数！！！

Reflect.has(obj,name)---------------------------返回布尔值，表示obj对象中有没有name属性。

**17.Promise---异步**

先来看ajax的异步：

```js
$(function(){
    $('#send').click(function(){
         $.ajax({
             type: "GET",
             url: "test.json",
             data: {username:$("#username").val(), content:$("#content").val()},
             dataType: "json",
             success: function(data){
                         $('#resText').empty();   //清空resText里面的所有内容
                         var html = ''; 
                         $.each(data, function(commentIndex, comment){
                               html += '<div class="comment"><h6>' + comment['username']
                                         + ':</h6><p class="para"' + comment['content']
                                         + '</p></div>';
                         });
                         $('#resText').html(html);
                      }
         });
    });
});
```

上面的例子实现了一个类似于表单提交的功能。

Promise的异步：

```js
let promise = new Promise(function(resolve, reject) {
  console.log('Promise');                        //实例化后立即执行
  resolve();                                     //任务（成功）完成
});

promise.then(function() {
  console.log('resolved.');                      //任务结束执行
});

console.log('Hi!');                              //在实例化promise的同时，执行
```

显示顺序："Promise"---"Hi"---"resolved"

可以看出，在promise执行的整个过程中（实例化到结束），并没有阻塞其他外部语句的执行，换句话说，其他语句

不用等到输出"resolved"之后再执行。

```js
function loadImageAsync(url) {
  return new Promise(function(resolve, reject) {
    const image = new Image();

    image.onload = function() {
      resolve(image);                        //promise对象状态变为resolved
    };

    image.onerror = function() {
      reject(new Error('Could not load image at ' + url));
    };                                       //promise对象状态变为rejected并抛出错误

    image.src = url;
  });
}
```

注意：上面状态改变时传入函数的参数（image、new Error），会传到之后then函数，作为then函数的参数的参数！！！

loadImageAsync(url).then( function(success){console.log(success);}  ,function(error){console.log(error);});

这里的success接收来自resolved状态的参数image，error接收来自rejected状态的参数new Error。

事实上then后面还可以加上一个catch函数用来捕捉rejected状态产生的错误,这样就可以省略掉then函数里面的第二个参数

promise.then(success()).catch(error()).finally(function(){});

看上去是不是类似于java的try...catch...finally呢？

其他方法请戳===>**[Promise](http://es6.ruanyifeng.com/#docs/promise)**。

**18.Iterator接口**

具备Iterator接口的原生数据结构：

Array---Map---Set---String---TypedArray---NodeList对象---函数的arguments对象。

实用场景：

解构赋值：let [x,y] = new Set([1,2,3])               //x=1;y=2

扩展运算符：[...iterable]                         //将实现Iterator接口的对象转化为数组

yield*：yield*[2,3,4]---yield 2;yield 3;yield 4;          //generator函数内部

....

实现了Iterator接口的数据类型，都会有一个属性[Symbol.iterator]，固定写法，它是一个函数，返回一个遍历器对象

```js
e.g:
let arr = ['a', 'b', 'c'];
let iter = arr[Symbol.iterator]();                 //返回一个遍历器
iter.next()                                        // { value: 'a', done: false }
iter.next()                                        // { value: 'b', done: false }
iter.next()                                        // { value: 'c', done: false }
iter.next()                                        // { value: undefined, done: true }
```

注意：

for...in循环：只能获取对象的键名

for...of循环：可以获得键值，只返回具有数字索引的属性（键或值）

```js
var arr = ['a', 'b', 'c', 'd'];

for (let a in arr) {
  console.log(a);                  // 0 1 2 3
}

for (let a of arr) {
  console.log(a);                  // a b c d
}
```

**19.Generator函数补充**

```js
let a =function*(){
    yield 3;
    yield 4;
    yield 5;
    return 6;
};
console.log([...a()]);              //[3,4,5]
```

只有执行a().next()，函数内部的语句才会执行一次，每调用一次next()函数执行一次内部函数。

e.g:

```js
function* dataConsumer() {
  console.log('Started');
  console.log(`1. ${yield}`);
  console.log(`2. ${yield}`);
  return 'result';
}

let genObj = dataConsumer();
genObj.next();            // Started；执行了第一条语句
genObj.next('a')          // 1. a；执行了第二条语句
genObj.next('b')          // 2. b；执行了第三条语句
```

next()函数有一个可选参数，用来表示上一次yield表达式值。

e.g:

```js
function* foo(x) {
  var y = 2 * (yield (x + 1));
  var z = yield (y / 3);
  return (x + y + z);
}

var b = foo(5);
b.next()                   // { value:6, done:false }
b.next(12)                 // { value:8, done:false }
b.next(13)                 // { value:42, done:true }
```

解析：

第一次next()，x=5，那么yield(x+1)=6---{value:6,done:false}

第二次next(12)，令yield(x+1)=12，那么y=24,输出yield(y/3)=8---{value:8,done:false}

第三次next(13)，令yield(y/3)=13，前面yield(x+1)=12，那么最终z=13，y=24，x=5，return (x+y+z)=42---{value:42,done:true}

throw:

两种throw：遍历器对象的throw()，全局命令throw

iter.throw(error),这个错误会被遍历器函数内部的catch捕获，

iter.throw(error),遍历器对象再次抛出错误，由于内部的catch已经执行了，那么这次的error会被外部的catch捕获

throw new Error(error),这是个全局命令，会被全局（外部）作用域的catch捕获，遍历器对象内部的catch是不能捕获的

遍历器抛出的错误优先被遍历器内部捕获，内部没有catch才会被外部catch捕获

①遍历器捕捉到错误之后，除了执行catch内部的命令之外，还会自动执行一次next()方法。

②Generator 执行过程中抛出错误，且没有被内部捕获，就不会再执行下去了。

如果此后还调用next方法，将返回一个value属性等于undefined、done属性等于true的对象。

③遍历器的return(参数)方法会终结函数，并返回一个对象{value:参数，done:true},参数为空，value为undefined。

如果有finally，那么这个return会在finally结束后执行。

④要在gen函数内部调用别的gen函数，要使用yield* gen()语句，如果没有这个*号，那么next().value返回的是一个遍历器对象

**20.async函数**

async就表示asynchronous（异步的），async函数会返回一个Promise对象，自然能够调用其方法：

promise.then(success()).catch(error()).finally(function(){});

```js
async function getStockPriceByName(name) {
    const symbol = await getStockSymbol(name);
    const stockPrice = await getStockPrice(symbol);
    return stockPrice;             //stockPrice是一个promise对象
}

getStockPriceByName('goog').then(function (result) {
    console.log(result);
});
```

可以看出，它和一般函数没多大区别，只是多了一个async标识。

注意：上面所说到的返回一个对象，这个对象本身没什么特别，只是他可以作为promise对象，在调用then方法的时候作为参数传

到函数里面。而且因为这个对象会被当做promisi对象，return关键字可以替换成await。

**21.class**

```js
class Point {
    constructor(x, y) {
        this.x = x;
        this.y = y;
    }

    toString() {
        return '(' + this.x + ', ' + this.y + ')';
    }
}
var a = new Point(1,2);
console.log(a.x);                      //1
console.log(a.toString());             //(1,2)
a.hasOwnProperty('x')                  // true
a.hasOwnProperty('y')                  // true
a.hasOwnProperty('toString')           // false
a.__proto__.hasOwnProperty('toString') // true
```

a是没有定义toString()方法的，所以从它的原型Point上调用此方法。

继承：extends关键字

```js
class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y);                                // 调用父类的constructor(x, y)
    this.color = color;
  }

  toString() {
    return this.color + ' ' + super.toString(); // 调用父类的toString()
  }
}
```

继承了父类的所有属性，也可以添加或者修改属性

**22.模块化**

```js
//lib.js
var counter = 3;
function incCounter() {
  counter++;
}
module.exports = {
  counter: counter,
  incCounter: incCounter,
};
```

这是一个js模块，对外暴露两个属性counter（变量）、incCounter（函数），然后再去加载这个模块

```js
// main.js
var mod = require('./lib');

console.log(mod.counter);  // 3
mod.incCounter();
console.log(mod.counter);  // 3
```

这样就可以去调用该模块对外暴露的属性了，



（我不怕千万人阻挡，只怕自己投降!）