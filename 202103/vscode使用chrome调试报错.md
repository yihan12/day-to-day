### 问题 

> vscode使用chrome调试报错"无法访问您的文件"或者"localhost 拒绝了我们的连接请求"。

### 解决 

ctrl+p  搜索launch.json文件 

改为：

```javascript
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "使用本机 Chrome 调试",
      "type": "chrome",
      "request": "launch",
        "file": "${file}",
      // "runtimeExecutable": "C:\\Program Files (x86)\\Google\\Chrome\\Application\\chrome.exe", // 改成您的 Chrome 安装路径
      "sourceMaps": true,
      "webRoot": "${workspaceRoot}",
      "userDataDir":"${tmpdir}",
      "port":9222
    }
  ]
}
```
