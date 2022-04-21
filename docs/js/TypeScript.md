# TypeScript

## 数据类型

number,string,boolean,null,undefined,symbol
void,Tuple(元组),enum(枚举),object,never,any,联合类型

## ts 和 js 区别

- ts 支持静态类型
- ts 在编译时报错，js 在运行时报错
- ts 支持一些如：泛型，接口等概念
- 编写代码时的提示都是由 ts 实现的
- ts 会进行类型推论：即不需要写明类型，它会根据上下文推断类型

## 联合类型

联合类型（Union Types）表示取值可以为多种类型中的一种。

```ts
let id: number | string;

//访问联合类型的属性必须是联合类型上的交集
```

## 元组

指定了具体类型的数组

```ts
//arr的元素有且仅有两个
let arr: [number, string];
```

## 枚举

枚举（Enum）类型用于取值被限定在一定范围内的场景，比如一周只能有七天，颜色限定为红绿蓝等。

```ts
enum Days {
  Sun,
  Mon,
  Tue,
  Wed,
  Thu,
  Fri,
  Sat,
}
```

## 接口

## 为什么选择 TS 而不是 JS

ts 在编译时报错，更加安全，而且类型推断和类型声明可以不需要写那么多文档

##
