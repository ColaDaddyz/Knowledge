# Webpack
## 代码体积优化
code-split，externals,CommonsChunkPlugin
使用了code-split后注意extraTextPlugin需要加alltrunks:true 将所有的样式文件打包到一起
## bundle分析
webpack-visualizer 和BundleAnalyzerPlugin 是两个用来分析bundle大小的工具，如果需要分析bundle的依赖的话可以用webpack生成的json，然后用官方的分析工具去分析

## 插件
- UglifyJsPlugin 不多说了，代码混淆压缩
- CommonsChunkPlugin 抽取公共代码
- DedupePlugin 消除重复的模块（webpack2已内置）
- OccurrenceOrderPlugin 让依赖次数多的模块靠前分到更小的id来达到输出更多的代码 (webpack2已内置)


## 优化开发体验
### 缩小文件搜索范围
将resolve.modules配置为`node_modules`，像使用 `impot "react"`这种时webpack遍历向上递归查到node_modules，但通常只有一个`node_modules`，为了减少可以直接写明

loader可以写include
比如 babel的loader可以只对src目录里的代码进行编译，忽略庞大的node_modules

```
{
	test:/\.js$/,
	loader:'babel-oader',
	include:path.resolve(__dirname,'src')
}

```
### 使用alias
发布到npm的库大多包含两个目录，一个是放cmd模块化的lib目录，一个是所有文件合并成的dist目录，多数入口文件是指向lib的。默认情况下webpack会去读lib目录下的入口文件再去递归加载其他以来的文件，这个过程非常耗时，`alias`可以让webpack直接使用dist目录的整体文件减少递归
### 使用noParse
配置哪些文件可以脱离Webpack解析，有些库是自成一体，不需要依赖别的库的，webpack无需解析他们的依赖

happyPack，DLLPlugin
happyPack使用后无法使用postcss


TODO
https://github.com/lcxfs1991/blog/issues/2



### 资源整理
webpack源码以及流程分析
http://taobaofed.org/blog/2016/09/09/webpack-flow/

如何解决hash的问题
https://github.com/zhenyong/Blog/issues/1
http://www.cnblogs.com/ihardcoder/p/5623411.html
https://github.com/zhenyong/webpack-stable-module-id-and-hash

如何写webpack插件
https://github.com/lcxfs1991/blog/issues/1
https://webpack.github.io/docs/how-to-write-a-plugin.html
https://webpack.github.io/docs/plugins.html#the-compiler-instance

