# 函数节流／函数防抖

## 引言

浏览器的的资源是非常宝贵的，我们不能在浏览器中频繁的执行一个操作（例如：浏览器的onscroll以及onsize事件等），有时频繁的操作会导致浏览器挂起，尤其是dom操作。函数节流／函数防抖会帮助我们避免这样的事情，优化我们的js执行。

## 反面实例1

在[实例1](./tip/index1.html)中，当我们改变浏览器的窗口大小时，浏览器的后台会打印很多num的值。这样会频繁的执行我们的js代码，消耗浏览器的资源。其实我们想要浏览器在改变窗口结束的时候执行一次就可以，不需要在改变的时候频繁立即执行事件。这是我们就用到函数防抖

## 反面实例2

另外一种情况是这样的：我们在移动端有分页的请求，我们会在滚动条到达距离底部150px时执行ajax请求，获取数据。但是我们有时会频繁的滑动屏幕，导致多次请求。这样我们需要在规定的时间里只执行一次。避免频繁的ajax请求。这是我们就用到函数节流

## 实例的区别

> 我们在这两个实例中都在一段时间内只执行一次事件函数。但是这两次执行的时间是不一样的。实例1中要求我们在事件频繁触发时，在最后一次触发时才执行一次。
实例2中要求我们在时间频繁出发时，在第一次触发时执行一次。明白其中的区别，我们的解决方案也是不一样的。

## 实例1解决方案

```
function throttle(method, context) {
  clearTimeout(method.tId);
  method.tId = setTimeout(function () {
    method.call(context);
  }, 1000);
}
```

## 实例2解决方案

```
function debounce(method, context) {
  if(!method.tId){
    method.tId = setTimeout(function () {
      method.call(context);
      clearTimeout(method.tId);
    }, 1000);
  }
}
```

## 说明

throttle／debounce函数的参数method为事件函数，context为函数的执行作用域，1000为触发的时间，可根据自己的需求调整。


