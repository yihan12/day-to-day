### 问题

>webpack 报错(Cannot find moudle 'webpack-cli/bin/config-yargs')

### 解决

webpack和webpack-dev-server版本兼容

webpack 3.5.5 webpack-dev-server 2.7.1可以用。


```javascript
npm uninstall webpack -D
npm uninstall webpack-dev-server -D
```

然后执行

```javascript
npm i webpack@3.5.5 -D
npm i webpack-dev-server@2.7.1 -D
```
