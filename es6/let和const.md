# let和const

### let

#### 不存在变量提升

```javascript
console.log(s)//undefind
var s;
console.log(y)//error
let y;
```

#### 暂时性死区（一个代码块中，不能在变量声明前使用变量）

```javascript
{
    console.log(y);//error
    let y;
}
```

#### 不允许重复声明

```javascript
var a=0;
let a=1;//error
let b=0;
let b=1;//error
```

#### 内层作用域可以定义外层作用域相同的变量
```javascript
let n=1;
{
    let n=2;    
}
```

### const

#### const声明一个常量，声明后不能更改

#### 声明的变量必须赋初值

#### 作用域与let相同

#### const定义的值不变是指const定义的变量指向的内存地址的指针不变，内存中保存的数据是可以变的

```javascript
const a={}
a.prop=123;
console.log(a.prop)//123
a={}//错误，指针指向的地址发生了变化
```

### 顶层对象

#### 使用var声明的全局变量在window对象下
```javascript
var a=1;
console.log(window.a)//1
```

#### 使用let声明的全局变量不在window下
```javascript
let a=1;
console.log(window.a)//undefind
```