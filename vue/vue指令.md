## 缩写

### v-bind 缩写

Vue.js 为两个最为常用的指令提供了特别的缩写：

```
<!-- 完整语法 -->
<a v-bind:href="url"></a>
<!-- 缩写 -->
<a :href="url"></a>
```

### v-on 缩写

```
<!-- 完整语法 -->
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```





# v-bind

v-bind 指令被用来响应地更新 HTML 属性

<div id="app">
    <pre><a v-bind:href="url">菜鸟教程</a></pre>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    url: 'http://www.runoob.com'
  }
})
</script>


1判断真假 增加 class 的值，如果为 true 使用 类的样式

v-bind:class="{'class的名称': 定义的属性}"

<div id="app">
  <label for="r1">修改颜色</label><input type="checkbox" v-model="use" id="r1">
  <br><br>
  <div v-bind:class="{'class1': use}">
    v-bind:class 指令
  </div>
</div>

<script>
new Vue({
    el: '#app',
  data:{
      use: false
  }
});
</script>
2可以多个   类名要加 字符串

<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
3也可以直接绑定数据里的一个对象：

 <div v-bind:class="classObject"></div>  
data: {
    classObject: {
      active: true,
      'text-danger': true
    }
  }

4 返回对象就可以 哪怕计算的

5数组语法

<div v-bind:class="[activeClass, errorClass]"></div>

data: {
    activeClass: 'active',
    errorClass: 'text-danger'
  }

6 三元表达式来切换列表中的 class 

<div v-bind:class="[errorClass ,isActive ? activeClass : '']"></div>

  data: {
    isActive: true,
	activeClass: 'active',
    errorClass: 'text-danger'
  }





1 **v-bind:style** 直接设置样式：

## 

<div id="app">
    <div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }">菜鸟教程</div>
</div>

2也可以直接绑定到一个样式对象

  <div v-bind:style="styleObject">菜鸟教程</div>

  data: {
    styleObject: {
      color: 'green',
      fontSize: '30px'
    }

3 可以使用数组将多个样式对象应用到一个元素上：

<div v-bind:style="[baseStyles, overridingStyles]">菜鸟教程</div>

 data: {
    baseStyles: {
      color: 'green',
      fontSize: '30px'
    },
	overridingStyles: {
      'font-weight': 'bold'
    }
  }

# v-on   事件处理器

事件监听可以使用 v-on 指令：

<button v-on:事件="函数">消息</button>

<button v-on:click="动作函数">反转消息</button>

  methods: {
动作函数: function () {
this.message = this.message.split('').reverse().join('')
}



v-on 修饰符  可以用v-on 缩写

```
事件修饰符 vue提供的方法  点(.)表示的指令后缀来调用修饰符。
```

- `.stop`
- `.prevent`
- `.capture`
- `.self`
- `.once`
- `.passive`

```
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即元素自身触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
<!-- 点击事件将只会触发一次 -->
<a v-on:click.once="doThis"></a>
<!-- 滚动事件的默认行为 (即滚动行为) 将会立即触发 -->
<!-- 而不会等待 `onScroll` 完成  -->
<!-- 这其中包含 `event.preventDefault()` 的情况 -->
<div v-on:scroll.passive="onScroll">...</div>
<!-- 只有在 `keyCode` 是 13 时调用 `vm.submit()` -->
<input v-on:keyup.13="submit"
<!-- 同上 -->
<input v-on:keyup.enter="submit">

<!-- 缩写语法 -->
<input @keyup.enter="submit">
2.键盘监听  按键修饰符
<!-- 只有在 keyCode 是 13 时调用 vm.submit() -->
<input v-on:keyup.13="submit">
记住所有的 keyCode 比较困难，所以 Vue 为最常用的按键提供了别名：

<!-- 同上 -->
<input v-on:keyup.enter="submit">
<!-- 缩写语法 -->
<input @keyup.enter="submit">

全部的按键别名：

.enter
.tab
.delete (捕获 "删除" 和 "退格" 键)
.esc
.space
.up
.down
.left
.right
.ctrl
.alt
.shift
.meta
实例

<p><!-- Alt + C -->
<input @keyup.alt.67="clear">
<!-- Ctrl + Click -->
<div @click.ctrl="doSomething">Do something</div>
```

------------------------------------------









 v-html 指令用于输出 html 代码：

## v-html 指令

<div id="app">
    <div v-html="message"></div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: '<h1>菜鸟教程</h1>'
  }
})
</script>







#  v-model 指令来实现双向数据绑定



**v-model** 指令用来在 input、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。





## 过滤器

```
<!-- 在两个大括号中 -->
{{ message | capitalize }}

<!-- 在 v-bind 指令中 -->
<div v-bind:id="rawId | formatId"></div>
```

过滤器函数接受表达式的值作为第一个参数。

以下实例对输入的字符串第一个字母转为大写：

## 实例

<div id="app">
  {{ message | capitalize }}
</div>

<script>
new Vue({
  el: '#app',
  data: {
    message: 'runoob'
  },
  filters: {
    capitalize: function (value) {
      if (!value) return ''
      value = value.toString()
      return value.charAt(0).toUpperCase() + value.slice(1)
    }
  }
})
</script>

过滤器可以串联：

```
{{ message | filterA | filterB }}
```

过滤器是 JavaScript 函数，因此可以接受参数：

```
{{ message | filterA('arg1', arg2) }}
```

这里，message 是第一个参数，字符串 'arg1' 将传给过滤器作为第二个参数， arg2 表达式的值将被求值然后传给过滤器作为第三个参数。



# 条件 v-if

<div id="id名称">
    <标签 v-if="数据名字"> 为true则显示<标签>
 </div >   

 var 生成的实例名字 = new Vue({
el: '#id名称',
data: {
seen: true
}
})

# 循环 v-for

绑定数组的数据来渲染一个项目列表

   <ol>
<li v-for="todo in 数组名字">
{{ todo.text }}
</li>
</ol>
data: {
数组名字: [
{ text: '学习 JavaScript' },
{ text: '学习 Vue' },
{ text: '整个牛项目' }
]
}