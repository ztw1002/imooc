### 学习方法

看千遍不如写一遍

### 学习内容

- ES6 是什么
- ECMAScript 是什么
- ECMAScript 的历史版本

- ECMAScript 的命名方式
- EVMAScript 与 JavaScript 的关系
- ES6 的兼容性

**（以上内容简单了解即可）**

- let 和 const 是什么
- let 、const 和 var 的区别
- let 和 const 的应用



### ES6

ECMAScript 是语言的标准，6是版本号
ECMAScript = 语法 + API（方法或函数）

### ES 与 JavaScript 的关系

- JavaScript（浏览器端）= ECMAScript（语法 + API）+ DOM + BOM



### let 和 const 

声明变量或常量

var、let声明变量
const 声明常量 constant

const声明的常量，允许在不重新赋值的情况下修改它的值（主要针对**引用数据类型**）

```javascript
<script>
    const person = {username:'Alex'};
    person.username = 'Mike';
    console.log(person)   //Mike
  </script>
```

实际开发中，不知道用什么可以先用 const

### let、const 和 var 的区别

1.**重复声明**：已经存在的变量或常量，又声明了一遍
var 允许重复声明，let、const 不允许

2.**变量提升**:var会提升变量的声明到当前作用域的顶部，let 和 const 不存在变量提升

3.**暂时性死区**：只要作用域内存在let、const，他们所声明的变量或常量就自动“绑定”这个区域，不再受到外部作用域的影响
let 和 const 存在暂时性死区

```javascript
let a = 2;
function func() {
  console.log(a);
  let a = 1;
}
func();
```

4.**window 对象的属性和方法**：全局作用域中，var 声明的变量，通过 function 声明的函数，会自动变成 window 对象的属性或方法，let 和 const 不会

5.**块级作用域（重要）**：var没有块级作用域，let 和 const 有块级作用域
作用域链：内层作用域->外层作用域->全局作用域

### let 和 const 的应用



HTML DOM **querySelectorAll()** 方法

```javascript
//获取文档中 class = "example"的所有元素：
var x = document.querySelectorAll(".example");
```



```javascript
//要求点击0号按钮时，打印出索引值0，1号打印出1，2号打印出2

//函数循环了3次，每次循环都给相应的按钮绑定了一个点击事件，这是事件处理函数

//分析循环的过程中作用域是怎样的：
//最外层是全局作用域，i = 3
//只有在函数被调用时，才存在函数作用域，没有调用函数就没有函数作用域，此时只有点击相应的按钮，才会调用相应的函数，形成函数作用域
//点击3个按钮会各自生成一个函数作用域

//结果打印出来的都是3
//1.var
    var btns = document.querySelectorAll('.btn');

    for (var i = 0; i < btns.length; i++) {
      btns[i].addEventListener(
        'click',
        function () {
          console.log(i);
        },
        false
      );
    }
```

一般使用闭包来解决相应的问题

```javascript
//2.闭包
var btns = document.querySeletorAll('.btn');

for(var i = 0; i < btns.length; i++) {
  (function (index) {
    btns[index].addEventListener(
    'click',
      function () {
      console.log(index);
    },
    false
    );
  })(i);
}
```

<img src="https://i.loli.net/2021/09/07/jmxHYJ7GV9DZE3I.png" alt="image-20210906155206125" style="zoom: 67%;" />

```javascript
//3. let/const
let btns = document.querySelectorAll(".btn");
	for(let i = 0; i < btns.length; i++) {
    btns[i].addEventListener(
    'click',
    function () {
      console.log(i);
    },
    false
    );
  }
```

<img src="https://i.loli.net/2021/09/07/714MJnhNPAdVKoZ.png" alt="image-20210906162722158" style="zoom:67%;" />

块级作用域

<img src="https://i.loli.net/2021/09/07/sjQmC6oHpyRPTaL.png" alt="image-20210906163237615" style="zoom:67%;" />



## 模板字符串

```javascript
//2个反引号
const username = `alex`
```

模板字符串与一般字符串的区别

```javascript
// 一般字符串
const person = {
  username:'Alex',
	age:18,
	sex:'male'
};

const info = '我的名字是：'+person.username+'，性别：'+person.sex+'今年'+person.age+'岁了';
console.log(info);
```

```javascript
// 模板字符串
const info = `我的名字是：${person.username},性别：${person.sex},今年${person.age}岁了`;
console.log(info);
```

模板字符串中，所有的空格、换行或缩进都会被保留在输出之中

2.输出 ` 和 \ 等特殊字符

```javascript
const info = `\`
```

3.模板字符串的注入:${}

```javascript
const username = 'alex';
const person = {age:18, sex:'male'};
const getSex = function {sex} {
  return sex === 'male'?'男':'女';
};

const info = `${username},${person.age+2},${getSex(person.sex)}`;
console.log(info);
```

**只要最终可以得出一个值得就可以通过 ${} 注入到模板字符串中**



### 案例：模板字符串的应用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
</head>
<style>
  body {
    padding: 50px 0 0 300px;
    font-size: 22px;
  }

  ul {
    padding: 0;
  }

  p {
    margin-bottom: 10px;
  }
</style>
<body>
  <p>学生信息表</p>
  <ul id="list">
    <li style="list-style:none;">信息加载中......</li>
  </ul>
  <script>
    //数据
    const students = [
    {username:'Alex',
      age: 18,
      sex:'male'
    },
    {
      username:'ZhangSan',
      age:28,
      sex:'male'
    },
    {
      username:'LiSi',
      age: 20,
      sex:'female'
    },
    ];
    
    const list = document.getElementById('list');

    let html='';

    for(let i = 0; i < students.length; i++) {
      html += `<li>我的名字是：${students[i].username},${students[i].sex},${students[i].age}</li>`;
    }
    list.innerHTML = html;
  </script>
</body>
</html>
```



## 箭头函数

```javascript
const add = (x,y) => {
  return x + y;
};

console.log(add(1,1));
```

**2.箭头函数的结构**

```javascript
const/let 函数名 = 参数 => 函数体
```

**3.如何将一般函数改写成箭头函数**

```javascript
//声明形式
function add() {}

//声明形式 -> 函数表达式形式
const add = function () {};

//函数表达式形式 -> 箭头函数
const add = function() {};
```

**箭头函数的注意事项**

- 单个参数 :可以省略圆括号。。无参数或者多个参数不能省略圆括号
- 单行函数体：可以省略 {} 和 return。必须同时去除。。**多行函数体不能简化**

- 单行对象：

```javascript
const add = (x, y) => ({
  value:x + y
});

console.log(add(1,1));

//如果箭头函数返回单行对象，可以在{}外面加上()，让浏览器不再认为那个是函数体的花括号
```



## this 指向

- 全局作用域中的 this 指向

```javascript
console.log(this);		// window
```

- 一般函数（非箭头函数）中的 this 指向

```javascript
function add() {
  console.log(this);
}

add();		//undefined -> window(非严格模式下会转成window)
// window.add();
//上面只是函数的声明，只有在函数调用的时候 this 指向才确定，不调用的时候，不知道指向谁
//this 指向和函数在哪儿调用没关系，只和谁在调用有关
```

```javascript
const calc = {
  add:add
};
calc.add();			//指向calc对象

const adder = calc.add;
adder();				//指向undefined，非严格模式下转成window

```

```javascript
document.onclick = function () {
  console.log(this);		//指向document
};

document.onclick();
```

```javascript
function Person(username) {
  this.username = username;
  console.log(this);
}

const p = new Person('Alex');
//构造函数中的this 指向的是构造函数实例化之后生成的那个对象
```

**箭头函数中的 this 指向**

箭头函数没有自己的 this

```javascript
const calc = {
  add:() => {
    console.log(this);
  }
};

calc.add();		// window
```



练习：

```javascript
const calc = {
  add:function () {
    const adder = () => {
      console.log(this);
  };
  adder();
	}
};

calc.add();		//calc
```

```javascript
const addFn() = calc.add;
addFn();		// undefined -> window
```



### 不适用箭头函数的场景

- 作为构造函数

- 需要 this 指向调用对象的时候
- 需要使用 arguments 的时候

arguments：主要作用：记录传进来了什么参数



### 箭头函数的应用

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        body{
            padding: 50px 0 0 250px;
            font-size: 30px;
        }

        #btn {
            width: 100px;
            height: 100px;
            margin-right: 20px;
            font-size: 30px;
            cursor: pointer;
        }
    </style>
</head>
<body>
    <button id="btn">开始</button>
    <span id="result">0</span>

    <script>
        const btn = document.getElementById('btn');
        const result = document.getElementById('result');

        const timer = {
            time:0,
            start:function(){
                btn.addEventListener(
                    'click',
                    () => {
                    setInterval(() => {
                        this.time++;
                        result.innerHTML = this.time;
                    },1000);
                },
                false
            );
        }
    };
        timer.start();
    </script>
</body>
</html>
```

### 总结

#### 模板字符串

- 使用反引号
- 通过${值}注入
- 空格、换行或缩进都会被保留在输出之中
- 特殊字符需要通过 \ 转义



#### 箭头函数是什么

- 函数的函数的一种简化形式
- 箭头函数的结构：const/let 函数名 = 参数 => 函数体
- 改写成箭头函数：声明形式 -> 函数表达式形式 -> 箭头函数

#### 箭头函数的注意事项

- 单个参数可以省略圆括号
- 单行函数体可以同时省略 {} 和 return
- 函数体是单行对象，省略 {} 和 return 后，需要在对象 {} 外面加上 ()

#### 非箭头函数中的 this 指向

- 全局作用域中的 this 指向 window
- 函数中的 this，只有所在函数被调用的时候，才有明确的指向
- this 指向调用其所在函数的那个对象
- 没有具体调用对象，this 指向 undefined ，在非严格模式下，转向window

#### 不适用箭头函数的场景

- 不适合作为构造函数

- 不适合需要 this 指向调用对象的时候
- 不适合需要使用 arguments 的时候



## 解构赋值

数组的解构赋值

**原理、应用是重点**，注意事项

对象的解构赋值

其它数据类型的解构赋值



### 数组的结构赋值

认识解构赋值

```javascript
const [a,b,c] = [1,2,3];
        console.log(a,b,c);
        // 解析某一数据的结构，将我们想要的东西提取出来，赋值给变量或常量
```

#### 数组结构赋值的原理

- 模式（结构）匹配
- 索引值相同的完成赋值

```javascript
const [a,b,c] = [1,2,3];
console.log(a,b,c);
```

```javascript
const [a, [,,b],c] = [1,[2,4,5],3];			//取到1 5 3
```









## 剩余参数 与 展开运算符

剩余参数

```javascript
//1.认识剩余参数
const add = (x,y,z, ...args) => {};
```

```javascript
//2.剩余参数的本质
const add = (x,y, ...args) => {
  console.log(x,y,args);
};
add(1,2,3,4);
//剩余参数永远是个数组，即使没有值，也是空数组
```

![image-20210906164414202](https://i.loli.net/2021/09/07/tuNiJxyzlqDpFU5.png)

注意事项：

1.箭头函数的剩余参数
箭头函数的参数部分即使只有一个剩余参数，也**不能省略圆括号**

```javascript
const add = (...args) => {};
```

2.使用剩余参数替代 arguments 获取实际参数

```javascript
/*const add = function() {
  console.log(arguments);
};
add(1,2);
*/

const add = (...args) => {
  console.log(args);
};
add(1,2);
```

3.剩余参数的位置：剩余参数只能是**最后一个参数**，之后不能再有其他参数，否则会报错

### 剩余参数的应用

```javascript
//1.add方法
const add = (...args) => {
  let sum = 0;
  
  for (let i = 0; i < args.length; i++) {
    sum += args[i];
  }
  
  return sum;
};
```

```javascript
//2.与解构赋值结合使用（剩余参数不一定非要作为参数函数使用）
```



## 数组展开运算符的基本用法

```javascript
    //1.认识展开运算符
    //[3,1,2] -> 3,1,2

    //2.数组展开的基本用法
    // console.log(Math.min(...[3,1,2]));
    //相当于 console.log(Math.min(3,1,2));
```



### 区分剩余参数 和 展开运算符

根本区别：

- 展开运算符：[3,1,2] -> 3,1,2
- 剩余参数：3,1,2 -> [3,1,2]



### 数组展开运算符的应用

1.复制数组

```javascript
const a = [1,2];
const c = [...a];
console.log(c);
```

2.合并数组

```javascript
const a = [1,2,3];
const b = [4,5];
const c = [6,7,8];

console.log(...a,...b,...c);
```

3.字符串转为数组：字符串可以按照数组的形式展开

```javascript
console.log(...'Alex');
//A l e x
```

4.常见的类数组转化为数组

```javascript
function func() {
  //console.log(arguments.push);
  console.log([...arguments]);
}
func(1,2);
```

```javascript
//Nodelist
//console.log(document.querySelectorAll('p'));
console.log(...document.querySelectorAll('p').push);
```



### 对象展开运算符

```javascript
//1.展开对象：把属性罗列出来，用逗号分隔，放到一个{}中，构成新对象
//对象不能直接展开，必须在{}中展开
    const apple = {
      color:'红色',
      shape:'球形',
      taste:'甜'
    };
    console.log({...apple})
```

```javascript
//2.合并对象
//新对象拥有全部属性，相同属性，后者覆盖前者
    const apple = {
      color:'红色',
      shape:'球形',
      taste:'甜'
    };

    const pen = {
      color:'黑色',
      shape:'圆柱形',
      use:'写字'
    };

    console.log({...pen, ...apple});
```

**对象展开运算符的注意事项**

1.空对象的展开：如果展开一个**空对象，则没有任何效果**
2.非对象的展开：如果**展开的不是对象，则会自动将其转为对象，再讲其属性罗列出来**
							  如果展开运算符后面是字符串，它会自动转成一个类似数组的对象，因此返回的不是空对象

```javascript
console.log({...'alex'});
console.log([...'alex']);
console.log(...'alex');
```

3.对象中的对象 属性的展开：**不会展开对象中的对象属性**



对象展开运算符的应用

1.复制对象

```javascript
const a = {x:1, y:2};
const c = {...a};
console.log(c);
```

2.用户参数和默认参数

```javascript
const logUser = userParam => {
  const defaultParam = {
    username:'Zhangsan',
    age:'0',
    sex:'male'
  };
  
  const {username, age, sex} = {...defaultParam, ...userParam};
  console.log(username, age, sex);
};
```



### 总结

**剩余参数**
...剩余参数名
剩余参数是数组
1,2 -> [1,2]

箭头函数中使用剩余参数时，不能省略圆括号
可以使用剩余参数替代 arguments 获取实际参数
剩余参数只能是最后一个参数

**数组的展开运算符**
...[]
[1,2] -> 1,2

**对象的展开运算符**
{...{}}
对象只能在 {} 中展开
展开对象时，把属性罗列出来，用逗号分隔，放到一个 {} 中，构成新对象



## SET

一系列无序、没有重复值的数据集合
Set 没有下表去标示每一个值，所以 Set 是无序的，也不能像数组那样通过下表去访问 Set 的成员

```javascript
//只能通过实例化构造函数创建SET
//console.log(new Array(1,2,1))

const s = new Set();

//add方法每次只能添加一个成员
s.add(1);
s.add(2);
console.log(s);
```

### Set 实例的方法和属性

```javascript
		// 1.方法
    // add
    // const s = new Set();
    // s.add(1).add(2);

    // has
    // console.log(s.has(1));

    // delete
    // s.delete(1);

    // clear
    // s.clear();

    // forEach
    // s.forEach(function (value, key, set){
    // Set 中 value = key
    // });

    // console.log(s);
    // 按照成员添加进集合的顺序遍历

    // 2.属性
    // size
      // console.log(s.size);
```

### Set 构造函数的参数

```javascript
    // 1.数组
    // const s = new Set(1,2,1);
    // console.log(s);

    // 2.字符串、arguments、NodeList、Set 等
    // console.log(new Set('hi'));
    // function func(){
    //   console.log(new Set(arguments));
    // }
    // func(1,2,1);
    // console.log(new Set(document.querySelectorAll('p')));

    // Set还可以作为参数传到新的构造函数中
    // const s = new Set([1,2,1]);
    // console.log(new Set(s));
    // console.log(s);
```

### Set 的注意事项

- 判断重复的方式（===）

```javascript
const s = new Set([1,2,1]);
const b = new Set([NaN,2,NaN]);		// Set 中 NaN 等于 NaN
```



- **什么时候使用 Set**

1.对数组和字符串去重的时候
2.不需要通过下标访问，只需要遍历时
3.为了使用 Set 提供的方法和属性时（add delete...）

### Set 的应用

```javascript
// 1.数组去重
// [1,2,1]
const s = new Set([1,2,1]);
console.log(...s);

// 2.字符串去重
// 'abbaadlcccddsdsad'
console.log([...new Set('abbaadlcccddsdsad')].join(''));		//adblcs

// 3.存放 DOM 元素
<body>
  <p>1</p>
  <p>2</p>
  <p>3</p>
  <script>
    const s = new Set(document.querySelectorAll('p'));
    console.log(s);
    s.forEach(function(elem) {
      elem.style.color = 'red';
      elem.style.backgroundColor = 'yellow';
    });
  </script>
</body>
```

## Map

Map 和对象都是**键值对的集合**

```javascript
const m = new Map();
m.set('name','alex');
m.set('age', 18);
console.log(m);

//2.Map 和对象的区别
//对象一般用字符串当作键
const obj = {
  name:'alex',
  true:'true',
  [{}]:'object'
};
```

基本数据类型：数字、字符串、布尔值、undefined、null
引用数据类型：对象（[]、{}、函数、Set、Map等）
以上都可作为 Map 的键

```javascript
const m = new Map();
m.set('name','alex');
m.set(true,'true');
m.set({},'object');
m.set(new Set([1,2]),'set');
m.set(undefined, 'undefined');
console.log(m);
```

### Map 实例的方法和属性

- 方法

```javascript
//向 Map 中添加成员
//set
	const m = new Map();
//使用 set 添加的新成员，键如果已经存在，后添加的键值对 会覆盖已有的
	m.set('age',18).set(true,'true').set('age',20);
	console.log(m);

//get：获取指定成员
console.log(m);
console.log(m.get('age'));
console.log(m.get('true'));
console.log(m.get(true));

// has：判断有没有指定的键，是布尔值
//console.log(m.has('age'));
//console.log(m.has('true'));

// delete：删除键
//m.delete('age');
//m.delete('name');

// clear：清空
//m.clear();

// forEach
//m.forEach(function(value, key, map){
//		console.log(this);
//},document);
```





- 属性

size：对象中有几个键值对

### Map 构造函数的参数

- 数组

```javascript
console.log(new Map([
  ['name','alex'],
  ['age',18]
])
);
```

- Set、Map

```javascript
//Set 中也必须体现出键和值
const s = new Set([
  ['name','alex'],
  ['age',18]
]);
console.log(new Map(s));
console.log(s);

//Map   此处复制了一个新的 Map
const m1 = new Map([
  ['name','alex'],
  ['age',18]
]);
console.log(m1);
const m2 = new Map(m1);
console.log(m2, m2 === m1);		// false
```

### Map 的注意事项

- **什么时候使用 Map**
  - 只需要 key -> value 的结构，或者需要字符串以外的值做键，使用 Map 更合适
  - forEach for in
  - size

- 只有模拟现实世界的实体时，才使用对象
  - const  person = {};

### Map 的应用

```javascript
<body>
  <p>1</p>
  <p>2</p>
  <p>3</p>
  <script>
     const [p1,p2,p3] = document.querySelectorAll('p');
    // const m = new Map;
    // m.set(p1,'red');
    // m.set(p2,'green');
    // m.set(p3,'blue');
    // console.log(m);
    const m = new Map([
      [p1,'red'],
      [p2,'green'],
      [p3,'blue']
    ]);

    m.forEach((color,elem) => {
      elem.style.color = color;
    });
    console.log(m);
  </script>
</body>
```

### 总结

Set 是一系列无序、没有重复值得数据集合

Map的本质是键值对的集合

**Set/Map 构造函数的参数**

Set：数组、字符串、arguments、NodeList、Set等

Map：数组......



## 遍历器 与 for 循环

Iterator：遍历器（迭代器），类似for循环，和 forEach 方法。Iterator 也是用来遍历的

```javascript
    // 使用 Iterator
    // it：可遍历对象（可迭代对象）
    // Symbol/iterator：可遍历对象的生成方法

    // 什么是 Iterator
    // Symbol.iterator （可遍历对象的生成方法） -> it（可遍历对象）-> it.next() -> it.next() -> （直到done为true）
    const it = [1,2][Symbol.iterator]();
    console.log(it.next());   //{value:1,done:false}
    console.log(it.next());   //{value:1,done:false}
    console.log(it.next());   //{value:undefined,done:true}
    console.log(it.next());   //{value:undefined,done:true}
```

为什么需要 Iterator 遍历器：Iterator 遍历器是一个**统一的遍历方式**

```javascript
console.log([][Symbol.iterator]());
```

**如何更方便滴使用Iterator**：我们一般不会直接使用 Iterator 去遍历，而是使用 Iterator 封装好的东西



**for...of**

```javascript
//for...of循环只会遍历出那些 done 为 false 时，对应的 value 值
const arr = [1,2,3];
for(const item of arr) {
  console.log(item);
}
```

```javascript
//for...of 与 break、continue 一起使用
const arr = [1,2,3];
for (const item of arr) {
  if (item === 2){
    break;
    //continue;
  }
  console.log(item);
}
```

```javascript
//3.在for...of 中取得数组的索引
const arr = [1,2,3];

// keys()得到的是索引的可遍历对象，可以遍历出索引值
console.log(arr.keys());
for (const key of arr.keys()) {
  console.log(key);
}
for (const value of arr) {
  console.log(value);
}

// entries() 得到的是索引+值组成的数组可遍历对象
for (const entries of arr.entries()) {
  console.log(entries);
}
```



什么是可遍历：只要有 Symbol.iterator 方法， 并且这个方法可以生成可遍历对象，就是可遍历的
只要可遍历就可以使用 for...of 循环来统一遍历



原生可遍历的有哪些

- 数组，字符串，Set，Map，arguments，NodeList

- - 遍历NodeList：

```javascript
for (const elem of document.querySelectorAll('p')) {
  console.log(item);
  elem.style.color = 'red';
}
```

非原生可遍历：一般的对象



**使用了 Iterator 的场合**

- 数组的展开运算符

```javascript
console.log(...[1,2,3]);
console.log(...new Set([1,2,3]));
```

- 数组的解构赋值

```javascript
const [a,b] = [1,2];

const [a,b] = [...new Set([3,4])];
console.log(a,b);
```

- Set 和 Map 的构造函数

```javascript
new Set(iterator)
new Map(iterator)
```



### 总结

**for...of**

- 在for...of中可以通过 keys() 或 entries() 取得数组的索引



## ES6 的新增方法

### 字符串

- includes()：判断字符串中是否含有某些字符
  - 第二个参数：表示默认开始的位置，默认是0

```javascript
console.log('abc'.inculde('a'));		// true
console.log('abc'.include('a',1));	// false
console.log('abc'.include('ac'));		// false
```

- **padStart()、padStart()：补全字符串长度**

```javascript
console.log('x'.padStart(5,'ab'));		//ababx
console.log('x'.padEnd(4,'ab'));			//xaba
```

注意事项：原字符串的长度，等于或大于最大长度，不会消减原字符串，字符串补全不生效，返回原字符串
					如果省略第二个参数，默认使用空格补全长度

```javascript
console.log('xxx'.padStart(2,'ab'));
```

### 应用：显示日期格式

```javascript
//2020-10-10
//2020-01-01

console.log('10'.padStart(2,0));
console.log('1'.padStart(2,0));
```

- trimStart()、trimEnd()：去除**字符串首部或尾部的空格**

应用：表单提交

```javascript
const usernameinput = document.getElementById('username');
    const btn = document.getElementById('btn');

    btn.addEventListener(
      'click',
      () => {
        console.log(usernameinput.value);
        //验证
        if (usernameinput.value.trim() !=='') {
          //可以提交
          console.log('可以提交');
        } else {
          //不能提交
          console.log('不能提交');
        }
        //手动提交
      },
      false
      );
```

### 数组的 includes() 方法

```javascript
//判断数组中是否含有某个成员
console.log([1,2,3].includes('2'));			//false
console.log([1,2,3].includes(2));				//true

//第二个参数表示搜索的起始位置
```

```javascript
//应用：对数组进行去重
const arr = [];
for (const item of [1,2,1]) {
  if(arr.includes(item)) {
    arr.push(item);
  }
}
	console.log(arr);
```

### Array.from()

将其他数据类型转换成数组

1.基本用法

```javascript
console.log(Array.from('123456'));
```

2.哪些可以通过 Array.from() 转换成数组

	2.1所有可遍历的：数组、字符串、Set、Map、NodeList、arguments

```javascript
console.log(Array.from(new Set([1,2,1])));

//推荐使用展开
console.log([...new Set([1,2,1])]);
```

	2.2拥有 length 属性的任意对象

```javascript
const obj = {
  '0':'a';
  '1':'b',
  length: 2
};

console.log(Array.from(obj));
```

3.第二个参数

作用类似于数组的 map 方法，用来对每个元素进行处理，将处理后的值放入返回的数组

```javascript
console.log(
[1,2].map(value => {
  return value * 2;
})
);
console.log(Array.from('12',value => value * 2));
console.log(Array.from('12').map(value => value * 2));
```

4.第三个阐述

修改 this 指向



### find() 和 findIndex()

find()：找到满足条件的一个立即返回

findIndex()：找到满足条件的一个，立即返回其索引

```javascript
console.log([1,5,10,15].find((value, index, arr) => {
  //console.log(value, index, arr);
  return value > 9;
	})
);
//返回具体的值


console.log([1,5,10,15].findIndex((value, index, arr) => {
  //console.log(value, index, arr);
  return value > 9;
	})
);
//返回具体的值对应的索引
```



### Object.assign()

1.基本用法

```javascript
Object.assign(目标对象,源对象1，源对象2,...):目标对象
```



Object.assign 直接合并到了第一个参数中，返回的就是合并后的对象

```javascript
//用来合并对象
const apple = {
  color:'红色';
  shape:'圆形',
  taste:'甜'
};

const pen = {
  color:'黑色';
  shape:'圆柱形';
  use:'写字'
};
```

```javascript
// 可以合并多个对象
console.log(Object.assign({}, apple, pen));
```

**注意事项**

1.基本数据类型作为源对象，与对象的展开类似，先转换成对象，再合并

```javascript
console.log(Object.assign({}, undefined));
```

2.同名属性的替换（后面的覆盖前面的）

```javascript
const apple = {
  color:['红色','黑色'],
  shape:'圆形',
  taste:'甜'
};

const pen = {
  color:['黑色','银色'],
  shape:'圆柱形';
  use:'写字'
};

console.log(Object.assign({}, apple, pen));
```



**应用：合并默认参数和用户参数**

```javascript
const logUser = useroptions => {
  const DEFAULTS = {
    username:'ZhangSan',
    age:0,
    sex:'male'
  };
  
  const options = Object.assign({}, DEFAULTS, userOptions);
  console.log(options);
};
logUser();
```



### Object.keys()、Object.values()、Object.entries()

键、值、键+值

```javascript
const person = {
  name:'alex';
  age:18
};

console.log(Object.keys(person));
console.log(Object.values(person));
console.log(Object.entries(person));
```

与数组类似方法的区别（不记混就行）

1.数组的 keys()、values()、entries()等方法是实例方法，返回的都是 Iterator
   对象的 Object.keys()、Object.value()、Object.entries() 等方法是构造函数方法，返回的是数组

**使用for...of循环遍历对象**

```javas
const person = {
	name:'alex',
	age:18
};

for (const [key, value] of Object.entries(person)) {
	console.log(key, value);
}
```

但是 Object.keys()/values()/entries()并不能保证顺序一定是你看到的样子，这一点和 for in 是一样的

### 总结

#### 字符串

includes(要查找的字符[, 开始查找的位置=0]): 布尔值

```javascript
'abc'.includes('bc',1);		//true
```

trimStart/trimEnd():最终字符串

```javascript
'a b c'.trimStart();	//‘a b c '
'a b c'.trimEnd();		//' a b c'
```

padStart/padEnd(目标长度[, 要填充的字符串=空格]):最终字符串

```javascript
'x'.padStart(4,'ab');		//abax
'x'.padEnd(4,'ab');			//xaba
```



#### 数组

includes(要查找的值[, 开始查找的位置=0]): 布尔值

```javascript
[1, 2, NaN].includes(NaN, 1);		//true
```

find(回调函数[, this 指向]):满足条件的第一个值或 undefined

```javascript
[1,4,-5,10].find(n => n < 0, document);		// -5
```

findIndex(回调函数[, this 指向]):满足条件的第一个值的索引或 -1（找不到）

```javascript
[1,4,-5,10].findIndex(n => n < 0,document);		// 2
```



Array.from()

```javascript
Array.from('123', x=> x * x, document);		// [1,4,9]
```

可遍历对象可以通过 Array.from 转换成数组
拥有length属性的对象可以通过 Array.from 转换成数组



#### 对象

Object.keys(对象)：key 数组/value数组/key, value二维数组

```javascript
Object.keys({name:'Alex', age: 18});	//["name","age"]
```



Object.assign()：用来合并对象（合并用户参数和默认参数）

```javascript
//Object.assign(目标对象[, 源对象...]):目标对象
	Object.assign({}, undefined, {color:'red'});		//{color:"red"}
//方法的返回值就是这个目标对象，而这个目标对象是会被修改的，一般的做法是在第一个对象位置上传一个空的对象
//源对象可以传任意个，合并流程是从右往左
```

基本数据类型作为源对象，先转换成对象，再合并
合并对象时，对于同名属性，后面的覆盖前面的