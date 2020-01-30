## # 条件判断v-if

## 

在元素 和 template 中使用 v-if 指令：

<div id="app">
    <p v-if="seen">现在你看到我了</p>
    <template v-if="ok">
      <h1>菜鸟教程</h1>
      <p>学的不仅是技术，更是梦想！</p>
      <p>哈哈哈，打字辛苦啊！！！</p>
    </template>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    seen: true,
    ok: true
  }
})
</script>

尝试一下 »

这里， v-if 指令将根据表达式 seen 的值(true 或 false )来决定是否插入 p 元素。

在字符串模板中，如 Handlebars ，我们得像这样写一个条件块：

```
<!-- Handlebars 模板 -->
{{#if ok}}
  <h1>Yes</h1>
{{/if}}
```

### v-else

可以用 v-else 指令给 v-if 添加一个 "else" 块：

## v-else 指令

随机生成一个数字，判断是否大于0.5，然后输出对应信息：

<div id="app">
    <div v-if="Math.random() > 0.5">
      Sorry
    </div>
    <div v-else>
      Not sorry
    </div>
</div>

<script>
new Vue({
  el: '#app'
})
</script>

尝试一下 »

### v-else-if

v-else-if 在 2.1.0 新增，顾名思义，用作 v-if 的 else-if 块。可以链式的多次使用：

## v-else 指令

判断 type 变量的值：

<div id="app">
    <div v-if="type === 'A'">
      A
    </div>
    <div v-else-if="type === 'B'">
      B
    </div>
    <div v-else-if="type === 'C'">
      C
    </div>
    <div v-else>
      Not A/B/C
    </div>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    type: 'C'
  }
})
</script>

尝试一下 »

> v-else 、v-else-if 必须跟在 v-if 或者 v-else-if之后。

### v-show

我们也可以使用 v-show 指令来根据条件展示元素：







## 循环语句

循环使用 v-for 指令。

v-for 指令需要以 **site in sites** 形式的特殊语法， sites 是源数据数组并且 site 是数组元素迭代的别名。

v-for 可以绑定数据到数组来渲染一个列表：

## v-for 指令

<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.name }}
    </li>
  </ol>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    sites: [
      { name: 'Runoob' },
      { name: 'Google' },
      { name: 'Taobao' }
    ]
  }
})
</script>

尝试一下 »

模板中使用 v-for：

<ul
  <template v-for="site in sites">
    <li>{{ site.name }}</li>
    <li>--------------</li>
  </template>
</ul>





### v-for 迭代对象

v-for 可以通过一个对象的属性来迭代数据：

<div id="app">
  <ul>
    <li v-for="value in object">
    {{ value }}
    </li>
  </ul>
</div>

<script>
new Vue({
  el: '#app',
  data: {
    object: {
      name: '菜鸟教程',
      url: 'http://www.runoob.com',
      slogan: '学的不仅是技术，更是梦想！'
    }
  }
})
</script>



v-for第二个的参数为键名：

<div id="app">
  <ul>
    <li v-for="(value, key) in object">
    {{ key }} : {{ value }}
    </li>
  </ul>
</div>

v-for第三个参数为索引：

<div id="app">
  <ul>
    <li v-for="(value, key, index) in object">
     {{ index }}. {{ key }} : {{ value }}
    </li>
  </ul>
</div>

### v-for 迭代整数         v-for 也可以循环整数

<div id="app">
  <ul>
    <li v-for="n in 10">
     {{ n }}
    </li>
  </ul>
</div>

