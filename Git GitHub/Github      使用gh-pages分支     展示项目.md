前置
git-add -A
git -commit -m "..."
命令把完成的项目上传到github


创建gh-pages分支,再将作品重新上传到该分支上

git checkout -b gh-pages  //创建分支

git push -u origin gh-pages       、//就是这个



上传某个文件夹     git subtree push --prefix={文件夹名字} origin gh-pages
展现dist目录下的静态文件，那最关键的语句来了

git subtree push --prefix=dist origin gh-pages





展示地址就是 Github用户名.github.io/创建的仓库名
http://yemengzi.top/jianshu/build/#/


react打包
在package.json配置文件中加一句："homepage": ".",


打包 需要使用json文件数据模拟
要把api文件夹 与 项目文件夹同级（同一个目录内）