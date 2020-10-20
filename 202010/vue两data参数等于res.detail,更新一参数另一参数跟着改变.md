### 问题

vue两data参数等于res.detail,更新一参数另一参数跟着改变

```javascript
import serviceSkill from "@service/skill"
export default{
  data(){
    return{
      datalist:{},
      dataOldlist:{},
    }
  },
  created(){
    this.changeSomething()
  },
  methods(){
    changeSomething(){
      const param = {}
      // 调用接口
      serviceSkill.update(param).then(res=>{
        this.datalist = res.data;
        this.dataOldlist = res.data
      })
    }
    // 点击更新
    clickUpdate(){
      this.datalist.name = "123";
      // 这里没有任何dataOldlist操作  打印this.dataOldlist.name   "123"
      console.log(this.dataOldlist.name) // "123"
    }
  },
}
```

### 解决

```javascript
this.datalist = JSON.parse(JSON.stringify(res.data));
this.dataOldlist = JSON.parse(JSON.stringify(res.data))
```
