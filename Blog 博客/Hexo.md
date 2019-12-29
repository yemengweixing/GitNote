访问地址 [http://localhost:4000](http://localhost:4000/)

hexo clean & hexo g & hexo s 

hexo s 预览& hexo d           //正常上传操作



使用 npm 安装 Hexo。



全局安装



安装 Hexo 完成后，请执行下列命令，Hexo 将会在指定文件夹中新建所需要的文件。



新建完成后，指定文件夹的目录如下：

| .   node_modules             依赖包    public：存放的是生成的页面 ├── _config.yml          整个博客的配置├── package.json├── scaffolds            命令生成文章等的模板   ├── source               用命令创建的各种文章 \|       ├── _drafts \|        └── _posts└── themes               主题    db.json：         source解析所得到的    package.json： 项目所需模块项目的配置信息 |
| ------------------------------------------------------------ |
|                                                              |

### _config.yml

网站的 [配置](https://hexo.io/zh-cn/docs/configuration) 信息，您可以在此配置大部分的参数。

_config.yml 用来存放hexo博客的个人描述, 博客小图标地址, 头像地址等等.

### package.json

应用程序的信息。[EJS](http://embeddedjs.com/), [Stylus](http://learnboost.github.io/stylus/) 和 [Markdown](http://daringfireball.net/projects/markdown/) renderer 已默认安装，您可以自由移除。

package.json



### scaffolds

[模版](https://hexo.io/zh-cn/docs/writing) 文件夹。当您新建文章时，Hexo 会根据 scaffold 来建立文件。

Hexo的模板是指在新建的markdown文件中默认填充的内容。例如，如果您修改scaffold/post.md中的Front-matter内容，那么每次新建一篇文章时都会包含这个修改。

### source

资源文件夹是存放用户资源的地方。除 _posts 文件夹之外，开头命名为 _ (下划线)的文件 / 文件夹和隐藏的文件将会被忽略。Markdown 和 HTML 文件会被解析并放到 public 文件夹，而其他文件会被拷贝过去。

 source下的_posts 存放你所有的博文.md文件 你可以通过 hexo n "xxx" 创建博客文章, 也可以直接把xxx.md 格式的文件直接拖入进去 themes 存放你的所有主题文件

### themes

[主题](https://hexo.io/zh-cn/docs/themes) 文件夹。Hexo 会根据主题来生成静态页面。



默认主题安装后

hexo g                    //generetor的缩写

hexo s                    开启本地服务器 

访问地址 [http://localhost:4000](http://localhost:4000/)  查看默认主题



**--------------------------------------------------------------------------**

**主题安裝後** 



hexo clean     清理缓存

一般是在配置不能生效, 或者文章发布了不显示, 等等异常情况下使用的. 当然有时候清除浏览器缓存也是必须的操作. 



hexo generate          生成静态页面                  简化 hexo g

重新生成静态网页, 所有发布文章, 修改文章, 修改hexo配置, 修改主题配置等等操作, 都需要.

hexo s  [http://localhost:4000](http://localhost:4000/) 本地預覽 可以边写文章, 边使用这个命令在本地预览, 包括修改各种配置, 都可以预览.     //hexo server



\-----------------------------------------------------------------------



上传GitHub         1     2

安裝Git 设置用戶名 郵箱 並且生成SSH公密钥 使電腦綁定到帳號

1     项目文件夹 _config.yml 修改

使用﻿ssh﻿



deploy:

type: git

repository: git@github.com:liuxianan/liuxianan.github.io.git

branch: master



错误写法：

deploy:

type: github

repository: https://github.com/liuxianan/liuxianan.github.io.git

branch: master

這個過時了！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！！

2

npm install hexo-deployer-git --save

//先装个插件压压惊 hexo d // 部署的命令 //等一会就好了



部署 hexo deploy      //上传github

在你博客站点文件夹下右键空白处，选择Git Bash Here

hexo clean          清理缓存

hexo generate         生成静态页面， 

hexo server             到localhost:4000预览博客效果，

以上非必備

hexo deploy           同步到github上

输入地址就可以访问自己的博客了 http://自己的用户名.github.io



hexo clean & hexo g & hexo d           //正常上传操作



域名

域名解析页面添加一条解析：

ping yemengweixing.github.io          得到ip 添加到a記錄

域名           添加到CNAME 



然后到你博客 根目录/source 目录下创建一个新文件CNAME 

在里面写上你刚刚配置的路径，比如我的是blog.improvecfan.cn，就直接在CNAME文件中写上这个地址就好了。

然后执行以下hexo g,hexo d，让后访问你自己的地址就可以跳转到博客了。











=======================================================================================================

# 写作

hexo new [layout] <title>

命令中指定文章的布局（layout），默认为 post，可以通过修改 _config.yml 中的 default_layout 参数来指定默认布局



博客文件夹\source\_posts 下的md文件







\-------------------------------------------------------------------------------------



背景图片

图片放到hexo\themes\modernist\source\css\images下

打开css\_base文件夹下的layout.styl

# 自定义样式

themes/next/source/css/_custom/custom.styl



# 文章背景透明 就是这个修改样式！！！！！！！！！！！！！！！！！

# 博客根目录 themes\next\source\css\_schemes\Pisces\_layout.styl这个文件的 

.content-wrap    的 background:删除掉

菜单

.header-inner 


  