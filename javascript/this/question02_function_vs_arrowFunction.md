## 普通函数 VS 箭头函数
箭头函数是es6新增的一种函数，使用起来更加简洁方便。
```js
//普通函数
function add(a,b){
  return a+b;
}

//箭头函数
const add = (a,b) => a+b
```  

这里主要讨论箭头函数与不同函数不同的地方，也是箭头函数的特性

### 1. 箭头函数的执行上下文中的this使用的是箭头函数所在环境（函数或者全局）的执行上下文中的this
普通函数中this值的四条绑定规则对于箭头函数并不生效。**箭头函数执行上下文中的this直接继承箭头函数所在环境执行上下文中的this。**

也就是说，**箭头函数的this值在声明函数的时候其实就可以确定下来了，和调用位置无关**。bind、call和apply方法对于箭头函数是**无效**的

```js
function foo(){
  return ()=>{
    console.log(this.a);
  }
}
var obj1={
  a:2
}
var obj2={
  a:3
}
var fn = foo.call(obj1);
fn.call(obj2);  //2 不是 3

var obj3={
  a: 4
}
var f = fn.bind(obj3);
f();  // 2 不是 4

var obj4={
  a: 5
}
fn.apply(obj2); // 2 不是 5
```  

### 2. 箭头函数不可以当做构造函数使用，使用new操作符会报错
```js
const Foo = ()=>{this.a = 23}
let f = new Foo(); // TypeError: Foo is not a constructor
```  

### 3. 箭头函数的执行上下文中不存在arguments对象，但是可以使用rest替代
```js
const foo=()=>{
  console.log(arguments);
}
foo(1,2,3,4); //ReferenceError: arguments is not defined

const foo1=(...rest)=>{
  console.log(rest);
}
foo1(1,2,3,4); //[1, 2, 3, 4]
```  

### 4. 箭头函数不能使用yield语句，不能作为Generator函数
因为箭头函数**没有function关键字**定义，所以无法定义成Generator函数  









