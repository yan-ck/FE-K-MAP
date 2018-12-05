# 原生ajax请求


## 引言
我们在平时写代码中很多都是用封装完整的ajax库，例如jquery的$.ajax,axios,vue-resources等等吧，但要对这个库有深入的了解，我们还需要了解原生ajax。下面就看看来回过头看看原声的ajax。

## XMLHttpRequest类

这个类是实现ajax请求的基础，现在浏览器都内置了XMLHttpRequest类。我们可以同过下面的代码创建一个ajax对象。

```
var xhr = new XMLHttpRequest()
```
## ajax请求代码实现

上面我们通过XMLHttpRequest类创建了xhr对象。我们都知道ajax有同步请求与异步请求。

> ajax同步请求，javascript代码会等待ajax请求成功之后再继续执行其他代码。

下面为一个基本的ajax同步请求代码

```
var xhr = new XMLHttpRequest()
xhr.open("get", "example.php", false);
xhr.send(null);
if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
    alert(xhr.responseText);
} else {
    alert("Request was unsuccessful: " + xhr.status);
}
```
首先我们调用open方法，open方法只是定义了ajax请求的信息并没有发送信息到服务器。open方法有三个参数第一个位请求方式（get或者post，也有其他的形式，用的比较少），第二个参数为请求的地址，第三个为Boolean型，false定义该次请求为同步请求。

其次调用send方法。send方法的参数定义了发送给服务器的数据。如果数据为空的话要用null（为了兼容一些浏览器），在这一步我们ajax把数据发送给服务器，等待服务器响应。

最后在收到响应时，响应的数据会自动填充xhr对象，相关的属性如下：

* responseText:作为响应主体被返回的文本。
* responseXML:如果响应的内容类型是"text/xml"或"application/xml"，这个属    性中将保存包含着响应数据的 XML DOM 文档。
* status:响应的 HTTP 状态。
* statusText:HTTP 状态的说明。

我们通过status属性来判断ajax是否成功，如果请求返回200表示成功，返回值为304表示数据源没有变化，可以使用浏览器的缓存。然后根据返回的状态码，执行响应的回调函数。

这是ajax的同步请求，但是我们大部分使用的是异步请求
> 由于javascript的单线程特性，javascript在发送ajax的异步请求之后，不会等待服务器的响应，javascript会继续执行其他的代码。

此时，可以检测 XHR 对象的 readyState 属性，该属性表示请求 /响应过程的当前活动阶段。这个属性可取的值如下：

* 0:未初始化。尚未调用 open()方法。
* 1:启动。已经调用 open()方法，但尚未调用 send()方法。
* 2:发送。已经调用 send()方法，但尚未接收到响应。
* 3:接收。已经接收到部分响应数据。
* 4:完成。已经接收到全部响应数据，而且已经可以在客户端使用了。

只要 readyState 属性的值由一个值变成另一个值，都会触发一次 readystatechange 事件。可 以利用这个事件来检测每次状态变化后 readyState 的值。通常，我们只对 readyState 值为 4 的阶 段感兴趣，因为这时所有数据都已经就绪。不过，必须在调用 open()之前指定 onreadystatechange 事件处理程序才能确保跨浏览器兼容性。

```
var xhr = createXHR();
xhr.onreadystatechange = function(){
    if (xhr.readyState == 4){
        if ((xhr.status >= 200 && xhr.status < 300) || xhr.status == 304){
              alert(xhr.responseText);
    } else {
          alert("Request was unsuccessful: " + xhr.status);
    }
} };
xhr.open("get", "example.txt", true);
xhr.send(null);
```

## ajax头部信息

ajax分为请求头信息与响应头信息

> 请求头信息在我们发送ajax时会自动携带一些头部信息。另外我们也可以自己设置自定义的头部信息。要成功发送请求头部信息，必须在调用 open()方法之后且调用 send()方法 之前调用 setRequestHeader()

```
xhr.open("get", "example.php", true); 
xhr.setRequestHeader("MyHeader", "MyValue"); 
xhr.send(null);
```
>调用 XHR 对象的 getResponseHeader()方法并传入头部字段名称，可以取得相应的响应头部信 息。而调用 getAllResponseHeaders()方法则可以取得一个包含所有头部信息的长字符串。

```
var myHeader = xhr.getResponseHeader("MyHeader");
var allHeaders = xhr.getAllResponseHeaders();
```
