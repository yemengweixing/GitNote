#### 原始的html文件中删除<src>和<link>标签 



webpack4最新文档，建议每个项目都是用单独的webpack，也就是局部安装。这样一个项目中的package.json都能管理好依赖的环境包了。再全局安装一遍webpack和webpack-cli用的是全局的，并没有起到局部安装的效果。

局部安装的时候，这些可执行包的执行文件，也就是cmd文件，都在项目的node_module/.bin目录下，npx命令就是自动去该目录下去找执行文件。

所以，局部安装该项目自己的webpack和webpack-cli，并且执行，就几条命令：

npm init -y
npm install webpack -D
npm install webpack-cli -D

//简化 npm i webpack webpack-cli -D

写好webpack配置文件后，打包命令:
npx webpack







```
全局安装
1 npm init

2 npm install -g webpack
//webpack -v             查看webpack 版本号
便在C:\Users\你的用户名\AppData\Roaming\npm\node_modules创建了webpack文件夹

3 npm install -g webpack-cli （17年出现 安装这个才能查看版本号）
```

//webpack -h                   查看webpack-cli 版本号

//-g webpack  或者webpack -g 在前在后 都可以安装



4 安装 npm install webpack-dev-server -g







本地安装



1项目文件夹 （

webpack-demo 常用例子命名的文件夹

）

命令行 cd到文件夹 //cd webpack-demo 

没有就mkdir webpack-demo 

或者 直接新建一个空的文件夹   



2 npm init

在终端中使用`npm init`命令可以自动创建这个package.json文件

内容就是一堆json数据

终端会问你一系列诸如项目名称，项目描述，作者等信息，不过不用担心，如果你不准备在npm中发布你的模块，这些问题的答案都不重要，回车默认即可。



```
3  npm i webpack -D
安装到你的项目目录
//不简化 npm install --save-dev webpack  （或者npm install webpack --save-dev 都可以）
```



```
4 简化命令 npm i webpack-cli -D
```

`输入命令【npm install --save-dev  webpack-cli 】`（或者npm install webpack-cli --save-dev 都可以）

```

webpack 4x以上，webpack将命令相关的内容都放到了webpack-cli，所以还需要安装webpack-cli
```



生成配置文件`webpack.config.js`



``

```


有了webpack.config.js这个文件之后，你可以调用Webpack且不需要任何参数。
```

``

//3+4 **简化 npm i webpack webpack-cli -D**

```



```

``

```

5模式区分   

配置项mode配置生产或开发环境     

默认有production（生产）和development（开发）两种模式可以设置（打包）


//默认没有配置

development：开发模式，打包默认不压缩代码，默认开启代码调试

优化开发时的增量构建，另外 process.env.NODE_ENV 会被设置为 development,无需再用 define 插件定义。

```

production：生产模式，上线时使用，打包压缩代码，不开启代码调试

```

会开启各种特性优化构建，使用 scope hoisting 和 tree-shaking,自动启用 uglifyjs 对代码进行压缩,并且会自动将 process.env.NODE_ENV 设置为 production。
进行打包，入口文件是'./src/index.js'，输出路径是'./dist/main.js'，其中src目录即index.js文件需要手动创建，而dist目录及main.js会自动生成

1可通过命令行 webpack --mode development/production   进行模式切换

2在配置文件中添加mode配置项进行模式选择


在package.json中scripts中加入两个：

1 "dev":"webpack --mode development",
2 "build":"webpack --mode production"

以后我们只需要在命令行执行npm run dev便相当于执行webpack --mode development，
执行npm run build便相当于执行webpack --mode productio （打包）


```

``

``

``

```

```

## `6     Html模板          //需要src/index.html文件`

```


通过一个模板实现打包出引用好路径的html来     插件     **html-webpack-plugin**

```



```
npm i html-webpack-plugin -D           安装插件
webpack.config里引用
let path = require('path');
// 插件都是一个类，所以我们命名的时候尽量用大写开头
let HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        filename: 'bundle..js',   
        path: path.resolve('dist')
    },
    plugins: [
        // 通过new一下这个类来使用插件
        new HtmlWebpackPlugin({
            // 用哪个html作为模板
            // 在src目录下创建一个index.html页面当做模板来用
            template: './src/index.html',
            hash: true, // 会在打包好的bundle.js后面加上hash串
        })
    ]
}

```

### `**多页面开发**`

```

module.exports = {
    // 多页面开发，怎么配置多页面
    entry: {
        index: './src/index.js',
        login: './src/login.js'
    },
    // 出口文件  
    output: {                       
        filename: '[name].js',
        path: path.resolve('dist')
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html',   
            filename: 'index.html',
            chunks: ['index']   // 对应关系,index.js对应的是index.html
        }),
        new HtmlWebpackPlugin({
            template: './src/login.html',
            filename: 'login.html',
            chunks: ['login']   // 对应关系,login.js对应的是login.html
        })
    ]
}


```



``

`7.1     `引用CSS文件          在src/index.js里引入css文件

打包后的css文件是以行内样式style的标签写进打包后的html页面中



```
**loader 模块（处理css文件 webpack不支持css文件类型，需要依赖loader）**
**命令 npm install css-loader style-loader --save-dev 简化 npm i css-loader style-loader -D**
**css-loader：使webpack可以处理css文件**

**style-loader：新建一个style标签，把css-loader处理过的文件放进去，然后插入到HTML标签中**
```



```
//src/ index.js
import './css/style.css';   // 引入css
import './less/style.less'; // 引入less
```

``

```
// webpack.config.js
module.exports = {
    entry: {
        index: './src/index.js'
    },
    output: {
        filename: 'bundle.js',
        path: path.resolve('dist')
    },
    module: {
        rules: [
            {
                test: /\.css$/,     // 解析css
                use: ['style-loader', 'css-loader'] // 从右向左解析
                /* 
                    也可以这样写，这种方式方便写一些配置参数
                    use: [
                        {loader: 'style-loader'},
                        {loader: 'css-loader'}
                    ]
                */
            }
        ]
    }
}
```

![img](https://img-blog.csdn.net/20180327133250981)新建一个css文件style.css，在index.js中引入   无效  安装模块前

安装之后使用（直接在文件前）：![img](https://img-blog.csdn.net/20180327134306356)

```

或者（在命令行）：

 
```

1. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `lenovo@DESKTOP-NL309GS MINGW64 /e/workspace/xampp/htdocs/text/webpackText`

   ```
   
   ```

   ```
   
   ```

2. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `$ webpack --mode development --module-bind 'css=style-loader!css-loader' // 给css绑定。。。。`

   ```
   
   ```

   ```
   
   ```

```

那每次更新都要执行一次，有没有自动更新的？？？

 
```

1. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `lenovo@DESKTOP-NL309GS MINGW64 /e/workspace/xampp/htdocs/text/webpackText`

   ```
   
   ```

   ```
   
   ```

2. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `$ webpack --mode development --module-bind 'css=style-loader!css-loader' --watch // watch参数监听，每次保存文件会自动执行`

   ```
   
   ```

   ```
   
   ```

```

（3）其他参数：

 
```

1. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `lenovo@DESKTOP-NL309GS MINGW64 /e/workspace/xampp/htdocs/text/webpackText`

   ```
   
   ```

   ```
   
   ```

2. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `$ webpack --mode development --module-bind 'css=style-loader!css-loader' --progress --display-modules --display-reasons`

   ```
   
   ```

   ```
   
   ```

```

--progerss：会出现打包过程，有百分比进度条

--display-modules：会把所有打包的模块列出来

--display-reasons：会把打包的原因列出来


```

###  

### 7.2拆分CSS

```
/ @next表示可以支持webpack4版本的插件
npm i extract-text-webpack-plugin@next -D
let path = require('path');
let HtmlWebpackPlugin = require('html-webpack-plugin');
// 拆分css样式的插件
let ExtractTextWebpackPlugin = require('extract-text-webpack-plugin');

module.exports = {
    entry: './src/index.js',
    output: {
        filaneme: 'bundle.js',
        path: path.resolve('dist')
    },
    module: {
        rules: [
            {
                test: /\.css$/,
                use: ExtractTextWebpackPlugin.extract({
                    // 将css用link的方式引入就不再需要style-loader了
                    use: 'css-loader'       
                })
            }
        ]
    },
    plugins: [
        new HtmlWebpackPlugin({
            template: './src/index.html',
        }),
        // 拆分后会把css文件放到dist目录下的css/style.css
        new ExtractTextWebpackPlugin('css/style.css')  
    ]
}
```

此时拆分完css后，打包的html页面就以link的方式去引入css

8

## 引用图片方面     需要loader

```
npm i file-loader url-loader -D
```

如果是在css文件里引入的如背景图之类的图片，就需要指定一下相对路径

```
module.exports = {
    module: {
        rules: [
            {
                test: /\.css$/,
                use: ExtractTextWebpackPlugin.extract({
                    use: 'css-loader',
                    publicPath: '../'
                })
            },
            {
                test: /\.(jpe?g|png|gif)$/,
                use: [
                    {
                        loader: 'url-loader',
                        options: {
                            limit: 8192,    // 小于8k的图片自动转成base64格式，并且不会存在实体图片
                            outputPath: 'images/'   // 图片打包后存放的目录
                        }
                    }
                ]
            }
        ]
    }
}
```

8.2页面img引用图片

页面中经常会用到img标签，img引用的图片地址也需要一个loader来帮我们处理好

```
npm i html-withimg-loader -D
module.exports = {
    module: {
        rules: [
            {
                test: /\.(htm|html)$/,
                use: 'html-withimg-loader'
            }
        ]
    }
}
```

这样再打包后的html文件下img就可以正常引用图片路径

### 8.3引用字体图片和svg图片

字体图标和svg图片都可以通过file-loader来解析

```
module.exports = {
    module: {
        rules: [
            {
                test: /\.(eot|ttf|woff|svg)$/,
                use: 'file-loader'
            }
        ]
    }
}
```

###  

## `9添加CSS3前缀`

```

通过postcss中的autoprefixer可以实现将CSS3中的一些需要兼容写法的属性添加响应的前缀，这样省去我们不少的时间

由于也是一个loader加载器，我们也需要先安装一下

npm i postcss-loader autoprefixer -D

安装后，我们还需要像webpack一样写一个config的配置文件，在项目根目录下创建一个**postcss.config.js**文件，配置如下：

module.exports = {
    plugins: [require('autoprefixer')]  // 引用该插件即可了
}

然后在webpack里配置postcss-loader

module.exports = {
    module: {
        rules: [
            {
                test: /\.css$/,
                use: ['style-loader', 'css-loader', 'postcss-loader']
            }
        ]
    }
}

```

``

```

```

## `10 Babel     转义ES6`

```

在实际开发中，我们在大量的使用着ES6及之后的api去写代码，这样会提高我们写代码的速度，不过由于低版本浏览器的存在，不得不需要转换成兼容的代码，于是就有了常用的Babel了

Babel会将ES6的代码转成ES5的代码

那么不再多说，既然要使用它，就先来安一下

npm i babel-core babel-loader babel-preset-env babel-preset-stage-0 -D

当把这些都安好后，我们就开始配置，由于要兼容的代码不仅仅包含ES6还有之后的版本和那些仅仅是草案的内容，所以我们可以通过一个.babelrc文件来配置一下，对这些版本的支持

// .babelrc
{
    "presets": ["env", "stage-0"]   // 从右向左解析
}

我们再在webpack里配置一下babel-loader既可以做到代码转成ES5了

module.exports = {
    module: {
        rules: [
            {
                test:/\.js$/,
                use: 'bable-loader',
                include: /src/,          // 只转化src目录下的js
                exclude: /node_modules/  // 排除掉node_modules，优化打包速度
            }
        ]
    }
}

```

``

```
///////////////////////////////////////////////////////////////////////////////////
```

``

```
每次打包之前将dist目录下的文件都清空

clean-webpack-plugin插件

npm i clean-webpack-plugin -D

let CleanWebpackPlugin = require('clean-webpack-plugin');

module.exports = {
    plugins: [
        // 打包前先清空
        new CleanWebpackPlugin('dist')  
    ]
}

```

``

```

```

## `11 启动静态服务器 webpack-dev-server`

```

要使用webpack开发工具，要单独安装 webpack-dev-server

# 安装 npm install webpack-dev-server -g
# 运行 webpack-dev-server --progress --colors


webpack-dev-server是一个小型的node.js Express服务器,它使用webpack-dev-middleware中间件来为通过webpack打包生成的资源文件提供Web服务。它还有一个通过Socket.IO连接着webpack-dev-server服务器的小型运行时程序。webpack-dev-server发送关于编译状态的消息到客户端，客户端根据消息作出响应。
```



```
module.exports = {
    devServer: {
        contentBase: './dist',
        host: 'localhost',      // 默认是localhost
        port: 3000,             // 端口
        open: true,             // 自动打开浏览器
        hot: true               // 开启热更新
    }
}
当然在npm run dev命令下，打包的文件存在于内存中，并不会产生在dist目录下

启动一个静态服务器，默认会**自动刷新**

webpack-dev-server有两种模式支持自动刷新——iframe模式和inline模式

```

- `在iframe模式下：页面是嵌套在一个iframe下的，在代码发生改动的时候，这个iframe会重新加载`
- `在inline模式下：一个小型的webpack-dev-server客户端会作为入口文件打包，这个客户端会在后端代码改变的时候刷新页面`

```

使用iframe模式，无需额外配置，只需在浏览器输入**localhost:3000**
```



### `**热更新和自动刷新的区别**`

```

**在配置devServer的时候，如果hot为true，就代表开启了热更新**

**But这并没那么简单，因为热更新还需要配置一个webpack自带的插件并且还要在主要js文件里检查是否有module.hot**

**下面就让我们直接看下代码是如何实现的**

// webpack.config.js
let webpack = require('webpack');

module.exports = {
    plugins: [
        // 热替换，热替换不是刷新
        new webpack.HotModuleReplacementPlugin()
    ],
    devServer: {
        contentBase: './dist',
        hot: true,
        port: 3000
    }
}

// 此时还没完虽然配置了插件和开启了热更新，但实际上并不会生效

// index.js
let a = 'hello world';
document.body.innerHTML = a;
console.log('这是webpack打包的入口文件');

// 还需要在主要的js文件里写入下面这段代码
if (module.hot) {
    // 实现热更新
    module.hot.accept();
}

**以上index.js中的内容，如果将变量a的值进行修改保存后，会在不刷新页面的情况下直接修改掉，这样就实现了热更新**

**那么热更新从现在看来和自动刷新浏览器的区别也不是太大嘛！自动刷新也是可以接受的啊**

**其实不然，热更新的好处可能在vue或者react中有更大的发挥，其中某一个组件被修改的时候就会针对这个组件进行热更新**

```

``

```

```

## `resolve解析`

```

在webpack的配置中，resolve我们常用来配置别名和省略后缀名

module.exports = {
    resolve: {
        // 别名
        alias: {
            $: './src/jquery.js'
        },
        // 省略后缀
        extensions: ['.js', '.json', '.css']
    },
}
```

## `提取公共代码`

```

在webpack4之前，提取公共代码都是通过一个叫CommonsChunkPlugin的插件来办到的。到了4以后，内置了一个一模一样的功能，而且起了一个好听的名字叫“优化”

下面我们就来看看如何提取公共代码

// 假设a.js和b.js都同时引入了jquery.js和一个写好的utils.js
// a.js和b.js
import $ from 'jquery';
import {sum} from 'utils';

那么他们两个js中其中公共部分的代码就是jquery和utils里的代码了

可以针对第三方插件和写好的公共文件

module.exports = {
    entry: {
        a: './src/a.js',
        b: './src/b.js'
    },
    output: {
        filename: '[name].js',
        path: path.resolve('dust')
    },
    // 提取公共代码
+   optimization: {
        splitChunks: {
            cacheGroups: {
                vendor: {   // 抽离第三方插件
                    test: /node_modules/,   // 指定是node_modules下的第三方包
                    chunks: 'initial',
                    name: 'vendor',  // 打包后的文件名，任意命名    
                    // 设置优先级，防止和自定义的公共代码提取时被覆盖，不进行打包
                    priority: 10    
                },
                utils: { // 抽离自己写的公共代码，utils这个名字可以随意起
                    chunks: 'initial',
                    name: 'utils',  // 任意命名
                    minSize: 0    // 只要超出0字节就生成一个新包
                }
            }
        }
+   },
    plugins: [
        new HtmlWebpackPlugin({
            filename: 'a.html',
            template: './src/index.html',  // 以index.html为模板
+           chunks: ['vendor', 'a']
        }),
        new HtmlWebpackPlugin({
            filename: 'b.html',
            template: './src/index.html',  // 以index.html为模板
+           chunks: ['vendor', 'b']
        })
    ]
}

通过以上配置，可以把引入到a.js和b.js中的这部分公共代码提取出来

```

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

``

```
上线地址

```

1. ```
   
   ```

   ```
   
   ```

   `output: { // 出口文件`

   ```
   
   ```

   ```
   
   ```

2. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `path: path.resolve(__dirname, 'dist'), // 出口文件位置`

   ```
   
   ```

   ```
   
   ```

3. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `filename: 'js/[name].js', // 出口文件名，`

   ```
   
   ```

   ```
   
   ```

4. ```
   
   ```

   ```
   
   ```

   

   ```
   
   ```

   ```
   
   ```

   ```
   
   ```

   `publicPath: 'http://cdn.com/' // 上线的地址`

   ```
   
   ```

   ```
   
   ```

5. ```
   
   ```

   

   ```
   
   ```

```

```



``



webpack常用命令

```

构建命令，webpack的常用参数

$ webpack --config webpack.min.js //另一份配置文件

$ webpack --display-error-details //显示异常信息

$ webpack --watch   //监听变动并自动打包
 
$ webpack -p    //压缩混淆脚本，这个非常非常重要！
 
$ webpack -d    //生成map映射文件，告知哪些模块被最终打包到哪里了
```



```


$ webpack

一些你应该知道的命令行选项

```

- `webpack– for building once for development(用于构建一个开发目录)`
- `webpack -p– for building once for development(用于构建一个生产目录(压缩过的))`
- `webpack --watch– for continuous incremental build(用于连续地构建)`
- `webpack -d– to include source maps(展示映射关系)`
- `webpack --colors– for making things pretty(用于美化展示的信息)`

```


```

``

```

```

