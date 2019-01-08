# Vue基础知识汇总 #

## 构造器 ##

实例化Vue的时候，需传入一个对象，它可以是数据、模板、挂载元素、方法和生命周期钩子

## 属性和方法 ##
	
	1 每个Vue实例都会代理data对象里所有的属性
	
	2 Vue实例暴露了一些有用的实例属性和方法，这些属性与方法都有前缀$，以便与代理的data属性区分

## 实例生命周期 ##

- created钩子：在实例被创建时被调用
- mounted：当编译好的HTML被挂载到对应的位置，这个操作完成后触发，也就是实例创建完成后触发
- updated：当data中的数据改变，并且虚拟DOM重新渲染完成后触发
- destroyed：实例挂载完成后销毁

**概要：**钩子的this指向调用它的实例

## 生命周期图示 ##

[https://cn.vuejs.org/images/lifecycle.png](https://cn.vuejs.org/images/lifecycle.png)

## 插值 ##

**文本：**

	双大括号
	
	v-text
**纯HTML：**

	v-html	

**属性：**

	v-bind（大双括号不能在属性中使用，因此需使用v-bind）

**使用JS表达式**

## 指令 ##

### 指令类型 ###

	v-bind
	
	v-on
	
	v-if
	
	v-for

v-if：

	<div id="app">
	<template v-if="ok==='username'">
	用户名: <input type="text" placeholder="请输入用户名" key="name-input">
	</template>
	<template v-else>
	密码: <input type="text"  placeholder="请输入密码" key="psd-input">
	</template>
	<button @click="toggle">点击切换类型</button>
	</div>
	
	new Vue({
	  el: "#app",
	  data: {
	    ok:'username'
	  },
	  methods: {
	  toggle: function(todo){
	      if(this.ok==='username'){
	      this.ok = 'psd'
	    }else{
	      this.ok = 'username';
	    }
	  }
	  }
	})

v-for：

	<div id="app">
	<ul>
	  <li v-for="item in items">{{item}}</li>
	</ul>
	</div>
	
	new Vue({
	el: "#app",
	data: {
	items:['a','b','c']
	},
	methods: {
	  toggle: function(todo){
	      todo.done = !todo.done
	  }
	}
	})

### 修饰符 ###

v-on：
	
	.stop:阻止单击事件冒泡<a v-on:click.stop="doThis"></a>
	.prevent提交事件不再重载页面
	.capture 添加事件侦听器时使用时间捕获模式
	.self只当事件在该元素本身(而不是子元素)触发时触发回调

## 过滤器 ##

过滤器的目的是用于文本转换,转化成你想要的格式






