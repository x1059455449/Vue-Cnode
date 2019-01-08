## MVVN ##

MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。

在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。

ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

![](https://i.imgur.com/XxRO2KD.png)

MVVN是把MVC里的Controller和MVP里的Presenter改成了ViewModel。Model+View+ViewModel。View的变化会自动更新到ViewModel，ViewModel的变化也会自动更新同步到View上显示。

> 翻译过来就是

只要视图层或者是数据层有一个发生改变，随即即可通过ViewModel同步更新到对应的视图层或者数据层，反之亦然。

View是HTML显示的页面
ViewModel（可视为一个桥梁）是业务层逻辑（一切的js都可以视为业务逻辑，比如表单按钮提交，自定义事件的注册和处理逻辑都在ViewModel里面负责监控两边的数据）。
Model数据基层是对数据的处理（比如增删改查）

MVVN模式的框架有：Angular+Vue.js 和 Knockout+Ember.js等

### 参考 ###

[MVC，MVP 和 MVVM 的图示](http://www.ruanyifeng.com/blog/2015/02/mvcmvp_mvvm.html)

[你对MVC、MVP、MVVM 三种组合模式分别有什么样的理解？](https://www.zhihu.com/question/20148405)

[对MVVN模式的理解](http://www.cnblogs.com/sirkevin/archive/2012/11/28/2793471.html)

[http://www.cnblogs.com/xueduanyang/p/3601471.html](http://www.cnblogs.com/xueduanyang/p/3601471.html)


## Vue.js有什么优点 ##

**低耦合**

视图（View）可以独立于Model变化和修改，一个ViewModel可以绑定到不同的"View"上，当View变化的时候Model可以不变，当Model变化的时候
View也可以不变。

**可重用性**

你可以把一些视图逻辑放在一个ViewModel里面，让很多view重用这段视图逻辑。

**独立开发**

开发人员可以专注于业务逻辑和数据的开发（ViewModel），设计人员可以专注于页面设计。

**可测试**

界面素来是比较难于测试的，而现在测试可以针对ViewModel来写
易用灵活高效

[与 React 相比，Vue.js 有哪些优点？](https://www.zhihu.com/question/266364449)

[对比其他框架](https://cn.vuejs.org/v2/guide/comparison.html)


----------

## 第一次页面加载会触发哪几个钩子 ##

beforeCreate created beforeMount mounted

----------

## v-bind的变量语法，数组语法，对象语法 ##

v-bind通常用来绑定属性的，格式是v-bind：属性名 = "值"，简写:属性名 = "值"
变量语法：v-bind：class = "变量"，变量形式 ,这里的变量的值，通常是在css定义好的类名；

数组语法：v-bind：class= "[变量1，变量2]" ，数组形式，其实跟上面差不多，只不过可以同时绑定多个class名；

对象语法：v-bind:class = {classname1：boolean，classname2：boolean}，对象形式，这里的classname1（2）其实就是样式表中的类名，这里的boolean通常是一个变量，也可以是常量、计算属性等，这种方法也是绑定class最常用的方式。

## 简述v-model的作用 ##

v-model的作用是:用于在表单类元素上双向绑定事件

## 对组件的理解 ##

[https://www.jianshu.com/p/79e4df63f31f](https://www.jianshu.com/p/79e4df63f31f)

[https://segmentfault.com/a/1190000010527064](https://segmentfault.com/a/1190000010527064)

组件 (Component) 是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素，Vue.js 的编译器为它添加特殊功能。在有些情况下，组件也可以表现为用 is 特性进行了扩展的原生 HTML 元素。所有的 Vue 组件同时也都是 Vue 的实例，所以可接受相同的选项对象 (除了一些根级特有的选项) 并提供相同的生命周期钩子