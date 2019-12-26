#### 1、vue基础要点

(1).MvvM->model/view/viewmodel
 ViewModel层封装了状态和行为
 Model层中只封装了状态
 View层中主要由css和html构成，为了更好的展示model好viewmodel中的数据有很多前端框架
如vue、freemark等
 View展示的是viewmodel中的数据(而非model层中数据)，实现了view和model的解耦
(2).双向绑定
 从View侧看，ViewModel中的DOM Listeners工具会帮我们监测页面上DOM元素的变化，如果
有变化，则更改Model中的数据；从Model侧看，当我们更新Model中的数据时，Data Bindings
工具会帮我们更新页面中的DOM元素。
(3).
 ①ViewModel是Vue.js的核心，它是一个Vue实例（new vue({el:" ",data:" "})）
②Vue实例的data属性指向exampleData，它是一个引用类型，改变了exampleData对象的属
性，同时也会影响Vue实例的data属性。
(4).
 ①Vue.js的指令是以v-开头的,它们作用于HTML元素,html元素上绑定指令如:

```html
  <h1 v-if="true">Yes</h1> <!-- 将会在页面显示‘Yes’字样 -->
```

②Ⅰ、常用指令v-show/v-if 区别是v-show会渲染该元素,同时给元素设置简单css样式如display
    Ⅱ、v-else 必须紧跟在v-show/v-if之后,会不会渲染到HTML取决于前面是v-show还是v-if
    Ⅲ、v-for="item in items" items为集合，item为临时变量类,似于c#foreach,如item为10
   则遍历时item从0开始，然后遍历到items –1结束
    Ⅳ、v-bind:argument="expression"（缩写 :argument="expression"） argument为html属性如：class

```html
<a href="#" v-bind:class="activeNumber == n + 1 ? 'active' : ''">{{ n + 1 }}</a>
 <script>  
 	var vm = new Vue({
            el: '#app',
            data: {
                activeNumber: 1,
                pageCount: 10
            }
        })
 </script>
```

  v-bind指令可以缩写为一个冒号，v-on指令可以缩写为@符号
    Ⅴ、v-on:（缩写 @） 给html元素添加监听事件,如

```html
<button v-on:click="greet">Greet</button>
<script>
	var vm = new Vue({
            el: '#app',
            data: {
                message: 'Hello, Vue.js!'
            },
            methods: {
                greet: function() {
                    //方法内 `this` 指向 vm实例
                    alert(this.message)
                },
                say: function(msg) {
                    alert(msg)
                }
            }
        })
</script>
<!--当然，也可以添加内嵌js代码,如--><button v-on:click="say('Hi')">Hi</button>
```

​    Ⅵ、Vue.js有多种数据绑定的语法，最基础的形式是文本插值，使用一对大括号语法，在运行时
​    {{ message }}会被数据对象的message属性替换
​      v-model="vue中data中属性名" 实现双向绑定，例:

```html
<p>{{ message }}</p>   <input type="text" v-model="message"/>
```

(5).我们可以使用 methods 来替代 computed，效果上两个都是一样的，但是 computed 是基于它的
依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数
总会重新调用执行;性能上computed更好，但不想用缓存就用methods。
  ①computed中属性默认只有get方法，但可以显示写出set方法
6.事件@,组件,表单

#### 4、拓展

vue-cli:脚手架
npm install -g vue-cli //安装
vue init webpack firstApp;//当前目录下创建一个基于Webpack模板的新项目
npm install; //需先进入项目,此过程为“安装项目依赖
	//安装后，会在项目中多出一个node_modules文件夹
npm run dev;//运行项目