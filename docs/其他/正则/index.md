# 正则表达式

regular expression
只能处理字符串，它用于验证字符串是否符合某个规则（test），也可以把字符串中符合规则的内容捕获（exec、match）

pattern：模式（模型）

## 正则创建方式

正则的创建方式有两种

```js
let reg1 = /\d+/; //字面量方式
let reg2 = new RegExp(); //构造函数模式，接收两个参数：元字符字符串（要记得转义），修饰符字符串
```

## 元字符

### 量词元字符

控制出现次数

```js
* ：0~多次
+ ：1~多次
？：0或1次
{n}：出现n次
{n,}：出现n到多次
{n,m}：出现[n,m]次
```

### 特殊元字符

单个或组合在一起表示特殊的含义

```js
\：转义字符
.：除 \n 以外的任意字符
^：以哪个元字符作为开始
$：以哪个元字符作为结尾
\n：换行符
\d：0~9之间的一个数字
\D：非0~9之间的一个数字
\w：数字、字母、下划线中的任意一个字符
\s：一个空白字符（包含空格，制表符，换页符）
\t：一个制表符
\b：匹配一个单词的边界
[xyz]：x或者y或者z中的一个字符
[^xy]：除了x/y以外的任意字符
[a-z]：指定a-z这个范围中的任意字符 [0-9a-zA-Z] === \w
[^a-z]：上一个取“非”
()：分组
(?:)：只匹配不捕获
(?=)：正向预查
(?!)：负向预查
```

### 普通元字符

普通元字符相当于字面量，匹配的是本身

## 修饰符

```js
i：ignoreCase忽略大小写
m：multiline多行匹配
g：global全局匹配
```

## 元字符详解

### 转义符

```js
let reg = /^2.3$/; // .不是小数点，是除/n外任意字符
console.log(reg.test('2.3')); //true
console.log(reg.test('23')); //false

let reg1 = /^2\.3$/; //
console.log(reg1.test('2.3')); //true
console.log(reg1.test('2@3')); //false
```

一个比较恶心的例子，字符串中的\也有特殊含义，因为有回车等符号

```js
let reg = /^\\d$/; // 把\转义
console.log(reg.test('\\d')); //true;字符串中的/也得小心处理才行;
console.log(reg.test('d')); //false

let reg = new RegExp('\\d+'); //reg === /\d+/；通过字符串形式创建正则的时候也需要处理
```

### 或字符

直接 x|y 会有很乱的优先级问题，一般用小括号来调整优先级

```js
let reg = /^18|29$/; //
console.log(reg.test('18')); //true
console.log(reg.test('29')); //true
console.log(reg.test('129')); //true
console.log(reg.test('189')); //true
console.log(reg.test('1289')); //true
console.log(reg.test('829')); //true
console.log(reg.test('182')); //true
console.log(reg.test('82')); //false
```

### []

中括号中的字符一般代表本身的含义，除了转义字符

```js
let reg = /^[@+]+/; //中括号中的加号就是加号的意思
console.log(reg.test('@@')); //true
console.log(reg.test('@+')); //true
let reg1 = /^[@+]/;
console.log(reg1.test('@+')); //false
```

中括号中不存在多位数

```js
let reg = /^[18]+/;
console.log(reg.test('1')); //true
console.log(reg.test('8')); //true
console.log(reg.test('18')); //false
let reg1 = /^[10-29]$/;  // 1或者0-2或者9
let reg1 = /^[(10-29)]$/;  // 1或者‘(’或者0-2或者9或者‘)’
```
