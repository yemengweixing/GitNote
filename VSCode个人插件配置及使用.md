---
title: VSCode个人配置及使用
date: 2019-2-28
categories: [编程,编辑器]
tags: [编程,编辑器]
---
## 个人使用插件
 - VSCode界面 左边侧栏 第五个图标便为 延伸模组（插件）


**Settings Sync 设置及插件同步的插件 （最推荐）**
  通过在GitHub上保存你的vscode设置，更换电脑也可以同步个人设置

  前提设置
  在GitHub生成token值  1.进入Settings（设置） 2.点击 左侧 最下面的Personal access tokens
3.点击按钮 Generate new token 4.随便输入 Token description 并且勾选  gist        得到Github Token值（复制） 
  
 - Upload Key : Shift + Alt + U（上传设置 成功则会在 控制台的输出界面 显示上传的插件清单）
  第一次需要输入Github Token值    快捷键shift+alt+U 在弹出的输入框 粘贴 之前得到Github Token值  
 - Download Key :Shift + Alt + D（本地同步已经上传的设置）
  其它电脑使用同步配置 安装后也需要第一次输入Github Token值 快捷键shift+alt+D 在弹出的输入框 粘贴 之前得到Github Token值


  
  可以通过以下方式查看你的上传设置
https://gist.github.com/{your_userName}/{gist_id}


 - **ESLint**                 
    检测JS
 
 - Auto Close Tag          
 自动闭合标记
  
 - Auto Rename Tag         
 自动重命名标记
 
 - HTML CSS support        
 css自动补齐
 
 - Path Intellisense       
 自动路劲补全，默认不带这个功能的

 - Bracket Pair Colorizer 
  括号配对着色
  
 - Indent Rainbow          
 彩虹缩进
  
 - Snippets                
 可以找到j各种代码常用单词（js react）的插件
 
 - Css Peek                
 能在源代码中的字符串中找到对应的css（类和ID）。显示在那个css - 文件里，还有在第几行。
  
 - Csscomb                 
 css 、less、sass 的代码格式化。
   
 - Import Cost             
 允许您查看导入模块的大小。 这对 Webpack 等打包工具来说是一个 - 巨大的帮助。 您可以查看是导入整个库还是仅导入特定实用程序
 
 - REST API                
 为了检查URL直接发送 HTTP 请求并查看响应
  
 - **美化**
 
 - Dracula Official        
 推荐主题
 - background-cover        
 可以设置背景图片
 ## 常见操作

 - ----------
 **窗口**
 - 打开一个新窗口： Ctrl+Shift+N
 - 关闭窗口： Ctrl+Shift+W
 - 新建文件 Ctrl+N
 - 历史打开文件之间切换 Ctrl+Tab，Alt+Left，Alt+Right
 - 切出一个新的编辑器（最多3个）Ctrl+\，也可以按住Ctrl鼠标点击Explorer里的文件名
 - 左中右3个编辑器的快捷键Ctrl+1 Ctrl+2 Ctrl+3
 - 3个编辑器之间循环切换 Ctrl+`
 - 编辑器换位置，Ctrl+k然后按Left或Right

  **常用快捷键**
 - Ctrl +　N           新建文件
 - Ctrl +              鼠标左键（单击字符串） 跳转到 当前字符串对应的 方法或变量 定义的地方
 - 查找 Ctrl+F
 - 查找替换 Ctrl+H
 - 整个文件夹中查找 Ctrl+Shift+F
 - 全屏：F11
 - zoomIn/zoomOut：Ctrl + =/Ctrl + - 
 - 侧边栏显/隐：Ctrl+B
 - 预览markdown Ctrl+Shift+V
 - ----------
 
 **整行 操作**
 - Alt+ ↑                  向上移动整行
 - Shift+Alt + ↓           向上复制整行
 - Ctrl+Enter              在下面换整行（这两个快捷键：很多地方通用）
 - Shift+Enter 在下面插入行
 - Ctrl+Shift+Enter        在上面插入整行
 - Ctrl+Shift+\            跳到匹配的括号
 - Ctrl + G                转到行...
 - Ctrl + I                选择当前行
 - Shift + Alt + F         格式化文档（整理代码之间空格）
 - Ctrl+K Ctrl+]           展开（未折叠）所有子区域
 - Ctrl+K Ctrl+0(num)      折叠（折叠）所有(num)层区域
----------
**多选择、行、列操作**
 -  Ctrl + D                向下查找匹配（选中字符）
 -  Alt +单击              指定位置插入光标（多列同时编辑）
 -  Ctrl + Alt +↑           向上插入光标（多列操作）
 -  Ctrl + Shift + Alt +↑   列（框）选择
 -  Shift + Alt + I         在选定区域的每一行的末尾插入光标
 -  Ctrl + Shift + L        选择当前选择的所有出现
 -  Ctrl + F2               选择当前字符串的所有出现
**格式调整**
 - Shift + Alt + F         格式化文档（整理代码之间空格）
 - 代码行缩进Ctrl+[， Ctrl+]     
 - 折叠打开代码块 Ctrl+Shift+[， Ctrl+Shift+]
 - Ctrl+C Ctrl+V如果不选中，默认复制或剪切一整行
 - 代码格式化：Shift+Alt+F，或Ctrl+Shift+P后输入format code
 - 修剪空格Ctrl+Shift+X
 - 上下移动一行： Alt+Up 或 Alt+Down
 - 向上向下复制一行： Shift+Alt+Up或Shift+Alt+Down
 - 在当前行下边插入一行Ctrl+Enter
 - 在当前行上方插入一行Ctrl+Shift+Enter
----------
**光标相关**
 - 移动到行首：Home
 - 移动到行尾：End
 - 移动到文件结尾：Ctrl+End
 - 移动到文件开头：Ctrl+Home
 - 移动到后半个括号 Ctrl+Shift+]
 - 选中当前行Ctrl+i（双击）
 - 选择从光标到行尾Shift+End
 - 选择从行首到光标处Shift+Home
 - 删除光标右侧的所有字Ctrl+Delete
 - Shrink/expand selection： Shift+Alt+Left和Shift+Alt+Right
 - Multi-Cursor：可以连续选择多处，然后一起修改，Alt+Click添加cursor或者Ctrl+Alt+Down 或 Ctrl+Alt+Up
 - 同时选中所有匹配的Ctrl+Shift+L
 - Ctrl+D下一个匹配的也被选中(被我自定义成删除当前行了，见下边Ctrl+Shift+K)
 - 回退上一个光标操作Ctrl+U
----------

**重构代码**

 - 跳转到定义处：F12
 - 定义处缩略图：只看一眼而不跳转过去Alt+F12
 - 列出所有的引用：Shift+F12
 - 同时修改本文件中所有匹配的：Ctrl+F12
 - 重命名：比如要修改一个方法名，可以选中后按F2，输入新的名字，回车，会发现所有的文件都修改过了。
 - 跳转到下一个Error或Warning：当有多个错误时可以按F8逐个跳转
 - 查看diff 在explorer里选择文件右键 Set file to compare，然后需要对比的文件上右键选择 Compare with 'file_name_you_chose'.
----------
