<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#orgheadline3">1. 简介</a>
<ul>
<li><a href="#orgheadline1">1.1. Redux</a></li>
<li><a href="#orgheadline2">1.2. 主旨</a></li>
</ul>
</li>
</ul>
</div>
</div>

# 简介<a id="orgheadline3"></a>

## Redux<a id="orgheadline1"></a>

Redux是一款为Javascript应用程序准备的状态可预测的容器。
它可以让你写的应用程序，行为一致，可以运行在不同的环境下（客户端，服务器 和原生应用)，并且容易测试。在这些之上，它提供一种很棒的开发体验，比如[实时代码编辑绑定一个时间旅行调试器。](https://github.com/gaearon/redux-devtools)
你可以配合着react使用redux, 或者和其他任何view层的库，它很小，加上依赖也只有2KB，

这里有Redux的作者制作的30个免费Redux学习视频:[Redux入门](https://egghead.io/series/getting-started-with-redux) 

影响力：
Redux是Flux思想的一个实现版本，为了避免复杂性，它吸取了Elm的精髓，不论你是否用过这些，Redux只需要几分钟就可以入门。

安装：
npm安装就可以，略去。

    npm install -S redux

这里假定你使用npm（node package manager）包管理器，现代模块绑定器如webpack或browserify 去包裹CommonJS的模块。
如果你还没用npm和任何一款现代模块绑定器，而是更愿意使用单个文件，UMD构建可以使Redux作为一个全局对象，你可以从[csnjs](https://cdnjs.com/libraries/redux) 得到一个预编译好的版本。我们不建议用这种方式去构建正式的引用程序， 因为大部分Redux依赖的库都只在npm上可用。

## 主旨<a id="orgheadline2"></a>

1.  你的应用的全部 **state** 都存在一个对象树上，在全局唯一的store里。
2.  改变state树的唯一办法是发动一个 **action** （action是一个描述发生了什么的对象）
3.  为了标明 **action** 是怎么修改 **state** 树的，你需要去写纯\*reducer\*。

就这么多东西。

    import { createStore } from 'redux'
    /**
     * This is a reducer, a pure function with (state, action) => state signature.
     * It describes how an action transforms the state into the next state.
     *
     * The shape of the state is up to you: it can be a primitive, an array, an object,
     * or even an Immutable.js data structure. The only important part is that you should
     * not mutate the state object, but return a new object if the state changes.
     *
     * In this example, we use a `switch` statement and strings, but you can use a helper that
     * follows a different convention (such as function maps) if it makes sense for your
     * project.
     */
    function counter(state = 0, action) {
      switch (action.type) {
      case 'INCREMENT':
        return state + 1
      case 'DECREMENT':
        return state - 1
      default:
        return state
      }
    }
    
    // Create a Redux store holding the state of your app.
    // Its API is { subscribe, dispatch, getState }.
    let store = createStore(counter)
    
    // You can subscribe to the updates manually, or use bindings to your view layer.
    store.subscribe(() =>
      console.log(store.getState())
    )
    
    // The only way to mutate the internal state is to dispatch an action.
    // The actions can be serialized, logged or stored and later replayed.
    store.dispatch({ type: 'INCREMENT' })
    // 1
    store.dispatch({ type: 'INCREMENT' })
    // 2
    store.dispatch({ type: 'DECREMENT' })
    // 1
