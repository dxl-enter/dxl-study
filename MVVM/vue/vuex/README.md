1. state(mapState)：状态数据，唯一的数据源

  ```
  // 获取方式1：
  computed:{
    count(){
      this.$store.state.count
    }
  }
  
  // 获取方式2：推荐
  import {mapState} from "vuex"
  computed:{
    ...mapState(["count"])
  }
  ```
  
2. getters(mapGetters)：computed

  ```
  // 获取方式1：
  computed:{
    filterList(){
      this.$store.gettters.filterList
    }
  }
  
  // 获取方式2：推荐
  import {mapGetters} from "vuex"
  computed:{
    ...mapGetters(["filterList"])
    // ...mapGetters({arr: "filterList",newVal:state=>{state.newState?state.newState:'还没有添加新值'}})
  }
  ```
  
3. mutations(mapMutations)：唯一改变state的方式,配合commit使用，在vue中methods使用。要遵循vue的响应规则，必须是同步函数

  ```
  // 调用方式1：
  methods:{
    handle(){
      this.$store.commit("add")
    }
  }
  
  // 调用方式2：推荐
  import {mapMutations} from "vuex"
  methods:{
    ...mapMutations({handleReduce: 'add'})
  }
  ```
  
4. actions(mapActions)：进行异步处理，在vue中methods使用

  ```
  // 调用方式1：
  methods:{
    handleAction(){
      this.$store.dispatch("modifyCount")
    }
  }
  
  // 调用方式2：推荐
  import {mapActions} from "vuex"
  methods:{
    ...mapActions({handleAction: 'modifyCount'})
  }
  ```
  
5. modules：模块化

  * 默认:modules\actions\getters 都是注册在全局上的，可以直接调用
  * 只有state是注册在不同的模块上面的
  * namespaced：true情况下，modules\actions\getters 是注册在局部上的 this.$store.dispatch("moduleA/modifyName")


  ```
  // 获取方式：
  computed:{
    moduleName(){
      this.$store.state.moduleA.name
    }
  }
  
  // 如果模块moduleA中要使用全局的属性应该怎么办？---rootState
  // 在 moduleA的store
  actions:{
    // 不带namespaced：true
    // modifyName({state,commit,rootState}){
    // commit("subAdd")
    // 带namespaced：true
    modifyName({dispath,commit,getters.rootGetters}){
      // 访问全局的action
      dispath("modifyCount",null,{root:true})
      // 访问全局的mutations
      commit("changeCount",null,{root:true})
    }
  }
  // 调用方式1：
  methods:{
    handleAction(){
      this.$store.dispatch("modifyName")
    }
  }
  ```
  
