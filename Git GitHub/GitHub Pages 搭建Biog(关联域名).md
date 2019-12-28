1
创建一个仓库     名字为     Github账号名.github.io          

2 
购买 域名
添加解析

2.1 记录ip地址
分别添加两个A 记录类型,

一个主机记录为 www,代表可以解析 www.qiubaiying.top的域名

另一个为 @, 代表 qiubaiying.top

记录值就是我们博客的IP地址，是 GitHub Pagas 在美国的服务器的地址 151.101.100.133

有人的博客都解析到 151.101.100.133 这个IP。

然后 GitHub Pages 再通过 CNAME记录 跳转到你的主页上。
-------------
解析命令，ip地址可以ping你的url：
命令   ping 你的github用户名.github.io

-------------
2.2 记录仓库链接
记录类型选择CNAME，记录值填写GitHub的仓库
-------------
添加两条记录类型为CNAME的解析，一条主机记录为@，一条主机记录为www，记录值都为你的格式为xxxx.github.io的地址。

------------







3
修改CNAME
最后一步，只需要修改 我们github仓库下的 CNAME 文件。

选择 CNAME 文件

使用的注册的域名进行替换,然后提交保存

-----------------------
public文件夹中创建CNAME，不带任何后缀名的文件;文件中填写上你的域名，不要写www



4 访问 博客地址 自动跳转 域名

登陆github选择gitpage仓库，选择settings，下滑找到Github Pages 在Custom domain里填入你的域名，然后点击Save，稍等一会就好了，之后会默认转成HTTPS。SSL证书来自Let's Encrypt