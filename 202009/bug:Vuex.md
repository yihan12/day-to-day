### 问题

v-model取值问题

>Vuex - Computed property “xxx” was assigned to but it has no setter

### 报错情形

```javascript
<template>
  <div v-model="checkStatus">
    123
  </div>
</template>

<script>
import {mapState} from "vuex"
export default {
  computed:{
    ...mapState({
      checkStatus:state => state.common.checkStatus
    })
  }
}
</script>
```

### 解决方案

```javascript
//In your Component

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
//In your store

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

### 我的解决方案

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
    ...mapState({
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
    ...mapState({
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
