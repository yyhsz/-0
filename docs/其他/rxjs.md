# RxJS

RxJS is a library for composing asynchronous and event-based programs by using observable sequences（可观察序列）.
RxJS 适合用来处理异步和基于事件的程序。

RxJS 是 ReactiveX 的 JS 版本。

RxJS is programming with asynchronous data streams.
RxJS 专门用于处理 stream。

那什么是 stream。
Stream are cheap and ubiquitous,anything can be a stream.
varables,user inputs,properties,caches,data structures.
stream 只是一个抽象概念，任何事物都能被抽象成 stream。

RxJS 基于观察者模式，迭代器模式，函数式编程实现。

## 核心概念

- Observable 可观察的对象

代表一组未来即将产生的事件数据

- Observer 观察者

用于接收观察结果的对象，包含三个 callback 属性：next，error，complete

- Subscription 订阅对象

代表正在执行 Observable/Observer 的执行个体（可用来取消订阅）

- Operators 运算子
  Operators 是纯函数，用于处理 Observable，把处理的结果传给 Observer

- Subject 主体对象
  如同 EventEmitter 一样，用来广播收到的事件给多位 Observer，看下面例子即可明白

- Schedulers 调度器
  用于集中管理与调度多重事件之间的数据，用于控制事件并发（control concurrency）

## 示例

```js
//RxJS所有API都来自RxJS和RxJS.operators这两个库
import {interval} from RxJS;
import {take} from RxJS.operators;

//interval(500)：创建定时器任务
//pipe(take(4))：定义一个管道，取定时器前四个输出
//subscribe：订阅这个任务
const subscrption = interval(500).pipe(take(4)).subscribe(console.log);
subscription.unsubscribe(); //取消订阅

```

```js
// 建立可观察对象，习惯上以$结尾的变量都认为是Observable
const click$ = rxjs.fromEvent(document, 'click');
// 建立观察者
const observer = {
  next: (x) => {
    console.log(x);
  },
};
// 建立订阅对象：订阅Observable，传入观察者；也可以只传单个回调函数
const sub$ = click$.subscribe(observer);
// 取消订阅
sub$.unsubscribe();
```

```js
//本例子通过运算子过滤数据
import {fromEvent} from RxJS;
import {filter,take} from RxJS.opeators;
const click$ = fromEvent(document,'click').pipe(
  filter(e=>e.clientX<100),
  take(4) //取前4次操作
);
const sub$ = click$.subscribe(console.log);
```

以上几个示例已经说明了 RxJS 如何运作的。

总结一下：

1. 生成 Observable（事件，异步操作）
2. 通过 pipe 传入运算子对 Observable 的数据进行操作，运算子可以有多个
3. 向 Observable 传入 Observer 订阅，得到一个 subscription

重点在于运算子的各种组合。

这个 pipe 和 redux 的 applyMiddleware 都是类似 compose 组合函数的实现。

## Subject 使用

Subject 被当作 Observer 向 Observable 订阅，而后由 Subject 向多个 Observer 广播触发的 Observable 事件。

```js
const click$ = rxjs.fromEvent(document, 'click').pipe(take(4));
const subject = new rxjs.Subject(); //创建Subject
click$.subscribe(subject); //使用subject订阅而不是observer
//再由subject去关联多个observer，由subject通知observer事件触发
const subs1$ = subject.subscribe(observer1);
const subs2$ = subject.subscribe(observer2);
//各自取消订阅
subs1$.unsubscribe();
subs2$.unsubscribe();
```

## operators

常用运算子有：formEvent、concat、share

## Observable

此处不是RxJS中Observable对象的实现，只是举个例子，便于理解

```js
class Observable {
  constructor(behavior) {
    //动态的方式把行为逻辑注入到Observable这个类中
    this.behavior = behavior; //定义这个可观察对象的行为，相当于RxJS的创建过程使用的运算子，如：fromEvent
  }
  subscribe(observer) {
    //根据行为调用observer提供的方法
    this.behavior(observer);
  }
}
const obs$ = new Observable(({ next, error, complete }) => {
  try {
    next(1);
    complete();
  } catch (e) {
    error(e);
  }
});
const observer = {
  next(d) {
    console.log(d);
  },
  error(e) {
    console.error(e);
  },
  complete(x) {
    console.log(x);
  },
};
obs$.subscribe();
```
