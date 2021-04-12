### 时间转变为时间戳的方法汇总  

```javascript
const date = new Date('2021-4-12 08:22:22');
console.log(date); // Mon Apr 12 2021 08:22:22 GMT+0800 (中国标准时间)
console.log(date * 1); //1618186942000
console.log(Number(date)); // 1618186942000
console.log(date.valueOf());  // 1618186942000
console.log(date.getTime()); // 1618186942000
```

### 转回标准时间

```javascript
const date = new Date('2021-4-12 08:22:22');
const timestamp = date.valueOf();
console.log(new Date(timestamp));  // Mon Apr 12 2021 08:22:22 GMT+0800 (中国标准时间)
```
