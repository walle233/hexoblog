---
title: 重学 css 之 flex布局
---

# Flex 布局是什么

Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
那我们如何实现一个flex布局呢。
首先，flex布局支持横向和纵向，这样我们就需要做一个抽象，我们把 flex 延伸的方向称为主轴，把跟它垂直的的方向称为交叉轴。这样，flex 项中的 width 和 height 就会称为交叉轴尺寸或者主轴尺寸。
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071004.png)



# 基本概念

采用 flex 布局的元素，称为 flex 容器（flex containr），简称“容器”，它所有子元素自动成为容器成员，称为 flex 项目（flex item）， 简称“项目”。

## 容器的属性
- flex-direction
- flex-wrap
- flex-flow
- justify-content
- align-items
- align-content

#### flex-direction 属性
flex-direction 属性决定主轴的方向。
```
.box {
  flex-direction: row | row-reverse | column | column-reverse;
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071005.png)
它可能有四个值
- row（默认值）：主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿。
  
### flex-wrap 属性
默认情况下，项目都排在一条线（又称"轴线"）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

```
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

它可能取三个值。
- nowrap（默认）：不换行。
- wrap：换行，第一行在上方。
- wrap-reverse：换行，第一行在下方。
  
### flex-flow 属性
flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
```
.box {
  flex-flow: <flex-direction> || <flex-wrap>;
}
```

### justify-content 属性
justify-content属性定义了项目在主轴上的对齐方式。
```
.box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071010.png)
它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。
- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等。
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-items 属性
align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```
.box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071012.png)
该属性可能取6个值。
- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。

## 项目的属性
以下6个属性设置在项目上。
+ order
+ flex-grow
+ flex-shrink
+ flex-basis
+ flex
+ align-self

### order 属性
order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。
```
.item {
  order: <integer>;
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071013.png)

### flex-grow 属性
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
```
.item {
  flex-grow: <number>; /* default 0 */
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071014.png)
如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### flex-shrink属性
flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```
.item {
  flex-shrink: <number>; /* default 1 */
}
```
如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

### flex-basis属性
flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
```
.item {
  flex-basis: <length> | auto; /* default auto */
}
```
它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### flex
flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选。

```
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### align-self属性
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。

```
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015071016.png)
该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

注：以上内容摘抄自 [阮一峰 flex 教程 ](https://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)




# flex 的应用

### 垂直居中
```
<div id="parent">
  <div id="child">
  </div>
</div>
```

```
#parent {
  display:flex;
  width:300px;
  height:300px;
  outline:solid 1px;
  justify-content:center;
  align-content:center;
  align-items:center;
}
#child {
  width:100px;
  height:100px;
  outline:solid 1px;
}
```
思路是创建一个只有一行的 flexbox，然后用 align-items:center; 和 align-content:center; 来保证行位于容器中，元素位于行中。

### 两列等高
```
<div class="parent">
  <div class="child" style="height:300px;">
  </div>
  <div class="child">
  </div>
</div>
<br/>
<div class="parent">
  <div class="child" >
  </div>
  <div class="child" style="height:300px;">
  </div>
</div>
```

```
.parent {
  display:flex;
  width:300px;
  justify-content:center;
  align-content:center;
  align-items:stretch;
}
.child {
  width:100px;
  outline:solid 1px;
}
```
思路是创建一个只有一行的 flexbox，然后用 stretch 属性让每个元素高度都等于行高。

### 自适应宽度
```

<div class="parent">
  <div class="child1">
  </div>
  <div class="child2">
  </div>
</div>
```

```

.parent {
  display:flex;
  width:300px;
  height:200px;
  background-color:pink;
}
.child1 {
  width:100px;
  background-color:lightblue;
}
.child2 {
  width:100px;
  flex:1;
  outline:solid 1px;
}
```
这个就是 Flex 设计的基本能力了，给要自适应的元素添加 flex 属性即可。