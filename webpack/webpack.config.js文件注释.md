```
配置：
webpack.config.js

在项目下创建一个webpack.config.js(默认，可修改)文件来配置webpack

module.exports = {
    entry: '',               // 入口文件
    output: {},              // 出口文件
    module: {},              // 处理对应模块
    plugins: [],             // 对应的插件
    devServer: {},           // 开发服务器配置
    mode: 'development'      // 模式配置
}

以上就是webpack的正常配置模块

★ 启动devServer需要安装一下webpack-dev-server

npm i webpack-dev-server -D

```



```
**package.json** 
```



```


"scripts": {

"test": "echo \"Error: no test specified\" && exit 1",

"dev": "webpack --mode development",      （调试）

"build": "webpack --mode production"     （生产）打包


```

 require('css-loader!./assets/css/hello.less')执行npm run dev 显示成功。打开页面，但是页面css并没有生效，想要文件生效，还需要用到style-loader less-loader 这里有个坑哇，一定要注意顺序。如下：

require('style-loader!css-loader!less-loader!./assets/css/hello.less')





```
多入口文件 打包成一个
entry: ['./src/index.js', './src/login.js'], 
output: {
         filename: 'bundle.js',
 

多入口和多出口需要写成对象的方式

entry: {
        index: './src/index.js',
        login: './src/login.js'
    },

output: {
        
        //  [name]就可以将出口文件名和入口文件名一一对应
        filename: '[name].js',      // 打包后会生成index.js和login.js文件
        path: path.resolve('dist')
    }

```











项目

const path = require('path');

const HtmlWebpackPlugin = require('html-webpack-plugin');

const ExtractTextWebpackPlugin = require('extract-text-webpack-plugin');

const webpack = require('webpack');

module.exports = {

entry:'./src/index.js',

output:{

path:path.resolve(__dirname,'dist'),

filename:'bundle..js' // 表示输出的js文件名

},

plugins: [

// 通过new一下这个类来使用插件

new HtmlWebpackPlugin({

// 用哪个html作为模板

// 在src目录下创建一个index.html页面当做模板来用

template: './src/index.html',

hash: true, // 会在打包好的bundle.js后面加上hash串

}),

new ExtractTextWebpackPlugin('css/style.css') ,

new webpack.HotModuleReplacementPlugin()

],

module: {

rules: [

{

test: /\.css$/, // 解析css

use: ExtractTextWebpackPlugin.extract({

// 将css用link的方式引入就不再需要style-loader了

use: 'css-loader' ,

publicPath: '../'

}) // 从右向左解析

/*

也可以这样写，这种方式方便写一些配置参数

use: [

{loader: 'style-loader'},

{loader: 'css-loader'}

]

*/

},

{

test: /\.(jpe?g|png|gif)$/,

use: [

{

loader: 'url-loader',

options: {

limit: 8192, // 小于8k的图片自动转成base64格式，并且不会存在实体图片

outputPath: 'images/' // 图片打包后存放的目录

}

}

]

},

{

test: /\.(htm|html)$/,

use: 'html-withimg-loader'

},

{

test: /\.(eot|ttf|woff|svg)$/,

use: 'file-loader'

},

{

test:/\.js$/,

use: 'bable-loader',

include: /src/, // 只转化src目录下的js

exclude: /node_modules/ // 排除掉node_modules，优化打包速度

} //babel

]

},

devServer: {

contentBase: './dist',

host: 'localhost', // 默认是localhost

port: 3000, // 端口

open: true, // 自动打开浏览器

hot: true // 开启热更新

},

resolve: {

// 别名

alias: {

$: './src/jquery.js'

},

// 省略后缀

extensions: ['.js', '.json', '.css']

},

};