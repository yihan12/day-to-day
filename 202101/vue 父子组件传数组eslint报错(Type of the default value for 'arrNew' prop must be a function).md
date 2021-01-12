### 报错  
Type of the default value for 'arrNew' prop must be a function. (vue/require-valid-default-prop)
```javascript
 arrNew: {
  type: Array,
  default:[]
}
```

### 解决  
```javascript
arrNew: {
  type: Array,
  default() {
    return []
  }
}
```
