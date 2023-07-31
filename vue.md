# vue

## 资源

官网：[简介 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/introduction.html#the-progressive-framework)

b站：[137_尚硅谷Vue3技术_使用vue-cli创建工程_哔哩哔哩_bilibili](https://www.bilibili.com/video/BV1Zy4y1K7SH?p=137&spm_id_from=pageDriver&vd_source=3df462645cc83041f18d2afe8280f7ee)

菜鸟教程：[[Vue3 安装 | 菜鸟教程 (runoob.com)](https://www.runoob.com/vue3/vue3-install.html)](https://www.yuque.com/cessstudy/kak11d)

## 笔记

## vue简介

### 前置工作

**1.给浏览器安装脚本Vue Devtools插件**

**2.标签引入vue包**

### vue案例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>


<div id="app">  000 {{ message }}</div>
<script>
    const { createApp } = Vue

    createApp({
        data() {
            return {
            message: 'Hello Vue!'
        }
        }
    }).mount('#app')
</script>
</body>
</html>
```

>  一个容器对应一个实例

### vue特点

1.遵循MVVM模式
2.编码简洁，体积小，运行效率高，适合移动/PC端开发
3.它本身只关注UI，可以引入其它第三方库开发项目
4.采用组件化模式，提高代码复用率，目让代码更好维护

## **Vue核心 模板语法 数据绑定**

### 模板语法

- `v-bind` :单向绑定解析表达式，可简写为 `:xxx`
- `v-model` :双向数据绑定
- `v-for` :遍历数组/对象/字符串
- `v-on` :绑定事件监听，可简写为 `@`
- `v-if` :条件渲染（动态控制节点是否存在）
- `v-else` :条件渲染（动态控制节点是否存在）
- `v-show`:条件渲染（动态控制节点是否展示）

#### 插值语法

```html
{{xxx}}

<div id="app">  000 {{ message }}</div>
<script>
    const { createApp } = Vue

    createApp({
        data() {
            return {
            message: 'Hello Vue!'
        }
        }
    }).mount('#app')
</script>

//输出
000 Hello Vue!
```



#### 指令语法

```html
// v-html 指令

<div id="example1" class="demo">
    <p>使用双大括号的文本插值: {{ rawHtml }}</p>
    <p>使用 v-html 指令: <span v-html="rawHtml"></span></p>
</div>

<script>
    const App = {
        data() {
            return {
                rawHtml: '<span style="color: red">这里会显示红色！</span>'
            }
        }
    }

    Vue.createApp(App).mount('#example1')
</script>
```

### 数据绑定

单向绑定：`v-bind`

双向绑定：`v-model`

> **v-model** 指令一般用在表单上
>
> 在、select、textarea、checkbox、radio 等表单控件元素上创建双向数据绑定，根据表单上的值，自动更新绑定的元素的值。



>  按钮的事件我们可以使用 v-on 监听，并对用户的输入进行响应。

```html
//v-bind 指令

<div id="app">
    <p><a v-bind:href="url">b站</a></p>
</div>
    
<script>
const app = {
  data() {
    return {
      url: 'https://www.bilibili.com/'
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>
```

```html
v-model

<div id="app">
    <p>{{ message }}</p>
    <input v-model="message">
</div>
 
<script>
const app = {
  data() {
    return {
      message: 'hello'
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>
```

```html
v-on

<div id="app">
    <p>{{ message }}</p>
    <button v-on:click="reverseMessage">反转字符串</button>
</div>
    
<script>
const app = {
  data() {
    return {
      message: 'Runoob!'
    }
  },
  methods: {
    reverseMessage() {
      this.message = this.message
        .split('')
        .reverse()
        .join('')
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>
```



`v-bind`简写语法

```html
<div :id="dynamicId"></div>

<div v-bind:id="dynamicId"></div>
```

`v-on`简写语法

```html
<a v-on:click="doSomething"></a>
<!-- 缩写 -->
<a @click="doSomething"></a>
```

### 条件语句

```html
v-if

<div id="app">
    <p v-if="seen">现在你看到我了</p>
</div>
    
<script>
const app = {
  data() {
    return {
      seen: true /* 改为false，信息就无法显示 */
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>

```

```html
v-else

<div id="app">
    <div v-if="Math.random() > 0.5">
      随机数大于 0.5
    </div>
    <div v-else>
      随机数小于等于 0.5
    </div>
</div>
    
<script>
Vue.createApp(app).mount('#app')
</script>
```

```html
v-for

<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.text }}
    </li>
  </ol>
</div>
<script>
const app = {
  data() {
    return {
      sites: [
        { text: 'Google' },
        { text: 'Runoob' },
        { text: 'Taobao' }
      ]
    }
  }
}

Vue.createApp(app).mount('#app')
</script>
```



## 响应式基础

### Vue3.0的响应式

- 实现原理:

  - 通过Proxy（代理）: 拦截对象中任意属性的变化, 包括：属性值的读写、属性的添加、属性的删除等。

  - 通过Reflect（反射）: 对源对象的属性进行操作。

  - MDN文档中描述的Proxy与Reflect：

    - Proxy：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy

    - Reflect：https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Reflect

      ```js
      new Proxy(data, {
          // 拦截读取属性值
          get (target, prop) {
              return Reflect.get(target, prop)
          },
          // 拦截设置属性值或添加新属性
          set (target, prop, value) {
              return Reflect.set(target, prop, value)
          },
          // 拦截删除属性
          deleteProperty (target, prop) {
              return Reflect.deleteProperty(target, prop)
          }
      })
      
      proxy.name = 'tom'   
      ```

### 响应式数据的判断

- isRef: 检查一个值是否为一个 ref 对象
- isReactive: 检查一个对象是否是由 `reactive` 创建的响应式代理
- isReadonly: 检查一个对象是否是由 `readonly` 创建的只读代理
- isProxy: 检查一个对象是否是由 `reactive` 或者 `readonly` 方法创建的代理

### 响应式状态

选用选项式 API 时，会用 `data` 选项来声明组件的响应式状态。此选项的值应为返回一个对象的函数。Vue 将在创建新组件实例的时候调用此函数，并将函数返回的对象用响应式系统进行包装。此对象的所有顶层属性都会被代理到组件实例 (即方法和生命周期钩子中的 `this`) 上。

```javascript
export default {
  data() {
    return {
      count: 1
    }
  },

  // `mounted` 是生命周期钩子，之后我们会讲到
  mounted() {
    // `this` 指向当前组件实例
    console.log(this.count) // => 1

    // 数据属性也可以被更改
    this.count = 2
  }
}
```

这些实例上的属性仅在实例首次创建时被添加，因此你需要确保它们都出现在 `data` 函数返回的对象上。若所需的值还未准备好，在必要时也可以使用 `null`、`undefined` 或者其他一些值占位。

虽然也可以不在 `data` 上定义，直接向组件实例添加新属性，但这个属性将无法触发响应式更新。

Vue 在组件实例上暴露的内置 API 使用 `$` 作为前缀。它同时也为内部属性保留 `_` 前缀。因此，你应该避免在顶层 `data` 上使用任何以这些字符作前缀的属性。

### 响应式代理 vs. 原始值

在 Vue 3 中，数据是基于 [JavaScript Proxy（代理）](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Proxy) 实现响应式的。使用过 Vue 2 的用户可能需要注意下面这样的边界情况：

js

```javascript
export default {
  data() {
    return {
      someObject: {}
    }
  },
  mounted() {
    const newObject = {}
    this.someObject = newObject

    console.log(newObject === this.someObject) // false
  }
}
```

当你在赋值后再访问 `this.someObject`，此值已经是原来的 `newObject` 的一个响应式代理。**与 Vue 2 不同的是，这里原始的 `newObject` 不会变为响应式：请确保始终通过 `this` 来访问响应式状态。**

### 声明方法

要为组件添加方法，我们需要用到 `methods` 选项。它应该是一个包含所有方法的对象：

js

```javascript
export default {
  data() {
    return {
      count: 0
    }
  },
  methods: {
    increment() {
      this.count++
    }
  },
  mounted() {
    // 在其他方法或是生命周期中也可以调用方法
    this.increment()
  }
}
```

Vue 自动为 `methods` 中的方法绑定了永远指向组件实例的 `this`。这确保了方法在作为事件监听器或回调函数时始终保持正确的 `this`。你不应该在定义 `methods` 时使用箭头函数，因为箭头函数没有自己的 `this` 上下文。

js

```javascript
export default {
  methods: {
    increment: () => {
      // 反例：无法访问此处的 `this`!
    }
  }
}
```

和组件实例上的其他属性一样，方法也可以在模板上被访问。在模板中它们常常被用作事件监听器：

template

```javascript
<button @click="increment">{{ count }}</button>
```

在上面的例子中，`increment` 方法会在 `<button>` 被点击时调用。

### 深层响应性

在 Vue 中，默认情况下，状态是深度响应的。这意味着当改变嵌套对象或数组时，这些变化也会被检测到：

js

```javascript
export default {
  data() {
    return {
      obj: {
        nested: { count: 0 },
        arr: ['foo', 'bar']
      }
    }
  },
  methods: {
    mutateDeeply() {
      // 以下都会按照期望工作
      this.obj.nested.count++
      this.obj.arr.push('baz')
    }
  }
}
```

### DOM 更新时机

当你修改了响应式状态时，DOM 会被自动更新。但是需要注意的是，DOM 更新不是同步的。Vue 会在“next tick”更新周期中缓冲所有状态的修改，以确保不管你进行了多少次状态修改，每个组件都只会被更新一次。

要等待 DOM 更新完成后再执行额外的代码，可以使用 [nextTick()](https://cn.vuejs.org/api/general.html#nexttick) 全局 API：

js

```javascript
import { nextTick } from 'vue'

export default {
  methods: {
    async increment() {
      this.count++
      await nextTick()
      // 现在 DOM 已经更新了
    }
  }
}
```

### 有状态方法

在某些情况下，我们可能需要动态地创建一个方法函数，比如创建一个预置防抖的事件处理器：

js

```javascript
import { debounce } from 'lodash-es'

export default {
  methods: {
    // 使用 Lodash 的防抖函数
    click: debounce(function () {
      // ... 对点击的响应 ...
    }, 500)
  }
}
```

不过这种方法对于被重用的组件来说是有问题的，因为这个预置防抖的函数是 **有状态的**：它在运行时维护着一个内部状态。如果多个组件实例都共享这同一个预置防抖的函数，那么它们之间将会互相影响。

要保持每个组件实例的防抖函数都彼此独立，我们可以改为在 `created` 生命周期钩子中创建这个预置防抖的函数：

js

```javascript
export default {
  created() {
    // 每个实例都有了自己的预置防抖的处理函数
    this.debouncedClick = _.debounce(this.click, 500)
  },
  unmounted() {
    // 最好是在组件卸载时
    // 清除掉防抖计时器
    this.debouncedClick.cancel()
  },
  methods: {
    click() {
      // ... 对点击的响应 ...
    }
  }
}
```

## 计算属性

实例

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>vue test</title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
</head>
<body>
<div id="app">
    <p>原始: {{ message }}</p>
    <p>计算后: {{ reversedMessage }}</p>
</div>

<script>
    const app = {
        data() {
            return {
                message: 'hello!!'
            }
        },
        computed: {
            // 计算属性的 getter
            reversedMessage: function () {
                // `this` 指向 vm 实例,即当前组件实例 
                return this.message.split('').reverse().join('')
            }
        }
    }

    Vue.createApp(app).mount('#app')
</script>

</body>
</html>
```

实例  中声明了一个计算属性 `reversedMessage` 。

提供的函数将用作属性 `vm.reversedMessage` 的 `getter` 。

`vm.reversedMessage` 依赖于 `vm.message`，在 `vm.message` 发生改变时，`vm.reversedMessage` 也会更新。



### computed vs methods

可以使用 `methods` 来替代 `computed`，效果上两个都是一样的

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Vue 测试</title>
    <script src="https://cdn.staticfile.org/vue/3.2.36/vue.global.min.js"></script>

</head>
<body>

<div id="app">
    <p>原始：{{message}}</p>
    <p>计算后  {{reversedMessage}}</p>
    <p>使用 methods {{ reversedMessage2() }}</p>
</div>

<script>
    const app = {
        data() {
            return {
                message:'Hello!'
            }
        },
        //
        computed: {
            reversedMessage :function (){
                return this.message.split('').reverse().join('')
            }
        },
        //
        methods: {
            reversedMessage2: function () {
                return this.message.split('').reverse().join('')
            }
        }
    }
    Vue.createApp(app).mount('#app')
    
</script>

</body>
</html>

结果

原始：Hello!

计算后 !olleH

使用 methods !olleH
```

 但是 computed 是基于它的依赖缓存，只有相关依赖发生改变时才会重新取值。而使用 methods ，在重新渲染的时候，函数总会重新调用执行。

>  即computed有缓存，method无缓存，每次调用都会重新计算。

### 可写计算属性

计算属性默认是只读的。当你尝试修改一个计算属性时，你会收到一个运行时警告。只在某些特殊场景中你可能才需要用到“可写”的属性，你可以通过同时提供 getter 和 setter 来创建：

```javascript
const app = {
    data() {
        return {
          firstName: 'John',
          lastName: 'Doe'
        }
      },
      computed: {
        fullName: {
          	// getter
          get() {
            return this.firstName + ' ' + this.lastName
          },
          	// setter
          set(newValue) {
            // 注意：我们这里使用的是解构赋值语法
            [this.firstName, this.lastName] = newValue.split(' ')
          }
        }
      }
}
```



现在再运行 `this.fullName = 'John Doe'` 时，setter 会被调用而 `this.firstName` 和 `this.lastName` 会随之更新。

## 类（class）与样式（style）绑定

class 与 style 是 HTML 元素的属性，用于设置元素的样式，我们可以用 v-bind 来设置样式属性。

v-bind 在处理 class 和 style 时， 表达式除了可以使用字符串之外，还可以是对象或数组。

**v-bind:class** 可以简写为 **:class**。

### 绑定样式

#### class属性绑定

*  写法`:class="xxx"`,xxx可以是字符串，数组，对象
*  `:style="[a,b]"`,其中a，b是样式对象
* `:style="{fontSize:xxx}"`,其中xxx是动态值

> 字符串写法适用于：类名不确定，要动态获取
>
> 数组写法适用于：要绑定多个样式，个数不确定，名字也不确定
>
> 对象写法适用于：要绑定多个样式，个数确定，名字也确定，但不确定用不用

实例中将 isActive 设置为 true 显示了一个绿色的 div 块，如果设置为 false 则不显示：

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>Vue 测试实例 </title>
    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
    <style>
        .active {
            width: 100px;
            height: 100px;
            background: green;
        }
    </style>
</head>
<body>
<div id="app">
    <div :class="{ 'active': isActive }">  </div>
</div>

<script>
    const app = {
        data() {
            return {
                isActive: true
            }
        }
    }

    Vue.createApp(app).mount('#app')
</script>
</body>
</html>
```

以在对象中写多个字段来操作多个 class

此外，**`:class`** 指令也可以与普通的 class 属性共存。

```html 
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">

    <script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>

    <style>
        .static{
            width: 1000px;
            height: 100px;
        }
        .active{
            background: aqua;
        }
        .text-danger{
            background: coral;
        }
    </style>
</head>

<body>
<div id="app">
    <div class="static" :class="{'active':isActive,'text-danger':hasError}"></div>
</div>

<script>
    const app={
        data() {
            return{
                isActive:true,
                hasError:false
            }
        }
    }
    Vue.createApp(app).mount('#app')
</script>
</body>
</html>
```

绑定一个返回对象的计算属性：

```html 
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">

<script src="https://unpkg.com/vue@3/dist/vue.global.js"></script>
<style>
.static {
	width: 100px;
	height: 100px;
}
.active {
	background: green;
}
.text-danger {
	background: red;
}
</style>
</head>
<body>
<div id="app">
    <div class="static" :class="classObject"></div>
</div>

<script>
const app = {
   data() {
      return {
         isActive: true,
         error: null
      }
   },
   computed: {
      classObject() {
         return {
            active: this.isActive && !this.error,
            'text-danger': this.error && this.error.type === 'fatal'
         }
      }
   }
}

Vue.createApp(app).mount('#app')
</script>
</body>
</html>
```

绑定数组

```html 
<div id="app">
    <div class="static" :class="[activeClass, errorClass]"></div>
</div>

<script>
const app = {
    data() {
        return {
            activeClass: 'active',
            errorClass: 'text-danger'
        }
    }
}

Vue.createApp(app).mount('#app')
</script>
```

### 在组件上使用

当你在带有单个根元素的自定义组件上使用 class 属性时，这些 class 将被添加到该元素中。此元素上的现有 class 将不会被覆盖。

```html
<div id="app">
    <runoob class="classC classD"></runoob>
</div>
 
<script>
// 创建一个Vue 应用
const app = Vue.createApp({})
 
// 定义一个名为 runoob的新全局组件
app.component('runoob', {
    template: '<h1 class="classA classB">I like runoob!</h1>'
})
 
app.mount('#app')
</script>
```

 **绑定内联样式**

在 **v-bind:style** 直接设置样式，可以简写为 **:style**：

```html
<div id="app">
    <div :style="{ color: activeColor, fontSize: fontSize + 'px' }"> hello </div>
</div>
```



## 条件渲染

v-if

* 写法 跟if else语法类似

* v-if="表达式“

  v-else-if="表达式”
  v-else="表达式”

  适用于：切换频率较低的场景，因为不展示的DOM元素直接被移除

  > 注意：v-if可以和v-else-if v-else一起使用，但要求结构不能被打断

v-show

* 写法:
  v-show=" 表达式”

* 适用于：切换频率较高的场景

* 特点：不展示的 DoM元素未被移除，仅仅是使用样式隐藏掉display:none

   `v-if`条件判断使用 v-if 指令，指令的表达式返回 true 时才会显示：

  > * 备注：使用 v-if的时，元素可能无法获取到，而使用v-show一定可以获取到template
  >   标签不影响结构，页面html中不会有此标签，但只能配合v-if，不能配合 v-show

```html 
<div id="app">
    <p v-if="seen">现在你看到我了</p>
</div>
    
<script>
const app = {
  data() {
    return {
      seen: true /* 改为false，信息就无法显示 */
    }
  }
}
 
Vue.createApp(app).mount('#app')
</script>

```

 `v-else` 为 `v-if` 添加一个“else 区块”。

```html 
<button @click="awesome = !awesome">Toggle</button>

<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

一个 `v-else` 元素必须跟在一个 `v-if` 或者 `v-else-if` 元素后面，否则它将不会被识别。

> v-else-if 即 v-if 的 else-if 块，可以链式的使用多次

## 列表渲染

`v-for`

```html
<li v-for="p in persons" :key="p.id">{{p.name}}</li>
```

```html
<li v-for="(p,index) in persons" :key="index">{{p.name}}</li>
```

### 循环语句

`v-for`

`v-for` 指令的值需要使用`item in items` 形式的特殊语法，其中 `items` 是源数据的数组，而 `item` 是迭代项的**别名**：

实例

```html
<div id="app">
  <ol>
    <li v-for="site in sites">
      {{ site.text }}
    </li>
  </ol>
</div>
<script>
const app = {
  data() {
    return {
      sites: [
        { text: 'Google' },
        { text: 'Runoob' },
        { text: 'Taobao' }
      ]
    }
  }
}

Vue.createApp(app).mount('#app')
</script>
```

> 你也可以使用 `v-for` 来遍历一个对象的所有属性。遍历的顺序会基于对该对象调用 `Object.keys()` 的返回值来决定。

 **在 `v-for` 里使用范围值**

`v-for` 可以直接接受一个整数值。在这种用例中，会将该模板基于 `1...n` 的取值范围重复多次。

template

```html
<span v-for="n in 10">{{ n }}</span>
```

注意此处 `n` 的初值是从 `1` 开始而非 `0`。

 **`<template>` 上的 `v-for`**

与模板上的 `v-if` 类似，你也可以在 `<template>` 标签上使用 `v-for` 来渲染一个包含多个元素的块。例如：

template

```javascript
<ul>
  <template v-for="item in items">
    <li>{{ item.msg }}</li>
    <li class="divider" role="presentation"></li>
  </template>
</ul>
```

### key原理

1.虚拟DoM中key的作用： key是虚拟DOM对象的标识，当状态中的数据发生变化时，Vue会根据【新数据】生成【新的虚拟DoM】， 随后Vue进行【新虚拟DoM】与【旧虚拟DOM】的差异比较，比较规则如下： 

2.对比规则： 

（1）.旧虚拟DOM中找到了与新虚拟DOM相同的key：

 o.若虚拟DOM中内容没变，直接使用之前的真实DOM！

 o.若虚拟DOM中内容变了，则生成新的真实DOM，随后替换掉页面中之前的真实DOm。 

（2）.旧虚拟DOM中未找到与新虚拟DOM相同的key 创建新的真实DOM，随后渲染到到页面。

3.用index作为key可能会引发的问题： 

1.若对数据进行：逆序添加、逆序删除等破坏顺序操作： 会产生没有必要的真实DOM更新==>界面效果没问题，但效率低。==

 2.如果结构中还包含输入类的DOM： 会产生错误DOM更新==>界面有问题。

 3.开发中如何选择key?： 1.最好使用每条数据的唯一标识作为key，比如id、手机号、身份证号、学号等唯一值。 2.如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的。

### 组件上使用v-for

我们可以直接在组件上使用 `v-for`，和在一般的元素上使用没有区别 (别忘记提供一个 `key`)：

template

```html
<MyComponent v-for="item in items" :key="item.id" />
```

但是，这不会自动将任何数据传递给组件，因为组件有自己独立的作用域。为了将迭代后的数据传递到组件中，我们还需要传递 props：

template

```html
<MyComponent
  v-for="(item, index) in items"
  :item="item"
  :index="index"
  :key="item.id"
/>
```

不自动将 `item` 注入组件的原因是，这会使组件与 `v-for` 的工作方式紧密耦合。明确其数据的来源可以使组件在其他情况下重用。

## 事件处理

### 监听事件

我们可以使用 `v-on` 指令 (简写为 `@`) 来监听 DOM 事件，并在事件触发时执行对应的 JavaScript。

**用法**：`v-on:click="handler"` 或 `@click="handler"`。

事件处理器 (handler) 的值可以是：

1. **内联事件处理器**：事件被触发时执行的内联 JavaScript 语句 (与 `onclick` 类似)。
2. **方法事件处理器**：一个指向组件上定义的方法的属性名或是路径。



通过 watch 来响应数据的变化

实例:使用 watch 实现计数器：

```html
<div id = "app">
    <p style = "font-size:25px;">计数器: {{ counter }}</p>
    <button @click = "counter++" style = "font-size:25px;">点我</button>
</div>
   
<script>
const app = {
  data() {
    return {
      counter: 1
    }
  }
}
vm = Vue.createApp(app).mount('#app')
vm.$watch('counter', function(nval, oval) {
    alert('计数器值的变化 :' + oval + ' 变为 ' + nval + '!');
});
</script>
```



## 生命周期

**生命周期**

* a.又名:生命周期回调函数、生命周期函数、生命周期钩子

* b.是什么：vue在关键时刻帮我们调用的一些特殊名称的函数

* c.生命周期函数的名字不可更改，但函数的具体内容是程序员根据需求编写的

* d.生命周期函数中的this指向是vm或组件实例对象

  **补充** 

- Vue3.0中可以继续使用Vue2.x中的生命周期钩子，但有有两个被更名：
  - `beforeDestroy`改名为 `beforeUnmount`
  - `destroyed`改名为 `unmounted`
- Vue3.0也提供了 Composition API 形式的生命周期钩子，与Vue2.x中钩子对应关系如下：
  - `beforeCreate`===>`setup()`
  - `created`===>`setup()`
  - `beforeMount` ===>`onBeforeMount`

### 注册周期钩子

举例来说，`mounted` 钩子可以用来在组件完成初始渲染并创建 DOM 节点后运行代码：

js

```javascript
export default {
  mounted() {
    console.log(`the component is now mounted.`)
  }
}
```

### 图像

[生命周期钩子 | Vue.js (vuejs.org)](https://cn.vuejs.org/guide/essentials/lifecycle.html#lifecycle-diagram)

## vue 组件

官网： https://cn.vuejs.org/guide/essentials/component-basics.html

实例

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>Vue 测试实例</title>
<script src="https://cdn.staticfile.org/vue/3.2.36/vue.global.min.js"></script>
</head>
<body>
    
<div id="app">
    <button-counter></button-counter>
</div>

<script>
// 创建一个Vue 应用
const app = Vue.createApp({})

// 定义一个名为 button-counter 的新全局组件
app.component('button-counter', {
  data() {
    return {
      count: 0
    }
  },
  template: `
    <button @click="count++">
      点了 {{ count }} 次！
    </button>`
})
app.mount('#app')
</script>
</body>
</html>
```

### 模块与组件

**模块**

a、理解：向外提供特定功能的程序，一般就是一个 js 文件
b.为什么：js 文件很多很复杂
c、作用：复用、简化js的编写，提高js 运行效率

**组件**

a.定义：用来实现局部功能的代码和资源的集合（html/css/js/image..)
b.为什么：一个界面的功能很复杂
c.作用：复用编码，简化项目编码，提高运行效率
**模块化**
当应用中的js都以模块来编写的，那这个应用就是一个模块化的应用
**组件化**
当应用中的功能都是多组件的方式来编写的，那这个应用就是一个组件化的应用

### 非单文件组件&单文件组件
非单文件组件：一个文件中包含有n个组件
单文件组件：一个文件中只包含有1个组件

### vue 中使用组件的三大步骤
**1.定义组件**
使用`vue.extend(options）`创建，其中 `options` 和 `new Vue(options）`时传入的 `options`几乎一
样，但也有点区别
data 必须写成函数，避免组件被复用时，数据存在引用关系
**2.注册组件**

* a.局部注册：
  `new vue()`的时候 `options`传入 `components`选项
* b.全局注册：`Vue.component（'组件名'，组件）`

**3.使用组件**

* 编写组件标签如`<school></school>`

### Prop

prop 是子组件用来接受父组件传递过来的数据的一个自定义属性。

父组件的数据需要通过 props 把数据传给子组件，子组件需要显式地用 props 选项声明 "prop"：

```javascript
<div id="app">
  <site-name title="Google"></site-name>
  <site-name title="Runoob"></site-name>
  <site-name title="Taobao"></site-name>
</div>
 
<script>
const app = Vue.createApp({})
 
app.component('site-name', {
  props: ['title'],
  template: `<h4>{{ title }}</h4>`
})
 
app.mount('#app')
</script>
```

> 一个组件默认可以拥有任意数量的 prop，任何值都可以传递给任何 prop。

### 动态 Prop

类似于用 v-bind 绑定 HTML 特性到一个表达式，也可以用 v-bind 动态绑定 props 的值到父组件的数据中。每当父组件的数据变化时，该变化也会传导给子组件：

```javascript
<div id="app">
  <site-info
    v-for="site in sites"
    :id="site.id"
    :title="site.title"
  ></site-info>
</div>
 
<script>
const Site = {
  data() {
    return {
      sites: [
        { id: 1, title: 'Google' },
        { id: 2, title: 'Runoob' },
        { id: 3, title: 'Taobao' }
      ]
    }
  }
}
 
const app = Vue.createApp(Site)
 
app.component('site-info', {
  props: ['id','title'],
  template: `<h4>{{ id }} - {{ title }}</h4>`
})
 
app.mount('#app')
</script>
```

### Prop 验证

组件可以为 props 指定验证要求。

为了定制 prop 的验证方式，你可以为 props 中的值提供一个带有验证需求的对象，而不是一个字符串数组。例如：

```javascript
Vue.component('my-component', {
  props: {
    // 基础的类型检查 (`null` 和 `undefined` 会通过任何类型验证)
    propA: Number,
    // 多个可能的类型
    propB: [String, Number],
    // 必填的字符串
    propC: {
      type: String,
      required: true
    },
    // 带有默认值的数字
    propD: {
      type: Number,
      default: 100
    },
    // 带有默认值的对象
    propE: {
      type: Object,
      // 对象或数组默认值必须从一个工厂函数获取
      default: function () {
        return { message: 'hello' }
      }
    },
    // 自定义验证函数
    propF: {
      validator: function (value) {
        // 这个值必须匹配下列字符串中的一个
        return ['success', 'warning', 'danger'].indexOf(value) !== -1
      }
    }
  }
})
```

当 prop 验证失败的时候，(开发环境构建版本的) Vue 将会产生一个控制台的警告。

type 可以是下面原生构造器：

- `String`
- `Number`
- `Boolean`
- `Array`
- `Object`
- `Date`
- `Function`
- `Symbol`

type 也可以是一个自定义构造器，使用 instanceof 检测。
