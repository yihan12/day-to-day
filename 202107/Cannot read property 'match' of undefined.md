### 问题

> Cannot read property 'match' of undefined

### 解决

1.一般解决：删除 package-lock.json，重新启动
如果还是不能解决，执行第二部


2.最终处理  
```javascript
rm -rf node_modules
rm package-lock.json
npm cache clear --force
npm install
```

然后重新启动
