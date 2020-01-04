npm init

进行项目初始化

项目文件夹内生成package.json文件

### Package.json 属性说明

- **name** - 包名。

- **version** - 包的版本号。

- **description** - 包的描述。

- **homepage** - 包的官网 url 。

- **author** - 包的作者姓名。

- **contributors** - 包的其他贡献者姓名。

- **dependencies** - 依赖包列表。如果依赖包没有安装，npm 会自动将依赖包安装在 node_module 目录下。

- **repository** - 包代码存放的地方的类型，可以是 git 或 svn，git 可在 Github 上。

- **main** - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。

- **keywords** - 关键字

  

mkdir



模块 -v

查看版本

全局安装

npm install -g 模块               简化npm i -g 模块                    

或者npm install 模块 -g                      简化npm i 模块 -g 



本地安装



npm install 模块 --save-dev     简化npm i 模块 -D

或者 npm install --save-dev 模块 npm i -D 模块

参数--save-dev的含义是代表把你的安装包信息写入package.json文件



设置镜像源



npm config set registry https://registry.npm.taobao.org --global

npm config set disturl https://npm.taobao.org/dist --global

 [cnpm](https://github.com/cnpm/cnpm) (gzip 压缩支持) 命令行工具代替默认的 npm: 不要安装 就设置镜像

$ npm install -g cnpm --registry=https://registry.npm.taobao.org

或者你直接通过添加 npm 参数 alias 一个新命令:

alias cnpm="npm --registry=https://registry.npm.taobao.org \

--cache=$HOME/.npm/.cache/cnpm \

--disturl=https://npm.taobao.org/dist \

--userconfig=$HOME/.cnpmrc"



\# Or alias it in .bashrc or .zshrc

$ echo '\n#alias for cnpm\nalias cnpm="npm --registry=https://registry.npm.taobao.org \

--cache=$HOME/.npm/.cache/cnpm \

--disturl=https://npm.taobao.org/dist \

--userconfig=$HOME/.cnpmrc"' >> ~/.zshrc && source ~/.zshrc

### 安装模块

从 [registry.npm.taobao.org](http://registry.npm.taobao.org/) 安装所有模块. 当安装的时候发现安装的模块还没有同步过来, 淘宝 NPM 会自动在后台进行同步, 并且会让你从官方 NPM [registry.npmjs.org](http://registry.npmjs.org/) 进行安装. 下次你再安装这个模块的时候, 就会直接从 淘宝 NPM 安装了.

$ cnpm install [name]

### 同步模块

直接通过 sync 命令马上同步一个模块, 只有 cnpm 命令行才有此功能:

$ cnpm sync connect

当然, 你可以直接通过 web 方式来同步: [/sync/connect](http://npm.taobao.org/sync/connect)

$ open https://npm.taobao.org/sync/connect

### 其它命令

支持 npm 除了 publish 之外的所有命令, 如:

$ cnpm info connect

















## 1.`npm install`本地安装

（1）将安装包放在 `./node_modules` 下（运行 npm 命令时所在的目录），如果没有 `node_modules` 目录，会在当前执行 `npm` 命令的目录下生成 `node_modules` 目录。 
（2）可以通过 `require()` 来引入本地安装的包。

## 2.`npm install -g`全局安装

(1) 将安装包放在 `/usr/local` 下或者你 `node` 的安装目录。 
(2)可以直接在命令行里使用。

## 3.`npm install --save`

(1)会把`msbuild`包安装到`node_modules`目录中 
(2)会在`package.json`的`dependencies`属性下添加`msbuild` 
(3)之后运行`npm install`命令时，会自动安装`msbuild`到`node_modules`目录中 
(4)之后运行`npm install --production`或者注明`NODE_ENV`变量值为`production`时，会自动安装`msbuild`到`node_modules`目录中

## 4.`npm install --save-dev`

(1)会把`msbuild`包安装到`node_modules`目录中 
(2)会在`package.json`的`devDependencies`属性下添加`msbuild` 
(3)之后运行`npm install`命令时，会自动安装`msbuild`到`node_modules`目录中 
(4)之后运行`npm install --production`或者注明`NODE_ENV`变量值为`production`时，不会自动安装`msbuild`到`node_modules`目录中



















npm install -d 就是npm install --save-dev

npm insatll -s 就是npm install --save



以前一直在纠结一个npm安装的包依赖管理的问题。是这样的：

我们在使用npm install 安装模块或插件的时候，有两种命令把他们写入到 package.json 文件里面去，他们是：

--save-dev

或

--save

首先需要说明的是Dependencies一词的中文意思是依赖和附属的意思，而dev则是

develop（开发）的简写。

所以它们的区别在 package.json 文件里面体现出来的就是，使用 --save-dev 安装的 插件，被写入到 devDependencies 域里面去，而使用 --save 安装的插件，则是被写入到 dependencies 区块里面去。

那 package.json 文件里面的 devDependencies  和 dependencies 对象有什么区别呢？

devDependencies  里面的插件只用于开发环境，不用于生产环境，而 dependencies  是需要发布到生产环境的。

比如我们写一个项目要依赖于jQuery，没有这个包的依赖运行就会报错，这时候就把这个依赖写入dependencies ；

而我们使用的一些构建工具比如glup、webpack这些只是在开发中使用的包，上线以

后就和他们没关系了，所以将它写入devDependencies。





























![img](https://app.yinxiang.com/shard/s64/res/bab2a212-7824-404d-b30d-b5fd733e8d64/20180131114719631.png)

yarn 全局安装

```
yarn global add xxx
等于npm install -g yarn
```





安装完 yarn 后同理也要设置镜像源：

yarn config set registry https://registry.npm.taobao.org --global

yarn config set disturl https://npm.taobao.org/dist --global



安装完 yarn 之后就可以用 yarn 代替 npm 了，例如用yarn代替npm install命令，用yarn add 某第三方库名代替npm install 某第三方库名。





初始化新项目

yarn init

添加依赖包

yarn add [package]

指定版本

yarn add [package]@[版本]

yarn add [package]@[tag]

将依赖项添加到不同依赖项类别

分别添加到 devDependencies、peerDependencies 和 optionalDependencies：

yarn add [package] --dev

yarn add [package] --peer

yarn add [package] --optional

升级依赖包

yarn upgrade [package]

更新指定版本

yarn upgrade [package]@[version]

yarn upgrade [package]@[tag]

将包更新到最新版本：yarn upgrade –latest [模块]

移除依赖包

yarn remove [package]

安装项目的全部依赖

yarn     或者     yarn install

本地安装

yarn add 模块 --dev



![è¿™é‡Œå†™å›¾ç‰‡æ��è¿°](https://app.yinxiang.com/shard/s64/res/bab2a212-7824-404d-b30d-b5fd733e8d64/20180131114719631.png)

















使用国内镜像加速npm和yarn

\1. npm config set registry=https://registry.npm.taobao.org

\2. yarn config set registry https://registry.npm.taobao.org

\3. 下载cnpm：npm install -g cnpm --registry=https://registry.npm.taobao.org

# npm使用国内淘宝镜像

临时使用

```
npm --registry https://registry.npm.taobao.org install express
```

## 永久使用

### 直接配置

```
npm config set registry https://registry.npm.taobao.org
```

通过如下命令可以查看是否配置成功

```
npm config get registry

npm info express
```

！！！如果需要恢复成原来的官方地址只需要执行如下命令:

```
npm config set registry https://registry.npmjs.org
```



安装cnpm

```cpp
npm i -g cnpm --registry=https://registry.npm.taobao.org
```

cnpm config ls 查看