# Vue.js 监听属性 watch

var vm = new Vue({ });

一

vm.$watch(' 监听的属性 名称 即data的属性名', function(变化前的值, 变化后的值) {回调将在 值  改变后调用});

二 直接写 Vue({ 里 })

<div id = "computed_props">
         千米 : <input type = "text" v-model = "kilometers">
         米 : <input type = "text" v-model = "meters">
      </div>
	   <p id="info"></p>
	  <script type = "text/javascript">
	     var vm = new Vue({
	        el: '#computed_props',
	        data: {
	           kilometers : 0,
	           meters:0
	        },
	        methods: {
	        },
	        computed :{
	        },
	        watch : {
	           kilometers:function(val) {
	              this.kilometers = val;
	              this.meters = this.kilometers * 1000
	           },
	           meters : function (val) {
	              this.kilometers = val/ 1000;
	              this.meters = val;
	           }
	        }