# npm install出现Unexpected end of JSON input while parsing near错误解决方法

# npm cache clean --force



















 # npm ERR! errno -4048

以为还真是权限不够，感觉有点奇怪，用管理员权限执行，有时还真有用，不过后面查了下，时缓存的问题，清理下缓存就行，不用管理员权限。

方法1、



需要删除npmrc文件。

强调：不是nodejs安装目录npm模块下的那个npmrc文件

而是在C:\Users\{账户}\下的.npmrc文件..

方法2、

或者直接用命令清理就行，控制台输入：

npm cache clean --force



或者

```cmd
npm cache verify
```

added 114 packages in 42.369s
E:\SouthernPowerGridProject\web_project\AutoOPS\autoops>npm cache clean --force
npm WARN using --force I sure hope you know what you are doing.


E:\SouthernPowerGridProject\web_project\AutoOPS\autoops>npm install
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.1.2 (node_modules\fsevents):
npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.1.2: wanted {"os":"darwin","arch":"any"} (current: {"os":"win32","arch":"x64"})


added 114 packages in 42.369s

成功了