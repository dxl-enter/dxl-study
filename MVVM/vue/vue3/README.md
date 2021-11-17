## vue3.0变化
一. 速度更快
  1. 虚拟DOM重写（Virtual DOM Rewrite）：将会有更多的编译时提示来减少运行时的开销
  2. 优化插槽生成（Optimized Slots Generration）：比如在2.0版本中父组件中更改了子组件中定义的props，子组件也会重新渲染；在vue3.0版本中我们可以单独渲染父子组件
  3. 静态树提升（Static Tree Hoisting）：在3.0版本中它可以检测静态的资源，不会再将其渲染，降低渲染的成本
  4. 静态属性提升（Static Props Hoisting）
  5. 基于Proxy的观察者机制：更快的组件初始化和修补，提升了两倍，但是对IE兼容性不是太好vue3.0也做了相应的处理


二. 体积更小
  1. 2.x版本压缩之后有20kb，而3.0压缩之后之后只有10kb的大小，这主要是通过删除vue中不重要的库，通过按需引入的方式来减少的


三. 更易于维护
  1. 从flow（静态代码检查，它是facebook公布的一个javascript的静态类型检查器，可以检查js中的一些错误）转向type（ts的静态类型检查以及ts的表现好）
  2. 解耦，是内容更加模块化：它依赖于自己的内包，就使得它可以自定义和灵活同时，还能提供透明性，是开发人员更好的进入源代码
  3. 编译器重写：更好的ide支持，当我们存在运行时错误时，它将会给出错误的位置和行号


四. 更面向原生开发
  1. 运行时与平台无关（现在好多跨平台的框架，都是面向原生的方式，更加灵活）


五. 更易于开发使用
  1. Exposed reactivity API
    
    * Provide standalone APIs for creating and observing reactive state
    我们众所周知，vue的核心竞争力是通过Object.defineProperty get/set改良了当时MVVM脏检查和get/set函数开始的，如今vue3.0使用es6中proxy这种代理模式升级成为reactivity api这种响应式的zpi
    ``` 
    import {observable, effect} from 'vue'
    const state = observable({
      count: 0
    })
    
    effect(()=>{
      console.log(`count is: ${state.count}`)
    }) // count is: 0
    
    state.count++  // count is: 1
    ```
    
    * easily identify why a componebt is re-rendering
    在3.0版本中新增了两个新的狗子函数onRenderTracked和onRenderTriggered，它使我们能够知道是什么导致了Vue实例中的重新渲染。

    ```
    const Component = {
      rederTriggered(event){
        console.log(`re-render of ` + this.$option.name + `component`, event)
      }
    }
    ```
    
    * improved typescript support w/TSX
    在3.0版本中在编译阶段就能找到好多错误

    ```
    interface HelloProps {
      text: string
    }
    
    class Hello extends Component<HelloProps> {
      count = 0
      
      render(){
        return <div>
          {this.count}
          {this.$props.text}
        </div>
      }
    }
    ```
    
  2. 
