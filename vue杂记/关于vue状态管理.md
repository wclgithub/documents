1. 我们可以使用props向下传递数据，使用自定义事件向上发送消息。我们如何能够传递数据和实现两个不同兄弟组件之间的通讯呢？

2. vue兄弟组件之间的数据通信有三种方式,从而处理应用程序的状态管理：

* 使用全局的EventBus  （事件中心）
* 使用简单的全局存储
* 类似于flux库的VueX  (大型项目中使用，小项目使用显得繁琐冗余)


### 全局的EventBus  （事件中心，可以参考兄弟组件传值部分内容）

EvemtBus是一个Vue实例，用于支持独立组件之间订阅和发布自定义事件。  我们在全局定义它，并挂在到vue原型上，就可以通用。

事件中心也需要事件触发和事件监听来完成数据交互

事件中心触发事件：

    EventBus.$emit('number-added', Number(this.number))

事件中心监听事件：

    EventBus.$on('number-added', number => { this.numbers.push(number) })
    
可以在任何组件中触发事件中心的事件，事件监听我们可以放在要结果的组件中

当项目的组件之间的传值多了的时候，由于事件中心的事件在任何地方都有可能被调用，不被追踪，维护起来是相当麻烦的事情，并可能成为bug来源

**这是为什么Vue指南声明EventBus不是Vue应用程序数据管理方法的主要原因之一。**


### 全局存储 存储（Store）

通过创建包含在组件之间共享数据存储的存储模式，可以实现一些简单的状态管理，存储（store）可以管理应用程序的状态以及负责更改状态的方法

我们来看这个例子：

    // store.js 
    export const store = { 
        state: { numbers: [1, 2, 3] },
        addNumber(newNumber) { this.state.numbers.push(newNumber) } 
    }

state 是我们应用共享的状态（数据）， addNumber函数 接受有效负载并直接更新状态值

这时我们用一个组件来显示这个数组：

    <!-- NumberDisplay.vue --> 
    <template> 
        <div> 
            <h2>{{ storeState.numbers }}</h2> 
        </div> 
    </template> 
    <script> 
    import { store } from '../store.js'; 
    export default { 
        name: 'NumberDisplay',
        data: () => ({
        storeState: store.state 
        }) } 
    </script>
    
用另一个组件来改变状态：

    <!-- NumberSubmit.vue --> 
    <template> 
        <div class="form"> 
            <input v-model="numberInput" type="number" /> 
            <button @click="addNumber(numberInput)">Add new number</button> 
        </div> 
    </template> 
    <script> 
    import { store } from '../store.js'; 
    export default { 
        name: 'NumberSubmit', 
        data: () => ({ numberInput: 0 }), 
        methods: { 
            addNumber(numberInput) { 
                store.addNumber(Number(numberInput)) 
                } 
            } 
        } 
    </script>

NumberSubmit组件中有一个addNumber()方法，它调用store.addNumber()变量并传递预期的有效负载。

store方法接收有效负载并直接改变store.numbers数组。

由于Vue的响应性（Vue reactivity）， 当存储状态中的number数组发生更改时，依赖于此值的相关DOM（NumberDisplay组件中的<template>）会自动更新。

当我们说组件相互交互时。这些组件不会对彼此做任何事情，而是通过存储相互调用更改。


#### 如果我们仔细观察所有与存储直接交互的所有部分，我们可以建立一个模式：
    
* NumberSubmit中的方法有责任直接对存储方法进行操作，因此我们可以将其标记为 存储操作 （Store action）

* 存储方法也有一定的责任 —— 直接改变存储状态。 所以我们会说这是一个 存储变量 （Store mutation）

* NumberDisplay并不真正关心存储或NumberSubmit中方法类型，只关心存储中获取信息。所以我们会说组件A是各种 Store getter

* 一个动作（Action）提交给一个变量（Mutation）。变量会改变状态，然后影响视图或组件。视图或组件使用 getter 检索存储数据。我们开始很接近类似Flux的状态管理。

#### 其中的原理很简单  store 中共享的状态在对象中  对象存储  按地址值传递   因此共享了数据  

* 亲测：本人应用在单页面中（也是组件），建议将共享数据深拷贝一份  在确定操作的时候改变共享数据值，期间数据交互不做改变
