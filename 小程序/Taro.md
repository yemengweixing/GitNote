```
├── config                 配置目录
|   ├── dev.js             开发时配置
|   ├── index.js           默认配置
|   └── prod.js            打包时配置
├── src                    源码目录
|   ├── components         公共组件目录
|   ├── pages              页面文件目录
|   |   ├── index          index 页面目录
|   |   |   ├── banner     页面 index 私有组件
|   |   |   ├── index.js   index 页面逻辑
|   |   |   └── index.css  index 页面样式
|   ├── utils              公共方法库
|   ├── app.css            项目总通用样式
|   └── app.js             项目入口文件
└── package.json

/** Quick Start With NPM Or Yarn **/
$ npm install -g @tarojs/cli
$ yarn global add @tarojs/cli
```



命令创建模板项目

```
$ taro init myApp
```





更新项目中 Taro 相关的依赖

```
$ taro update project
```