# 惰性载入函数

## 引言

首先看一个例子
```
function createXHR(){
        if (typeof XMLHttpRequest != "undefined"){
            return new XMLHttpRequest();
        } else if (typeof ActiveXObject != "undefined"){
            if (typeof arguments.callee.activeXString != "string"){
                var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
                                "MSXML2.XMLHttp"],i,len;
                for (i=0,len=versions.length; i < len; i++){
                     try {
                         new ActiveXObject(versions[i]);
                         arguments.callee.activeXString = versions[i];
                          break;
                     } catch (ex){
//跳过 }
            return new ActiveXObject(arguments.callee.activeXString);
        } else {
            throw new Error("No XHR object available.");
        }
}
```
上面是创建ajax请求时，我们需要根据浏览器的兼容性，来创建xhr对象。但是我们每请求一次就要对if语句做一次判断，这样会浪费浏览器的资源。

## 优化方案1

```
function createXHR() {
  if (typeof XMLHttpRequest != "undefined") {
    createXHR = function () {
      return new XMLHttpRequest();
    }
  } else if (typeof ActiveXObject != "undefined") {
    createXHR = function () {
      if (typeof arguments.callee.activeXString != "string") {
        var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
          "MSXML2.XMLHttp"], i, len;
        for (i = 0, len = versions.length; i < len; i++) {
          try {
            new ActiveXObject(versions[i]);
            arguments.callee.activeXString = versions[i];
            break;
          } catch (ex) {
            //skip }
          }
        }
        return new ActiveXObject(arguments.callee.activeXString);
      };
    }
  } else {
    createXHR = function () {
      throw new Error("No XHR object available.");
    };
  }
  return createXHR();
}
```
其实我们可以在浏览器第一次调用createXHR函数时，根据浏览器的兼容性给createXHR重新赋值，这样在下次调用的时候就不需要重复执行if语句。

## 优化方案2

第二种方案和第一种类似。利用js自执行函数创建createXHR，然后赋值给一个变量（例如变量createXHR）。然后下次创建xhr对象时，只需createXHR（）就可以调用正确的xhr创建方法，无需根据if语句在判断。
代码如下：

```

var createXHR = (function () {
  if (typeof XMLHttpRequest != "undefined") {
    return function () {
      return new XMLHttpRequest();
    };
  } else if (typeof ActiveXObject != "undefined") {
    return function () {
      if (typeof arguments.callee.activeXString != "string") {
        var versions = ["MSXML2.XMLHttp.6.0", "MSXML2.XMLHttp.3.0",
          "MSXML2.XMLHttp"], i, len;
        for (i = 0, len = versions.length; i < len; i++) {
          try {
            new ActiveXObject(versions[i]);
            arguments.callee.activeXString = versions[i];
            break;
          } catch (ex) {
            //skip }
          }

        }
        return new ActiveXObject(arguments.callee.activeXString);
      };
    }
  } else {
    return function () {
      throw new Error("No XHR object available.");
    };
  }
})();
```

## 总结

惰性载入函数是一种优化代码的方式，在实际的工作开发工程中经常会用到。
