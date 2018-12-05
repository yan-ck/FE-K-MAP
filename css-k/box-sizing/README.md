# box-sizing

## 引入

盒子模型是css的基础，他涉及到一个容器的content／border/padidng，但是你你正常编码时可能并不会用到，因为浏览器有默认的盒子模型。

## 实例

在我们的[实例](./tip/index.html)中,我们定义了2个div盒子，并为她们编写了2段css

```
.box-content{
  width:200px;
  height:200px;
  border: 5px solid #ddd;
  padding:50px;
  box-sizing: content-box;
}
.box-border{
  width:200px;
  height:200px;
  border: 5px solid #ddd;
  padding:50px;
  box-sizing: border-box;
}
```

我们在浏览器中打开实例文件，发现2个div覆盖的区域差别很大。但是两个的css唯一的区别是box-sizing属性。其实我们就是通过box-sizing来定义盒子模型的，从而让浏览器对div的width／height作出不同的响应。

## 盒子模型分类

盒子模型分2种:

标准盒子模型(浏览器默认)
```
box-sizing: content-box;
```
> 在标准盒子模型中div占据的空间包括：content（width／height）+padding+border

ie盒子模型

```
box-sizing: border-box;
```
> 在标准盒子模型中div占据的空间包括：content（width／height）



