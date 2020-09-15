### 问题

>多个组件通信问题
>
>EventBus传值,频繁会导致接口重复调用

我以为eventBus是专门处理兄弟组件之间通信的，但是实际上，eventBus是专门处理同一个路由下的复杂组件之间通信的。
如果涉及夸路由的组件通信。可以考虑利用$route对象传参或者Vuex

### vuex完美解决

由于涉及v-model,需要特殊处理:

bug
>computed property "XXX" was assigned to but it has no setter

#### 处理

component
```javascript
computed: {
  ...mapGetters({
      nameFromStore: 'name'
  }),
  name: {
     get(){
       return this.nameFromStore
     },
     set(newName){
       return newName
     } 
  }
}
```

store
```javascript
export const store = new Vuex.Store({
   state:{
     name : "Stackoverflow"
   },
   getters: {
     name: (state) => {
       return state.name;
     }
   }
}
```

#### 我的处理

component 页面 
```javascript
<template>
  <div v-model="common.checkStatus">
    123
  </div>
</template>
<script>
import {mapState} from "vuex"
export default {
//component 页面 computed部分
//computed
  computed: {
    ...mapGetters({
        common:state => state.common,
        checkStatus:state => state.common.checkStatus
    }),
  }
  //component 页面 watch部分
  //watch 实时监听checkStatus
  watch: {
    checkStatus(newVal){
      if(newVal){

      }else{

      }
    }
  }
}
</script>
```


store下的common.js
```javascript
const state = {
  checkStatus:false
}
const getters = {}
const actions = {}
const mutations = {
  setCheckStatus(state,payload){
    state.checkStatus = payload
  }
}

export default {
  state,
  getters,
  actions,
  mutations
}
```

其他 component页面 实时监听checkStatus
```javascript
import {mapState} from "vuex"
export default {
  computed: {
    ...mapGetters({
        checkStatus:state => state.common.checkStatus
    }),
  },
  //watch 实时监听checkStatus
  watch: {
    checkStatus(newVal){
      if(newVal){

      }else{

      }
    }
  }
}
```

其他 component页面 更新checkStatus
```javascript
import {mapState} from "vuex"
export default {
  methods:{
    clickOpen(){
      this.$store.commit("setCheckStatus",true)
    },
    clickClose(){
      this.$store.commit("setCheckStatus",false)
    }
  }
}
```


