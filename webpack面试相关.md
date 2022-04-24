## webpack 中的source-map 是什么？ 生产环境怎么使用





**source-map**

- source map是将**编译、打包、压缩后的代码映射回源代码的过程**。打包压缩后的代码不具备良好的可读性，想要调试源码就需要 soucre map。  -> 简单来说就是源代码的映射



**生产环境使用 source-map**

hidden-source-map：借助第三方错误监控平台Sentry使用

nosources-source-map：只会显示具体行数以及查看源代码的错误栈。安全性比source map高

source：通过nginx设置将.map文件只对白名单开放(公司内网)







## webpack 的 hash 分类

