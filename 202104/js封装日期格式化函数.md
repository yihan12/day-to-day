```javascript
// 封装日期格式化函数
const date = new Date('2021-4-12 10:22:22');
function dateFormat (date, format = 'YYYY-MM-DD HH:mm:ss') {
    const config = {
        YYYY: date.getFullYear(),
        MM: date.getMonth()+1,//getMonth() 方法根据本地时间返回指定日期的月份（从 0 到 11）
        DD: date.getDate(),
        HH: date.getHours(),
        mm: date.getMinutes(),
        ss: date.getSeconds(),
    }
    for(const key in config){
        format = format.replace(key, config[key])
    }
    return format
}
console.log(dateFormat(date)); // 2021-4-12 10:22:22
console.log(dateFormat(date, 'YYYY年MM月DD日')); // 2021年4月12日
console.log(dateFormat(date, 'YYYY年MM月DD日 HH时mm分ss秒')); // 2021年4月12日 10时22分22秒
```
