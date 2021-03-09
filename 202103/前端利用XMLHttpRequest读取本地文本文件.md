### 问题 

> 前端常见是通过input按钮上传读取文件信息，此时知道本地文件路径需要直接js读取本地文件内的信息

### 注意 

本地测试，需要解决本地浏览器跨域问题，如：
![浏览器跨域问题](https://img-blog.csdnimg.cn/20210309224219638.png)


可查看此链接解决：
[解决本地浏览器运行项目是的跨域问题](https://blog.csdn.net/weixin_38545763/article/details/103800676)


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
    xhrFile.send();
}
const filePath = `E:/学习/JavaScript/txt.txt`
readTextFile(filePath, (textDetail) => {
    console.log(textDetail)
})
```
