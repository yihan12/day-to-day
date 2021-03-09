### 问题 

> 前端常见是通过input按钮上传读取文件信息，此时知道本地文件路径需要直接js读取本地文件内的信息

### 解决 

利用XMLHttpRequest获取到文件的信息。

```javascript
function readTextFile(filePath, callback) {
  const xhrFile = new XMLHttpRequest();
  xhrFile.open("GET", filePath, true);
  xhrFile.onload  = function() {
      const allText = xhrFile.response;
      callback(allText)
  }
  rawFile.send();
}
const filePath = "D://123/123.txt"
readTextFile(filePath, (textDetail) => {
  console.log(textDetail)
})
```
