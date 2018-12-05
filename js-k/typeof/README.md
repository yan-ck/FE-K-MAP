# 类型检测

## 引言

我们经常需要做类型检测，我们可以使用typeof和instanceof ，但是我们要说的是另外一种检测方法。

## typeof && instanceof

具体的实例看[这里](./tio/index.html)

## 其他检测方法

具体的实例看[这里](./tio/index.html)

```
function isObject(value){
  return Object.prototype.toString.call(value) == "[object Object]";
}

function isArray(value){
  return Object.prototype.toString.call(value) == "[object Array]";
}
 
function isFunction(value){
  return Object.prototype.toString.call(value) == "[object Function]";
}

function isRegExp(value){
  return Object.prototype.toString.call(value) == "[object RegExp]";
}
```



