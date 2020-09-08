### let str=true+11+null+9+undefined+"javascript"+false+null+9+[]+[" "]计算str

```javascript
console.log(true+11) //12

console.log(12+null) //12

console.log(12+9) //21

console.log(21+undefined) //NaN

console.log(NaN+"javascript") //"NaNjavascript"

console.log("NaNjavascript" +false) //"NaNjavascriptfalse"

console.log("NaNjavascriptfalse"+null) //"NaNjavascriptfalsenull"

console.log("NaNjavascriptfalsenull"+9) //"NaNjavascriptfalsenull9"

console.log("NaNjavascriptfalsenull9"+[]) //"NaNjavascriptfalsenull9"

console.log("NaNjavascriptfalsenull9"+[" "] //"NaNjavascriptfalsenull9 "
```

### Number()

```javascript
console.log(Number("hello word")); //NaN

console.log(Number("")); //0

console.log(Number("000011")); //11

console.log(Number("true")); //NaN

console.log(Number(true)); //1

console.log(parseInt([3,2,3])); //3

console.log(parseFloat([1,2,3])); //1
```

### 数字,字符串计算

```javascript
console.log(10 + "10"); //"1010"

console.log("10" + "10"); //"1010"

console.log(+"10"+ + "10"); //20

console.log((+"10") + (+"10")); // 20

console.log(-"10"+ 10); //0
```
