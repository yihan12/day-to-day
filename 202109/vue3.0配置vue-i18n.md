### 项目安装vue-i18n  

```javascript
npm install vue-i18n --save
```

或者用yarn
```javascript
yarn add vue-i18n --save
```

### 在项目src文件夹中新建lang文件夹

新建lang文件夹，在lang文件夹中新建三个js文件:

zh-CN.js  
```javasctipt
module.exports = {
  header:{
    text:'学习'
  }
}
```

zh-TW.js  
```javasctipt
module.exports = {
  header:{
    text:'學習'
  }
}
```

index.js  
```javascript
import { createI18n } from 'vue-i18n'

import zh_CN from './zh-CN'
import zh_TW from './zh-TW'

// 语言库
const messages = {
  'zh-CN': zh_CN,
  'zh-TW': zh_TW
}

// 默认语言
// const langDefault = 'zh-CN'
const langDefault = 'zh-TW'
const i18n = createI18n({
  locale: langDefault,		//默认显示的语言 
  messages
})

export default i18n; // 将i18n暴露出去，在main.js中引入挂载
```

### 将i18n暴露出去，在main.js中引入挂载

main.js  
```javascript
import i18n from './lang'
import { createApp } from "vue";
import App from "./App.vue";

const app = createApp(App); // 创建实例

app.use(i18n);
app.mount("#app");
```

### 页面中使用  

```javascript
{{$t('header.text')}}
```

