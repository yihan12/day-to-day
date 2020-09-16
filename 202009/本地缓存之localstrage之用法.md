HTML5中，新加入了一个localStorage特性，这个特性主要是用来作为本地存储来使用的，解决了cookie存储空间不足的问题(cookie中每条cookie的存储空间为4k)，localStorage中一般浏览器支持的是5M大小，这个在不同的浏览器中localStorage会有所不同。

### 1.储存数据,更改数据

```javascript
localStorage.setItem('Token',  res.data.result.accessToken)
localStorage.setItem('Token',  res.data.result.newAccessToken)
```

### 2.取出数据

```javascript
localStorage.getItem('Token')
```

### 3.删除储存数据

```javascript
localStorage.removeItem('Token')
```
