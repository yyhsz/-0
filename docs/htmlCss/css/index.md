# 垂直居中

```html
<div id="a">
  <div id="b"></div>
</div>
```

```css
#a {
  height: 200px;
  width: 200px;
  border: 1px solid;
}
#b {
  height: 100px;
  width: 100px;
  border: 1px solid;
}
```

## 法 1 子元素相对定位

```css
#b {
  position: relative;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```

## 法 2 子元素绝对定位，marginauto

```css
#a {
  position: relative;
}
#b {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  margin: auto;
}
```

## 法 3 flex 布局

```css
#a {
  position: flex;
  justify-content: center;
  align-items: center;
}
```

# sadfa
