# JavaScript编程风格

命名风格遵循JavaScript的规范。特别是命名风格。统一了大家协作互相调用的时候才不会出现拼写错误。并且好的编程风格可以有助于写出质量更高，错误更少，易于维护的程序。使代码更清晰易懂。

- 缩进使用4个空格；
- 结尾不写分号；
- 字符串使用单引号；
- 尽量用async/await而不用then；
- 使用let/const而不用var，优先用const；
- 尽量用forEach/map/filter/reduce/every/some而不用for循环；
- 尽量用includes而不用indexOf；
- 尽量用模板字符串而不用字符串拼接；
- 回调使用箭头函数以免污染this；
- 对变量进行判空，即判断是否为0/''/undefined/null/false时，都可以简单地使用 `!value` ；
- ES6默认为严格模式，因此无需再显式写出严格模式`"use strict"`；
- 避免使用String一类的原始包装类型创建新的对象；
- 避免使用eval()、Function构造器、with语句；
- 避免在字符串末尾使用斜线另起一行；
- 避免使用科学计算法或八进制直接量表示数字；
- Promise用bluebird版本；
- 简单的工具函数去lodash里面找（比如数组乱序，groupBy等）
- 数组浅拷贝使用扩展运算符`newItems = [...items]`
- 不要手动敲空格调整格式，应该用编辑器的格式化快捷键


## 一、表示语句块起首的大括号，不单独占一行

## 二、留白
在逻辑相关的代码之间添加空行代码可以提高代码的可读性。
**两行空行**仅限于在如下情况下使用：
- 在不同的源代码文件之间。
- 在类和接口定义之间。

**单行空行**仅限在如下情况中使用。
- 方法之间。
- 方法中局部变量和第一行语句之间。
- 方法中逻辑代码块之间以提升代码的可读性。

**空格**应当在如下的情况下使用。
- 关键词后跟括号的情况应当用空格隔开，匿名函数的function与圆括号之间不应有空格。
- 参数列表中逗号之后应当保留一个空格。
- 所有的除了点(.)之外的二元运算符，其操作数都应当用空格隔开。
- 单目运算符的操作数之间不应该用空白隔开，例如一元减号，递增(++)，递减(--)。
- for 语句的表达式之间应当用空格隔开。
- 圆括号与参数之间不应有空格。

按照上面的规则，下面的写法都是不规范的：
```javascript
foo (bar)
return(a+b)
if(a === 0){...}
function foo (b){...}
function(x){...}
for (var i=0; i<count; i++) {...}
for ( let i = 0; i < count; i++ ) {
    process( i )
}
object.method = function () {...}
```

## 三、使用严格相等（ === ）和严格不相等（ !== ）
因为“相等”运算符会自动转换变量类型，造成很多意想不到的情况：
```javascript
0 == "" //true
1 == true //true
2 == true //false
0 == "0" //true
false == "false" //false
false == "0" //true
"\t\r\n" == 0 //true
```

## 四、不要将赋值语句与其它语句，合并成一行
合并条件语句和赋值语句容易造成误读。
```javascript
if(a = b) {...}
```
也不应该在同一行中赋值多个变量：
```javascript
let a = b = 0
```

## 五、避免使用全局变量
Javascript最大的语法缺点，可能就是全局变量对于任何一个代码块，都是可读可写的。这对代码的模块化和重复使用，非常不利。
> **如果不得不使用，用大写字母表示变量名，比如UPPER_CASE，最好使用随机字符串做变量名。**


## 六、注释
使用简洁明了的注释有助于他人理解你的代码。如下情况应当使用注释。
- 代码晦涩难懂。
- 可能被误认为错误的代码。
- 必要但不明显的针对特定浏览器的代码。
- 对于对象、方法或者属性，生成文档时有必要的（使用恰当的文档注释）。

#### **单行注释**
单行注释应当用来说明一行代码或者一组相关的代码。单行注释可能有三种使用方式。
- 独占一行的注释，用来解释下一行代码。
- 在代码行的尾部的注释，用来解释它之前的代码。
- 多行，用来注释掉一个代码块。
```javascript
// 好的写法
if (condition) {
    // 如果代码执行到这里，则表明通过了所有安全检查
    allowed()
}

if (condition) {
// 不好的写法：错误的缩进
    allowed()
    //不好的写法：斜线和文字间没有空格
    allowed()// 不好的写法：代码和注释间没有足够的空格
}

// 好的写法：在注释掉一个代码块时，应使用单行注释，多行注释不应当使用在此种情况下。
// if (condition) {
//     allowed() // 执行**函数
// }
```

#### **多行注释**
多行注释应当在代码需要更多文字去解释的时候使用。文件头部、函数和类的介绍应当用多行注释

注释参考[JSDoc](http://www.css88.com/doc/jsdoc/index.html)语法
```javascript

    /**
     * 函数说明
     * @param {string|null} name 参数说明
     * @param {number} x 参数说明
     * @param {number?} y 选填参数说明
     * @param {object={}} config 有默认值的选填参数说明
     * @param {number} config.type 对象参数成员说明，枚举类型应举例标明其取值
     * @returns {boolean} 返回值说明
     */
    function fooBar(name, x, y, config = {}) {
        // code
    }
```

#### **注释声明**
注释有时候也可以用来给一段代码声明额外的信息。这些声明的格式以单个单词打头并紧跟一个冒号。可以使用的声明如下：
- **TODO**:说明代码还为完成。应当包含下一步要做的事。
- **HACK**:表明代码实现走了一个捷径。应当包含为何使用hack的原因。这样可能表明该问题可能有更好的解决办法。
- **XXX**:说明代码是有问题的并应当尽快修复。
- **FIXME**:说明代码是有问题的并应当尽快修复。重要性略次于XXX。
- **REVIEW**:说明代码有任可能的改动都需要评审。
这些声明可能在一行或多行注释中使用，并且应当遵循同一般注释类型相同的格式规则。

## 七、命名
变量和函数在命名应仅限于数字字母字符，采用驼峰命名格式。最好不要在任何命名中使用($)、反斜杠(\\)或下划线(_)。
**变量命名**应当是名词，或形容词+名词短语以避免和函数混淆。
**函数命名**应当是动词，或动宾短语来避免同变量混淆。
**类名**和**枚举集合名**首字母大写
```javascript
let accountNumber = "test001"
function getAccountNumber() {
    // code
}
class DataProvider {
	constructor() {
		// code
	}
}
const DataType = {
	STRING: 1,
	NUMBER: 2,
	DATE: 3,
}
```

**常量**（值不会被改变的变量）的命名应当是所有大写字母，不同单词之间单个下划线隔开。
```javascript
const TOTAL_COUNT = 10
```

**对象的属性**同变量的命名规则相同。对象的方法和函数的命名规则相同。
如果每行一个属性或方法，则在最后一个属性或方法末尾加逗号。否则以后添加属性时，还需要在上一行末尾添加逗号，导致版本库中产生了多余的修改记录
```javascript
// 好的写法
const people = {
	name: 'Bob',
	age: 12,
}
// 不好的写法
const people = {name: 'Bob', age: 12,}
```

## 八、变量与函数声明
#### **变量声明**
多处使用的变量尽量定义在函数开头，每行一个变量。每行都应该有let/const关键字。变量定义时尽量初始化。
```javascript
// 好的写法
let count = 10
let emptp = null
```

#### **函数声明**
函数声明时的空格规则如下。为了避免代码逻辑不被打散，可以先使用，后定义函数。
```javascript
// 好的写法
function outer() {
    const count = 10
    const name = "jeri"
    // 调用inner()的代码
    function inner() {
        // code
    }
}
```

## 九、运算符
#### **三元操作符**
三元操作符应当仅仅用在条件赋值语句中，而不要作为if语句的替代品。
```javascript
// 好的写法
const value = condition ? value1 : value2

// 不好的写法：没有赋值，应当使用if表达式
condition ? doSomething() : doSomethingElse()
```

#### **逻辑运算符**
适当运用逻辑运算符简化判空语句，而不要作为if语句的替代品。
```javascript
// 好的写法
const value = obj && obj.a && obj.a.b || 0

// 不好的写法
let value = 0
if (obj && obj.a && obj.a.b) {
    value = obj.a.b;
}

// 不好的写法：没有赋值，应当使用if表达式
value && doSomething() || doSomethingElse()
```

## 十、语句
#### **简单语句**
每一行最多只包含一条语句

#### **返回语句**
返回语句不应当使用圆括号包裹返回值

#### **if语句**
不允许在if语句中省略花括号。
```javascript
// 不好的写法：少了一个空格
if (condition){
    doSomething()
}

// 不好的写法：所有代码都在一行
if (condition) { doSomething() }

// 不好的写法：所有代码都在一行且没有花括号
if (condition) doSomething()
```

#### **for语句**
for类型的语句应当使用ES6中的let和const，避免使用var，否则循环结束后变量依然存在。
```javascript
// 好的写法
for (let i = 0, len = 0; i < len; i++) {
    // code
}
// 好的写法
for (const prop in object) {
    // code
}
// 不好的写法，声明和for分离
let i, len
for (i = 0, len = 0; i < len; i++) {
    // code
}
```

#### **while 语句**
while 类的语句应当是下面的格式。
```javascript
while (condition) {
    statement
}
```
#### **do 语句**
do 类的语句应当是下面的格式。
```javascript
do {
    statements
} while (condition)
```
#### **switch 语句**
switch下的每一组语句（除了default）都应当以break、return、throw结尾，或者用一行注释表示跳过。
```javascript
// 好的写法
switch (value) {
    case 1:
        /* falls through */
    case 2:
        doSomething()
        break;
    case 3:
        return true
    default:
        throw new Error("Some error")
}
```
如果一个switch语句不包含default情况，应该保留空的default部分。
```javascript
// 好的写法
switch (value) {
    case 1:
        return 'a'
    case 2:
        return 'b'
    default:
        // 没有default
}
```

#### **try 语句**
try类的语句应当格式如下。
```javascript
try {
    statements
} catch (variable) {
    statements
}
```