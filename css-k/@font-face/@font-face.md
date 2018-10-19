
# @font-face


## 引言
我们在使用iconfont的字体图标库会引入这样的一段代码：

```
@font-face {font-family: 'iconfont';
    src: url('iconfont.eot');
    src: url('iconfont.eot?#iefix') format('embedded-opentype'),
    url('iconfont.woff') format('woff'),
    url('iconfont.ttf') format('truetype'),
    url('iconfont.svg#iconfont') format('svg');
}
.iconfont{
    font-family:"iconfont" !important;
    font-size:16px;font-style:normal;
    -webkit-font-smoothing: antialiased;
    -webkit-text-stroke-width: 0.2px;
    -moz-osx-font-smoothing: grayscale;}

<i class="iconfont">&#x33;</i>
```
那么这段代码时什么意思呢？

我们首先看@font-face

>font-family: 'iconfont';

这行代码定义了一种字体名称叫做iconfont（方便后续设置字体的font-family）

>src: url('iconfont.eot?#iefix') format('embedded-opentype')

告诉浏览器字体文件的来源，并且告诉浏览器文件的格式。

然后定义css类iconfont的统一样式，并在样式中定义字体图标的字体

```
font-family:"iconfont" !important;
```

最后把字体文件的代码写在<i>标签内渲染

## 使用

### 用途 

>@font-face除了使用iconfont的字体文件以外，我们也可以在浏览器中引入自定义的字体文件(其实iconfont也是一种字体文件)，这应该是@font-face最原始的用途。

### 实例

具体的demo实例在[这里](./tip/index.html).
在这个实例中我们在浏览器中引入了一种类似lcd的字体。




