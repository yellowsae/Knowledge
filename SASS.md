# Sass

Sass 是一款强化 CSS 的辅助工具，它在 CSS 语法的基础上增加了变量 (variables)、嵌套 (nested rules)、混合 (mixins)、导入 (inline imports) 等高级功能，这些拓展令 CSS 更加强大与优雅。使用 Sass 以及 Sass 的样式库（如 [Compass](http://compass-style.org/)）有助于更好地组织管理样式文件，以及更高效地开发项目。





**特色功能：** 

- 完全兼容CSS3
- 在 CSS 基础上增加变量、嵌套 (nesting)、混合 (mixins) 等功能
- 通过[函数](http://sass-lang.com/docs/yardoc/Sass/Script/Functions.html)进行颜色值与属性值的运算
- 提供[控制指令 (control directives)](https://www.sass.hk/docs/#t8)等高级功能
- 自定义输出





**语法格式：**

Sass 有两种语法格式。首先是 SCSS (Sassy CSS) —— 也是本文示例所使用的格式 —— 这种格式仅在 CSS3 语法的基础上进行拓展，所有 CSS3 语法在 SCSS 中都是通用的，同时加入 Sass 的特色功能。此外，SCSS 也支持大多数 CSS hacks 写法以及浏览器前缀写法 (vendor-specific syntax)，以及早期的 IE 滤镜写法。这种格式以 .scss 作为拓展名。



另一种也是最早的 Sass 语法格式，被称为缩进格式 (Indented Sass) 通常简称 "Sass"，是一种简化格式。它使用 “缩进” 代替 “花括号” 表示属性属于某个选择器，用 “换行” 代替 “分号” 分隔属性，很多人认为这样做比 SCSS 更容易阅读，书写也更快速。缩进格式也可以使用 Sass 的全部功能，只是与 SCSS 相比个别地方采取了不同的表达方式，具体请查看 [the indented syntax reference](http://sass-lang.com/docs/yardoc/file.INDENTED_SYNTAX.html)。这种格式以 .sass 作为拓展名。



一般使用 `.scss` 比较多

# 安装Sass

```bash
// 全局安装
npm install -g sass



// 编译scss 文件
sass input.scss ouput.css

// 监视模式
sass -w  input.scss ouput.css
```



# 1. 注释



sass的注释有两种

```css
/*
  注释一
*/

// 注释二
```

当sass编译为css时， 第一种注释会被编译到 css 文件，  而第二种不会， 只会在scss文件看到





# 2. 变量

*变量（定义变量后，在选择器里可以直接引用）：*

```scss
// 1. 使用变量 
// 1. 变量（定义变量后，在选择器里可以直接引用）：

$yanse: rgb(223, 148, 148);

// 边框使用变量， -> 使用变量 -> 类似套娃
$kuang: 10px solid $yanse;


body {
  margin: 0;
  padding: 0;
  h2 {
    // 使用 SASS 的变量
    color: $yanse;
    // 使用 定义边框的语句
    border: $kuang;
  }
}
```











# 3. 嵌套



```scss
body {
  margin: 0;
  padding: 0;
  h2 {
    // 使用 SASS 的变量
    color: $yanse;
    // 使用 定义边框的语句
    border: $kuang;
  }

  // 不止选择器，属性里也可以嵌套，如这样写： 
  div {
    height: 100px;
    background: {
      color: blue;
    }
    // 属性嵌套
    font: {
      family: "fangsong";
      size: 20px;
      weight: 700;
    }
    border: $kuang {
      left: 0;
      top: 0;
    }
  }


  // 使用定义的 mixin 混合参数
  span {
    @include hunhe;
  }
}
```







