src

​     ├──components # 组件

​     ├── layouts # 公用UI，比如 header/footer

​     ├── pages # 所有的页面，文件名即访问路径

​     └── templates # 模板，之后详细讲



gatsby build (构建一个生产、静态生成的项目版本)

gatsby develop(启动一个热加载的web开发服务器) 



1

先全局安装 `gatsby.js`

npm i -g gatsby-cli



2 mkdir 项目 cd项目            创建 进入项目文件夹



//如果安装不成功  npm install windows-build-tools -g 这个工具可以自动化配置好编译需要的东西 

3

```
gatsby new 项目                         或者gatsby new 项目 && cd $_
```

该命令将创建 项目文件夹，然后进入该目录 

**并且可供开发的环境已经搭建** 



3.5或者

gatsby new 项目文件名 <https://github.com/gatsbyjs/gatsby-starter-blog>



后面新加的部分就是模板地址（这里使用的是默认模板）

构建完毕后执行 cd gatsby-site（你的项目名），

最后执行 gatsby develop部署项目，在浏览器中打开[localhost:8000](https://link.jianshu.com/?t=http://localhost:8000/)



http://localhost:8000/___graphql



`pages` 文件夹下添加 `.md` 文件就能自动生成新博客文章







定位到当前目录后

1. 执行  gatsby develop ，此时Gatsby会自动启动热更新后台服务器，地址为:  localhost:8000 
2. 自己可以尝试修改  src/pages  目录下的文件，保存后，会马上热更新到浏览器的页面上。
3. 执行  gatsby build ，此时Gatsby会在 public 目录下构建生产环境用的优化过的静态网站所需的一切静态资源、静态页面与js代码。如果要发布到自己的网站空间上，可以直接把此目录下面所有东西(除.map为后续的文件名的文件)丢过去自己的空间。如果有用过hexo的朋友们应该会比较熟悉，目录结构类似。
4. 执行  gatsby serve , 此时Gatsby会启动静态网页服务器供你测试刚才“gatsby build”生成的静态网页。









功能插件

- [
  `gatsby-plugin-catch-links`
  ](https://www.colabug.com/goto/aHR0cHM6Ly93d3cuZ2F0c2J5anMub3JnL3BhY2thZ2VzL2dhdHNieS1wbHVnaW4tY2F0Y2gtbGlua3Mv)
  - 实现了历史 `pushState`
    API, 不需要页面重载就可以导航到博客的不同页面
- [
  `gatsby-plugin-react-helmet`
  ](https://www.colabug.com/goto/aHR0cHM6Ly93d3cuZ2F0c2J5anMub3JnL3BhY2thZ2VzL2dhdHNieS1wbHVnaW4tcmVhY3QtaGVsbWV0Lw==)
  - [react-helmet](https://www.colabug.com/goto/aHR0cHM6Ly9naXRodWIuY29tL25mbC9yZWFjdC1oZWxtZXQ=)
    是一种允许修改 `head`
    标签的工具 Gatsby 静态地呈现这些头部标签的变化

使用下面的命令：

```
yarn add gatsby-plugin-catch-links gatsby-plugin-react-helmet`
```

我们用的是 [yarn](https://www.colabug.com/goto/aHR0cHM6Ly95YXJucGtnLmNvbS9lbi8=)
，但是使用 npm 也很容易： `npm i --save [deps]`
。 在安装了这些功能插件之后，我们将编辑 `gatsby-config.js`



siteMetadata: {

​    title: `Your Name - Blog`, author: `Your Name`, },

​    plugins: [

​         'gatsby-plugin-catch-links',                         1

​         'gatsby-plugin-react-helmet', ],                 2

}





### 源插件                          gatsby-source-filesystem

源插件创建节点，然后通过一个转换器插件将其转换为可用的格式。例如，一个典型的工作流通常需要使用[gatsby-source-filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)它从磁盘上加载文件，例如 Markdown 文件，然后指定一个 Markdown 转换器将 Markdown 转换成 HTML 。 因为博客的大部分内容都使用 Markdown 格式，让我们添加[gatsby-source-filesystem](https://www.gatsbyjs.org/packages/gatsby-source-filesystem/)，与我们之前的步骤类似，我们将安装插件，然后将其注入到我们的 gatsby-config.js,像这样：

```
`yarn add gatsby-source-filesystem`
module.exports = {
  // previous configuration
  plugins: [
    'gatsby-plugin-catch-links',
    'gatsby-plugin-react-helmet',
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
        name: 'pages',
      },
    }
  ]
}
一个options 对象可以传递给一个插件，我们正在传递文件系统路径(也就是我们的 Markdown 文件将被定位的位置)，然后是源文件的名称。
既然 Gatsby 知道了我们的源文件，我们就可以开始应用一些有用的转换器来将这些文件转换为可用的数据！
```

### `转换器插件                                   gatsby-transformer-remark`

```

正如前面提到的，转换器插件采用了一些底层的数据格式，这种格式在当前的表单中是不可用的（Markdown，json，yaml等），我们可以用 GraphQL 查询把它转换成 Gatsby 能够理解的格式。filesystem 源插件将从我们的文件系统中加载文件节点(如 Markdown )，然后 Markdown 转换器将接管并转换为可用的 HTML 。 我们将只使用一个转换器插件(用于 Markdown )，所以让我们安装它。

```

- ```
  
  ```

  `gatsby-transformer-remark`

  ```
  
  ```

  - `使用 remark Markdown解析器进行转换磁盘上的 md 文件为 HTML 。 此外，该转换器还可以选择使用插件来进一步扩展功能，例如通过 gatsby-remark-prismjs来添加语法高亮，通过 gatsby-remark-copy-linked-files 复制在 markdown 中指定的相关文件，通过 gatsby-remark-images 压缩图像，并使用 srcset 添加响应性图像等等。`

  ```
  
  ```

```

这个过程现在应该很熟悉了，安装之后再添加到配置中。

`yarn add gatsby-transformer-remark`

编辑 gatsby-config.js

module.exports = {
  // previous setup
    plugins: [
    'gatsby-plugin-catch-links',
    'gatsby-plugin-react-helmet',
    {
      resolve: `gatsby-source-filesystem`,
      options: {
        path: `${__dirname}/src/pages`,
        name: 'pages',
      },
    },
    {
      resolve: 'gatsby-transformer-remark',
      options: {
        plugins: [] // just in case those previously mentioned remark plugins sound cool :)
      }
    },
  ]
};

```















## 创建 React 模板



当 Gatsby 支持服务器端渲染(对字符串)的 React 组件时，我们可以使用 React 编写我们的模板（ 也可以使用Preact ）。 我们创建一个 src/templates/blog-post.js文件（请创建一个src/templates文件夹）

```
import React from 'react';
import Helmet from 'react-helmet';

// import '../css/blog-post.css'; // make it pretty!

export default function Template({
  data // this prop will be injected by the GraphQL query we'll write in a bit
}) {
  const { markdownRemark: post } = data; // data.markdownRemark holds our post data
  return (
    <div className="blog-post-container">
      <Helmet title={`Your Blog Name - ${post.frontmatter.title}`} />
      <div className="blog-post">
        <h1>{post.frontmatter.title}</h1>
        <div className="blog-post-content" dangerouslySetInnerHTML={{ __html: post.html }} />
      </div>
    </div>
  );
}
```

