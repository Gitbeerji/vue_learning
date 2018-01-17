### 2018-01-17

#### 复习
* vue单文件方式 xxx.vue
* 1: 准备好配置文件 package.json(包括描述文件 && 封装命令 num run dev) + webpack.config.js文件 (打包的配置文件)
* 2: 创建index.html (单页面应用的页)
* 3: 创建main.js (入口文件)
* 4: 引入vue和相关的文件 xx.vue
* 5: new Vue(options)
* 6: options(选项)
	- data
	- methods
	- components(组件内声明子组件)
	- props
* 7: 实例
	- 在组件内 (xxx.vue) 中的this
	- new Vue()
	- 事件
		+ this.$on
		+ this.$emit
		+ this.$once
		+ this.$off
* 8: 全局
	- Vue.component('组件名', 组件对象) 在哪里都可以使用
* 9: 组件传值
	- 父传子: 属性作为参数
		+ 常量 title='xx' 子组件声明接收参数 props:['xxx']
		+ 变量 :title='num' 子组件声明接收参数 props:['xxx']
	- 子传父: vuebus

#### 今日重点
* vue组件的使用
* 组件间通信
* vue-router使用
* vue-resource发起http请求
* axios

#### 过滤器
* content|过滤器，vue中没有提供相关的内置过滤器，可以自定义过滤器
* 组件内的过滤器 +  全局过滤器
	- 组件内过滤器就是options中的一个filters的属性(一个对象)
		+ 多个key就是不同过滤器名，多个value就是与key对应的过滤方式函数体
	- Vue.filter(名, fn)
* 输入的内容 字符串做一个反转
* 总结
	- 全局： 范围大，权利小
	- 组件内： 权利大，范围小

#### 获取DOM元素
 * 救命稻草，前端框架就是为了减少DOM操作，但是特定情况下，也留了后门
 * 在指定的元素上，添加ref="名称A"
 * 在获取的地方加入 this.$refs.名称A
 	- 如果ref放在了原生DOM元素上， 获取的数据就是原生DOM对象
 		+ 可以直接操作
 	- 如果ref放在了组件对象上，获取的就是组件对象
 		+ 1: 获取到DOM对象，通过this.$refs.sub.$el, 进行操作
 	- 对应的事件
 		+ created 完成了数据的初始化， 此时还未生成DOM，无法操作DOM
 		+ mounted 将数据已经转载到了DOM之上， 可以操作DOM

#### wappalyzer
* 获取到当前网站使用的技术