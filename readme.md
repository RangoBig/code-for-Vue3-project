# Vue3 系统入门与项目实战

全方位知识点+高匹配度项目，轻松入门，深度掌握

# 第1章 Vue语法初探

> 这里使用了一个非常经典的方法:

```JavaScript
split()方法将一个字符串对象的每个字符拆出来，并且将每个字符串当成数组的每个元素
reverse()方法用来改变数组，将数组中的元素倒个序排列，第一个数组元素成为最后一个，最后一个变成第一个
join() 方法用于把数组中的所有元素放入一个字符串，元素是通过指定的分隔符进行分隔的。
```



这一章做了两个小例子,第一个是反转字符串,一个是显示隐藏字符

## 1.0 简单的拆分组件



> 





![image-20220217033307021](https://gitee.com/rango007/pic-md1/raw/master/20220217033307.png)



# 第2章 Vue基础语法



## 2.1 Vue中应用和组件的基础概念

> 使用vue创建一个应用,这个应用挂载到root结点上,创建应用会传递一些参数进去
>
> 一个网页是由一个个组件组成的,最外层的大组件就是由你传入的参数决定的

```JavaScript
<script>
    /**
     * createApp表示创建一个Vue应用,,存储到app变量中
     * 传入的参数表示,这个应用最外层的组件应该如何展示, 
     */
    const app = Vue.createApp({
        data() {
            return {
                message: `hello world`
            }
        },
        template: `<div> {{message}}<div>`
    });
    app.mount('#root')
</script>
```

> 创建一个应用之后,我如何获取该组件对应的根组件,实际上调用mount方法的时候,它的返回值就是根组件,



```JavaScript
//vm代表的就是vue的根组件
    const vm = app.mount('#root');
```

在这里我们能感知到vue的编程就是面向数据的编程,我在Vue对象中定义了数据,定义了模板,vue会自动的将数据和模板关联起来变成我们现在想要展示的效果,==实际上vue的这种面向数据编程的模式是参考了mvvm设计模式==

- m -> model 数据 在vue对象中对象data,
- v -> view 视图 在vue对象中对应template
- vm ->viewModel 视图数据连接层 模板和数据会自动的做连接,这层其实就是视图数据连接层,

> 视图数据连接层其实就是vue的一个个的组件,数据和视图的关系是由vm来关联的,我们可以借助vm

![image-20220221134242863](https://gitee.com/rango007/pic-md1/raw/master/20220221134242.png)



## 2.2 理解vue中的生命周期函数

> 我们平常在vue中所写的方法,需要触发才能执行,但是我们写一个mounted方法,加载页面之后,就可以立即执行

```JavaScript
mounted() {
          alert('立即执行');
      },
```

> ==Vue生命周期==:Vue实例从开始创建,初始化数据,编译模板,挂载DOM,更新渲染,卸载等一些列的过程,我们称这是Vue的生命周期
>
> ==Vue生命周期的作用==:Vue所有功能实现都是围绕生命周期进行,在不同阶段调用对应的钩子,实现组件数据管理和DOM渲染
>
> ==生命周期函数(钩子)==
>
> 生命周期函数是指在某一个时刻自动执行的函数

![vue生命周期函数](https://gitee.com/rango007/pic-md1/raw/master/20220221211937.png)

![img](https://gitee.com/rango007/pic-md1/raw/master/20220221212010.png)

> 从图中可以看出,Vue的生命周期包括==初始化==,==挂载==,==更新==和==销毁==四个阶段,八个生命周期

## 2.3 Vue各生命周期函数的描述





| Vue生命周期函数 | 描述                                            |
| --------------- | ----------------------------------------------- |
| beforeCreate()  | 在实例生成之前,立即执行的函数                   |
| create()        | 在实例生成之后,自动执行的函数                   |
| beforeMount()   | 在组件挂载到页面之前,立即执行的函数             |
| mounted()       | 在组件挂载到页面之后,自动执行的函数             |
| beforeUpdate()  | 当数据更新时,立即执行的函数                     |
| updated()       | 当数据更新页面重新渲染后,自动执行的函数         |
| beforeUmount()  | 当vue应用销毁时,立即执行的函数                  |
| unmounted()     | 当vue应用销毁时且DOM完全销毁之后,自动执行的函数 |

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>lesson 06</title>
    <script src="https://unpkg.com/vue@next"></script>
  </head>
  <body>
    <div id="root"></div>
  </body>
  <script>
    //生命周期函数:在某一时刻会自动执行的函数
    const app = Vue.createApp({
      data() {
        return {
          message: "墨迹阿婆",
        };
      },
      //   第一个生命周期函数
      beforeCreate() {
        // console.log("beforeCreate");
      },
      //   第二个生命周期函数
      created() {
        // console.log("created");
      },
      //   第三个生命周期函数,这个时候template已经被vue底层包装到了render函数里面了
      // 组件内容被渲染到页面之前自动执行的函数
      beforeMount() {
        // console.log(document.getElementById("root").innerHTML);
        // console.log("beforeMount");
      },
      // 第四个生命周期函数,发生在虚拟dom已经渲染
      // 在组件内容被渲染到页面之后,会自动执行的函数
      mounted() {
        // console.log(document.getElementById("root").innerHTML);
        // console.log("mounted");
      },
    //   当data中的数据发生变化时会自动执行的函数
    //   当数据发生变化时会立即自动执行的函数
      beforeUpdate() {
          console.log(document.getElementById("root").innerHTML+`beforeUpdate`);
      },
    //   当data数据发生变化,同时页面更新后,会自动执行的函数
    //   当数据发生变化,页面重新渲染后,会自动执行的函数
    updated() {
        // console.log(document.getElementById("root").innerHTML+`updated`);
    },
    // 当vue应用失效的时候,自动执行的函数,vue实例销毁时会自动执行的函数
    beforeUnmount() {
        console.log(document.getElementById("root").innerHTML+'beforeUnmount');
    },
    // 当Vue应用失效时,且dom完全销毁之后,自动执行的函数
    unmounted() {
        console.log(document.getElementById("root").innerHTML+'unmounted');
    },
      template: `<div>{{message}}</div>`,
    });
    const vm = app.mount("#root");
  </script>
</html>

```

## 2.4 常用模板语法讲解

> - Vue.js使用了基于HTML的模板语法,允许开发者声明式地将DOM绑定至底层组件实例的数据所有 Vue.js 的模板都是合法的 HTML，所以能被遵循规范的浏览器和 HTML 解析器解析。
> - 在底层的实现上，Vue 将模板编译成虚拟 DOM 渲染函数。结合响应性系统，Vue 能够智能地计算出最少需要重新渲染多少组件，并把 DOM 操作次数减到最少。

- 插值 {{message}}
- 原始HTML :双大括号会将数据解释为普通文本，而非 HTML 代码。为了输出真正的 HTML，你需要使用[`v-html` 指令](https://v3.cn.vuejs.org/api/directives.html#v-html)：

- Attribute: 对于布尔 attribute (它们只要存在就意味着值为 `true`)，`v-bind` 工作起来略有不同，在这个例子中：

  ```html
  <button v-bind:disabled="isButtonDisabled">按钮</button>
  ```

- 使用 JavaScript 表达式,对于所有的数据绑定,Vue.js都提供了完全的JavaScript表达式支持

```JavaScript
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ message.split('').reverse().join('') }}

<div v-bind:id="'list-' + id"></div>
```

这些表达式会在当前活动实例的数据作用域下作为 JavaScript 被解析。有个限制就是，每个绑定都只能包含**单个表达式**，所以下面的例子都**不会**生效。

```JavaScript
<!--  这是语句，不是表达式：-->
{{ var a = 1 }}

<!-- 流程控制也不会生效，请使用三元表达式 -->
{{ if (ok) { return message } }}
```



- 缩写: 同时，在构建由 Vue 管理所有模板的单页面应用程序 [(SPA - single page application)](https://en.wikipedia.org/wiki/Single-page_application) 时，`v-` 前缀也变得没那么重要了。因此，Vue 为 `v-bind` 和 `v-on` 这两个最常用的指令，提供了特定简写：
  - v-bind缩写为":"
  - v-on缩写为@
- 动态参数:也可以在指令中使用JavaScript表达式,方法是用方括号括起来

```JavaScript
<!--
注意，参数表达式的写法存在一些约束，如之后的“对动态参数表达式的约束”章节所述。
-->
<a v-bind:[attributeName]="url"> ... </a>
```

同样地，你可以使用动态参数为一个动态的事件名绑定处理函数：

```JavaScript
<a v-on:[eventName]="doSomething"> ... </a>
```

在这个示例中，当 `eventName` 的值为 `"focus"` 时，`v-on:[eventName]` 将等价于 `v-on:focus`



- 修饰符:饰符 (modifier) 是以半角句号 `.` 指明的特殊后缀，用于指出一个指令应该以特殊方式绑定。例如，`.prevent` 修饰符告诉 `v-on` 指令对于触发的事件调用 `event.preventDefault()`：

```JavaScript
<form v-on:submit.prevent="onSubmit">...</form>
```

在接下来对 [`v-on`](https://v3.cn.vuejs.org/guide/events.html#事件修饰符) 和 [`v-for`](https://v3.cn.vuejs.org/guide/forms.html#修饰符) 等功能的探索中，你会看到修饰符的其它例子。

## 2.5 Vue修饰符详解

> 事件修饰符:
>
> 1. .stop阻止事件继续传播
> 2. .prevent阻止标签默认行为
> 3. .capture使用事件捕获模式,即元素自身触发的事件先在此处理,然后才交给内部元素进行处理
> 4. .self只当在event.target是当前元素自身时触发处理函数
> 5. .once事件将只会触发一次
> 6. .passive告诉浏览器你不想阻止事件的默认行为



## 2.6 Data Property 和方法

<font color="red" size=5>Vue 自动为 `methods` 绑定 `this`，以便于它始终指向组件实例。这将确保方法在用作事件监听或回调时保持正确的 `this` 指向。在定义 `methods` 时应避免使用箭头函数，因为这会阻止 Vue 绑定恰当的 `this` 指向。</font>

 ```html
 <!DOCTYPE html>
 <html lang="en">
   <head>
     <meta charset="UTF-8" />
     <meta http-equiv="X-UA-Compatible" content="IE=edge" />
     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
     <title>Document</title>
     <script src="https://unpkg.com/vue@next"></script>
   </head>
   <body>
     <div id="root"></div>
   </body>
   <script>
     /**
      * data & methods & computed & watcher
      * message是data返回的第一层中的数据
      */
     const app = Vue.createApp({
       data() {
         return {
           message: "你好,世界!",
         };
       },
       methods: {
         //   在vue里面,这些方法里面的this指向统一的都指向vue的实例
         // 因为箭头函数指向的是外层的this,外层的this是window
           handClick() {
               console.log('click',this);
           }
       },
       template: `
       <div @click="handClick">{{message}} </div>
       `,
     });
     const vm = app.mount("#root");
   </script>
 </html>
 
 ```

## 2.7 计算属性和监听器

> 模板内的表达式非常便利，但是设计它们的初衷是用于简单运算的。在模板中放入太多的逻辑会让模板过重且难以维护。

<font color="red" size=5>计算属性和方法的区别,计算属性内部会带有缓存机制,当计算属性依赖的内容发生变化变更时,才会重新执行计算</font>

**侦听器**

虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 `watch` 选项提供了一个更通用的方法来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

> 侦听器会监听某一个属性的变化,当属性变化的时候,异步操作可以在watch中做一下,如果是同步操作,不如computed

## 2.8 Class与Style绑定

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <title>lesson 2_8</title>
      <script src="https://unpkg.com/vue@next"></script>
      <style>
          .red{
              color: red;
          }
          .green{
              color: green;
          }
      </style>
</head>
<body>
    <div id="root"></div>
</body>
<script>
    const app = Vue.createApp({
        data() {
            return {
                classString: 'red',
            }
        },
        template: `
        <div :class="classString">你好</div>
        
        `,
    });
    const vm = app.mount('#root');
</script>
</html>
```

> 可以使用多种数据格式来定义

```JavaScript
data() {
        return {
          classString: "red",
          //可以使用一个对象
          classObject: {red: false, green: true},
        //   可以使用数组,也可以在数组中再写一个对象
        classArray: ["red" ,"green" ,{
            brown: false
        }]
        };
```

> 子组件外层有多个组件的时候,不能直接在子组件上面设置样式

```JavaScript
    //展示一个小组件
    app.component("demo", {
        template: `
        <div :class="$attrs.class">single_小组件</div>
        <div>single_小组件</div>
        `
    });
```

> 如何写行内样式?可以使用字符串绑定style样式,也可以通过数组绑定样式

```JavaScript
const app = Vue.createApp({
      data() {
        return {
          classString: "red",
          styleString: 'color: yellow',
          styleObject: {
              color: 'orange',
              background: 'yellow'
          }
        };
      },
      template: `
        <div :style="styleObject">
            你好
        </div>
        `,
    });
```

## 2.9 条件渲染

<font color="red" size=5>因为 `v-if` 是一个指令，所以必须将它添加到一个元素上。直接移除该元素</font>

> v-if设置隐藏的时候是控制DOM直接移除该元素,而v-show隐藏的时候是设置`style="display: none;"`

## 2.10 列表渲染

> 使用v-for对对象做一些循环的时候

```JavaScript
const app = Vue.createApp({
        data() {
            return {
                list: ['dell', 'lee', 'teacher'],
                listObject: {
                    firstName: 'Dell',
                    lastName: 'Teacher',
                    job: 'Teacher'
                }
            }
        },
        template:
        `
        <div>
            <div v-for="(value,key,index) in listObject">
                {{value}}--->{{key}}--->{{index}}
            </div>
        </div>
        `
    });
```

> 列表循环,添加数据的时候,为了避免重复渲染页面,可以绑定一个":key=' ' "属性

```JavaScript
  template: `
        <div>
            <button @click="handleAddBtnClick">新增</button>
            <div v-for="(value,index) in list" :key="index">
                {{value}}--->{{index}}
            </div>
        </div>
        `,
```

> 如何向数组中添加新数据

## 2.11 数组更新检测-变更数组

> ==变更方法==

Vue 将被侦听的数组的变更方法进行了包裹，所以它们也将会触发视图更新。这些被包裹过的方法包括：

- `push()`  将新元素添加到数据的末尾,并返回新的长度
- `pop()`  删除数组的最后一个元素,并返回该元素
- `shift()` 删除数组的第一个元素,并返回该元素
- `unshift()` 将新元素添加到数组的开头,并返回新的长度
- `splice()` 从数组中添加/删除元素
- `sort()` 对数组元素进行排序
- `reverse()` 反转数组中元素的顺序

你可以打开控制台，然后对前面例子的 `items` 数组尝试调用变更方法。比如 `example1.items.push({ message: 'Baz' })`



## 2.12 列表循环渲染

> 当它们处于同一节点，`v-if` 的优先级比 `v-for` 更高，这意味着 `v-if` 将没有权限访问 `v-for` 里的变量：

使用v-for嵌套一个v-if的时候,会使展示数据都会多一层展示内容

<font color="red" size=5>使用template占位符</font>

可以把 `v-for` 移动到 `<template>` 标签中来修正：

```JavaScript
<template v-for="todo in todos" :key="todo.name">
  <li v-if="!todo.isComplete">
    {{ todo.name }}
  </li>
</template>
```

## 2.13 事件绑定

> 1.如何即传入参数,又传入event,(2,$event)

```JavaScript
  * 1.如何即传入参数,又传入event,(2,$event)
       */
      methods: {
        handleAddBtnClick(num,event) {
            console.log(event.target);
          this.counter += num;
        },
      },
      template: `
        <div>{{counter}}
            <button @click="handleAddBtnClick(2,$event)"> 按钮</button>
        </div>
        `,
```

> 2.事件绑定多个函数要使用引用

> 3.绑定的事件会冒泡触发,即内部的触发,会引发外部嵌套的触发
>
> 使用事件修饰符.stop可以停止事件冒泡
>
> 阻止默认行为.prevent
>
> .capture捕获模式,可以从外到内进行事件捕获,

点击子元素的时候,不要触发自己.self

```JavaScript
 template: `
        <div>{{counter}}
            <div @click="handleDivClick">
            <button @click.stop="handleAddBtnClick"> 按钮</button>
            </div>
        </div>
        `,
```



> - 事件修饰符:stop, prevent, capture, self, once, passive
> - 按键修饰符:enter tab delete esc up down left right
> - 鼠标修饰符left right middle
> - 精准修饰符: exact
>
> 使用修饰符时，顺序很重要；相应的代码会以同样的顺序产生。因此，用 `@click.prevent.self` 会阻止**元素本身及其子元素的点击的默认行为**，而 `@click.self.prevent` 只会阻止对元素自身的点击的默认行为。

## 2.14 表单输入绑定

> 基础语法:你可以用 v-model 指令在表单 `<input>`、`<textarea>` 及 `<select>` 元素上创建双向数据绑定。它会根据控件类型自动选取正确的方法来更新元素。尽管有些神奇，但 `v-model` 本质上不过是==语法糖==。它负责监听用户的输入事件来更新数据，并在某种极端场景下进行一些特殊处理。

1. input框的双向绑定

```html
<div>{{message}}
            <input v-model=" message"/>
</div>
```

2. textarea的写法,单标签闭合就行

```html
<div>{{message}}
            <textarea v-model=" message"/>
</div>
```

3. 复选框 (Checkbox)

```JavaScript
 <script>
    const app = Vue.createApp({
        data() {
            return {
                message: []
            }
        },
        template: `
        <div>{{message}}
        jack<input type="checkbox" v-model="message" value="jack" />
        dell<input type="checkbox" v-model="message" value="dell" />
        lee<input type="checkbox" v-model="message" value="lee" />
        </div>
        `
    });
    const vm = app.mount("#root");
  </script>
```

4. 单选框 (Radio)

```JavaScript
 <script>
    const app = Vue.createApp({
        data() {
            return {
                message: []
            }
        },
        template: `
        <div>{{message}}
        jack<input type="radio" v-model="message" value="jack" />
        dell<input type="radio" v-model="message" value="dell" />
        lee<input type="radio" v-model="message" value="lee" />
        </div>
        `
    });
    const vm = app.mount("#root");
  </script>
```

5. 可以使用v-for配合select进行使用

```JavaScript
 <script>
    const app = Vue.createApp({
      data() {
        return {
          message: [],
          options: [
            {
              text: "A",
              value: "A",
            },
            {
              text: "B",
              value: "B",
            },
            {
              text: "C",
              value: "C",
            },
          ],
        };
      },
      template: `
            <div>{{message}}
            <select v-model="message">
                <option v-for="item in options" :value="item.value">{{item.text}}</option>
            </select>
            </div>
            `,
    });
```

> 使用值选中状态

```JavaScript
 <script>
    const app = Vue.createApp({
      data() {
        return {
          message: 'hello',
        };
      },
      template: `
            <div>{{message}}
                <input type="checkbox" v-model="message" true-value="hello" false-value="world" />
            </div>
            `,
    });
```

6. 表单修饰符

> `.lazy`
>
> 在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了[上述](https://v3.cn.vuejs.org/guide/forms.html#vmodel-ime-tip)输入法组织文字时)。你可以添加 `lazy` 修饰符，从而转为在 `change` 事件之后进行同步：

> `.number`
>
> 如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```JavaScript
 <script>
    const app = Vue.createApp({
      data() {
        return {
          message: 'hello',
        };
      },
      template: `
            <div>{{typeof message}}
                <input type="number" v-model="message"  />
            </div>
            `,
    });
```

> `.trim`
>
> 如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符：
>
> ```html
> <input v-model.trim="msg" />
> ```

# 第3章 探索组件的理念

> 1. 组件的定义
> 2. 组件具有复用性
> 3. 全局组件,只要定义了,处处可以使用,性能不高,但是使用起来简单,名字建议,小写字母单词,中间用
> 4. 局部组件,定义了,要注册之后才能使用,性能比较高,使用起来比较麻烦,建议大写字母开头,驼峰命名
> 5. 局部组件使用时,要做一个名字和组件间的映射对象,你不写映射,Vue底层也会自动尝试办你做映射



![components](https://gitee.com/rango007/pic-md1/raw/master/20220224171718.png)

## 3.1 全局组件

> 这些组件是**全局注册**的。也就是说它们在注册之后可以用在任何新创建的组件实例的模板中。比如：
>
> 在所有子组件中也是如此，也就是说这三个组件在各自内部也都可以相互使用。
>

```JavaScript
 <script>
    /**
     * 1.创建vue应用的时候,会接收一个参数,这个参数会决定vue的根组件怎么渲染
     * 2.组件是可以被复用和,而且数据不是公用的,而是独享的
     * 3.全局组件,只要定义了,处处都可以用,性能不高,但是使用起来简单
     */
    const app = Vue.createApp({
      template: `
        <div>
            hello
        </div>
        `,
    });
    app.component("counter-parent",{
        template: `<counter/>`
    })
    app.component("counter", {
        data() {
            return {
                count: 1 
            }
        },
      template: `<div @click="count+=1">{{count}}</div>`,
    });
    const vm = app.mount("#root");
  </script>
```

```JavaScript
<div id="app">
  <component-a></component-a>
  <component-b></component-b>
  <component-c></component-c>
</div>
```

## 3.2 局部组件

```JavaScript
 <script>
    /**
     * 1.创建vue应用的时候,会接收一个参数,这个参数会决定vue的根组件怎么渲染
     * 2.组件是可以被复用和,而且数据不是公用的,而是独享的
     * 3.全局组件,只要定义了,处处都可以用,性能不高,但是使用起来简单
     */
    // 定义一个常量,它是局部组件,但是在vue中不可以直接用,以为在vue中是感知不到的,
    // 如何让vue关联到常量组件
    const Conter = {
      data() {
        return {
          count: 1,
        };
      },
      template: `<div @click="count +=1">{{count}}</div>`,
    };
    const HelloWorld = {
      template: `<div>hello 你好</div>`,
    };
    const app = Vue.createApp({
      components: {
        // 将常量组件名字赋值给,字符串
        Conter, HelloWorld,
      },
      template: `
        <div>    
            <hello-world />
            <conter />
        </div>
        `,
    });

    const vm = app.mount("#root");
  </script>
```

## 3.3 组件间传值

## 3.4 Prop验证

> 我们可以为组件的 prop 指定==验证要求==，例如你知道的这些类型。如果有一个要求没有被满足，则 Vue 会在浏览器控制台中警告你。这在开发一个会被别人用到的组件时尤其有帮助。

```JavaScript
    const app = Vue.createApp({
        data() {
            return {
                num: ()=>{
                    alert('nihao')
                }
            }
        },
      template: `<div> <test v-bind:content="num" /> </div>`,
    });
    /**
     * 创建一个子组件test,可以验证String Boolean,Array,Object,Function
     */
    app.component("test", {
        props: {
            content: Function
        },
        template: `<div>{{typeof content}}</div>`
    });
    const vm = app.mount("#root");
  </script>
```

```JavaScript
    /**
     * 创建一个子组件test,可以验证String Boolean,Array,Object,Function,Symbol
     * 使用required参数,这个参数表示,必须要有值
     * required: 必填
     * default: 默认值
     * 
     */
    app.component("test", {
        props: {
            content: {
                type: Number,
                default: 789
            }
        },
        methods: {
            handleClick(){

            }
        },
        template: `<div @click="">{{ content}}</div>`
    });
    const vm = app.mount("#root");
  </script>
```

> 还可以使用函数进行校验`validator`可以判读数字大小

## 3.5 单项数据流的理解

> v-bind="params"
>
> 等同于 :content="params.content" :a="params.a"
>
> 单项数据流:
>      * 父组件可以向子组件传递一些数据,但是子组件绝对是不可以更改的,
>      * 那么如何修改从父组件中传递的值,我们可以把从父组件中传递过来的值,复制一份,再使用

```JavaScript
<script>
    const app = Vue.createApp({
      data() {
        return {
          params: {
            content: 1234,
            a: 1,
            b: 2,
            c: 3,
          },
        };
      },
      template: `<div> <test v-bind="params"/> </div>`,
    });
    app.component("test", {
      props: ["content", "a", "b", "c"],
      template: `<div>{{content}}--{{a}}--{{b}}--{{c}}</div>`,
    });
    const vm = app.mount("#root");
  </script>
```

<font color="red" size=5>为什么vue中会有单向数据流的概念?子组件为什么不能改变父组件的数据哪?</font>

如果子组件能双向更改父组件里面的数据,那么可能会出现数据耦合,这样

## 3.6 Non-Props属性是什么



>  /**
>   * Non-prop属性:就是父组件向子组件
>   * 我们希望最外层的结点上不展示这个绑定属性
>   * 做样式修饰
>
>`<div v-bind="$attrs">Counter </div>`
>
>1. vue中，默认情况下，调用组件时，传入一些没有在props中定义的属性，会把这些“非法”属性渲染在组件的根元素上（有一些属性除外），而这些“非法”的属性会记录在$attrs属性上。
>
>2. 如何控制不把这些非法的属性渲染在组件的根元素上呢？答案是在组件内部设置inheritAttrs:false即可。
>
>3. 通过v-bind="$attrs"可以把“非法”的属性渲染到指定的组件某个元素上。

```JavaScript
app.component("counter", {
        // inheritAttrs: false,
        template: `
        <div >Counter </div>
        <div >Counter </div>
        <div v-bind="$attrs">Counter </div>
        `
    });
    const vm = app.mount("#root");
  </script>
```



![image-20220226130108861](https://gitee.com/rango007/pic-md1/raw/master/20220226131845.png)

> 也可以使用函数进行测试

```JavaScript
mounted() {
            console.log(this.$attrs.msg);  
},
```

## 3.7 父子组件间如何通过事件进行通信

> - 子组件也可以向父组件传递参数

```JavaScript
 <script>
    const app = Vue.createApp({
      data() {
        return {
          count: 1,
        };
      },
      methods: {
        handleAddOne(param) {
          this.count += param;
        },
      },
      template: `
        <div>
            <counter :count="count" @add-two="handleAddOne" />
        </div>
        `,
    });
    /**
     * 子组件如何告诉父组件,修改数据内容
     * 注意:触发事件的时候用驼峰,监听事件的时候,我们用"-"间隔
     */
    app.component("counter", {
      props: ["count"],
      methods: {    
        handleItemClick() {
          this.$emit("addTwo",3);
        },
      },
      template: `<div @click="handleItemClick"> {{count}} </div>`,
    });
    const vm = app.mount("#root");
  </script>
```

> **定义自定义事件**:可以通过 `emits` 选项在组件上定义发出的事件。

```javascript
app.component('custom-form', {
  emits: ['inFocus', 'submit']
})
```

> 验证抛出去的事件

## 3.8 `v-model` 参数

> 默认情况下，组件上的 `v-model` 使用 `modelValue` 作为 prop 和 `update:modelValue` 作为事件。我们可以通过向 `v-model` 传递参数来修改这些名称：

```JavaScript
    <div>
            <input v-model="text" />
            <counter v-model="count" />
        </div>
 <script>
    const app = Vue.createApp({
      data() {
        return {
          count: 1,
          text: 'hello world'
        };
      },
    
      template: `
        <div>
            <input v-model="text" />
            <counter v-model="count" />
        </div>
        `,
    });
    /**
     * 子组件如何告诉父组件,修改数据内容
     * 注意:触发事件的时候用驼峰,监听事件的时候,我们用"-"间隔
     */
    app.component("counter", {
      props: ["modelValue"],
      //   emit的意义在于,使我们清楚的看到对外触发了什么组件,
      // emits 选择要与$emit里面的保持一致
      //   emits: ['addTwo'],
      methods: {
        handleItemClick() {
          this.$emit("update:modelValue", this.modelValue + 2);
        },
      },
      template: `<div @click="handleItemClick"> {{count}} </div>`,
    });
    const vm = app.mount("#root");
```

在本例中，子组件将需要一个 `title` prop 并发出 `update:title` 事件来进行同步：

```js
app.component('my-component', {
  props: {
    title: String
  },
  emits: ['update:title'],
  template: `
    <input
      type="text"
      :value="title"
      @input="$emit('update:title', $event.target.value)">
  `
})
```

## 3.9 多个v-model绑定

```html
<script>
    const app = Vue.createApp({
      data() {
        return {
          count: 1,
          count1: 1,
        };
      },
      //如何使用多个v-model
      template: `
        <div>
            <counter v-model:count="count" v-model:count1="count1" />
        </div>
        `,
    });

    app.component("counter", {
      props: ["count", "count1"],
      methods: {
        handleItemClick() {
          this.$emit("update:count", this.count + 2);
        },
        handleItemClick1() {
          this.$emit("update:count1", this.count1 + 3);
        },
      },
      template: `
      <div @click="handleItemClick"> {{count}} </div>
      <div @click="handleItemClick1"> {{count1}} </div>
      `,
    });
    const vm = app.mount("#root");
  </script>
```

```JavaScript
app.component('user-name', {
  props: {
    firstName: String,
    lastName: String
  },
  emits: ['update:firstName', 'update:lastName'],
  template: `
    <input 
      type="text"
      :value="firstName"
      @input="$emit('update:firstName', $event.target.value)">

    <input
      type="text"
      :value="lastName"
      @input="$emit('update:lastName', $event.target.value)">
  `
})
```

## 3.10 处理 `v-model` 修饰符

我们学习表单输入绑定时，我们看到 `v-model` 有[内置修饰符](https://v3.cn.vuejs.org/guide/forms.html#修饰符)——`.trim`、`.number` 和 `.lazy`。但是，在某些情况下，你可能还需要添加自己的自定义修饰符。

让我们创建一个示例自定义修饰符 `capitalize`，它将 `v-model` 绑定提供的字符串的第一个字母大写。

添加到组件 `v-model` 的修饰符将通过 `modelModifiers` prop 提供给组件。在下面的示例中，我们创建了一个组件，其中包含默认为空对象的 `modelModifiers` prop。

请注意，当组件的 `created` 生命周期钩子触发时，`modelModifiers` prop 会包含 `capitalize`，且其值为 `true`——因为 `capitalize` 被设置在了写为 `v-model.capitalize="myText"` 的 `v-model` 绑定上。



# 插槽

## 1.0 插槽内容

> 插槽里可以放字符串,组件,

## 2.0 slot数据作用域

<font color="red" size=5>父级模板里的所有内容都是在父级作用域中编译的；子模板里的所有内容都是在子作用域中编译的。</font>

![slot](https://gitee.com/rango007/pic-md1/raw/master/20220228143932.png)

```JavaScript
<script>
    /**
     * slot插槽
     * slot是没有办法绑定事件的
     * 1.slot不仅可以传递字符串,还可以传递子组件
     * 2.需要注意的点,父模板里调用的数据属性,使用的都是父模板里的数据,
     * 子模板里调用的数据属性,使用的都是子模板里的数据
     */
    const app = Vue.createApp({
        data() {
            return {
                text: '提交1'
            }
        },
      template: `
        <myform>
            <div>{{text}}</div>
        </myform>

        <myform>
            <button>{{text}}</button>
        </myform>

        `,
    });
    app.component('test',{
        template: '<div>test</div>',
    });
    app.component("myform", {
      methods: {
        handleClick() {
          alert(123);
        },
      },
      template: `
        <div> 
            <input />
            <span @click="handleClick">
            <slot></slot>
            </span>
        </div>
        `,
    });
    const vm = app.mount("#root");
  </script>
```

## 3.0 使用插槽和具名插槽解决组件内容传递问题

> 具名插槽:

```html
<script>
  // slot 插槽
  // slot 中使用的数据，作用域的问题
  // 父模版里调用的数据属性，使用的都是父模版里的数据
  // 子模版里调用的数据属性，使用的都是子模版里的数据
  // 具名插槽
  const app = Vue.createApp({
    template: `
      <layout>
        <template v-slot:header>
          <div>header</div>
        </template>
        <template v-slot:footer>
          <div>footer</div>
        </template>
      </layout>
    `
  });

  app.component('layout', {
    template: `
      <div>
        <slot name="header"></slot>
        <div>content</div>
        <slot name="footer"></slot>
      </div>
    `
  });

  const vm = app.mount('#root');
</script>
```

## 4.0 作用域插槽

> 有时让插槽内容能够访问子组件中才有的数据是很有用的。当一个组件被用来渲染一个项目数组时，这是一个常见的情况，我们希望能够自定义每个项目的渲染方式。
>
> 例如，我们有一个组件，包含一个待办项目列表。

要使 `item` 在父级提供的插槽内容上可用，我们可以添加一个 `<slot>` 元素并将其作为一个 attribute 绑定：

```html
<ul>
  <li v-for="( item, index ) in items">
    <slot :item="item"></slot>
  </li>
</ul>
```

可以根据自己的需要将任意数量的 attribute 绑定到 `slot` 上：

```html
<ul>
  <li v-for="( item, index ) in items">
    <slot :item="item" :index="index" :another-attribute="anotherAttribute"></slot>
  </li>
</ul>
```

绑定在 `<slot>` 元素上的 attribute 被称为**插槽 prop**。现在，在父级作用域中，我们可以使用带值的 `v-slot` 来定义我们提供的插槽 prop 的名字：



```html
<todo-list>
  <template v-slot:default="slotProps">
    <i class="fas fa-check"></i>
    <span class="green">{{ slotProps.item }}</span>
  </template>
</todo-list>
```

![image-20220301110545110](https://gitee.com/rango007/pic-md1/raw/master/20220301110545.png)

## 5.0 动态组件和异步组件

```JavaScript
<script>
    /**
     * 动态组件,需要一个组件来控制,控制input框和数据展示
     */
    const app = Vue.createApp({
        data() {
            return {
                currentItem: ' input-item'
            }
        },
        methods: {
            handleClick(){
                if (this.currentItem === 'input-item') {
                    this.currentItem = 'common-item';
                }else {
                    this.currentItem = 'input-item';
                }
            }
        },
      template: `
        <input-item v-show=" currentItem ==='input-item' " />
        <common-item v-show=" currentItem ==='common-item' " />
        <button @click="handleClick"> 切换</button>
        `,
    });

    app.component("input-item", {
      template: `
        <input />
        `,
    });
    app.component("common-item", {
      template: `
        <div>hello world</div>
        `,
    });
    const vm = app.mount("#root");
  </script>
```

> 上述的切换组件动作过于繁琐,我们直接使用动态组件`    <component :is="currentItem" />`
>
> 使用这种缓存有一个弊端,就是在输入框中输入的数据,切换一下,数据就会丢失,` <keep-alive>
>         <component :is="currentItem" />
>       </keep-alive>`

## 6.0 基础语法和查漏补缺

> - v-once 让元素























# 第4章 Vue中的动画



# 第5章 Vue中的高级语法



# 第6章 Composition API



# 第7章 Vue项目开发配套工具讲解



# 第8章 "京东到家"项目首页开发

# 第9章 登录功能开发

# 第10章 商家展示功能开发(上)

# 第11章 商家展示功能开发(下)

# 第12核心购物链路开发

# 第13章 真机调试及工程发布流程

