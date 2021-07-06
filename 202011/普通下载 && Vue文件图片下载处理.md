一般的下载,也就a标签加个链接地址,标签内加个download属性.  当地址是后端提供时:可通过创建a标签, 随即给a便签附下载链接,文件名和属性, 最后再创建点击效果,最后清楚生成的a标签.  再则是图片地址提供:可以通过Base64加canvas,对图片的下载可以进行处理. 下面就是相关方法处理函数  HTML与文件下载

### HTML与文件下载

```html
<a href="large.jpg" download>下载</a>
```

### 文件下载配合后端表格导出

```javascript
export function downloadFile(url, filename) {
    // 创建隐藏的可下载链接
    let link = document.createElement('a');
    link.href = url;
    link.download = filename;
    link.target = '_blank';
    link.style.display = 'none';
    document.body.appendChild(link);
    // 触发点击
    link.click();
      // 然后移除
    document.body.removeChild(link);
    link = null;
}
```

### 加参数:

```javascript
export function generateQS(baseurl, paramObj) {
    let returnUrl = baseurl + '?'
    for (const key in paramObj) {
    // Object.hasOwnProperty(prop)用来判断对象是否含有指定属性
    // 返回值boolean
        if (paramObj.hasOwnProperty(key)) {
            const element = paramObj[key];
            returnUrl += key + '=' + element + '&';
        }
    }
    return returnUrl;
}
```

### 借助HTML5 Blob实现文本信息文件下载

```javascript
const funDownload = function (content, filename) {
    // 创建隐藏的可下载链接
    let eleLink = document.createElement('a');
    eleLink.download = filename;
    eleLink.style.display = 'none';
    // 字符内容转变成blob地址
    let blob = new Blob([content]);
    eleLink.href = URL.createObjectURL(blob);
    // 触发点击
    document.body.appendChild(eleLink);
    eleLink.click();
    // 然后移除
    document.body.removeChild(eleLink);
};
```

### 借助Base64实现任意文件下载

```javascript
let funDownload = function (domImg, filename) {
    // 创建隐藏的可下载链接
    let eleLink = document.createElement('a');
    eleLink.download = filename;
    eleLink.style.display = 'none';
    // 图片转base64地址
    let canvas = document.createElement('canvas');
    let context = canvas.getContext('2d');
    let width = domImg.naturalWidth;
    let height = domImg.naturalHeight;
    context.drawImage(domImg, 0, 0);
    // 如果是PNG图片，则canvas.toDataURL('image/png')
    eleLink.href = canvas.toDataURL('image/jpeg');
    // 触发点击
    document.body.appendChild(eleLink);
    eleLink.click();
    // 然后移除
    document.body.removeChild(eleLink);
};
```

### HTML Blob文件下载优化

```javascript
export const downloadFile = (blob, fileanme) => {
  // 兼容IE和EDGE无法打开Blob URL链接方法
  if (typeof window.navigator.msSaveBlob !== 'undefined') {
    window.navigator.msSaveBlob(blob, fileanme)
  } else {
    let URL = window.URL || window.webkitURL;
    // 使用获取到的blob对象创建的blobUrl
    const blobUrl = URL.createObjectURL(blob);
    const a = document.createElement('a');
    if (typeof a.download === 'undefined') {
      window.location = blobUrl
    } else {
      document.body.appendChild(a)
      a.style.display = 'none'

      a.href = blobUrl;
      // 指定下载的文件名
      a.download = fileanme;
      a.click();
      document.body.removeChild(a)
      // 移除blob对象的blobUrl
      URL.revokeObjectURL(blobUrl);
    }
  }
}
```

### 结束语

在Chrome浏览器下，模拟点击创建的a元素即使不append到页面中，也是可以触发下载的，但是在Firefox浏览器中却不行，因此，上面的funDownload()方法有一个appendChild和removeChild的处理，就是为了兼容Firefox浏览器。

[普通下载 && Vue文件图片下载处理](https://github.com/yihan12/day-to-day/blob/master/202011/%E6%99%AE%E9%80%9A%E4%B8%8B%E8%BD%BD%20%26%26%20Vue%E6%96%87%E4%BB%B6%E5%9B%BE%E7%89%87%E4%B8%8B%E8%BD%BD%E5%A4%84%E7%90%86.md)
