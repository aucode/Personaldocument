### Vue的基本认识  [`声明式编程`](https://baike.baidu.com/item/%E5%A3%B0%E6%98%8E%E5%BC%8F%E7%BC%96%E7%A8%8B/9939512?fr=aladdin)
> 是一个渐进式`javascript框架`<br/>
即：需要什么功能就添加什么插件

- 官网
    + [`英文官网`](https://vuejs.org/)
    + [`中文官网`](https://cn.vuejs.org/) 
  
- 作者 
    > 尤雨溪
- Vue库 
    > 核心库、以及相关插件 

    + 核心库 
        > 小、能实现基本功能。

    + 相关插件&nbsp;[`Vue扩展插件`](https://blog.csdn.net/qq193423571/article/details/90201303) 
        > 需要某一个功能时添加相应功能的插件 

        + vue-cli 
            > vue 脚手架：`脚手架`是为了保证各施工过程顺利进行而搭设的工作平台<br/>
            即`vue-cli是一个工作平台` 
            
        + vue-resource`常用axios`
            > ajax请求 
        + vue-router 
            > 路由 
            
        + vuex
            > 状态管理
            
        + vue-lazyload
            > 图片赖加载
            
        + vue-scroller
            > 页面滑动相关`实现页面滑动`
            
        + mint-ui
            > 基于vue的UI组件库（移动端）
            
        + element-ui
            > 基于vue的UI组件库（PC端） 
            
- [`Vue教程`](https://cn.vuejs.org/v2/guide/)

### Vue生命周期
![enter image description here](https://cn.vuejs.org/images/lifecycle.png)

### Vue的特点 
- 资循MVVM模式 
```
        MVVM：
			M：数据部分（model） 
			V：选择器里的内容（html标签内容）（view）
			VM：new出来的实例（viewModel） 

```

- 编码简洁、体积小、运行效率高，适合移动/PC端开发
- 关注UI，可以轻松引入vue插件或其他第三方库开发项目
- 借鉴angular 的模板和数据绑定技术
- 借鉴react 的组件化和虚拟DOM技术 

### Vue 安装
- 安装
    + vue 方法一[`安装`](https://learning.dcloud.io/#/?vid=1)
        + 通过`script`标签引用vue.js，[`点击下载`](https://cn.vuejs.org/v2/guide/installation.html)，选择[`开发版本`](https://cn.vuejs.org/js/vue.js)（开发时使用）或[`生产版本`](https://cn.vuejs.org/js/vue.min.js) ，与JavaScript一样在`script`里写代码
        + CDN引用vue.js
            > 在用 Vue 构建大型应用时推荐使用 NPM 安装 
            
```
    // 1)引用vue   在html文件用script标签添加引用
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script> 
    //在控制台提示以下，则成功
    Download the Vue Devtools extension for a better development experience:
    https://github.com/vuejs/vue-devtools

    You are running Vue in development mode.
    Make sure to turn on production mode when deploying for production.
    See more tips at https://vuejs.org/guide/deployment.html
    //2) CDN引用vue.js 在html文件用script标签添加引用
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>

```

- vue 安装方法二 `命令行工具 (CLI)`
    + vue安装脚手架[`命令行安装`](https://www.vuemastery.com/courses/real-world-vue-js/vue-cli/) 
    + 前提安装[`Node.js`](https://nodejs.org/en/)
    + 可以使用下列任一命令安装
```
npm install -g @vue/cli
# OR
yarn global add @vue/cli
#检查其版本是否正确
vue --version
```

+ `vue ui` 命令启动

### Vue语法 
- 基础语法 
```
<script>
        //插件vue实例
		const vm=new Vue({ //配置对象
			el:'#app', //element：选择器（决定Vue会管理的DOM）类型：string | HTMLElement
			data:{ //数据（model）类型：Object | Function（组件当中的data必须是一个函数）
				massage:'Hello Vue'
			},
			methods: {//定义方法（s）类型：{[key：string]：Function}
				add: function(){
					console.log('定义方法一'); 
				},
				sub: function(){
					console.log('定义方法二'); 

				}
			}
		});
</script>

```


- 常用命令 [`API`](https://cn.vuejs.org/v2/api/) 
+ v-text、mustache语法（大括号）：显示数据 
    > 更新元素的 textContent。如果要更新部分的 textContent ，需要使用 `{{ string }}` 插值。`注意`：v-text 会覆盖原来的文本。

```
    <span v-text="msg"></span>
    // 和下面的效果一样 
    <span>{{msg}}</span> //使用v-text指令的另一种使用方式 
    <span>{{msg + lasmsg}}</span>  
    <span>{{msg + ' ' + lasmsg}}</span>  
    <span>{{msg}} {{lasmsg}}</span>  

```

+ v-html：把字符串解析为html代码 
    > 更新元素的 `innerHTML` 。**注意**：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译 。如果试图使用 v-html 组合模板，可以重新考虑是否通过使用组件来替代。<br/>
     **警告**：在网站上动态渲染任意 HTML 是非常危险的，因为容易导致 XSS 攻击。只在可信内容上使用 v-html，`永不用在用户提交的内容上`。

+ v-show：条件渲染 `（以 display:none 的形式隐藏 ：切换频率高使用）`
    > 根据表达式之真假值，切换元素的 display CSS 属性。指令触发`过渡效果`。**注意**：v-show 不支持 `<template>` 元素，也不支持 `v-else`。

+ v-if：条件渲染 `（直接删除 ：切换频率低使用）` 
    > 根据表达式的值的真假条件渲染元素。在切换时元素及它的数据绑定 / 组件被销毁并重建。如果元素是` <template> `，将提出它的`内容作为条件块`。

+ v-else、v-else-if：条件渲染 
    > 前一兄弟元素必须有 v-if 或 v-else-if。
```
    //v-if和v-else指令使用
    <div v-if="表达式">
        Now you see me
    </div>
    <div v-else>
        Now you don't
    </div>

```

+ v-for 
```
    <div v-for="(item, index) in items"></div>
    <div v-for="(val, key) in object"></div>
    <div v-for="(val, name, index) in object"></div>
```

+ v-on：缩写=> `@` 
    > [`查看文档`](https://cn.vuejs.org/v2/api/#v-on) 

+ v-on 修饰符 阻止事件冒泡
    > <button @click.stop="btnClick(123,$event)"></button>

+ v-bind：动态绑定标签属性  缩写=> `:` 
    > [`查看文档`](https://cn.vuejs.org/v2/api/#v-bind)
```
    <img v-bind:src="属性名" alt="">
    <img :src="属性名" alt="">
    //动态绑定class（对象语法） 
    <h2 v-bind:class="{类名1: boolean,类名2：boolean}"></h2>//当boolean值为true类名添加到h2上，否则不添加

```


+ v-slot: 缩写=> `#` 
    > [`查看文档`](https://cn.vuejs.org/v2/api/#v-slot)

+ v-model：双向数据绑定 
    > `v-model="message"` ==>相当与（原理） `v-bind:value="message" v-on:input="message = $event.target.value"` 的结合

+ v-model 表单绑定（与表单使用）
```
    <input v-model="message" placeholder="edit me">
    <p>Message is: {{ message }}</p>
    //v-model 表单绑定（与表单使用）

```

+ v-model 修饰符 
```
    //1.修饰符 lazy 按回车键才绑定
    <input type="text" v-model.lazy="message" > 
    //2.修饰符 number  绑定的值是数字； type="number" 只能输入数字
    <input type="number" v-model.number="message" > 
    //3.修饰符 trim  去除两边的空格；
    <input type="number" v-model.trim="message" > 


```


+ v-pre：不解析语法当前 
    > 跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。
```
    <span v-pre>{{ this will not be compiled }}</span>
```

+ v-cloak：
    > 这个指令保持在元素上直到关联实例结束编译。和 CSS 规则如 `[v-cloak] { display: none }` 一起用时，这个指令可以`隐藏未编译`的 `Mustache` 标签直到实例准备完毕。
```
    //css样式
    [v-cloak] {
    display: none;
    }
    //代码
    <div v-cloak>
    {{ message }}
    </div>
```

+ v-once：
    > 只渲染元素和组件一次。当变量发生改变不更新。 
```
    <h2 v-once:>{{msg}}</h2>
```

### 计算属性`computed` 
> 复杂逻辑的处理、有缓存的，如果多次使用计算属性只会调用一次，个人理解： `相当与属性和方法的结合`

```
computed: {//计算属性 复杂逻辑的处理   使用方法和属性一样
				cupName(属性): function(){//拼接属性
					return this.firstComputed + '  ' + this.lastComputed;
				},
				totalPrice(属性): function(){//总价格
					let result = 0;
					for (let i=0;this.books.length;i++){
						result +=this.books[i].price;
					}
					return result;
				}
			},

```

+ setter 和 getter 
    > 每一个属性都有一个`setter(设置)`和`getter(读取)` 一般情况只需实现`get方法`，`set方法`一般不用，当没有set方法则是只读属性。

```
computed: {
    //计算属性完成写法 
    fullName: {
        set: function(){

        },
        get: function(){
            return 'acb'
        }
    }
}
    //
    //使用写法 二 只写get方法
    fullName: {
        get: function(){
            return 'acb'
        }
    }
    // 等于 ===>
    fullName: function(){
            return 'acb'
        }
    //使用计算属性
    <p>{{fullName}}</p>// => 输出 abc


```
+ 计算属性和methods的对比 `（计算属性和缓存）` 
    > 方法`methods`调用一次执行一次，计算属性  `computed` 运行一次多次使用 原因`缓存`


### 事件监听 `主要用： v-on`
+ 获取event对象`$event ` 
```
//代码案例 手动获取到浏览器参数的event对象
<button @click="btnClick(123,$event)"></button>
```
+ v-on 修饰符 
> `@click.stop`阻止事件冒泡 `@click.enter`回车键 `@click.prevent`阻止默认事件 `@click.native`监听自定义组件事件  `@click.once`只触发一次回调 


```
//事件冒泡   （点击内层外层也会执行）点击按钮会执行divClick、btnClick两个点击事件 在js中用event对象阻止
<div @click="divClick">
<button @click="btnClick">按钮</button>
</div>
//v-on 修饰符 阻止事件冒泡
<div @click="divClick">
<button @click.stop="btnClick">按钮</button>
</div>

```

+ 监听键盘事件`keydown点下去` `keyup点击事件` 

### 组件 `components,Vue.extend()`
- 注册组件（有作用域）
    + 创建组件构造器 `Vue.extend()`
    + 注册组件 `components`
        > 全局注册、局部注册

    + 使用组件  
```
    //注册组件步骤
    //1.Vue.extend() 插件组件构造器对象
    const cpnC = vue.extend({
        template: `
        <div>
            <h2>我是标题</h2>
            <p>我是内容，哈哈</p>
            <p>我是内容，呵呵</p>
        </div>`
    });
    //2.Vue.component(组件标签名，组件构造器) 注册组件（全局组件）
    Vue.component('my-cpn',cpnC)
    //局部组件
    components： {
        my-cpn: cpnC
    }
    //3.Vue在实例的作用范围内使用组件
    <div id="app">
        <my-cpn></my-cpn>
    <div>

```

- 注册组件 `语法糖注册`
```
//方法一开始
    //全局组件
    Vue.component('my-cpn',{
        template: `
        <div>
            <h2>我是标题</h2>
            <p>我是内容，哈哈</p>
            <p>我是内容，呵呵</p>
        </div>`
    });
    //Vue实例  局部组件
    const app = new Vue({
        el: '#app',
        data: {
            message: '组件',
        },
        components: {//在Vue实例里注册组件
            cpn2: {
                template: `
                    <div>
                        <h2>我是标题</h2>
                        <p>我是内容，哈哈</p>
                        <p>我是内容，呵呵</p>
                    </div>`
                }
        }
    });

```

- 注册组件 `模板分离`
```
//方法一
<script type="text/x-template" id="cpn">
    <div>
        <h2>模板分离方法一</h2>
        <p>我是内容，哈哈</p>
        <p>我是内容，呵呵</p>
    </div>

</script>

    //Vue实例
    const app = new Vue({
        el: '#app',
        data: {
            message: '组件',
        },
        components: {//在Vue实例里注册组件
            cpn: {
                template: '#cpn'
            }
        }
    });

//方法二
    <template id="cpn">
        <div>
            <h2>模板分离方法二</h2>
            <p>我是内容，哈哈</p>
            <p>我是内容，呵呵</p>
        </div>
    </template>
    Vue.component('my-cpn',{
        template: '#cpn'
    })

```


- 父组件和子组件 
```
    //第一个组件构造器（子组件）
    const cpnC1 = vue.extend({
        template: `
        <div>
            <h2>第一个组件构造器</h2>
            <p>我是内容，呵呵</p>
            <p>我是内容，呵呵</p>
        </div>`
    });
    //第二个组件构造器（父组件）
    const cpnC2 = vue.extend({
        template: `
        <div>
            <h2>第二个组件构造器</h2>
            <p>我是内容，哈哈</p>
            <p>我是内容，哈哈</p>
            <cpn1></cpn1>
        </div>`,
        components: {//在组件构造器里注册组件  可以在该构造器使用注册的组件
            cpn1: cpnC1
        }
    });
    //Vue实例
    const app = new Vue({
        el: '#app',
        data: {
            message: '组件',
        },
        components: {//在Vue实例里注册组件
            cpn2: cpnC2
        }
    });
    // Vue实例（Root）-->第二个组件构造器（父组件）-->第一个组件构造器（子组件）
    // Vue实例里注册第二个组件构造器里注册第一个组件构造器

```

- 父组件子组件通信
    > 父组件通过`props`向子组件传递数据 **注意：**`用v-bind传值目前不支持驼峰、props属性 一定通过父组件属性进行修改、props不能用v-model`<br/>



```
    <div id="app">
        //(2)父传子
        <cpn :cmovies="movies" ></cpn>
    </div>


    //创建模板
    <template id="cpn">
        <div>
            <!-- 显示父组件传过来的值 -->
            {{cmovies}}
        </div>
    </template>
    //插件组件构造器（子）
    const cpn = {
        template: '#cpn',//引用模板
        propos: {  //(3)父传子 
            //1.可以限制类型
            cmovies: String,
            //2.提供默认值、required必须传该值
            cmovies: {
                type: String,
                default: '设置默认值',
                required: true
            },
            cmovies: {//类型是对象或数组是，默认值必须是函数
                type: Array,
                default(){
                    return []
                },
                //自定义验证函数
                validator: function(value){
                    return /^[0-9]{11}$/.test(val)
                }
            }
        }   
    }
 
    //root（父）
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            movies: ['海王'，'海贼王','海尔兄弟']//(1)父传子
        },
        components: {//注册组件
            cpn
        }
    });

```

    > 子组件通过 自定义事件`$emit`向父组件传递数据 

```
    <div id="app">
        //(2)子传父 父组件通过v-on监听子组件发送的事件
        <cpn :cmovies="movies" @:itemclick="cpnClick"></cpn>
    </div>


    //创建模板
    <template id="cpn">
        <div>
            <button v-for="item in categories" @click="btnClick(item)">
                {{item.name}}
            </button>
        </div>
    </template>

    //插件组件构造器（子）
    const cpn = {
        template: '#cpn',//引用模板
        data() {
            categories: [
                {id: 0, name: '热门推荐'},
                {id: 1, name: '手机数码'},
                {id: 2, name: '家用电器'},
                {id: 3, name: '电脑办公'}
            ]
        },
        method: {
            btnClick(item) {
                //(1)子传父 发送一个事件(自定义类型  itemclick)
                this.$emit('itemclick',item);
            }
        }
          
    }
 
    //root（父）
    const app = new Vue({
        el: '#app',
        data: {
            message: '你好啊',
            movies: ['海王'，'海贼王','海尔兄弟']
        },
        components: {//注册组件
            cpn
        },
        methods: {//(3)子传父 
            cpnClick(item) {
                console.log(item)
            }
        }
    });


```

















