### 一、浏览器自带(性能较差)

```javascript
const num=1234.6789

console.log(num.toLocaleString());;//"1,234.679"
```

### 二、正则匹配

```javascript
 function format (num) {
  return (num+ '').replace(/(\d{1,3})(?=(\d{3})+(?:$|\.))/g,'$1,');
}
console.log(format(13124122223.12333));//13,124,122,223.12,333
```

### 三、自写逻辑

```javascript
 /**
 *  千分位
 **/
 function format(n) {
  let num = n.toString()
  let decimals = ''
  let integer = ''
  // 判断是否有小数
  if(num.indexOf('.') > -1 ){
    decimals = num.split('.')[1] 
    integer=num.split('.')[0] 
  }else{
    integer=num
  }
  let len = integer.length
  if (len <= 3) {
    return num
  } else {
    let temp = ''
    let remainder = len % 3
    decimals ? temp = '.' + decimals : temp
    if (remainder > 0) { // 不是3的整数倍
      return num.slice(0, remainder) + ',' + num.slice(remainder, len).match(/\d{3}/g).join(',') + temp
    } else { // 是3的整数倍
      return num.slice(0, len).match(/\d{3}/g).join(',') + temp
    }
  }
}
console.log(format(1235643.99765)); //1,235,643.99765
```
