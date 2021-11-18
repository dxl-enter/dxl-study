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
