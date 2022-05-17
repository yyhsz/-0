# TypeScript

## object types

为对象定义类型：
定义为 `object` 和 `{}` 等同；这两种方式没有定义具体的属性，不是一种好的实践。

```ts
//像这个具体的某个对象可以让ts自己推断
const person : object {
  name:'yyh',
  age:24,
}
```

## array types

想定义混合类型

## Tuple

fixed length and fixed type array
元组类型：`[string,boolean]`

```ts
type roleTuple = [number, string]; //定义一个元组类型，仅有两个元素
//注意它和数组类型的区别，数组类型：string[]
let role: roleTuple = [1, 'yyh']; //role是长度为2，第一个元素为string，第二个元素为number的类型
role.push(2); //需要小心的是，元组类型并不能检测这里代码错误，这句代码是可以执行的
```

## Enum

enums 属性通常 uppercase , that's no a must-do;

```ts
enum Role {
  ADMIN,
  READ_ONLY_USER,
  AUTHOR, //Role.ADMIN === 1,后面的依次累加
}
enum Role {
  ADMIN = 5,
  READ_ONLY_USER,
  AUTHOR, //Role.ADMIN === 5,后面的依次累加
}
//也可以传string和其他number
enum Role {
  ADMIN = 5,
  READ_ONLY_USER = 100,
  AUTHOR = 'author',
  //Role.ADMIN === 5,后面的依次累加
}
```

## Union Type

typescript 不会检测联合类型里面有什么

```ts
function combine(input1: number | string, input2: number | string | boolean) {
  return input1 + input2; //这里ts会提示错误，因为它不知道联合类型里有没有不能用+拼接的部分
}

//要改成下面这样才不会报错，但是这样很麻烦，我们来看看写法
function combine1(input1: number | string, input2: number | string) {
  if (typeof input1 === 'number' && typeof input2 === 'number') {
    return input1 + input2;
  } else {
    return input1.concat(input2);
  }
}
```

## Literal Type

## type alias

## Function Type

2 different way

```ts
//1.
const add: (a: number, b: number) => number = (x, y) => x + y;
//2. 其实此处可以不指明函数返回值类型，可以通过ts推断得出
function add2(a: number, b: number): number {
  return a + b;
}
```

回调函数的类型限制

```ts
//该例子限定了cb 的类型，通过ts对cb的限定，不怕使用者乱传参导致报错，也不用做太多的容错处理
const foo: (x: string, cb: (a: string) => string) => void = (x, cb) => {
  cb(x);
};
```

## void

void 表示函数没有返回值，但实际上它并不检查限制函数返回值的任何操作，即你可以有返回值，但实际使用最好不应该有

## never

举几个情况会出现 never

1. 函数内部出错，导致不会执行到返回值的代码
2. 函数内出现无限循环

## unknown

unknown 类型一般不能被赋值给具体类型，如果要这样做，必须先进行判断，对 unknown 类型进行一个收窄

```ts
let a: unknown = 'aa';
let b: string = a; //提示错误

//对类型进行判断
if (typeof a === 'string') {
  b = a; //此时不提示错误
}
```
