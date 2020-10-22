### Object.assign()

> Object.assign() 方法用于将所有可枚举属性的值从一个或多个源对象分配到目标对象。它将返回目标对象。

### 更新对象

```javascript
const target = { a: 1, b: 2 };
const source = { b: 4, c: 5 };

const returnedTarget = Object.assign(target, source);

console.log(target); // { a: 1, b: 4, c: 5 }

console.log(returnedTarget); // { a: 1, b: 4, c: 5 }
```

### 复制一个对象

```javascript
const obj = { a: 1, b: 2, c: 3 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1, b: 2, c: 3 }
```

### 合并对象

```
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const obj3 = { c: 3 };

const obj = Object.assign(obj1, obj2, obj3);
console.log(obj1); // { a: 1, b: 2, c: 3 }
console.log(obj);  // { a: 1, b: 2, c: 3 }, 目标对象自身也会改变。
```

### 拷贝

> Object.assign拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）。

```javascript

Object.assign({b: 'c'},
	Object.defineProperty({}, 'invisible', {
		enumerable: false,
		value: 'hello'
	})
)
// { b: 'c' }
```

### 属性名为 Symbol 值的属性，也会被Object.assign拷贝

```javascript
Object.assign({ a: 'b', b: 'c'}, { [Symbol('c')]: 'd' })
// { a: 'b', b: 'c', Symbol(c): 'd' }
```

### 总结

1.为对象添加属性

```javascript
class Point {
	constructor(x, y) {
		Object.assign(this, {x, y});
	}
}
```

2.为对象添加方法

```javascript
Object.assign(mainContent.prototype, {
	oneMethod(arg1, arg2) {
	},
	anotherMethod() {
	}
});
```

等同于下面的写法

```javascript
mainContent.prototype.oneMethod = function (arg1, arg2) {
};
mainContent.prototype.anotherMethod = function () {
};
```

3.复制一个对象

```javascript
const obj = { a: 1, b: 2, c: 3 };
const copy = Object.assign({}, obj);
console.log(copy); // { a: 1, b: 2, c: 3 }
```

4.合并对象

```
const obj1 = { a: 1 };
const obj2 = { b: 2 };
const obj3 = { c: 3 };

const obj = Object.assign(obj1, obj2, obj3);
console.log(obj1); // { a: 1, b: 2, c: 3 }
console.log(obj);  // { a: 1, b: 2, c: 3 }, 目标对象自身也会改变。
```

5.为属性指定默认值

```javascript
const DEFAULTS = {
	logLevel: 0,
	outputFormat: 'html'
};
function processContent(options) {
	let options = Object.assign({}, DEFAULTS, options);
}
```

### MDN

拷贝访问器

```
const obj = {
  foo: 1,
  get bar() {
    return 2;
  }
};

let copy = Object.assign({}, obj); 
console.log(copy); // { foo: 1, bar: 2 } copy.bar的值来自obj.bar的getter函数的返回值

// 下面这个函数会拷贝所有自有属性的属性描述符
function completeAssign(target, ...sources) {
  sources.forEach(source => {
    let descriptors = Object.keys(source).reduce((descriptors, key) => {
      descriptors[key] = Object.getOwnPropertyDescriptor(source, key);
      return descriptors;
    }, {});

    // Object.assign 默认也会拷贝可枚举的Symbols
    Object.getOwnPropertySymbols(source).forEach(sym => {
      let descriptor = Object.getOwnPropertyDescriptor(source, sym);
      if (descriptor.enumerable) {
        descriptors[sym] = descriptor;
      }
    });
    Object.defineProperties(target, descriptors);
  });
  return target;
}

copy = completeAssign({}, obj);
console.log(copy);
// { foo:1, get bar() { return 2 } }
```
