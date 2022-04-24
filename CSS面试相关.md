

## CSS选择器 



- id选择器  -   #myid
- 类选择器  -  .myclass
- 属性选择器 -  a[rel='external']
- 伪类选择器 -   :hover   ::before ::after
- 标签选择器   -   div   h1  p 
- 兄弟选择器  -   h1 + p 
- 子类选择器  -   div >  p  
- 后代选择器   -  ul  li  
- 通配符选择器 -   * 





## 选择器的优先级



- `!important` 
- 内联样式 -  1000
- id 选择器 -  100
- 类选择器、 属性选择器、伪类选择器  - 10 
- 元素选择器 、 伪元素 选择器   - 1 
- 关系选择器 、 通配符选择器  - 0 



`!important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性`







## position 属性的值有哪些及其区别



**固定定位 fixed** :   元素相对于浏览器窗口是固定位置 ， 即使窗口滚动它也不会移动。 Fixed 定位脱离文档流，不会占据空间，注意的是 Fixed 定位会与其他元素重叠

**相对定位： relative** :  相对定位,  占用标准流 （文档流 ），他会出现在文档中该出现的位置。 可以通过设置偏移值改变其位置， 相对于自身做偏移 

**绝对定位： absolute** : 绝对定位 ， （ 脱离文档流），单独使用相对于 body 做偏移 ( left / top / right / buttom)。如果绝对定位和相对定位结合起来使用， 它相对的父级是 relative 定义的元素做偏移。relative的元素必须是 absolute 的父级在项目开发中，一般使用 relative +  absolute 结合使用最多 

**静态定位： static**   :   静态定位， 默认值 ，没有定位， 不能设置偏移 （ left  /  top  / bottom / right ）, 占用标准流  （文档流），也就是占用元素本来的位置 。 



>  总结：这些定位的关系；什么场景使用什么的定位的方法。 



## box-sizing 的属性



box-sizing 规定两个并排的带边框的框，语法为 box-sizing：content-box/border-box/inherit

- **content-box**：宽度和高度分别应用到元素的内容框，在宽度和高度之外绘制元素的内边距和边框。【标准盒子模型】

- **border-box**：为元素设定的宽度和高度决定了元素的边框盒。【IE 盒子模型】
- **inherit**：继承父元素的 box-sizing 值。





> box-sizing:  用在对盒子的宽度 和 盒子所在的区域进行 瓜分。 
>
> content-box :   表示的设置的盒子模型的所有宽度都加起来 形成的盒子
>
> border-box： 表示所有的盒子模型 瓜分了 盒子 本身的宽度



## CSS的盒子模型

CSS 盒模型本质上是一个盒子，它包括：**边距，边框，填充和实际内容**。CSS 中的盒子模型包括 IE 盒子模型和标准的 W3C 盒子模型。

在标准的盒子模型中，`width 指 content 部分的宽度`。

在 IE 盒子模型中，`width 表示 content+padding+border 这三个部分的宽度`。





故在计算盒子的宽度时存在差异：

**标准盒模型：** 一个块的总宽度 = width+margin(左右)+padding(左右)+border(左右)

**怪异盒模型：** 一个块的总宽度 = width+margin（左右）（既 width 已经包含了 padding 和 border 值）







## BFC 块级格式上下文 



`BFC`是 `Block Formatting Context` 的缩写， 块级格式上下文。

BFC 是CSS布局的一个概念，是一个独立的渲染区域， 规定了内部box如果布局，并且这个区域的子元素不会影响到外面的元素

其中比较重要的布局规则有内部 box 垂直放置，计算 BFC 的高度的时候，浮动元素也参与计算。

> 简单理解： BFC 就是 在布局页面中 独立出来的 一层 元素， 可以独立的渲染， 不会影响到外面的元素 （跟脱离文档流一样） 



*BFC的原理布局规则*

- 内部的Box会在 `垂直方向` ， 一个接着一个放置 （共同脱离文档流的元素）
- Box `垂直方向上的距离由 margin 决定` 。 属于同一个BFC的两个相邻Box的margin会发生重叠
- 每个元素的margin box的左边， 与包含块border box的左边相接触(对于从左往右的格式化，否则相反）
- BFC的区域  不会与 float box 重叠
- BFC是一个独立的容器， 容器里面 *子元素不会影响外面的元素*
- 计算BFC的高度时，浮动元素也会参与运算
- 元素的类型和`display属性，决定了这个Box的类型`。不同类型的Box会参与不同的`Formatting Context`



*如何创建BFC* 

- 根元素 HTML 元素
- float 的值不为 none 
- position 为 absolute 或 fixed
- display 的值为 inline-block 、  table-cell  、table-caption
- overflow的值不为 visible



*BFC的使用场景*

- 去除边距重叠现象
- 清除浮动（让父元素的高度包含子浮动元素）
- 避免某元素被浮动元素覆盖
- 避免多列布局由于宽度计算四舍五入而自动换行



## 水平居中



- 对行内元素：  `text-align: center`
- 对于确定的宽度： 
  - width和margin实现。`margin: 0 auto`;
  - 绝对定位和margin-left: (父width - 子width）2, 前提是父元素position: relative
  - 加上 `transform: translate(-50%, -50%)`

- 对于宽度未知的块级元素

  （1）`table标签配合margin左右auto实现水平居中`。使用table标签（或直接将块级元素设值为 display:table），再通过给该标签添加左右margin为auto。

  （2）inline-block实现水平居中方法。display：inline-block和text-align:center实现水平居中。

  （3）`绝对定位+transform`，translateX可以移动本身元素的50%。

  （4）flex布局使用`justify-content:center`







## 垂直居中



1. 利用 `line-height` 实现居中，这种方法适合纯文字类
2. 通过设置父容器 相对定位 ，子级设置 `绝对定位`，标签通过margin实现自适应居中
3. 弹性布局 flex :父级设置display: flex; 子级设置margin为auto实现自适应居中
4. 父级设置相对定位，子级设置绝对定位，并且通过位移 transform 实现
5. `table 布局`，父级通过转换成表格形式，`然后子级设置 vertical-align 实现`。（需要注意的是：vertical-align: middle使用的前提条件是内联元素以及display值为table-cell的元素）。









## 隐藏某个元素的方法



1. ` opacity: 0` ,   透明度为0 ， 将该元素隐藏起来了，但不会改变布局， 并且， 如果该元素绑定事件，点击元素， 还是会触发事件
2. `visibility: hidden`， 该元素隐藏起来了，但不会改变页面布局，但是 不会触发 该元素绑定的事件，隐藏元素， 在文档布局中任然保留原来的空间 
3. `display: none `   把元素隐藏起来， 会改变页面的布局， 可以理解为页面把该元素给删除了。不会显示对应的元素，在文档布局中 不再分配空间





## 实现三角形 



盒子宽高均为0 ， 三面边框皆透明

```scss
div::after {
  width: 0;
  height: 0;
  content: "";
  position: absolute;
  border: {
    right: 100px solid transparent;
    top: 100px solid #000;
    left: 100px solid transparent;
    bottom: 100px solid transparent;
  }
}
```







## 页面布局



### flex 布局 

布局的传统解决方案，基于盒状模型，依赖 display 属性 + position 属性 + float 属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。



flex 布局， 也叫 “弹性布局”，用来为盒子模型提供最大的灵活性。 使用 弹性布局  只需要在该元素 加上`display: flex` ,    然后它的 子元素 就可以按照弹性布局 的属性进行布局 

容器的属性 ： 

- `flex-direction` 决定主轴的方向（即子 item 的排列方法）flex-direction: row | row-reverse | column | column-reverse; 
- `flex-wrap` :  决定换行规则 flex-wrap: nowrap | wrap | wrap-reverse;
- `flex-flow`： .box { flex-flow: || ; }
- `justify-content`:  对齐方式， 水平主轴对齐方式
- `align-items` :  对齐方式， 竖直轴线方向
- `align-content` 



项目的属性（元素的属性）：

- order 属性：定义项目的排列顺序，顺序越小，排列越靠前，默认为 0

- flex-grow 属性：定义项目的放大比例，即使存在空间，也不会放大

- flex-shrink 属性：定义了项目的缩小比例，当空间不足的情况下会等比例的缩小，如果 定义个 item 的 flow-shrink 为 0，则为不缩小

- flex-basis 属性：定义了在分配多余的空间，项目占据的空间。

- flex：是 flex-grow 和 flex-shrink、flex-basis 的简写，默认值为 0 1 auto。

- align-self：允许单个项目与其他项目不一样的对齐方式，可以覆盖

- align-items，默认属 性为 auto，表示继承父元素的 align-items 比如说，用 flex 实现圣杯布局









### rem布局



### 百分比布局





### 浮动布局





## 实现rem 或 viewport 进行移动端适配



`rem` 适配原理

改变了一个元素在不同设备上占据的 CSS 像素的个数



rem适配的优缺点

- 优点： 没有破坏完美的视口
- 缺点： px 值转 rem 太过复杂





**viewport适配的原理**

viewport适配方案中，每一个元素在不同设备上占据的css像素的个数是一样的。但是css像素和物理像素的比例是不一样的，等比的

viewport适配的优缺点

- 在我们设计图上所量取的大小即为我们可以设置的像素大小，即所量即所设
- 缺点破坏完美视口







## 清除浮动的方式



- `clear: both` :   在该元素添加
- `overflow: hidden` :  在父元素添加
- 

