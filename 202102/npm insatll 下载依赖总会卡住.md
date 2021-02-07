### 问题  

```javascript
npm ERR! code ENOTFOUND
npm ERR! errno ENOTFOUND
npm ERR! network request to https://registry.npmjs.org/babel-plugin-import failed, reason: getaddrinfo ENOTFOUND registry.npmjs.org registry.npmjs.org:443
npm ERR! network This is a problem related to network connectivity.
npm ERR! network
npm ERR! network If you are behind a proxy, please make sure that the
npm ERR! network 'proxy' config is set properly.  See: 'npm help config'

npm ERR! A complete log of this run can be found in:
npm ERR!     C:\Users\xdu\AppData\Roaming\npm-cache\_logs\2020-03-18T13_41_41_721Z-debug.log
```

### 解决 

把代理去掉
```javascript
npm config set proxy null
```
