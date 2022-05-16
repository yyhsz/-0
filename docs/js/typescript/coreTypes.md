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
