# 声明式渲染
Vue.js 的核心是一个允许采用简洁的模板语法来声明式地将数据渲染进 DOM 的系统：

    <div id="app">
      {{ message }}
    </div>
    var app = new Vue({
      el: '#app',
      data: {
        message: 'Hello Vue!'
      }
    })

### v-bind修改属性   可以简写成:title
    <div id="app-2">
      <span v-bind:title="message">
        鼠标悬停几秒钟查看此处动态绑定的提示信息！
      </span>
    </div>
    var app2 = new Vue({
      el: '#app-2',
      data: {
        message: '页面加载于 ' + new Date().toLocaleString()
      }
    })

# 条件与循环
控制切换一个元素是否显示也相当简单：

    <div id="app-3">
      <p v-if="seen">现在你看到我了</p>
    </div>
    var app3 = new Vue({
      el: '#app-3',
      data: {
        seen: true
      }
    })




v-if在true时会删除dom节点，v-show和v-if有一样的效果，v-show不会删除节点

v-for 指令可以绑定数组的数据来渲染一个项目列表：每次循环todos，将获取的变量放在todo变量里去

    <div id="app-4">
      <ol>
        <li v-for="todo in todos">
          {{ todo.text }}
        </li>
      </ol>
    </div>
    var app4 = new Vue({
      el: '#app-4',
      data: {
        todos: [
          { text: '学习 JavaScript' },
          { text: '学习 Vue' },
          { text: '整个牛项目' }
        ]
      }
    })


为了让用户和你的应用进行交互，我们可以用 v-on 指令添加一个事件监听器，通过它调用在 Vue 实例中定义的方法： v-on：click可以用@click来代替

    <div id="app-5">
      <p>{{ message }}</p>
      <button v-on:click="reverseMessage">逆转消息</button>
    </div>
    var app5 = new Vue({
      el: '#app-5',
      data: {
        message: 'Hello Vue.js!'
      },
      methods: {
        reverseMessage: function () {
          this.message = this.message.split('').reverse().join('')
        }
      }
    })


Vue 还提供了 v-model 指令，它能轻松实现表单输入和应用状态之间的双向绑定。属性双向绑定

    <div id="app-6">
      <p>{{ message }}</p>
      <input v-model="message">
    </div>
    var app6 = new Vue({
      el: '#app-6',
      data: {
        message: 'Hello Vue!'
      }
    })
    Hello Vue!

# 定义全局组件
定义名为 todo-item 的新组件

    Vue.component('todo-item', {
      template: '<li>这是个待办项</li>'
    })
    
Prop可以使子组件接受父组件的属性

    Vue.component('todo-item', {
      // todo-item 组件现在接受一个
      // "prop"，类似于一个自定义特性。
      // 这个 prop 名为 todo。
      props: ['todo'],   
      template: '<li>{{ todo.text }}</li>'
    })
每一个vue组件就是一个vue的实例

创建vue实例：

New vue（）

Object.freeze(obj)可以阻止修改属性

# 插值

    <span>Message: {{ msg }}</span>

只要msg属性改变，插值的内容就会改变

    <span v-once>这个将不会改变: {{ msg }}</span>

加上v-once，是一次性插入

双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用 v-html 指令：

    <p>Using mustaches: {{ rawHtml }}</p>
    <p>Using v-html directive: <span v-html="rawHtml"></span></p>


# 动态参数


    <a v-bind:[attributeName]="url"> ... </a>

这里的 attributeName 会被作为一个 JavaScript 表达式进行动态求值，求得的值将会作为最终的参数来使用。例如，如果你的 Vue 实例有一个 data 属性 attributeName，其值为 "href"，那么这个绑定将等价于 v-bind:href。


# 计算属性  computed

    <div id="example">
      <p>Original message: "{{ message }}"</p>
      <p>Computed reversed message: "{{ reversedMessage }}"</p>
    </div>
    var vm = new Vue({
      el: '#example',
      data: {
        message: 'Hello'
      },
      computed: {
        // 计算属性的 getter
        reversedMessage: function () {
          // `this` 指向 vm 实例
          return this.message.split('').reverse().join('')
        }
      }
    })


计算属性默认只有 getter ，不过在需要时你也可以提供一个 setter ：

    computed: {
      fullName: {
        // getter
        get: function () {
          return this.firstName + ' ' + this.lastName
        },
        // setter
        set: function (newValue) {
          var names = newValue.split(' ')
          this.firstName = names[0]
          this.lastName = names[names.length - 1]
        }
      }
    }


# 事件修饰符

.stop  阻止冒泡

.prevent  阻止默认事件  如a的跳转事件

.captrue  添加事件侦听器时使用事件捕获模式 
捕获就是冒泡的相反

.self  只当事件在该元素本身（比如不是子元素）触发时触发回调  可以阻止自身冒泡，不影响其他元素

.once   事件只触发一次

eval解析一段字符串并返回结果

    var str = “2” + “*” + “3”;
    var result = eval(str)    //结果是6

通过属性绑定为元素设定class
:class=[“类名”,”类名”]
:class=[{“类名”:对象值}]

# 全局过滤器

    Vue.fliter(“过滤器名称”,function(“调用过滤器的值”,”参数”){
    })

调用过滤器的方法：值 | 过滤器名称（”参数”），可以同时调用多个过滤器
 

# 自定义全局按键修饰符

@keyup 可以监听键盘

Keyup可以点一个按键，可以使用官方已给出的按键名，如enter。

也可以自己定义，如

    Vue.config.keyCodes.f2 = 113

113是官方定义的按键码，可以查文档

# 定义全局指令

如定义v-focus

参数1：指令的名称，不需要加v-前缀

参数2：一个对象，在这个对象身上，有一些指令相关的函数，可以在特定阶段执行相关的操作。

钩子函数：

    Vue.directive(“focus”,{
    	Bind:function(el){
        }//第一个参数永远是el，表示被绑定的元素
    })

Bind表示指令绑定到元素上的时候，会立即执行这个bind函数，只执行一次

Inserted:inserter表示元素插入到DOM中的时候，会执行inserted函数，执行一次

Updated: 当Vnode更新的时候，会执行updated，可能多次触发。

和js有关的操作最好绑定在inserted中，和css有关的最好绑定在bind中

# 生命周期函数
 
### beforeCreate
实例完全被创建出来之前执行。Data和methods中的数据都还未初始化

### created   
data和methods已初始化，这是最早能调用到data和methods的函数

### beforeMount

模板已经编译完成，但是还没有渲染在页面上，只是进入到了内存。

### mounted

表示内存中的模板已经真实的挂载在页面中。Mounted是实例创建期间最后一个生命周期函数，执行完后表示vue已经被完全创建好了。如果没有后续操作，则该实例在内存中。如果要通过某些插件操作dom，最早要在mounted中执行。

接着进入运行阶段的生命周期函数

### beforeUpdate和updated

只有在data数据改变时才会触发

### beforeUpdate 

data数据已经更新，但界面还未更新

### updated  

data和页面都已经更新为最新的。

最后销毁阶段

### beforeDestroy 

vue实例已经从运行阶段进入到了销毁阶段，实例身上所有的data、methods等都处于可用状态，还没有真正执行销毁。

### Destroyed  

组件已经被完全销毁。

Vue的get请求

引入vue-resource.js文件

    this.$http.get(“url”).then(function(result){
    })    数据为result.body

    This.$http.post(“url”,{发送的数据},{一些属性}).then(function(result){
    }) 

一般用post发送第三个参数填写{emulateJSON:true}   设置提交的内容类型为普通表单数据格式，可以避免一些错误

    This.$http.jsonp(“url”).then(function(result){
    })


为什么要用jsonp发起请求？
由于浏览器的安全性限制，不允许AJAX访问协议不同、域名不同、端口号不同的数据接口（跨域）

# Vue动画

v-enter，v-leave-to可以写为同一样式

v-enter-to，v-leave同样

对使用动画的元素用<transition>标签包裹，如果你使用一个没有名字的 <transition>，则 v-
是这些类名的默认前缀。如果你使用了

    <transition name="my-transition">

那么 v-enter 会替换为 my-transition-enter。

使用第三方animate.css

引入animate.css后，以下为使用例子，也可以写在transition内

    <h1 class="animated infinite bounce delay-2s">Example</h1>

但使用以上两种方法都无法实现半场动画，需要使用动画的生命周期函数实现。
 
每个函数都有一个el参数。

特别注意：如果要实现动画，必须加上el.offsetWidth这句话，这句话没有实际作用，可以认为是强制刷新动画，
 
当只用 JavaScript 过渡的时候，在 enter 和 leave 中必须使用==done==进行回调。否则，它们将被同步调用，过渡会立即完成。

在使用列表过渡的时候，如果需要过渡的元素是通过v-for循环渲染出来的，不能使用transition，需要使用==transition-Group==

而给v-for循环的元素设置动画需要设置：==key==属性

做删除动画时，需要使用
 
==v-move==表示位移时候的动画，而==v-leave-active==绝对定位是为了在删除一项时后面的项能往上实现动画。

给transitiongroup添加appear属性，实现页面刚展示出来入场时候的效果

Transitiongroup会在页面在渲染为一个span元素，这样的设定并不好，因此可以用==tag==属性指定transitiongroup渲染为一个指定元素。如

    tag=“ul”

# 创建全局组件

    Var com1 = Vue.extend({    //这是一个组件对象
    })
    第一种写法：Vue component(“组件名”,”组件对象”)
    第二种写法：Vue component(“组件名”,{
    })
    第三种写法：Vue component(“组件名”,{
    Template:”#id”
    })   

然后在挂载元素外部用template标签并给出id

# 定义私有组件

在Vue实例内用components{}

组件内可以有data，但是必须是一个function，而且必须返回一个对象。为什么必须是一个函数呢？因为每个实例可以维护一份被返回对象的独立的拷贝，不会影响其他Vue实例的对象。

### 使用组件实现切换功能

Vue提供了component标签，来展示对应名称的组件

    <component    :is:”’组件名’”> </component>

### 组件动画

直接用==transition==包裹component标签，不需要写key，同时组件的动画提供了一个属性mode，设置进出的模式，如mode=”out-in”  先出后进

父组件向子组件传值，在子组件中自定义属性，属性的值为父组件data值就行，然后子组件用props接受自定义的属性，接受的值只可读。

父组件向子组件传方法，@自定义名称=“父组件的方法”   然后在子组件内的methods用==this.$emit==(“自定义名称”)   也可以向父组件传参，（“名称”，参数）

### 用ref获取dom元素和组件

给标签写上ref=“名称”

在vue实例内部用时，用this.$refs.名称


# 创建路由对象，VueRouter
 

    <html>
    <div id="app">
    	<router-view></router-view>
    </div>
    <script>
    	var login = {
    		template:'<h1>登陆组件</h1>'
    	}
    	var register = {
    		template:'<h1>注册组件</h1>'
    	}
    		// 创建路由组件
    	var routerobj = new VueRouter({
    		routes:[
    			{path:'/login',component:login},
    			{path:'/register',component:register}
    		]
    	})
    	var vm = new Vue({
    		el:"#app",
    		data:{
    		},
    		methods:{
    		},
    		router:routerobj
    	})
    </script>


使用a标签切换路由，href=”#login”
也可以用router-link标签

有时候进入页面需要指定默认的页面，则可以用重定向
在routes数组里面，{path:’/’,redirect:’/login’}   redirect是重定向的意思

在使用router-link时，会附加一个class router-link-active
在配置路由时可以对其进行更改，使用linkActiveClass

 
可以使用this.$routerobj.query来获取参数

### 第二种获取参数的方法
 
在path后面用/:id的方式设置将来login路径后面应当存放一个参数
 
可以使用this.$routerobj.params

路由的嵌套
 

路由匹配多个组件
 
在router-view内要设置name属性，default为默认
