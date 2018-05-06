# vue 面试题汇总

**1、active-class 是哪个组件的属性？嵌套路由怎么定义**

　　(1)、active-class 是 vue-router 模块的 router-link 组件的属性
　　(2)、使用 children 定义嵌套路由

**2、怎么定义 vue-router 的动态路由? 怎么获取传过来的值**

　　在 router 目录下的 index.js 文件中，对 path 属性加上 /:id。

　　使用 router 对象的 params.id 获取

**3、vue-router 有哪几种导航钩子?**

　　三种，

　　(1)、全局导航钩子

　　　　router.beforeEach(to, from, next), 

　　　　router.beforeResolve(to, from, next), 

　　　　router.afterEach(to, from ,next)

　　(2)、组件内钩子
　　　　
　　　　beforeRouteEnter, beforeRouteUpdate, beforeRouteLeave

　　(3)、单独路由独享组件

　　　　beforeEnter

**4、v-model 是什么？怎么使用？ vue中标签怎么绑定事件**

　　v-model 可以实现双向绑定，

　　绑定事件：<input @click="doLog" />

**5、axios 是什么？怎么使用？描述使用它实现登录功能的流程**

　　axios 是请求后台资源的模块。 npm i axios -S

　　如果发送的是跨域请求，需在配置文件中 config/index.js 进行配置

**6、vuex 是什么？怎么使用？哪种功能场景使用它**

　　vuex 是专门为 vue 开发的数据状态管理模式。组件之间数据状态共享

　　使用场景：音乐播放、登录状态、购物车

	// 新建 store.js
	import vue from 'vue'
	import vuex form 'vuex'
	vue.use(vuex)
	export default new vuex.store({
		//...code
	})
	 
	//main.js
	import store from './store'
	...

**7、mvvm 框架是什么？它和其他框架(jquery) 的区别是什么？哪些场景适合**

　　mvvm 是 model + view + viewmodel 框架，通过 viewmodel 连接数据模型model 和 view

　　区别：vue 是数据驱动，通过数据来显示视图层而不是节点操用

　　场景：数据操作比较多的场景，更加快捷

**8、自定义指令(v-check, v-focus) 的方法有哪些? 它有哪些钩子函数? 还有哪些钩子函数参数**

　　全局定义指令：在 vue 对象的 directive 方法里面有两个参数, 一个是指令名称, 另一个是函数。

　　组件内定义指令：directives

　　钩子函数: bind(绑定事件出发)、inserted(节点插入时候触发)、update(组件内相关更新)

　　钩子函数参数： el、binding

**9、说出至少 4 种 vue 当中的指令和它的用法**

　　v-if(判断是否隐藏)、v-for(把数据遍历出来)、v-bind(绑定属性)、v-model(实现双向绑定)

**10、vue-router 是什么?它有哪些组件**

　　vue-router 是 vue 的路由插件,

　　组件：router-link router-view

**11、vue 的双向绑定的原理是什么**

　　vue.js 是采用数据劫持结合发布者-订阅者模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

　　具体步骤：

　　第一步：需要 observe 的数据对象进行递归遍历，包括子属性对象的属性，都加上 setter 和 getter 
这样的话，给这个对象的某个值赋值，就会触发setter，那么就能监听到了数据变化

　　第二步：compile解析模板指令，将模板中的变量替换成数据，然后初始化渲染页面视图，并将每个指令对应的节点绑定更新函数，添加监听数据的订阅者，一旦数据有变动，收到通知，更新视图

　　第三步：Watcher订阅者是Observer和Compile之间通信的桥梁，主要做的事情是:

　　1、在自身实例化时往属性订阅器(dep)里面添加自己

　　2、自身必须有一个update()方法

　　3、待属性变动dep.notice()通知时，能调用自身的 update() 方法，并触发Compile中绑定的回调，则功成身退。

　　第四步：MVVM作为数据绑定的入口，整合Observer、Compile和Watcher三者，通过Observer来监听自己的model数据变化，通过Compile来解析编译模板指令，最终利用Watcher搭起Observer和Compile之间的通信桥梁，达到数据变化 -> 视图更新；视图交互变化(input) -> 数据model变更的双向绑定效果。

**12、请详细说下你对vue生命周期的理解**

　　总共分为8个阶段创建前/后，载入前/后，更新前/后，销毁前/后。

　　**创建前/后** 

　　在beforeCreated阶段，vue实例的挂载元素$el和数据对象data都为undefined，还未初始化。

　　在created阶段，vue实例的数据对象data有了，$el还没有。

　　**载入前/后**

　　在beforeMount阶段，vue实例的$el和data都初始化了，但还是挂载之前为虚拟的dom节点，data.message还未替换。

　　在mounted阶段，vue实例挂载完成，data.message成功渲染。

　　**更新前/后**

　　当data变化时，会触发beforeUpdate和updated方法。

　　**销毁前/后**

　　在执行destroy方法后，对data的改变不会再触发周期函数，说明此时vue实例已经解除了事件监听以及和dom的绑定，但是dom结构依然存在




