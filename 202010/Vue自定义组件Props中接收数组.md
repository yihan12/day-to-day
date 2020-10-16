### 问题

报错

```javascript
props: {
    showcontent: {
      type: Array,
      default: []
    },
}
```

### 报错信息


[Vue warn]: Invalid default value for prop "showcontent": Props with type Object/Array must use a factory function to return the default value.


### 问题解决

```javascript
props: {
    showcontent: {
      type: Array,
      default: function () { return [] }
    },
}
```

ES6

```javascript
props: {
    showcontent: {
      type: Array,
      default: () => []
    },
}
```
