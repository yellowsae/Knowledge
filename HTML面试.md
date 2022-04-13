

## 01. src 和 href 的区别

src和href都是**用来引用外部的资源**，它们的区别如下：

- src ：表示对资源的引用， 它指向的内容会嵌入到当前标签所在的位置。 src 会将其指向的资源下载并应用到文档内， 如请求 js 脚本。 当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载，编译，执行完毕，所以一般js脚本放在页面的底部 
- href ： 表示超文本引用， 它指向一些网络资源，建立和当前元素或文档的链接关系。 当浏览器识别到它指向的文件时，就会并行下载，不会停止对当前文档的处理， 通常用来 a  link 等标签上



> 本总结：
>
> src 和 href 都是对外部资源的引用。  
>
> src 引用的资源会插入到当前标签所在位置
>
> href 对元素或者文本生成对应的链接关系
>
> 浏览器解析 src 会暂停其他资源的下载，知道src引入的资源 加载、编译、执行完毕
>
> 浏览器 解析 href 不会暂停当前文档的处理，而是并行下载









## 02 对HTML语义化的理解

语义化表示根据内容结构的语义化 （内容语义化）， 选择合适的标签 （代码语义化） 。

通俗来讲就是使用正确的标签来做正确的事



HTML语义化的好处 

- 对机器友好，带有语义的文字表现力丰富，更适合搜索引擎的爬虫爬取有效信息，有利于SEO。除此之外，语义类还支持读屏软件，根据文章可以自动生成目录
- 对开发者友好，使用语义类标签增强了可读性，结构更加清晰，开发者能清晰的看出网页的结构，便于团队的开发与维护。



常见的语义化标签

```html
<header></header>  头部

<nav></nav>  导航栏

<section></section>  区块（有语义化的div）

<main></main>  主要区域

<article></article>  主要内容

<aside></aside>  侧边栏

<footer></footer>  底部
```





##  03`<!DOCTYPE html>` 文档类型的作用



`<!DOCTYPE html>` 不是一个标签而是一个声明 `DOCTYPE `  ，大写， 必须大写。 **它的作用就是告诉浏览器使用那个版本的HTML来解析文档** 。 不同的渲染模式会影响浏览器对 CSS 代码或JavaScript 脚本解析。 必须在写第一行



扩展： 浏览器选择页面的两种模式

- *`CSS1Compat `标准模式，W3C兼容性模式*  ,  默认模式，浏览器使用W3C的标准解析渲染页面。在标准模式中，浏览器以其支持的最高标准呈现页面
- *`BackCompat`  浏览器的怪异模式* : 浏览器使用自己的怪异模式解析渲染页面。在怪异模式中，页面以一种比较宽松的向后兼容的方式显示。





## 04. script标签中defer和async的区别

如果没有 `defer` 和 `async` ， 浏览器会立即加载并执行相应的脚本。 它不会等待后续加载的文档元素，而是读取到就开始加载执行， 这样就堵塞了后续文档的加载。



文档加载图

![image-20220410113650033](C:\Users\28415\AppData\Roaming\Typora\typora-user-images\image-20220410113650033.png)

其中蓝色代表js脚本网络加载时间，红色代表js脚本执行时间，绿色代表html解析。



相同： 

**`defer` 和   `anycn` 属性都是去异步加载外部的JS脚本， 它们都不会阻塞页面的解析** 

 

区别： 

- **执行顺序：** 多个带`async`属性的标签，不能保证加载的顺序；多个带defer属性的标签，按照加载顺序执行；
- **脚本是否并行执行：async属性，表示后续文档的加载和执行与js脚本的加载和执行是并行进行的**, 即异步执行；defer属性，加载后续文档的过程和js脚本的加载(此时仅加载不执行)是并行进行的(异步)，js脚本需要等到文档所有元素解析完成之后才执行，DOMContentLoaded事件触发执行之前。



> 自总结： 
>
> 在浏览器没有 async 和  defer 属性时， 浏览器解析到 script 标签，会对标签所指向的资源进行加载，编译，执行操作，会影响到文章后的资源加载
>
> 当浏览器使用了  async 和 defer 属性时，加载资源是并行加载的，并不会影响到后续资源的加载。

> async 和  defer 的区别： 
>
> - 执行顺序 ：
>   - 多个async 属性不能保证加载的顺序
>   - 多个defer 属性能够保证加载按照顺序来执行
> - 脚本是否并行执行：
>   - async 属性，表示后续文档的加载和执行和 JS 脚本执行是并行的



## 05 常用的 meta 标签有哪些



`meta` 标签由 `name`  和  `content` 属性定义， **用来描述网页文档的属性**， 比如网页的作者，网页描述，关键词等，除了HTTP标准固定了一些`name`作为大家使用的共识，开发者还可以自定义name。

常用的meta标签： 

（1）`charset`，用来描述HTML文档的编码类型：

```html
<meta charset="UTF-8" / >
```

（2）`keywords`, 页面关键词 

```html
<meta name="keywords" content="关键词" />
```

（3） `refresh` ， 页面重定向和刷新

```html
<meta http-equiv="refresh" content="0;url=" />
```

（4） `description`，页面描述：

```html
<meta name="description" content="页面描述内容" />
```

（5）`viewport`，适配移动端，可以控制视口的大小和比例：

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">
```

其中，`content` 参数有以下几种：

- `width viewport` ：宽度(数值/device-width)
- `height viewport` ：高度(数值/device-height)
- `initial-scale` ：初始缩放比例
- `maximum-scale` ：最大缩放比例
- `minimum-scale` ：最小缩放比例
- `user-scalable` ：是否允许用户缩放(yes/no）

（6）搜索引擎索引方式：

```html
<meta name="robots" content="index, follow" />
```

其中，`content` 参数有以下几种：

- `all`：文件将被检索，且页面上的链接可以被查询；
- `none`：文件将不被检索，且页面上的链接不可以被查询；
- `index`：文件将被检索；
- `follow`：页面上的链接可以被查询；
- `noindex`：文件将不被检索；
- `nofollow`：页面上的链接不可以被查询。



> 自总结： 
>
> meta 标签用来描述网页文档的属性， 由  name 和 content 属性定义
>
> - 定义编码类型 `charset`
> - 定义页面关键词   `keywords`
> - 网页的描述 `description`
> - 页面的重定向  `refresh`
> - 适配移动端 `viewport` 
> - 搜索引擎索引方式 `robots`





## 06 HTML5 有哪些更新 



#### 1. 语义化标签

- `header` 定义文档的页眉（头部）；
- `nav`  定义页面的导航栏
- `footer`  定义页面的底部或尾部
- `article`   定义页面的文章内容
- `section` 定义文档中的节（section、区段）
- `aside` 定义文档中的侧边内容
- `main`  页面的主题内容



#### 2. 媒体标签

这些`HTML5` 添加的新的标签 代替了 旧时网站使用 `flash ` 

1.  `audio`  音频

   ```html
   <audio src="" controls  autoplay loop='true'></audio>
   ```

   属性：

   - `controls `控制面板
   - `autoplay` 自动播放
   - `loop='true'` 循环播放

2. `video`

   ```html
   <video src='' poster='imgs/aa.jpg' controls></video>
   ```

   属性：

   - poster：指定视频还没有完全下载完毕，或者用户还没有点击播放前显示的封面。默认显示当前视频文件的第一帧画面，当然通过poster也可以自己指定。
   - controls 控制面板
   - width
   - height

3. `source`标签 因为浏览器对视频格式支持程度不一样，为了能够兼容不同的浏览器，可以通过source来指定视频源。

   ```html
   <video>
    	<source src='aa.flv' type='video/flv'></source>
    	<source src='aa.mp4' type='video/mp4'></source>
   </video>
   ```



#### 3 表单标签

**表单类型：**

- email ：能够验证当前输入的邮箱地址是否合法
- url ： 验证URL
- number ： 只能输入数字，其他输入不了，而且自带上下增大减小箭头，max属性可以设置为最大值，min可以设置为最小值，value为默认值。
- search ： 输入框后面会给提供一个小叉，可以删除输入的内容，更加人性化。
- range ： 可以提供给一个范围，其中可以设置max和min以及value，其中value属性可以设置为默认值
- color ： 提供了一个颜色拾取器
- time ： 时分秒
- data ： 日期选择年月日
- datatime ： 时间和日期(目前只有Safari支持)
- datatime-local ：日期时间控件
- week ：周控件
- month：月控件

**表单属性：**

- placeholder ：提示信息
- autofocus ：自动获取焦点
- autocomplete=“on” 或者 autocomplete=“off” 使用这个属性需要有两个前提：
  - 表单必须提交过
  - 必须有name属性。
- required：要求输入框不能为空，必须有值才能够提交。
- pattern=" " 里面写入想要的正则模式，例如手机号patte="^(+86)?\d{10}$"
- multiple：可以选择多个文件或者多个邮箱
- form=" form表单的ID"

**表单事件：**

- oninput 每当input里的输入框内容发生变化都会触发此事件。
- oninvalid 当验证不通过时触发此事件。



#### 4 进度条、度量器

- progress标签：用来表示任务的进度（IE、Safari不支持），max用来表示任务的进度，value表示已完成多少
- meter属性：用来显示剩余容量或剩余库存（IE、Safari不支持）
  - high/low：规定被视作高/低的范围
  - max/min：规定最大/小值
  - value：规定当前度量值



#### 5 DOM的查询 

- `document.querySelector()` 
- `document.querySelectorAll()` 

它们选择的对象可以是标签，可以是类(需要加点)，可以是ID(需要加#)



#### 6 Web存储

HTML5 提供了两种在客户端存储数据的新方法：

- `LocalStorage`  :   没有时间限制的存储
- `SessionStorage`  ： 针对一个 session 的存储



#### 7 其他

- 拖放：拖放是一种常见的特性，即抓取对象以后拖到另一个位置。设置元素可拖放：

```html
<img draggable="true"/>
```



- 画布 (canvas) :  `canvans` 元素的使用 JavaScript 在网页上绘制图像

  ```html
  <canvas id="myCanvas" width="200" height="100"></canvas>
  ```

- SVG：SVG 指可伸缩矢量图形，用于定义用于网络的基于矢量的图形，使用 XML 格式定义图形，图像在放大或改变尺寸的情况下其图形质量不会有损失，它是万维网联盟的标准
- 地理定位：Geolocation（地理定位）用于定位用户的位置



**总结：** （1）新增语义化标签：nav、header、footer、aside、section、article （2）音频、视频标签：audio、video （3）数据存储：localStorage、sessionStorage （4）canvas（画布）、Geolocation（地理定位）、websocket（通信协议） （5）input标签新增属性：placeholder、autocomplete、autofocus、required （6）history API：go、forward、back、pushstate

**移除的元素有：**

- 纯表现的元素：basefont，big，center，font, s，strike，tt，u;
- 对可用性产生负面影响的元素：frame，frameset，noframes；







## 07 img 的 srcset 属性的作用



当响应式页面中 用到根据屏幕密度设置不同的图片。  会用到 img  的 srcset  属性。 

`srcset` 属性用于设置不同屏幕下，img 会加载不同的图片。 

```html
<img src="image-128.png" srcset="image-256.png 2x" />
```

使用上面的代码，就能实现在屏幕密度为1x的情况下加载image-128.png, 屏幕密度为2x时加载image-256.png。



用到就去查 

> 结论：  img 的 `srcset` 属性的作用就是 根据屏幕的大小宽度， 来展示不同图片





## 08 行内元素有哪些？块级元素有哪些？ 空(void)元素有那些？

常见的 

- 行内元素： `a  b span  img strong i input select`
- 跨级元素：`div  p  h1~h6  dd  dt  ol  ...`
- 空元素：  `br hr  img  input  link  meta `

空元素，即没有内容的HTML元素。空元素是在开始标签中关闭的，也就是空元素没有闭合标签：







## 09  说一下 web worker 



在 HTML 页面中，如果在执行脚本时，页面的状态是不可相应的，直到脚本执行完成后，页面才变成可相应。web worker 是运行在后台的 js，独立于其他脚本，不会影响页面的性能。 并且通过 `postMessage` 将结果回传到主线程。这样在进行复杂操作的时候，就不会阻塞主线程了。

如何创建 web worker：

1. 检测浏览器对于 web worker 的支持性
2. 创建 web worker 文件（js，回传函数等）
3. 创建 web worker 对象



> 总结来说： web worker  就是 运行在浏览器后台的js ， 独立其他脚本， 不会影响页面的性能。 





## 10 HTML5 的离线存储怎么使用， 它的工作原理什么



离线存储指的是： 在用户没有联网时， 可以正常的访问站点或应用。  在用户连上网时，更新用户机器上的缓存文件。



**原理** ： HTML5 的离线缓存是基于一个新建的 `.appcache` 文件的缓存机制（不是存储技术），通过这个文件上的解析清单离线存储资源， 这些资源会像 cookie 一样被存储下来。当网络处于离线状态时，浏览器会通过被离线存储的数据进行页面展示。



**使用方法： 	** 

1. 创建一个和 `html` 同名的 `manifest` 文件， 然后在`html`页面头部加入 `manifest` 属性

   ```html
   <html lang='en' manifest='index.manifest'>
    <!--- manifest='index.manifest' -- >
   ```

2. 在 `cache.manifest` 文件中编写需要离线存储的资源

   ```html
   CACHE MANIFEST
       #v0.11
       CACHE:
       js/app.js
       css/style.css
       NETWORK:
       resourse/logo.png
       FALLBACK:
       / /offline.html
   ```

   **CACHE**: 表示需要离线存储的资源列表，由于包含 manifest 文件的页面将被自动离线存储，所以不需要把页面自身也列出来。

   **NETWORK**: 表示在它下面列出来的资源只有在在线的情况下才能访问，他们不会被离线存储，所以在离线情况下无法使用这些资源。不过，如果在 CACHE 和 NETWORK 中有一个相同的资源，那么这个资源还是会被离线存储，也就是说 CACHE 的优先级更高。

   **FALLBACK**: 表示如果访问第一个资源失败，那么就使用第二个资源来替换他，比如上面这个文件表示的就是如果访问根目录下任何一个资源失败了，那么就去访问 offline.html 。

   
   
3. 在离线状态时， 操作 `window.applicationCache` 进行离线存储



**如果更新缓存： ** 

- 更新 `manifest` 文件
- 通过 `javascript` 操作
- 清除浏览器缓存



**注意事项： **

- 浏览器对缓存数据的容量可能不一样 （一般都是 5MB）
- 如果 manifest 文件，或者内部列举的某一个文件不能正常下载，整个更新过程都将失败，浏览器继续全部使用老的缓存。
- 引用 manifest 的 html 必须与 manifest 文件同源，在同一个域下。
- FALLBACK 中的资源必须和 manifest 文件同源。
- 当一个资源被缓存后，该浏览器直接请求这个绝对路径也会访问缓存中的资源。







## 11  浏览器是如何对 HTML5 的离线储存资源进行管理和加载？

   

- 在线的情况下： 

  **浏览器发现 html 头部有 manifest 属性，它会请求 manifest 文件，如果是第一次访问页面 ，那么浏览器就会根据 manifest 文件的内容下载相应的资源并且进行离线存储。**如果已经访问过页面并且资源已经进行离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的 manifest 文件与旧的 manifest 文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，就会重新下载文件中的资源并进行离线存储。

- 在离线的情况下： 浏览器会直接使用离线存储的资源。





## 12  title 与  h1 的区别、b 与 strong 的区别、i 与 em 的区别



- title 属性没有明确意义只表示 是一个 标签 ,   H1 则表示层面明确的标签， 对页面信息的抓取有很大的影响
- strong 标签有语义化， 加强语气的效果， 而 b 标签没有，只是个简单的加粗而已。在页面上，浏览器更侧重 strong 标签
- i 在内容展示的是  斜体， em 表示强调的文本



## 13 iframe 有哪些优缺点



iframe 元素会创建包含另一个文档的内联框架 -> 行内框架

优点： 

- 用来加载速度较慢的内容 -> 例如广告
- 可以使脚本可以并行下载
- 可以实现跨子域通信

缺点：

- iframe 会阻塞主页面的 onload 事件
- 无法被一些搜索引擎识别
- 会产生很多页面 ， 不容易管理



## 14   label 标签的作用是什么

label 标签来定义表单控件的关系：当用户选择 label 标签时， 浏览器会自动聚焦到 label 标签相关的表单控件上。 

```html
<label for='mobile'>Number</label>
<input type='text' id='mobile' />
```

```html
<label>Date: <input type='text' /></label>
```



## 15  img 的 title 和 alt 作用和区别 



`img `标签的中的 `title `和 `alt `属性基本都是对 `img `图片本身的描述

只不过  title 在鼠标停在图片上时，出现对img 描述的文本内容

而 `alt`属性是 当 `img`遇到一些原因导致显示不出来， `alt `才在图片位置显示，提示图片的加载出错的字体描述



## 16 Canvas 和 SVG 的区别

https://juejin.cn/post/6905294475539513352#heading-14





## 17 head 标签有什么作用，其中什么标签是必不可少 



`head` 标签用于定义文档头部， 它是所有头部元素的容器， head 标签中的元素可以引入脚本、指示浏览器在哪里找到样式，提供元信息等。 



文档的头部描述了文档的各种属性和信息， 包括文档的标题、在Web 中的位置以及和其他文档的关系等  。绝大多数文档头部数据都不会真正作为内容显示给读者 



`<base>  <link>  <script>  <style>  <title>`  这些标签都是用在 `head` 标签中

其中 `<title>` 定义文档的标题，它是 head 部分中唯一必需的元素。



## 18 文档声明（Doctype）和`<!Doctype html>`有何作用? 严格模式与混杂模式如何区分？它们有何意义?



**文档声明的作用** ： 文档声明是为了告诉浏览器， 当前HTML文档使用什么版本的　HTML　来写的，这样的浏览器才能安装声明的版本在正确解析。　

`<!DOCTYPE html>`作用：　就是告诉浏览器进入标准模式，使用最新的HTML5  标准来解析渲染页面； 如果不写，浏览器就会进入混杂模式。 



**严格模式与混杂模式的区分：**

- 严格模式： 也是标准模式，是指浏览器安装 W3C 标准来解析代码 
- 混杂模式： 又称浏览器的怪异模式 ， 是指 浏览器使用自己本身方式来解析代码 ，混杂模式通常模拟老式浏览器的行为，以防止老站点无法工作；



总之 ， **严格模式让各个浏览器统一执行一套规范兼容模式保证了旧网站的正常运行。**



## 19 浏览器乱码的原因是什么？如何解决？



**产生乱码的原因**

- 网页的源代码是 `gbk` 的编码 内容中的 中文 文字是 `utf-8` 编码。 这样浏览器打开会出现 html 乱码
- `html`网页编码是`gbk`，而程序从数据库中调出呈现是`utf-8`编码的内容也会造成编码乱码；
-  浏览器不能自动检测网页编码，造成网页乱码。



**解决办法：**

- 使用软件编辑HTML网页内容；
- 如果网页设置编码是`gbk`，而数据库储存数据编码格式是`UTF-8`，此时需要程序查询数据库数据显示数据前进程序转码；
- 如果浏览器浏览时候出现网页乱码，在浏览器中找到转换编码的菜单进行转换。
