### 问题描述
>  解决JS处理api返回number字段精度丢失问题:前端在ajax方式调用第三方接口时出现了一个诡异的问题，同一个接口url通过axios访问接口获取到的数据与浏览器访问的数据id不一致

### 解决代码

```javascript
const something = `/123/123`
export function getsomething (data) {
  return request({
    headers: {
      "Authorization": getToken(),
    },
    method: "post",
    url: `${something}/query`,
    params: data,
    // 将对应返回的属性的数据修改
    transformResponse: [response => JSON.parse(response.replace(/("orderUserId":)(\d{0,})(,)/g, '$1' + '"' + '$2' + '"' + '$3').replace(/("id":)(\d{0,})(,)/g, '$1' + '"' + '$2' + '"' + '$3'))]
  })
}
```
