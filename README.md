# 全局安装 vue-cli
$ npm install --global vue-cli
## 创建一个基于 webpack 模板的新项目
$ vue init webpack my-project
## 安装依赖 走你
- $ cd my-project
- $ npm install
- $ npm run dev

##  一些项目依赖扩展

>**项目状态管理vuex**

```
$ npm install vuex --save

```
> **fetch ajax 通信**

```
$ npm install axios

不过在post提交的时候

在node环境中可以使用Qs模块,Qs.stringify(data)来处理数据

安装qs 

npm install qs --save

```
> **支持vue文件的autofix插件:vuefix 开启eslint校验以后可以自动补全错误**


```
$ npm install eslint-plugin-vuefix --save-dev

在“.eslintrc” 文件中添加插件声明

{
    "plugins": [
        "vuefix"
    ]
}
```
> **安装fastclick 解决移动端 click 事件响应慢和点透问题**

```
$ npm install fastclick --save

引用fastclick
import FastClick from 'fastclick'

//注册fastClick
FastClick.attach(document.body);

```
# 一些好的方法

- 阻止默认事件 @click.prevent.stop
- 阻止冒泡事件 @click.stop
- 阻止移动端滑动事件 @touchmove.prevent.stop
- 事件修饰符
```
<!-- 阻止单击事件冒泡 -->
<a v-on:click.stop="doThis"></a>
<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>
<!-- 修饰符可以串联  -->
<a v-on:click.stop.prevent="doThat"></a>
<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>
<!-- 添加事件侦听器时使用事件捕获模式 -->
<div v-on:click.capture="doThis">...</div>
<!-- 只当事件在该元素本身（比如不是子元素）触发时触发回调 -->
<div v-on:click.self="doThat">...</div>
```
指定已创建的实例之父实例，在两者之间建立父子关系。子实例可以用 this.$parent 访问父实例，子实例被推入父实例的 $children 数组中。

```
同时使用 $parent 和 $children 有冲突 - 他们作为同一个入口 。更推荐用 props 和
events 实现父子组件通信
```
# props

要让子组件使用父组件的数据，我们需要通过子组件的 props 选项。

子组件通知父组件来进行操作，需要使用this.$emit('function',a,b)

父组件数据如果动态改变，子组件如果接受的是一个object类型的数据，父组件就需要使
用this.$set(object,'参数','new参数')来进行修改

#####  export default PvTrack es6模块化抛出

## watch 监听数据变化

```
watch: {
    a: function (val, oldVal) {
      console.log('new: %s, old: %s', val, oldVal)
    },
    // 方法名
    b: 'someMethod',
    // 深度 watcher
    c: {
      handler: function (val, oldVal) { /* ... */ },
      deep: true
    }
  }
```
# 兼容性处理

项目中发现，在安卓4.3及以下的手机不支持axios的使用，主要就是无法使用promise。加上以下polyfill就可以了。

项目中安装es6-promise


```
cnpm install es6-promise --save-dev
```


在axios.min.js开头和调用axios的时候加上


```
require('es6-promise').polyfill();
```
## 遇到的问题

vue 模块化引用外部js的时候 因为vue会默认开启es6的严格模式，所以外部js不能随便使用this 因为严格模式下，this的值为undefined，所以"!this"为true。
```
this.$router.go(0) 可以刷新页面 vue-router
```