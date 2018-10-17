
# @font-face


## 引入
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

这行代码定义了一种字体名称叫做iconfont，方便后续设置字体的font-family

>src: url('iconfont.eot?#iefix') format('embedded-opentype')

告诉浏览器字体文件的来源，并且告诉浏览器文件的格式。

然后定义css类iconfont的统一样式，

最后把字体文件的代码写在<i>标签内渲染

## 使用

#### 用途 

>@font-face除了使用iconfont的字体文件以外，我们也可以在浏览器中引入自定义的字体文件，这应该是@font-face最原始的用途,应该也是现代浏览器发展的方向。

### 其他属性

>除了设置字体文件的名称(font-family)以及来源（url），我们还可以使用字体文件的font-weight／font-style,但是使用的前提是我们的字体文件包中要包含相应的文件。（暂略）

## 兼容性

我们在iconfont的使用说明中有这样一句话

>兼容性最好，支持ie6+，及所有现代浏览器。

主ie7-ie8支持EOT格式的字体文件；ie9开始支持WOFF；所以有ie6-ie8兼容性要求的需要引入eot文件，ie9以及以上的浏览器就不需要引入eot文件了



