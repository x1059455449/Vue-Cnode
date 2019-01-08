# 2018-12-26 #

## 一  ##

> vueJS是什么？

	简单小巧，渐进式。功能强大的技术栈

> 为什么学习Vuejs?

1. 学习曲线平缓。易上手。功能强大，轻便
2. 目前最流行的三大框架之一，使用范围广

> vuejs的模式

MVVM模式，视图层和数据层的双向绑定，让我们无需再去关心DOM操作的事情，更过的精力放在数据和业务逻辑上去

> vueJS环境搭建

1. script
2. vue脚手架工具vue-cli搭建。后面章节会详细讲述


----------

# 2018-12-27 #

## 二(1) 数据绑定，指令，事件 ##

> vue实例和数据绑定

1. `
<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
`

通过构造函数 Vue 就可以创建一个 Vue 的根实例，并启动 Vue 应用---入口

	var app ＝new Vue({
	el:'',
	data:{
	}
	})

 必不可少的一个选项就是 el 。 el 用于指定一个页面中己存在的 DOM 元素来挂载Vue实例.el可以是标签,也可以是css语法

2. 通过 Vue 实例的 data 选项，可以声明应用内需要双向绑定的数据。建议所有会用到的数据都预先在 data 内 声明，这样不至于
将数据散落在业务逻辑中，难以维护。也可以指向一个已经有的变量

3. 挂载成功后，我们可以通过

	app.$el

来访问该元素。Vue 提供了很多常用的实例属性与方法，都以$开头，比如

$$el.Vue实例本身也代理了data对象里的所有属性，所以可以这样访问：

	访问vue实例的属性--都是以$开头，如app.$el,app.$data

	访问data元素的属性-- 直接app.属性名，app.msg

>  生命周期钩子

jquery---$(document).ready()

* created 实例创建完成后调用，此阶段完成了数据的观测等，但尚未挂载， $el 还不可用。需要初始化处理一些数据时会比较有用，后面章节将有介绍．----还未挂载
* mounted el 挂载到实例上后调用，一般我们的第一个业务逻辑会在这里开始 。相当于 $(document).ready()---刚刚挂载
* beforeDestroy 实例销毁之前调用。主要解绑一些使用 addEventListener 监听的事件等。

>  文本插值和表达式

**语法**：使用双大括号（ Mustache 语法）“｛｛｝｝”是最基本的文本插值方法，它会自动将我们双向绑定的数据实时显示出来

**用法**

在｛｛｝｝中，除了简单的绑定属性值外，还可 以使用 JavaScript 表达式进行简单的运算 、 三元运算等

	Vue .js 只支持单个表达式，不支持语句和流控制。
	{{ 6+6 *3}}---可以进行简单的运算 <br>
	{{ 6<3 ? msg :a}}---可以用三元运算符 <br>
	{{if(6>3){}}-----注意：文本插值的形式，其中不能书写表达式,支持单个表达式
	{{var a = 6}}--也是多行表达式----var a ;a = 6;
	〈！一这是语旬，不是表达式 一〉
	{ { var book = ’ Vue . js 实战 ’ ｝｝
	〈！一不能使用流控制，要使用三元运算 一〉
	{{ if (ok) return msg ))

## 二(2) 数据绑定，指令，事件 语法糖 ##

**过滤器**

Vue 支持在｛｛｝｝插值的尾部添加一小管道符 “ | ” 对数据进行过滤，经常用于格
式化文本，比如字母全部大写、货币千位使用逗号分隔等。过滤的规则是自定义的，通过给 Vue 实例添加选项 filters 来设置

过滤器：{{ data | filter1 |filter2}}

{{date | formatDate(66,99)}} 中的第一个和第二个参数，分别对应过滤器的第二个和第三个参数

**指令和事件**

指令（ Directives ）是 Vue 模板中最常用的一项功能，它带有前缀 v－，能帮我们快速完成DOM操作。循环渲染。显示和隐藏

本节目标 v-text , v-html , v-bind , v-on

	v­text:­解析文本 和{{ }} 作用一样
	
	v­html:解析html
	
	v­bind：基本用途是动态更新 HTML 元素上的属性，比如 id 、class 等,本节只介绍基本章节，后面章节会更加深入详细讲述
	
	v­on：它用来绑定事件监听器

> v-on具体介绍

在普通元素上，v-on可以监听原生的DOM时间，除了click外，还有dblclick、 keyup, mousemove 等。表达式可以是一个方法名，这些方法都写在Vue实例里面的methods属性内，并且是以函数的形式，函数内的this只想的是当前Vue实例本身，因此可以直接使用this.xxx的形式来访问或者修改数据

**vue中用 到的所有方法都定义在methods中**

两个按钮，点击同时加数字？？？？思考

## 语法糖 ##

语法糖是指在不影响功能的情况下，添加某种简洁方法实现同样的效果 ，从而更加方便程序开发。

	v-bind:冒号
	v-on:@

----------

# 2018-12-28 #

## 三 计算属性 ##

### 什么是计算属性 ####

我们己经可以搭建出一个简单的 Vue 应用，在模板中双向绑定一些数据或表达式了。但是表达式如果过长，或逻辑更为复杂时，就会变得雕肿甚至难以阅读和维护

	<div>
		{{ text.split ( ’,’ ) •reverse () . join (’,’)}}
	</div>

这里的表达式包含 3 个操作，并不是很清晰，所以在遇到复杂的逻辑时应该使用**计算属性**

**注** 

	所有计算属性都以函数的形式写在Vue实例内的computed选项内，最

	终返回计算后的结果

### 计算属性的用法 ###

在一个计算属性里可以完成各种复杂的逻辑，包括运算，函数调用等，只要最终返回一个结果就行。除了上例简单的用法，计算属性还可以依赖多个VUE实例的数据，**只要其中任一数据发生变化，计算属性就会重新执行，试图也会更新**

》》》 Vue-Cnode\third demo\shopping cart.html


> getter 和 setter

每一个计算属性都包含－个 getter 和一个 setter，我们上面的两个示例都是计算属性的默认用法 ， 只是利用了 getter来读取。在你需要时，也可以提供一个setter函数，当手动修改计算属性的值就像修改一个普通数据那样时，就会触发 setter函数，执行一些自定义的操作

**计算属性除了上述简单的文本插值外，还经常用于动态地设置元素的样式名称 class 和内联样式 style**

## 小Tips ##

- 计算属性可以依赖其他计算属性
- 计算属性不仅可以依赖当前Vue实例的数据，还可以依赖其他实例的数据

### 计算属性缓存 ###

- 调用methods里的方法也可以与计算属性起到同样的作用(计算属性能实现的，methods也能实现)
- **页面中的方法：如果是调用方法，只要页面重新渲染，方法就会重新执行，不需要渲染，则不需要重新执行**
- **计算属性：不管渲染与否，只要计算属性依赖的数据未发生变化，则永恒不变**

## 结论 ##

**没有使用计算属性，在 methods 里定义了一个方法实现了相同的效果，甚至该方法还可以接受参数，使用起来更灵活。既然使用 methods 就可以实现，那么为什么还需要计算属性呢？原因就是计算属性是基于它的依赖缓存的。 一个计算属性所依赖的数据发生变化时，它才会重新取值，所以text 只要不改变，计算属性也就不更新**

> 何时使用

使用计算属性还是 methods 取决于你是否需要缓存，当遍历大数组和做大量计算时，应当使用计算属性，除非你不希望得到缓存


----------

## 2018-12-29 ##

## 四 v­bind以及class与style的绑定 ##

**应用场景:** DOM 元素经常会动态地绑定一些 class 类名或 style 样式

### 了解bind指令 ###

> v­bind的复习

**链接的 href 属性和图片的 src 属性都被动态设置了，当数据变化时，就会重新渲染。**

在数据绑定中，最常见的两个需求就是元素的样式名称 class 和内联样式 style 的动态绑定，它们也是 HTML的属性，因此可以使用 v­bind 指令。我们只需要用 v­bind计算出表达式最终的字符串就可以，不过有时候表达式的逻辑较复杂，使用字符串拼接方法较难阅读和维护，所以 Vue.js 增强了对 class 和 style 的绑定。

## 绑定 class 的几种方式 ##

- **对象语法**

给 v­bind:class 设置一个对象，可以动态地切换 class，* **值对应true ,false**
当 class 的表达式过长或逻辑复杂时，还可以绑定一个计算属性，这是一种很友好和常见的
用法，**一般当条件多于两个时， 都可以使用 data 或 computed**

- **数组语法**

当需要应用多个 class 时可以使用数组语法,给：class 绑定一个数组，应用一个 class
列表：

**数组成员直接对应className--类名**

> 可以用三目运算实现,对象和数组混用

- 在组件上使用 : 暂时不考虑

- **绑定内联样式**

使用 v­bind:style （即：style ）可以给元素绑定内联样式，方法与：class 类似，
也有对象语法和数组语法，看起来很像直接在元素上写 CSS:

**注意 : css 属性名称使用驼峰命名（ came!Case ）或短横分隔命名（ kebab­case
）**

- 应用多个样式对象时 ， 可以使用数组语法 ：在实际业务 中,style 的数组语法并不常
用 ， 因为往往可以写在一个对象里面 ： 而较为常用 的应当是计算属性

- 使用 :style 时， Vue .js 会自动给特殊的 css 属性名称增加前缀，比如 transform 。
**无需再加前缀属性！！！！**


----------

## 2019-01-01 ##

## 五 vueJS中的内置指令 ##

### 基本指令 ###

> v-cloak一般与display:none进行结合和使用

	作用：解决初始化慢导致页面闪动的最佳实践

> v-once

	定义它的元素和组件只渲染一次

### 条件渲染指令 ###

> v-if v-else-if v-else

	用法： 必须跟着屁股走

**v-if的弊端**

Vue在渲染元素的时候，出于效率的考虑，会尽可能德复用已有的元素而非重新渲染，因此渲染时可能会和我们预想中的不一样
只会渲染变化的元素，也就是说,input元素被复用了

> 解决方法

	加key，唯一，提供key值可以来决定是否服用该元素 

> v-show 

	只改变了css属性display

## v­-if和v­-show的比较 ##

v-if

	实时渲染：页面显示时就渲染，不显示，就会移除，可以从DOM元素结

	构上看到

v-show

	v-show的元素永远存在页面中，实时改变了css的diaplay的属性

## 列表渲染指令v­for ##

**用法：**

当需要将一个数组遍历或枚举一个对象属性的时候循环显示，就会用到列表渲染指令

> 使用场景

- 遍历多个对象
- 便利一个对象的多个属性

##  数组更新，过滤与排序 ##

> 改变数组的方法

- push() 在末尾添加元素
- pop() 将数组最后一个元素移除
- shift() 删除数组的第一个元素
- unshift() 在数组的第一个位置添加一个元素
- sort()
- reverse()
- splice() 可以添加或者删除函数---返回删除的元素

	**三个参数：**
	
	第一个：表示开始操作的位置
	第二个：要操作的长度
	第三个：为可选参数

> 两个数组变动Vue检测不到

	1. 改变数组的指定项
	2. 改变数组长度

> 过滤：filter	   

**解决方法**

	1. set
	2. splice

* 改变指定项：Vue.set(app.arr,1,"car")
* app.arr.splice(1):改变数组长度，长度为1(app.arr.splice(0)全部删除)

## 方法和事件 ##

[object MouseEvent]

### 基本用法 ###

v-on 绑定的事件；类似于原生的onclick等写法

	methods:{
	handle:function (count) {
	count = count || 1;
	this.count += count;
	}
	}

**如果方法中带有参数，但是没有加括号，默认穿原生事件对象event,即**

### 修饰符 ###

	在Vue中传入event对象用$event
	
	向上冒泡：
	
	stop:阻止单击事件向上冒泡
	
	prevent:提交事件并且不重载页面
	
	self:只是作用在元素本身而非子元素的时候调用
	
	once:只执行一次的方法
	
	可依监听键盘事件：
	
	<input @keyup.13 ="submitMe"> ——­指定的keyCode

	vueJS为我们提供了：

	.enter
	.tab
	.delete

----------

## 2019-01-02 ##

## 六 表单与v­model ##

## 基本用法 ##

**v-modal**

Vue提供了v-modal指令，用于在**表单类元素**上双向绑定事件

**input和textarea**

	可以用于input框，以及textarea等
 
**注意：**所显示的值只依赖于所绑定的数据，不再关心初始化时的插入的value

### 单选按钮 ###

1. 单个单选按钮，直接用v­bind绑定一个布尔值，用v­model是不可以的
2. 如果**是组合使用，就需要v­model来配合value使用，绑定选中的单选框的value值，此处所绑定的初始值可以随意给**

### 复选框 ###

1. 单个复选框，直接用定一个布尔值，可以用v­model可以用v­bind
2. 多个复选框， **如果是组合使用，就需要v­model来配合value使用，v­model绑定一个数组** 如果绑定的是字符串，则会转化为true或false，与**所有绑定的复选框**的checked属性相对应

### 下拉框 ###

1.  如果是单选，所绑定的value值初始化可以为数组，也可以为字符串，有value直接优先匹配一个value值，没有value就匹配一个text值
2.  如果是多选，就需要v­model来配合value使用，v­model绑定一个数组，与复选框类似
3.  v­model一定是绑定在select标签上

## 总结 ##

如果是单选，初始化最好给定字符串，因为v­model此时绑定的是静态字符串或者布尔值

如果是多选，初始化最好给定一个数组

## 绑定值 ##

* 单选按钮

	只需要用v­bind给单个单选框绑定一个value值，此时，v­model绑定的就是他的value值

* 复选框
* 下拉框

	在select标签上绑定value值对option并没有影响

### 修饰符 ###

* lazy

	v-­model默认是在input输入时实时同步输入框的数据，而lazy修饰符，可以使其在失去焦点或者敲回车键之后在更新

* number

	—将输入的字符串转化为number类型

* trim

	trim自动过滤输入过程中收尾输入的空格


----------

## 2019-01-04 ##

## 七 可复用性的组件详解（涉及的代码可以在github的seventh demo查看） ##

## 使用组件的原因 ##

作用：提高代码的可复用性

##  组件的使用方法 ##

> 全局注册

	Vue.component('my-component',{
		template:'<div>我是组件的内容</div>'
	})

- 优点：所有的Vue实例都可以使用
- 缺点：权限太大，容错率降低

> 局部注册

	var app = new Vue({
		el:'#app',
		components:{
			'my-component':{
				template: '<div>我是组件的内容</div>'
				}
			}
	})

> 受限制的情况

Vue组件的模板在某些情况下会受到html标签的限制，如<table\>中只能含有<td\>,<tr\>,<tbody\>这些元素，所以直接在table中使用组件是无效的，**此时可以使用is属性来挂载组件**

	<table>
		<tbody is="my-component"></tbody>
	</table>

##  组件使用的技巧 ##

1. 推荐使用小写字母+"-"进行命名（）必须，如child,my-component等对组件进行命名
2. template中的内容**必须**被一个DOM元素包括，也可以嵌套
3. 在组件的定义中，除了template之外的还有其他选项，诸如data,computed,methods等
4. **data必须是一个方法**

## 使用props传递数据 父组件向子组件传递数据 ##

1. 在组件中使用props来从父组件接受参数，**请注意**，在props中定义的属性，都可以在组件中直接使用
2. **props来自父级，而组件的data return的数据就是组件自己的数据，两种抢矿的作用域就是组件本身，可以在template，computed，methods中直接使用**
3. props的值有两种，一种是数组，一种是对象
4. 可以使用v-bind动态绑定父组件来的内容

## 单向数据流 ##

- **解释：**通过props传递数据是单向的，也就是父组件数据变化时会传递给子组件，但是反过来不行
- **目的：**尽可能将父子组件解稿，避免子组件无意中修改了父组件的状态
- **应用场景：**业务中常用到的两种需要改变props的情况

**两种情况**

> 第一种

一种是父组件传递初始值进来，子组件将它作为初始值保存起来，在自己的作用域下可以随意修改和使用。这种情况可以在组件data内再声明一个数据，引用父组件的prop

1. 步骤一：注册组件
2. 步骤二：将父组件的数据传递进来，并在子组件中庸props接收
3. 步骤三：将传递进来的数据通过初始值保存起来

代码示例：

	<div id="app">
		<my-comp init-count="666"></my-comp>
	</div>
	<script>
	var app = new Vue({
		el:'#app',
		components:{
			'my-comp':{
				props:['init-count'],
				template:'<div>{{init-count}}</div>',
				data:function () {
					return{
					count:this.initCount
					}
				}
			}
		}
	})
	</script>

> 第二种

另一种情况就是prop作为需要被转变的原始值传入。这种情况使用计算属性即可

1. 步骤一：注册组件
2. 步骤二：将父组件的数据传递进来，并在子组件中用props接收
3. 步骤三：将传递进来的数据通过计算属性进行重新计算

代码示例：

	<inputtype="text" v-model="width">
	<my-comp :width="width"></my-comp>
	<script>
	var app = new Vue({
		el:'#app',
		data:{
			width:''
		},
		components:{
			'my-comp':{
				props:['init-count','width'],
				template:'<div :style="style">{{init-count}}</div>',		
			computed:{
				style:function () {
					return{
						width:this.width+'px',
						background:'red'
						}
					}
				}
			}
		}
	})
	</script>

## 数据验证 ##

### 命名方式 ###

vue组件中camelCased (驼峰式) 命名与 kebab­case（短横线命名）

**注意事项**

1. **在html中, myMessage 和 mymessage 是一致的,,因此在组件中的html中使用必须使用kebab­case（短横线）命名方式。强调：在html中不允许使用驼峰**
2. **在组件中, 父组件给子组件传递数据必须用短横线。在template中，必须使用驼峰命名方式，若为短横线的命名方式。则会直接保错**
3. **在组件的data中,用this.xxx引用时,只能是驼峰命名方式。若为短横线
的命名方式则会报错**

### 验证类型 ###

- String
- Number
- Boolean
- Object
- Array
- Function

代码示例：

	Vue.component （ ’ my-compopent ’， ｛
		props : {
			//必须是数字类型
			propA : Number ,
			//必须是字符串或数字类型
			propB : [String , Number] ,
			//布尔值，如果没有定义，默认值就是 true
			propC: {
				type : Boolean ,
				default : true
			},
			//数字，而且是必传
			propD: {
				type: Number ,
				required : true
			},
			//如果是数组或对象，默认值必须是一个函数来返回
			propE: {
			type : Array ,
				default : function () {
				return [] ;
			}
			},
			//自定义一个验证函数
			propF: {
				validator : function (value) {
				return value > 10;
			}
			}
		}
	});

## 组件通信 ##

组件关系可分为父子通信组件、兄弟通信组件、跨级租间通信

> 自定义事件—子组件给父组件传递数据

使用v-on除了监听DOM事件外，还可以用于组件之间的自定义事件。

**JavaScript 的设计模式：**观察者模式，dispatchEvent 和 addEventListener这两个方法。 Vue组件也有与之类似的一套模式,子组件用$emit（）来 触发事件，父组件用$on()来监昕子组件的事件

**步骤**

1. 自定义事件
2. 在子组件中庸$emit触发事件，第一个参数是事件名，后面参数是要传递的数据
3. **在自定义时间中用一个参数来接受**

代码示例：

	<div id="app">
		<p>您好,您现在的银行余额是{{total}}元</p>
		<btn-compnent @change="handleTotal"></btn-compnent>
	</div>
	<script src="js/vue.js"></script>
	<script>
		var app = new Vue({
			el:'#app',
			data:{
				total:0
			},
			components:{
				'btn-compnent':{
					template:'<div>\
						<button @click="handleincrease">+1</button> \
						<button @click="handlereduce">-1</button>\
						</div>',
					data:function(){
						return {
							count:0
						}
					},
					methods:{
						handleincrease :function () {
							this.count++;
							this.$emit('change',this.count);
						},
						handlereduce:function () {
							this.count--;
							this.$emit('change',this.count);
						}
					}
				}
			},
			methods:{
				handleTotal:function (total) {
					this.total = total;
				}
			}
		})
	</script>

> 在组件中使用v­model

$emit代码，这行代码实际上会触发一个Input事件，'input'后的参数就是传递给v-model绑定的属性的值

v-model其实就是一个语法糖，这背后的两个操作：

	1 v-bind绑定一个value值
	
	2 v-on指令给当前元素绑定input事件

要使用v-model，要做到：

	1 接收 一个value属性
	
	2 在有新的value时触发input事件

代码示例：

	<div id="app">
		<p>您好,您现在的银行余额是{{total}}元</p>
		<btn-compnent v-model="total"></btn-compnent>
	</div>
	<script src="js/vue.js"></script>
	<script>
		var app = new Vue({
			el:'#app',
			data:{
				total:0
			},
			components:{
				'btn-compnent':{
					template:'<div>\
						<button @click="handleincrease">+1</button> \
						<button @click="handlereduce">-1</button>\
					</div>',
					data:function(){
						return {
						count:0
						}
					},
					methods:{
					handleincrease :function () {
						this.count++;
						----------------------注意观察.这一行,emit的是input事件----------------
						this.$emit('input',this.count);
					},
					handlereduce:function () {
						this.count--;
						this.$emit('input',this.count);
					}
					}
				}
			},
			methods:{
				/* handleTotal:function (total) {
				this.total = total;
				}*/
			}
		})
	</script>

> 非父组件之间的通信

[官网：非父组件之间的通信](https://cn.vuejs.org/v2/guide/state-management.html)

[https://juejin.im/post/5a4353766fb9a044fb080927](https://juejin.im/post/5a4353766fb9a044fb080927)

![](https://i.imgur.com/bmYXtIH.png)

子链：this.$refs:提供了为子组件提供索引的方法，用特殊的属性ref为其增加一个索引

详细代码请参考：

[非父组件之间的通信](https://x1059455449.github.io/Vue-Cnode/seventh%20demo/%E9%9D%9E%E7%88%B6%E7%BB%84%E4%BB%B6%E4%B9%8B%E9%97%B4%E7%9A%84%E4%BC%A0%E9%80%92.html)

## 使用slot分发内容 ##

> 什么是slot（插槽）

为了让组件可以组合，我们需要一种方式来混合父组件的内容与子组件自己的模板。这个过程被称为内容分发.Vue.js 实现了一个内容分发 API，使用特殊的 ‘slot’ 元素作为原始内容的插槽

> 编译的作用域

在深入内容分发 API 之前，我们先明确内容在哪个作用域里编译。假定模板为：

	<child-component>
		{{ message }}
	</child-component>

message 应该绑定到父组件的数据，还是绑定到子组件的数据？答案是父组件。组件作用域简单地说是：

	父组件模板的内容在父组件作用域内编译
	
	子组件模板的内容在子组件作用域内编译

> 插槽的用法


父组件的内容与子组件相混合，从而弥补了视图的不足
**混合父组件的内容与子组件自己的模板**

单个插槽：

	<div id="app">
	        <my-component>
	            <p>我是父组件的内容</p>
	        </my-component>
	</div>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
	    <script>
	    Vue.component('my-component',{
	        template:'<div>\
	        <slot>\
	            如果父组件没有插入内容，我就作为默认出现\
	        </slot>\
	        </div>'
	    })    
	    var app = new Vue({
	        el:'#app',
	        data:{
	
	        }
	    })
	</script>

具名插槽：

	<div id="app">
	        <my-component>
	            <p>我是父组件的内容</p>
	        </my-component>
	        <hr>
	        具名插槽: <br>
	        <name-component>
	            <h3 slot="header">标题</h3>
	            <p>正文</p>
	            <p>内容</p>
	            <p slot="footer">底部</p>
	        </name-component>
	    </div>
	<script src="https://cdn.jsdelivr.net/npm/vue@2.5.16/dist/vue.js"></script>
	    <script>
	
	        Vue.component('my-component', {
	            template: '<div>\
	        <slot>\
	            如果父组件没有插入内容，我就作为默认出现\
	        </slot>\
	        </div>'
	        })
	        Vue.component('name-component', {
	            template: '<div><div class="header">\
	                <slot name="header">\
	                    \
	                </slot>\
	            </div>\
	            <div class="container">\
	                <slot>\
	                    \
	                </slot>\
	            </div>\
	            <div class="footer">\
	                <slot name="footer">\
	                    \
	                </slot>\
	            </div></div>'
	        })
	        var app = new Vue({
	            el: '#app',
	            data: {
	
	            }
	        })
	    </script>

> 作用域插槽

作用域插槽是一种特殊的slot，使用一个可以复用的模板来替换已经渲染的元素
——从子组件获取数据

**注意：**template模板是不会被渲染的

[slot插槽](https://x1059455449.github.io/Vue-Cnode/seventh%20demo/%E4%BD%9C%E7%94%A8%E5%9F%9F%E6%8F%92%E6%A7%BD.html)

> 访问slot

通过this.$slots.(NAME)

	mounted: function () {
                //实例挂载完成后，访问slot
                //本次访问的slot会出现Vnode这个虚拟节点，访问时要加[0]
                var header = this.$slots.header
                var text = this.$slots.header[0].elm.innerText
                var outertext = this.$slots.header[0].elm.outerText
                var html = this.$slots.header[0].elm.innerHTML
                var outerhtml = this.$slots.header[0].elm.outerHTML
                console.log(header)
                console.log(text)
                console.log(outertext)
                console.log(html)
                console.log(outerhtml)
            }

## 组件高级用法–动态组件 ##

VUE给我们提供 了一个元素叫component
作用是： 用来动态的挂载不同的组件
实现：使用is特性来进行实现的

[动态组件](https://x1059455449.github.io/Vue-Cnode/seventh%20demo/%E5%8A%A8%E6%80%81%E7%BB%84%E4%BB%B6.html)


----------

## 2018-01-08 ##

## 自定义指令 ##

### 自定义指令的基本用法 ###

和组件类似分全局注册和局部注册，区别就是把component换成了derective

### 钩子函数 ###

指令定义函数提供了几个钩子函数（可选）：

bind: 只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作。

inserted: 被绑定元素插入父节点时调用（父节点存在即可调用，不必存在于 document中）。

update: 被绑定元素所在的模板更新时调用，而不论绑定值是否变化。通过比较更新前后的绑定值，可以忽略不必要的模板更新（详细的钩子函数参数见下）。

componentUpdated: 被绑定元素所在模板完成一次更新周期时调用。

unbind: 只调用一次， 指令与元素解绑时调用。

### 钩子函数的参数有： ###

el: 指令所绑定的元素，可以用来直接操作 DOM 

binding: 一个对象，包含以下属性：

	name: 指令名，不包括 v­ 前缀。

	value: 指令的绑定值， 例如： v­my­directive=”1 + 1”, value 的值是 2。

	oldValue: 指令绑定的前一个值，仅在 update 和 componentUpdated 钩子中可用。无论值是否改变都可用。

	expression: 绑定值的字符串形式。 例如 v­my­directive=”1 + 1” ， expression 的值是“1 + 1”。

	arg: 传给指令的参数。例如 v­my­directive:foo， arg 的值是 “foo”

	modifiers: 一个包含修饰符的对象。 例如： v­my­directive.foo.bar, 修饰符对象,,,modifiers 的值是 { foo: true, bar: true }。
vnode: Vue 编译生成的虚拟节点。

oldVnode: 上一个虚拟节点，仅在 update 和 componentUpdated 钩子中可用。

[Vue官网：自定义指令](https://cn.vuejs.org/v2/guide/custom-directive.html#ad)