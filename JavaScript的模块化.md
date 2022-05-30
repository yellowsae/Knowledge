## 模块化



模块化解决的问题： 

1. 加载顺序
2. 污染全局作用域
3. 模块独立并且可以相互依赖





#### 早期的JavaScript模块化

早期使用模块化，都是将使用的模块写为一个 `js` 的文件，然后通过在 HTML的 `script` 的 `src` 属性引入该JS文件 



```js
// a.js 
var a = "testa"

// b.js 
var b = "testb"

// c.js 
var c = "testc"

// index.js
console.log(a)
console.log(b)
console.log(c)


// index.html
<script  src="a.js" />
<script  src="b.js" />
<script  src="c.js" />
<script  src="index.js" />
```



> 这样写的缺陷： 变量覆盖  ->  变量重名 ->  污染全局





#### 立即执行函数的模块化



使用了立即执行函数， 对模块内容进行封装， 解决了 *污染全局的问题* ，  *模块于模块之间可以依赖了*

```js
// a.js 
var ModuleA = (function () {
  // 作用域 独立 
  // 模块化的独立作用域
  var a = [1,2,3,4,5]
  
  // 引出去
  return {
    a: a
  }
})();

// b.js 
var ModuleB  = (function (ModuleA) { // 使用 ModuleA 注入参数
	var b = ModuleA.a.concat([6,7,8,9,10])
  // 引出去
  return {
    b: b
  }
})(ModuelA);


// c.js 
var ModuleC  = (function (ModuleB) {
  var c = ModuleB.b.join("-")
  return {
    c: c
  }
})(ModuleB);





// index.js
;(function (ModuleA,ModuleB,ModuleC) {
  console.log(ModuleA.a)
  console.log(ModuleB.b)
  console.log(ModuleC.c)
})(ModuleA,ModuleB,ModuleC);




// index.html
<script  src="a.js" />
<script  src="b.js" />
<script  src="c.js" />
<script  src="index.js" />
```



> 立即执行函数的模块化，不能够解决 *顺序问题* ， 只能解决*污染全局*和*模块的相互依赖*







#### NodeJS出现CommonJS 规范的模块化 

```js
// 引入模块 
require('xxx');  

// 导出模块 
module.exports
```

NodeJS的出现可以正式的对JS文件，进行导入和导出，  不依赖 HTML页面了， 必须要运行在Node环境中



CommonJS 规范的模块化体验

```js
// 基于webpack  
// 省略初始化 和 webpack 的配置

// a.js 
var a = (function () {
	return [1,2,3,4,5].reverse(); 
})();

// 引出 ModuleA 
module.exports =  {
  a: a
}

// b.js 
var ModuleA = require("./a.js")  // 引入A 模块
var b  = (function () {
	return ModuleA.a.concat([6,7,8,9,10])
})();
// 引出 B 模块 
module.exports =  {
  b: b
}


// c.js 
var ModuleB = require("./b.js")  // 引入A 模块
var c  = (function () {
	return ModuleB.b.join("-")
})();
// 引出 C 模块 
module.exports  = {
  c: c
}


// index.js   // webpack 的入口文件

var ModuleA = require("./a.js"),
	  ModuleB = require("./b.js"),
    ModuleC = require("./c.js");

console.log(ModuleA.a)
console.log(ModuleB.b)
console.log(ModuleC.c)


// index.html 
<script  src="index.js" />
```



NodeJS 相关的CommonJS  规范

> `CommonJS`  它是不是一种JS， 而是一种规范，模块化的规范，  来源于NodeJS 。 使用同步的方法。
>
> *服务端*使用的 `koa` 和` express ` 都是使用 `require()` 的方式引入



使用CommonJS 的好处 

> `CommonJS`  ->  `require` ，
>
> 1. 只要使用了 `require` 引入模块，  那么就会创建一个模块的实例    -> 实例化 
>
> 2. 因为Node运行的服务端， 使用`CommonJS`引入的模块， 就具备 **缓存机制** ； 只要使用了一次 `require` 引入的模块，接下来就是使用缓存
> 3. 使用 `CommonJS `的规范， 就一定是在 `NodeJS `上运行， 客户端上运行不了； 也就是说不依赖 `webpack` 解析node的话， `require` 就使用不了



`require()` 引入的本质

> `require` **不是一个全局变量**， 本质是一个 **立即执行函数**； *模块之间的引入，导出其实是使用了提前设置好的变量， 这些变量组成 require 引入的方法*   
>
> `exports, require, module, __filename, __dirname`
>
> ```js
> 
> // require() 引入的方法 本质
> 
> ;(function (exports, require, module, __filename, __dirname) {
>   
> })()
> ```









#### 客户端的 CommonJS —— AMD 规范 

**AMD  （Asynchronous Module  Definition ）  异步模块定义**  

```js
//  AMD 的语法

// 定义模块 
 // 参数： 1. 模块名， 2. 需要引入的模块名，3.本身的回调函数
define(moduleName,  [module],  factory); 

// 引入模块 
require([module], callback);
```

为什么会出现 `AMD`，  因为 `CommonJS `的规范在客户端运行不了，  出现 `AMD` 为了 解决 在客户端 (浏览器) 也能实现 模块之间的相互引用;



AMD 与 CommonJS 的 区别：

- AMD 是异步模块化定义 
- CommonJS  是同步





目前需要实现 AMD 的方式引入模块化 ： 使用 `RequireJS ` 

RequireJS 是一个能够实现了AMD规范的库； 用到需要下载 require.js 



AMD 的规范使用  :  ` defind() `   `require()`

```js

// index.html 
// 引入 AMD 的规范 require.js 
<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.3.6/require.js" />
<script src="./index.js" />
  
  
// a.js 
define(ModuleA,  function () {
  var a = [1,2,3,4,5]
  return {
    a: a.reverse()
  }
});




// b.js 
define(ModuleB, ['ModuleA'], function (ModuleA) {
  var b = [6,7,8,9]
  return {
    b: ModuleA.a.concat(b)
  }
});




// c.js
define(ModuleC, ['ModuleB'], function (ModuleB) {
  return {
    c: ModuleB.b.join('-')
  }
});


// index.js  
// 需要配置路径
require.config({
  paths: {
    ModuleA: './a.js',
    ModuleB: './b.js',
    ModuleC: './c.js',
  }
})

require(['ModuleA', 'ModuleB', 'ModuleC'], function (ModuleA, ModuleB,ModuleC) {
  console.log(ModuleA.a)
  console.log(ModuleB.b)
  console.log(ModuleC.c)
})
```









#### CMD 规范 

CMD 的规范与AMD 类似，  由 阿里开发

CMD （Common Module Definition）  通用模块化定义 

```js
// CMD 的语法使用

// 定义模块 
define(function (require, exports, module) {})
// require 加载    define 定义   exports 导出   module 操作模块


// 使用模块
seajs.use([modu路径], function (moduelA, moduleB, moduleC) {})
```

使用 CMD 与 AMD 相同， 需要使用  `seajs` 这个库

CMD 规范的使用

```js
// index.html

// 引入 seajs 
<script src="https://cdn.jsdelivr.net/npm/seajs@3.0.3/lib/sea.min.js"></script>


// 其他的步骤和  AMD 基本一样 使用就去查 
```

 

*AMD 和  CMD 的区别* : 

AMD ： 先导入， 先加载 ， 再执行

CMD ： 依赖就近 ， 按需加载 



需要查 文档







#### ES6 模块化 

语法 : 

```js
// 导入模块 
import module from "xxx"  

// 导出模块 
export module 
```



使用 es6 模块化 

```js
// a.js 

export default {
  a: [1,2,3,4,5].reverse()
}

// b.js 
import ModuleA  from "./a.js"

export default {
  b: ModuleA.a.concat([6,7,8,9,10])
}


// c.js
import ModuleB  from "./b.js"

export default {
  c: ModuleB.b.join('-')
}



// index.js
import ModuleA  from "./a.js"
import ModuleB  from "./b.js"
import ModuleC  from "./c.js"

console.log(ModuleA.a)
console.log(ModuleB.b)
console.log(ModuleC.c)
```



> 为什么有时候  import {}  /  import xxx   ;   
>
> 因为 使用了 `default` 关键字 ,   在使用 `export default`  表示默认导出一个对象使用一个 变量接收就行， 所以 `import ModuleA  from "xxx"`
>
> 在使用 `export const ModuleA = {}` ， 就使用 `import {ModuelA} from 'xxx'` 进行引入， `{ModuelA}` 表示解构出 ModuleA 









###  ES6 模块化 和 CommonJS 的区别 

1. ES6 使用 `import / export ` ,  而 CommonJS 使用 `require / module.export`
2. 二者的加载结果不同，CommonJS 输出的是一个值的拷贝（初始化时就拷贝）， 而ES6 输出的是值的引用
3. commonJS 模块是在运行时加载 （程序运行时存在了模块），ES6模块是在编译时加载（在编译时就是一个模块了）



YUI :  扩展知识









### 总结

https://www.bilibili.com/video/BV1K54y1S7zx

1、从JS诞生依赖的开发讲起，走JS文件调用越来越复杂，人们开始试图通过html文件来初步组织“模块化”的代码，但是为啥我JS模块化要依赖于你HTML，同时，对于程序的加载顺序和全局污染也带来了迫切的需求；（这个全局污染是不是被Java的封装降维打击了？）
2、于是，nodejs创新的搞出了模块化，给开发者带来了前所未有的体验；CommonJS规范应运而生！但是，nodejs是服务器端，受限于过去生态中浏览器各家厂商谁看谁不顺眼，浏览器端怎么办？模块化多好啊
3、于是，AMD YES！而RequireJS就是实现这个AMD规范的最佳范例，看代码的组织逻辑，确实过去的技术并不代表落后，我还是很喜欢RequireJS的代码组织逻辑和结构，感觉很像JAVA。（规范足够强，工程性就足够强！）
4、同时，阿里也为程序员搞出了CMD规划，通用模块定义，实现方式是seajs。但是和requirejs相比，cmd是依赖就近，而AMD是依赖前置，这是个效率问题的改进。
5、最终，ECMA“迫于压力”，为了程序员的幸福工作，推出了ES6模块化规范，import export！
6、但是CommonJS和ES6模块由本质的区别，CommonJS是拷贝，类似于类的对象；而ES6是直接的引用；所以，一个是运行时加载，一个是编译时加载（当然这句话的理解还是停留在表面）；



总结：
模块化其实本质解决的是加载顺序和全局污染，当然还有代码复用等程序员开发遇到的现实问题；
模块化最初尝试由nodejs提出，但是你不能只服务端啊，浏览器端也需要啊，于是AMD和CMD规范诞生；
模块化这个工作，其实更应该是EMCA来搞啊，可惜你没想到web发展如此之快，也没想到浏览器霸主ie掉落神坛了，于是迫于压力，推出了ES6模块化（甚至想搞类Class也搞的不伦不类）。