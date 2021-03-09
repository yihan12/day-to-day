### 问题 

> 前端常见是通过input按钮上传读取文件信息，此时知道本地文件路径需要直接js读取本地文件内的信息

### 解决 

利用XMLHttpRequest获取到文件的信息。

```javascript
/**
 * XMLHttpRequest.open() 初始化请求参数
 * XMLHttpRequest.send() 发送网络请求
 * XMLHttpRequest.onload() 监听请求结果
 * XMLHttpRequest.responseType 对响应结果进行声明，来对结果自动进行处理(text,json,blob,document)
 * XMLHttpRequest.onerror() 请求中断等错误发生时的处理
 * XMLHttpRequest.status 为HTTP状态码 如 404/422/403等，当为200时为正确响应
 * XMLHttpRequest.statusText HTTP状态码内容，200时为ok,404 为Not Found
 * XMLHttpRequest.response 服务器端响应的内容
 */
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
