---
title: DOM
tags: 新建,模板,小书匠
grammar_cjkRuby: true
---


普通的事件绑定写法如下：

var btn = document.getElementById('btn1')
btn.addEventListener('click', function (event) {
    // event.preventDefault() // 阻止默认行为
    // event.stopPropagation() // 阻止冒泡
    console.log('clicked')
})