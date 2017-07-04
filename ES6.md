# ES6

@(ES6)

#### 使用严格模式来书写ES6

### 箭头函数中没有this指向
```
"use strict"
```
### ES6定义变量
>用let 定义变量
>
>1.没有变量提升（预解释）
```
 console.log(a);//报错a is not defined
    let a=0;
 function fn() {
        console.log(a);//报错
        let a=0;
    }
```
>2.不能重复定义（报错已经声明过了）
```
let a=1;

let a=2//报错Identifier 'a' has already been declared

function a() {}//报错

function a(n) {
      let n=2;
      console.log(n);//报错
  };
```
>3.虽然不进行预解释但是代码执行之前会把let定义的变量过滤一遍，一旦不合法，就直接报错，代码也不执行了
```
  console.log(a);//报错（已经声明过了）
   let a=1;
  let a=2;
   console.log(a);//报错（已经声明过了）
```

### ES6块级作用域
>用{ }括起来的是私有作用预，叫块级作用域
```
 "use strict";
    let a=10;
    if(a){
        console.log(a);//报错a is not defined
       let a=1;
        console.log(a);//1
    }
    console.log(a);//10
```
>如果括号里没有声明的该变量，就会向上找，括号里面的给外面的变量修改依然有效
```
		  
```
>因为在ES6括号是私有作用域，所以下面的循环里面，循环一次就会形成一个私有作用域。（不必用自定义存储和闭包保护）
```
 "use strict";
for(let i=0;i<oLis.length;i++){
        oLis[i].onclick=function () {
            console.log(i);//输出：0，1，2，3
        }
    }
```

### ES6自执行函数
>写法
```
 "use strict";
    {
        let a;
        console.log(a);
    }	
```

### const 定义静态变量
>不能修改值，必须要赋值
```
 "use strict";
  const a=10;
    a=20;
    console.log(a);//报错
	    
const a,//报错 没有赋值
```
>在同一个作用域不能重复定义（不同作用域可以）
```
const a=10;
const a=20;
console.log(a);//报错
```
>不同作用域可以重复赋值
```
 const a=10;
    console.log(a);//10
    if(a){
        const a=20;
        console.log(a);//20
    }
    console.log(a);//10
```

## 数组解构赋值
```
    "use strict";
   let [a,b,c]=[1,2,3];
    console.log(a,b,c)//1,2,3
```
```
 "use strict";
var ary=[1,2,3,4,5,6];
    let[a,b,c]=ary;
    console.log(a,b,c)//1,2,3
```
```
 "use strict";
var ary=[1,2];
    let[a,b,c]=ary;
    console.log(a,b,c)//1,2,undefined
```

### 1.嵌套赋值
```
"use strict";
    let [x,y,[s],[[f]]]=[1,2,[3],[[4]]];
    console.log(x,y,s,f);//1,2,3,4
```

### 2.省略赋值
```
"use strict";
var ary=[1,2,3,4,5]
    let [a,,,b]=ary;
    console.log(a, b);//1,4
 var ary=[1,2];
    let[a,,,b]=ary;
    console.log(a, b);//1,undefined
```
### 3.不定赋值
```
"use strict";
let [a,...b]=[1,2,3,4,5];
 console.log(a, b);//a=1,b=[2,3,4,5]
```

### 对象赋值
>1.变量名必须和属性名一样
```
"use strict";
  let obj={
        n1:"p1",
        n2:"p2"
    };
    let {n1,n2}=obj;
    console.log(n1, n2);
```
>2.如果不想变量名和属性名一样
```
"use strict";
 let {n,m:m1}={n:"1",m:"11"};
    console.log(n, m1);//1,11
```
>3.空对象，null，undefined
```
"use strict";
let {a,b}={};
console.log(a, b);//undefined,undefined
```
>4.赋的值是其他数据类型（不是一个对象）
```
let {x,y,z}=1;
console.log(x,y,z)//undefined,undefined,undefined
```


### 对象数组嵌套

```
"use strict";
  var obj={a1:[1,2,3],a2:"123"};
    let {a2,a1:[x,y]}=obj;
    console.log(a2, x, y);	//123,1,2
```

```
"use strict";
 var obj1={s:{n:"1"},n:[1,"2",3,"4"],m:[[1]]};
    let {m:[a1],s:{n},n:[,...a3]}=obj1;
console.log(a1, n, a3);//[1],"1",["2",3,"4"]
```

### 默认值

```
"use strict";
let [x="1",y="2",z="3"]=[,2,3];
console.log(x, y, z);//"1",2,3
```
```
"use strict";
let {x1:x="x",y="y",z="z"}={x1:"rx",z:"rz"};
    console.log(x, y, z);//"rx","y","rz"
```

### 默认参数
```
"use strict";
 function fn(x=1,y=2) {
        console.log(x + y);//"12"
    }
    fn("1");
```

```
"use strict";
 function fn1([x,,,,y]) {
        console.log(arguments[0].length);//5
        console.log(x, y);//1,4
    }
    fn1([1,2,3,4,5])
```

```
"use strict";
function fn2({x,y}={x:1,y:2}) {
       console.log(x, y);
   }
   fn2();//1,2
   fn2({});//undefined,undefined
   fn2(1);//undefined,undefined
```

```
"use strict";
function fn3({x=1,y=2}={}) {
     console.log(x+y);
 }
 fn3();//3
    fn3({});//3
 fn3({x:"1"})//"12"
```

```
"use strict";
function fn4(x=1,y=2,z=3) {
     console.log(x, y, z);
 }
 fn4(10,undefined,30);//10,2,30
 fn4(10,null,30)//10,null,30
```

```
"use strict";
function fn5(...others) {
     console.log(arguments);
     console.log(others);(将类数组转为数组)
 }
 fn5(1,2,3,4,5)
```
>参数所在的作用域是私有的作用域
```
"use strict";
let a=1;
function fn6(n,m=a) {
    let a=0;
    console.log(m);//1
}
fn6(1)
```
```
"use strict";
function fn6(n,m=a) {
    let a=0;
    console.log(m);
}
fn6(1)//报错
```

```
"use strict";
let [x,y,z,m]=[1,2,3,4];
function fn7(x,y,z=x+m) {
    let m=2;
    console.log(x, y, z, m);//10,20,14,4
}
fn7(10,20);
```

### 扩展运算符（...[]）
>扩展运算符可以在传参数的时候使用，可以在任何位置使用，
```
"use strict";
var num=[1,2,3,4,5];
   function fn1(x,y) {
       let sum=x+y;
       console.log(sum);//3
   }
   fn1(...num);
```
>可以代替apply使用
```
"use strict";
let ary=[1,2,3];
   var max=Math.max.apply(null,ary);
    console.log(max);//3
    
    var max=Math.max(...ary);
    console.log(max);//3
```
>拼接
```
"use strict";
 var ary=[1,2];
    var ary1=[2,4];
   console.log(ary.concat(ary1));//[1,2,2,4]
   
  let ary2=[...ary,...ary1];,
    console.log(ary2);//[1,2,2,4]
```
>字符串转为数组
```
 let str="123哈哈";
    console.log([...str].reverse().join(""));//哈哈321
```
>将类数组转为数组
```
function to() {
      return [...arguments]
  }
    console.log(to());//[]
```

### 箭头函数
>只要是匿名函数都可以写成箭头函数
>箭头函数其实就是匿名函数的一种简写方式
>如果箭头函数后面是一个{}，需要写return

```
 "use strict";
    let a=1;
普通匿名函数的写法：
    let fn=function (a) {
        return a;
    }
箭头函数的写法（一个参数）：
 let fn（变量）=a（形参）=>a（return出来的内容）;
 fn();
 箭头函数的写法（多个参数）：
 let fn=(a,b)=>a+b;
	 fn(1,2)//3
```
>例子：
```
普通函数：
function a(b){
    return function (d){
        return b+d
    }
}
箭头函数：
let a=b=>d=>b+d;
```
>可以通过箭头函数解决this指向问题
```
let obj={
   a:function(){
       setTimeout(()=>{
           console.log(this);
       })
   }
};
console.log(obj.a（）);//this 是obj
```

#### 箭头函数应用
>数组的方法
```
"use strict";
let ary=[1,3,5];
    ary=ary.map(item=>item+1);
          console.log(ary);//2,4,6
```
```
"use strict";
let ary=[1,3,5];
          console.log(ary.sort((a, b) => b-a));//[5,3,1]

```
### findIndex遍历数组
```
"use strict";
         console.log(ary.sort((a, b) => b-a));//[5,3,1]
          let ary=[1,3,5];
    var a=ary.findIndex(function (item,index,input) {
        return item===1
    });
          console.log(a);//索引0
```
>箭头函数的写法
```
"use strict";
 let ary=[1,3,5];
 var a=ary.findIndex(it=>it===1);
          console.log(a);//索引0
```

### 箭头函数this问题
>严格模式下，函数执行的时候前面没有点，this就是undefined
```
 "use strict";
    function fn() {
        console.log(this);
    }
    fn();
```
#####在箭头函数中的this默认就是window
>特殊情况：当箭头函数作为参数的时候，并且实在一个对象的某个属性值中，this就是这个对象。

|
>下面的例子中：输出this.a,this是window，因为箭头函数的this就是window，上面的let只是定义了一个变量，并不是给window下增加了一个属性，所以this.a是undefined。如果上面写的是window.a=1;this.a 输出1.
```
 "use strict";
 let a=1;
    let obj={
        a:"a",
        fn1:()=>{
            let a="aa";
            console.log(this.a);//undefined
            return a;
        },
        fn2:function () {
            window.setTimeout(()=>{
                console.log(this);
            },1000)
        },
        fn3:{
            a:"a3",
            fn:()=>this.a
        }
    };
    let fn1=obj.fn1;
    console.log(obj.fn1());//"aa"
    console.log(fn1());//"aa"
```

### 高阶函数

```
普通函数：
 "use strict";
    let fun=(a)=>{
        return (b)=>{
            return (c)=>{
                return a+b+c
            }
        }
    };
    fun(1)(2)(3);//6
    高阶函数：
    let fn=a=>b=>c=>a+b+c;
    fun(1)(2)(3)//6
```

### Symbol

```
"use strict";
let str1="1";
let str2="1";
console.log(str1 === str2);//true


let str1=Symbol("index");
let str2=Symbol("index");
console.log(str1 === str2);//false
```
>用法，添加自定义属性（这样添加下面的不会覆盖上面的）
```
"use strict";
  let oBox=document.getElementById("box");
 let str1=Symbol("index");
 let str2=Symbol("index");
    oBox[str1]=5;
    oBox[str2]=6;
    console.dir(box);
    console.log(oBox[str1] === oBox[str2]);//false
```

### 字符串
>includes()： 
>判断字符串中有没有指定字符，有返回true，没有返回false。第二个参数是开始查找的索引，默认是0。
```
 "use strict";
    let str="abcde";
    str.indexOf("a");//0
    str.includes("a");//true
    str.includes("a",2);//false
    str.includes("A");//false
```
>startsWith()：
>判断是不是以某个字符作为开头
```
"use strict";
let str="abcde";
str.startsWith("a");//true
```
>endsWith()：
>判断是不是以某个字符作为结尾
```
"use strict";
let str="abcde";
    str.endsWith("e");//true

```
>repeat()：
>将字符串重复n次返回，原字符串不变
```
"use strict";
let str="abcde";  console.log(str.repeat(2));//abcdeabcde
```

### 模板字符串
>1.模板字符串中有特殊意义的是：``，$，{}
```
    "use strict";
    //123`${123}
    var str=`123\`\$\{123\}`;
    console.log(str);//123`${123}

let str=`123`${123}`;
    console.log(str);//报错
```
>2.插入变量
```
"use strict";
 let a=1;
 let str0=`123${a}`;
 console.log(str0);//1231
```
>3.换行符
```
"use strict";
  var str=`<div>\
<span>span1</span>\
<span>span2</span>\
</div>`;
    document.body.innerHTML=str;
    页面输出：span1span2（中间没有空格）
```
>4.插入表达式(里面也可以是判断)
```
"use strict";
function fn(a,b) {
    return a+b;
}
let str=`1+2=${fn(2,3)}`;
    console.log(str);//1+2=5
let str=`1+2=${true?"3":"5"}`;
```
>5.自动类型转换
```
"use strict";
let str=`${{A:"A"}}`;
console.log(str);//[object Object]

let str=`${[1,2]}`;
console.log(str);//1,2
```
>不知道什么玩意
```
    "use strict";
    let x="x";
    let y="y";
    let s=temp`${x}1${2}`;
    function temp(a,...b) {
        console.log(a);//["", "1", "", raw: Array(3)]
        console.log(b);//["x", 2]
    }
```