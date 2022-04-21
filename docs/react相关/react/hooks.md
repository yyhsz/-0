# Hooks

## 定义

hook 是钩子函数，让函数组件能够“钩入”一些特性。

为什么要有 hook（官网原话）：1. Class 组件语法太复杂 2. 为了实现逻辑的复用（HOC 和 render props 不好用） 3. Class 大型组件难以拆分

### 注意事项

不要在 循环，条件，子函数中调用 hook 函数；

以`useState`为例，每一个声明的状态都是存储在 `Fiber Node`一个数组中，如果在函数组件重新执行的时候，不按之前的顺序执行对应的`useState`，就会出错

自定义 hook，会与在组件中声明的 hook 进行合并

## 使用

### useRef

让函数组件能**用 ref**

```js

```

### forwardRef

让函数组件能够**具有 ref** 这个属性，注意与`useRef`进行区分

```js
const x = (props, ref) => {
  ...
};
export default forwardRef(x)
```

### useImperativeHandle

定义函数组件的 ref 值，应该叫 setRef 更合适

```js
const x = (props, ref) => {
  useImperativeHandle(ref,()=>{
    return {
      //ref具体内容
      ...
    }
  });
  ...
};
export default forwardRef(x)
```

### useReducer

字面意思：使用 reducer。当需要管理的状态是个对象且比较复杂，或下一个 state 依赖于之前的 state，可以使用 `useReducer`

它的语法优点类似于 redux，但是注意`initState`要一起传给`useReducer`，而不是像 redux 一样把`initState`当默认参数传给 reducer

```js
const reducer = (state,action) => {
  switch(action.type){
    case INCREATE : {
      return { ... };
    };
  };
};

const [state,dispatch] = useReducer(reducer,initState);//获取读写api
```

### useMemo、useCallback

两者都用于缓存引用类型的 props。如果一个子函数组件被`React.memo`缓存了，它接收的 prop 有一个引用类型，而这 prop 内容没变，只是随着父组件更新每次生成了不同的地址值，但子组件却会不得以随之更新。这时候就需要 `useMemo、useCallback` 把引用类型的 props 进行缓存。

第二个参数是依赖。

```js
useMemo(() => {
  return fn;
}, [a, b]);
useMemo(fn, [a, b]);
```

### useEffect、useLayoutEffect

useEffect、useLayoutEffect 只有执行时机的区别，`useLayoutEffect`在生成 dom 之后，实际渲染之前被调用。
