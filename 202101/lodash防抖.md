### 一

```javascript
import _ from "lodash";
const infoBoxDebounce = _.debounce(fc => fc(), 500, { leading: true });

//方法
clickMethod(){
  infoBoxDebounce(()=>{
  
    //代码块
 
 })
}
```

### 二

```javascript
<script>
import _ from 'lodash'
export default {
  methods: {
    //方法
    clickMethod：_.debounce(function(){

    //代码块

    },1000)
  }
}
</script>
```

### 三

```javascript
<script>
import _ from 'lodash'
export default {
  methods: {
    //方法
    clickMethod：_.debounce(() => {

        //代码块

    },1000)
  }
}
</script>
```
