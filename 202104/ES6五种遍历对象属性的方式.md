ES6五种遍历对象属性的方式
```javascript
function allObj(){
  this.name = '张三'; // 自有属性
  this.age = '12'; // 自有属性
  this.invisible = {
    enumerable: false,
    value: 'hello'
  },
  this.invisible = {
    enumerable: false,
    value: 'hello'
  }
}
allObj.prototype.disEnum = {
  enumerable: false,
  value: 'disEnum'
}
allObj.prototype.Enum = {
  enumerable: true,
  value: 'Enum'
}
let obj = new allObj
Object.assign(obj, {
  a: '1',
  b: '2',
  c: '3',
  [Symbol('c')]: 'c',
})
Object.assign(obj,
  Object.defineProperty({}, 'visible',{
    enumerable: true,
    value: 'word'
  })
)
console.log(obj); // allObj {a: "1",age: "12",b: "2",c: "3",invisible: {enumerable: false,value: 'hello'},name: "张三",visible: "word",Symbol(c): "c",__proto__:Enum: {enumerable: true, value: "Enum"},disEnum: {enumerable: false, value: "disEnum"}}
// for...in循环遍历对象自身的和继承的属性（不含Symbol属性）
for(let key in obj){
  console.log(key);
  // name
  // age
  // invisible
  // a
  // b
  // c
  // invisible
  // visible
  // disEnum
  // Enum
}

// Object.keys()返回一个数组，包括对象自身(不含继承的)的所有属性（不含Symbol属性）
console.log(Object.keys(obj)); // ["name", "age", "invisible", "a", "b", "c", "visible"]

// Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含Symbol属性，但是包括不可枚举属性 ）
console.log(Object.getOwnPropertyNames(obj)); // ["name", "age", "invisible", "a", "b", "c", "visible"]

// Object.getOwnPropertySymbols() 返回一个数组，包含所有对象自身的所有Symbol属性
console.log(Object.getOwnPropertySymbols(obj)); // [Symbol(c)]

// Reflect.ownKeys()返回一个数组，包含对象自身的所有属性，不管属性名是Symbol还是字符串，也不管是否可枚举
console.log(Reflect.ownKeys(obj)); // ["name", "age", "invisible", "a", "b", "c", "visible", Symbol(c)]
```

解决`for..in`遍历对象时,原型链上的所有属性都将被访问  

```javascript
function allObj(){
  this.name = '张三'; // 自有属性
  this.age = '12'; // 自有属性
  this.invisible = {
    enumerable: false,
    value: 'hello'
  },
  this.invisible = {
    enumerable: false,
    value: 'hello'
  }
}
allObj.prototype.disEnum = {
  enumerable: false,
  value: 'disEnum'
}
allObj.prototype.Enum = {
  enumerable: true,
  value: 'Enum'
}
let obj = new allObj
Object.assign(obj, {
  a: '1',
  b: '2',
  c: '3',
  [Symbol('c')]: 'c',
})
Object.assign(obj,
  Object.defineProperty({}, 'visible',{
    enumerable: true,
    value: 'word'
  })
)
console.log(obj);
for(let key in obj){
  if(obj.hasOwnProperty(key)===true){
    console.log(key);
    // name
    // age
    // invisible
    // a
    // b
    // c
    // visible
  }
}
```
