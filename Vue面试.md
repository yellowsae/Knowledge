# Vue 相关面试



## 对Vue的理解

vue， 是一个JavaScript的框架，主要用于开发单页面应用，它的官网上给他的的定义是渐进式框架，在前端这个行业受许多人喜欢。 

vue具有自己的数据驱动 ， (MVVM)模型 和 组件化编程， 内部优秀的指令系统。

与其他框架相比vue比较简单， 上手快。




## vue的MVVM模型

vue的数据驱动 MVVM。 
M - > Model 模型层  负责处理逻辑业务和服务端的交互

V - > View 视图层  负责将数据模型，转为UI展示出来，可以理解为HTML

VM -> View Model  视图模型层， 用来连接 Model 和 View 层的，实现模型层和视图层的通信， 是它们两个之间的通信的桥梁



## vue组件化的好处
组件化， 就是将开发的代码中的某一个模块，进行封装为一个组件，需要时候随时可以使用

在vue中组件化的好处

- 降低整个体系的耦合度、在保持接口不变的情况下， 可以替换不同的组件完成需求
- 调试方便，某一个组件出现问题， 可以放快速找到该组件 进行修复或移除
- 提高可维护性，由于每个组件的职责单一，并且组件在系统中是被复用的，所以对代码进行优化可获得系统的整体升级



## vue的指令系统
- v-if 
- v-for
- v-html
- v-show
- v-on
- v-bind
- v-model
- ...



## 讲对SPA单页面的理解

SPA 全称： Single Page Application,  即单页面应用。

SPA 页面是 它所需要的资源， 如HTML\CSS\JS 等，在一次请求中加就加载完成，也就是不刷新的动态加载。而对于普通的页面来说，所有的页面渲染、逻辑处理、页面路由、接口请求、都是在浏览器中发生。 对SPA页面来说， 页面的切换就是组件或是视图的切换

SPA页面只有一个HTML页面，在vue中通过vue-router 来对局部切换组件，而非刷新整个页面，来实现无刷新切换页面的技术





**单页面应用的优缺点**

优点：

- 具有桌面应用的即时性、网站的可移植性和可访问性
- 用户体验好、快，内容的改变不需要重新加载整个页面
- 良好的前后端分离，分工更明确



缺点： 

- 不利于搜索引擎的抓取
- 首次渲染速度相对较慢





## SPA和MAP的区别
单页面应用和多页面应用的区别

MPA -> MultiPage-page Application  多页面应用
MPA 中的每一个页面都是一个主页，在访问另一个页面时候都需要重新加载 html、css、js 等文件



单页面应用和多页面应用的区别

> |                 | 单页面应用（SPA）         | 多页面应用（MPA）                   |
> | :-------------- | :------------------------ | :---------------------------------- |
> | 组成            | 一个主页面和多个页面片段  | 多个主页面                          |
> | 刷新方式        | 局部刷新                  | 整页刷新                            |
> | url模式         | 哈希模式                  | 历史模式                            |
> | SEO搜索引擎优化 | 难实现，可使用SSR方式改善 | 容易实现                            |
> | 数据传递        | 容易                      | 通过url、cookie、localStorage等传递 |
> | 页面切换        | 速度快，用户体验良好      | 切换加载资源，速度慢，用户体验差    |
> | 维护成本        | 相对容易                  | 相对复杂                            |







## v-show 和 v-if 的区别和使用场景



#### v-if 和 v-show 的共同点

v-if 和 v-show 都能控制元素在页面是否展示。

- 当表达是为 true 时， 都会占据页面的位置
- 当表达式为 false 时， 都不会占据页面



#### v-if 和 v-show 的区别

- v-show 是给元素加上 `css--display: none`  , `dom` 元素依旧存在， v-if 显示和隐藏则是将 `dom` 元素整个添加或删除
- v-if 消耗性能较高、 v-show 在初始渲染时消耗较高
- v-if 绑定的表达式由 true -> false 时， 会触发vue的声明周期钩子 ， 比如 `mountde beforeCreated beforeDestory`  ，  而 v-show 并不会触发声明组件的生命周期



####  v-if 和 v-show 的使用场景

v-if  与  v-show 都能控制 dom  元素页面显示

v-if 于 v-show 相比开销更大 （直接操作DOM的添加与删除）

如果需要非常频繁的切换， 使用 v-show 更好

如果在运行时条件很少改变 ， 使用 v-if 更好







## 为什么Vue中不建议 v-if 和 v-for 一起连用



搜先   v-if  指令用于条件渲染一块内容。 这块内容当 v-if 为true值渲染

v-for 指令基于一个数组来渲染一个列表。 `v-for` 指令需要使用 `item in items` 形式的特殊语法，其中 `items` 是源数据数组或者对象，而 `item` 则是被迭代的数组元素的别名

在 `v-for` 的时候，建议设置`key`值，并且保证每个`key`值是独一无二的，这便于`diff`算法进行优化



用法： 

```vue
<data v-if="isShow"  />

<data v-for="item in items" :key="item.id">
	{{item.data}}
</data>
```





**优先级**

`v-if`与`v-for`都是`vue`模板系统中的指令

在`vue`模板编译的时候，会将指令系统转化成可执行的`render`函数

最终结论：`v-for`优先级比`v-if`高





**注意事项**

1. 永远不要把 `v-if` 和 `v-for` 同时用在同一个元素上，带来性能方面的浪费（每次渲染都会先循环再进行条件判断）

2. 如果避免出现这种情况，则在外层嵌套`template`（页面渲染不生成`dom`节点），在这一层进行v-if判断，然后在内部进行v-for循环

   ```vue
   <template v-if="isShow">
       <p v-for="item in items">
   </template>
   ```

3. 如果条件出现在循环内部，可通过计算属性`computed`提前过滤掉那些不需要显示的项





## 对vue生命周期的理解 



**生命周期的理解**

生命周期`（Life Cycle）`的概念应用很广泛，特别是在政治、经济、环境、技术、社会等诸多领域经常出现，其基本涵义可以通俗地理解为“从摇篮到坟墓”`（Cradle-to-Grave）`的整个过程**在`Vue`中实例从创建到销毁的过程就是生命周期，即指从创建、初始化数据、编译模板、挂载Dom→渲染、更新→渲染、卸载等一系列过程**





**vue的生命周期有哪些**

vue的生命周期可以分为8个阶段 ： 创建前后、 载入前后、更新前后、以及一些特殊场景的生命周期



> | 生命周期      | 描述                               |
> | :------------ | :--------------------------------- |
> | beforeCreate  | 组件实例被创建之初                 |
> | created       | 组件实例已经完全创建               |
> | beforeMount   | 组件挂载之前                       |
> | mounted       | 组件挂载到实例上去之后             |
> | beforeUpdate  | 组件数据发生变化，更新之前         |
> | updated       | 组件数据更新之后                   |
> | beforeDestroy | 组件实例销毁之前                   |
> | destroyed     | 组件实例销毁之后                   |
> | activated     | keep-alive 缓存的组件激活时        |
> | deactivated   | keep-alive 缓存的组件停用时调用    |
> | errorCaptured | 捕获一个来自子孙组件的错误时被调用 |



![vue](C:\Users\28415\Desktop\vue2生命周期.png)

**使用场景分析**

> | 生命周期      | 描述                                                         |
> | :------------ | :----------------------------------------------------------- |
> | beforeCreate  | 执行时组件实例还未创建，通常用于插件开发中执行一些初始化任务 |
> | created       | 组件初始化完毕，各种数据可以使用，常用于异步数据获取         |
> | beforeMount   | 未执行渲染、更新，dom未创建                                  |
> | mounted       | 初始化结束，dom已创建，可用于获取访问数据和dom元素           |
> | beforeUpdate  | 更新前，可用于获取更新前各种状态                             |
> | updated       | 更新后，所有状态已是最新                                     |
> | beforeDestroy | 销毁前，可用于一些定时器或订阅的取消                         |
> | destroyed     | 组件已销毁，作用同上                                         |







## 什么是虚拟DOM

`Virtual DOM `  是 `DOM ` 节点在 `JavaScript` 中的一种抽象的数据结构，之所以需要虚拟`DOM` , 是因为浏览器操作 `DOM` 的代价比较昂贵， 频繁的操作`DOM` 会产生性能问题。 



虚拟 `DOM` 的作用是在每一次响应式数据发生变化引擎页面重新渲染时， `Vue` 对比更新前后的虚拟 `DOM` , 匹配找出尽可能需要更新真实 `DOM` ,  从而达到提升性能的目的



虚拟`DOM`的实现原理主要包括以下3个部分

- 用 `JavaScript` 对象模拟真实 `DOM`数， 对真实`DOM`进行抽象
- `diff `算法 —— 比较两棵虚拟`DOM`树的差异
- `pach` 算法 —— 将两个虚拟`DOM`对象的差异应用到真正的`DOM`树





## vue组件间的传值方式



- `props /  $emit`  适用于 父子组件间的通信

- ref  适用于 父子组件间的通信

  `ref`：如果在普通的 `DOM` 元素上使用，引用指向的就是 `DOM` 元素；如果用在子组件上，引用就指向组件实例

- **`EventBus`** (`$emit / $on`) 适用于 父子、隔代、兄弟组件通信

  这种方法通过一个空的 `Vue` 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

- `provide / inject` 使用与隔代间组件的通信

- `Vuex` 适用于 父子、隔代、兄弟组件通信

  `Vuex` 是一个专为 `Vue.js` 应用程序开发的状态管理模式。每一个 `Vuex` 应用的核心就是 `store`（仓库）。`store` 基本上就是一个容器，它包含着你的应用中大部分的状态 ( `state` )。

  - `Vuex` 的状态存储是响应式的。当 `Vue` 组件从 `store` 中读取状态的时候，若 `store` 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
  - 改变 `store` 中的状态的唯一途径就是显式地提交 `(commit) mutation`。这样使得我们可以方便地跟踪每一个状态的变化。

> 父子组件
>
> - `props / $emit `  
> - `ref`   写在子组件中  
>
> 全局事件总线
>
> - `$emit /  $on `  
>
> 深度组件间的通信 
>
> - `provide /  inject`  
>
> Vuex ： vue的的仓库， 通过API访问数据
>
> - 全局访问



## `vue-router`  有几种模式

`vue-router` 有3种路由模式 ： `history` `hash`  `abstract`  

- `history` :  依赖 `HTML5 History API `  和服务器配置
- `hash` :  使用 `URL hash` 值来做路由。 支持所有浏览器
- `abstract` :  支持所有  `JavaSctipt` 运行环境， 如 `NodeJS` 服务器端。 如果发现浏览器的 API ， 路由会自动强制进入这个模式



> 总结： vue的路由有3中模式， 分别是 `hash`  `history`  `abstract`  。 

- history 模式
- hash  模式
- abstract 模式



## hash  和  history 模式的区别



#### hash 模式的实现原理

早期的前端路由实现是基于 `location.hash` 来实现的。 实现原理就是 `location.hash` 的值就是 `URL ` 中 `#` 后面的内容。 例如： `https://www.word.com#search `

`hash` 路由模式实现主要是基于以下几个特性

- `URL` 中 `hash` 值只是客户端的一种状态，也就是说当向服务器端发出请求时，`hash` 部分不会被发送；
- `hash` 值的改变，都会在浏览器的访问历史中增加一个记录。因此我们能通过浏览器的回退、前进按钮控制 `hash` 的切换；
- 可以通过 `a` 标签，并设置 `href` 属性，当用户点击这个标签后，`URL` 的 `hash` 值会发生改变；或者使用 `JavaScript` 来对 `loaction.hash` 进行赋值，改变 `URL` 的 `hash` 值；
- 我们可以使用 `hashchange` 事件来监听 `hash` 值的变化，从而对页面进行跳转（渲染）。



> 总结 hash模式：   hash 模式是 在 URL 路径中 带 `#` 号，
>
> url 中 hash 值是客户端的一种状态， hash 值的改变 浏览器的访问历史记录



#### history 模式的实现原理

`HTML5` 提供了 `History API` 来实现 URL 的变化。 其中做最主要的 API  主要有两个 `history.pushState()` 和 `history.replaceState()` 。 这两个 API 可以在不断刷新的情况下， 操作浏览器的历史纪录。 唯一不同的是，前者是新增一个历史记录，后者是直接替换当前的历史记录，如下所示： 

```js
window.history.pushState(null, null, path);
window.history.replaceState(null, null, path);
```

`history` 路由模式的实现主要基于存在下面几个特性：

- `pushState` 和 `replaceStace` 两个 API 来操作 URL的变化
- 我们可以使用  `popstate` 事件来监听URL的变化，从而对页面进行跳转（渲染）
- `history.pushState()` 或 `history.replaceState()` 不会触发 `popstate` 事件，这时我们需要手动触发页面跳转（渲染）。



> 总结： history 主要是根据浏览器的两个API  来检测URL的变化。  `history.pushState()  history.replaceState() `   ->  一个新增历史记录， 一个替换当前历史记录。
>
> 主要操作浏览器的历史记录 



## Vuex有哪些属性 

- State  :  定义默认的数据， 数据的初始状态
- Getter ： 能从 State 中获取数据， 并对 State 的数据进行加工修改。 类似于vue中的计算属性
- Mutation ： 是唯一更改 `store` 中状态的方法，且必须是同步函数。发送请求获取数据，保存到State中
- Action ： 用于提交 `mutation`，而不是直接变更状态，可以包含任意异步操作。
- Module ： 允许将单一的 `Store` 拆分为多个 `store` 且同时保存在单一的状态树中。



> 

Vuex 的原理图

![](https://vuex.vuejs.org/vuex.png)
