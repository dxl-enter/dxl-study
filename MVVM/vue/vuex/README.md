1. state(mapState)：状态数据，唯一的数据源

  ```
  // 获取方式：
  computed:{
    count(){
      this.$store.state.count
    }
  }
  ```
  
2. getters(mapGetters)：computed

3. mutations(mapMutations)：唯一改变state的方式

4. actions(mapActions)：进行异步处理

5. modules：模块化
