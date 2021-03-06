# learn_beerji
### 2018-01-05 webpack vue学习

#### webpack-ES6的处理
* ES6的模块，vue本身默认支持ES6的模块导入导出
* babel
	- babel-loader(内部依赖babel-core)
		+ 关键字( presets es2015)
		+ 函数( plugins babel-plugin-transform-runtime)

### 2018-01-08

#### ES6中的模块
* 默认
	- 导入 `import [,..xxx] [,..from] './xxx.ext'`
	- 导出 `export default obj;`

* 声明式
	- 1导出 `export var obj = xxx;`
	- 2导出 `export var obj2 = {};`
	- 3单独导出 `export {stu};`
	- 导入 `import {obj, obj2, stu} from './xxx.js'`,直接使用obj
* 全体
* 默认导出和声明式导出在使用上的区别
	- 要注意，声明式导入的时候，必须{名称} 名称要一致(按需导入)
	- 默认导入，可以随意的使用变量名

```javascript
	
	{
		default:"默认导出结果",
			// import xx from './cal.js' 会获取到整个对象的default属性
		obj1:"声明式导出1",
		obj2:"声明式导出2",
		obj3:"声明式导出3",
		obj4:"声明式导出4"
	}

			// import * as allObj from './cal.js' 获取的就是一整个对象

```

* import 和 export 一定要写在顶级， 不要包含在 {}内

#### ES6中代码变化
* 对象属性的声明

```javascript 
	var name = 'abc';
	var person = { name }; //简写 -> var person = {name: name};

	//声明函数
	var cal = {
		add: function(){
			return 1;
		},
		add2(){
			return 2;
		},
		add3: function (n1, n2){
			return n1 + n2;
		},
		add4(n1, n2){	//省略function
			return n1 + n2;
		}
	}
```

* 当属性的key和变量的名相同，而要使用变量的值做value
* 就可以简写 {name} -> {name: name}
* es6中函数声明
	- 省略了 :function

### 2018-01-09

#### vue单文件方式
* 单文件就是以 *.vue结尾的文件，最终通过webpack也会编译成*.js在浏览器运行
* 内容： <template></template> + <script></script> + <style></style>
	- 1: template中只能有一个根节点 2.X
	- 2: script中 按照 export default {配置} 来写
	- 3: style中 可以设置scoped属性，让其只在 template中生效

#### 以单文件的方式启动
* webpack找人来理解单文件代码
	- vue-loader, vue-template-complier 代码中依赖 vue

* 启动命令
* `..\\node_modules\\.bin\\webpack-dev-server --inline --hot --open`

#### vue介绍
*  JS框架
	- 2014年 Vue诞生 尤雨溪
	- 2013年 react 
	- 2009年 angularjs  核心： 模块化 双向数据绑定(脏检测:一个数组($watch))
* 核心概念： 组件化 双向数据流(基于ES5中的defineProperty来实现的)IE9才支持
	- __细分代码__
		+ 头部： 页面、样式、动态效果
		+ 代码： template script style
* 框架对比，建议学完vue再看
* https://cn.vue.js.org/v2/guide/comparison.html#React

#### 双向数据流
* js内存属性发生改变，影响页面的变化
* 页面的改变影响js内存属性的改变

#### vue中常用的v-指令演示
* 常用指令
* v-text 是元素的 innerText 只能在双标签中使用
* v-html 是元素的 innerHtml 不能包含<!-- {{xxx}} -->
* v-if 元素是否移除或插入
* v-show 元素是否显示或隐藏
* v-model 双向数据绑定 v-bind是单项数据绑定(内存js改变影响页面)

### 2018-01-11

#### class结合v-bind使用
* 需要根据可变的表达式的结果来给class赋值，就需要用到 v-bind:class='xxx'
* v-bind:属性名='表达式'，最终表达式运算结束的结果赋值给该属性名
	- 简化写法 '属性名="表达式"'
* class: 结果的分类
	- 一个样式: 返回字符串(三元表达式和key和样式的对象清单)
	- 多个样式: 返回对象(样式做key, true或false做值)

#### methods 和 v-on 的使用
* 绑定事件的方法
	- `v-on:事件名="表达式||函数名"`
	- 简写： `@事件名="表达式||函数名"`
* 函数名如果没有参数，可以省略() 只给一个函数名称
* 在 export default这个对象的根属性加上methods属性，其实一个对象
	- key 是函数名 值是函数体
* 在export default 这个对象的根属性加上data属性，其实一个函数，返回一个对象
	-对象的属性是我们初始化的变量的名称
* 凡是在template中使用变量或者函数，不需要加this
* 在script中使用就需要加上this

#### v-for的使用
* 可以单独使用操作数组 (item, index)
* 可以使用操作对象 (value, key, index)

* key是类似于 trank by 的一个属性，为的是告诉vue，js中的元素，与页面之间的关联， 当试图删除元素的时候，是单个元素的删除，而不是全部替换，所以需要关联关系， 设置(必须，性能)
* 2.2.0+ 的版本里，当在组件中使用 v-for 时， key是必须的

### 2018-01-15

#### 父子组件使用
* 父和子， 使用的是父， 被用的是子
* 父需要声明子组件， 引入子组件对象， 声明方式如下

```javascript
	import 子组件对象 from './xxx.vue';
		{	
			components: {
				组件名: 子组件对象
			}
		}
```

* 全局组件， 使用更为方便， 不需要引入和声明， 直接用
* 在main.js中引入一次， 在main.js中使用 `vue.component('组件名', 组件对象);`
* 所有的组件就可以直接通过组件名，使用

#### 父传子
* 父组件通过子组件的属性将值进行传递
	- 方式有另两种
		+ 常量: prop1 = "变量值" 
		+ 变量: prop2 = "变量名"
* 子组件需要声明
	- 根属性 props: ['prop1', 'prop2']
	- 在页面直接使用{{prop1}}
	- 在js中应该如何使用prop1?  this.prop1 可以获取

#### 子向父组件通信(vuebus)
* 通过new Vue()这样的一个对象，来$on('事件名', fn(prop1, prop2))
* 另一个组件映入同一个vuebus，来$emit('事件名', prop1, prop2)

### 2018-01-17

#### 查看文档的对象分类
* 1.全局的代表Vue
* 2.实例的代表this.或者new Vue()
* 3.选项代表new Vue()的参数或者 export default里面的属性



