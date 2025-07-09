如果网页可以正常访问视频（例如直接打开链接能播放），但使用 `<video>` 标签无法播放，可能是以下几个原因导致的：

---

## **1. CORS（跨域资源共享）问题**
即使视频能直接访问，但 `<video>` 标签加载跨域资源时，浏览器会检查 CORS 头。如果 OSS 未正确配置 CORS，浏览器会阻止加载。

### **检查方法**
- 在 Chrome DevTools（F12）的 **Network** 选项卡中查看视频请求：
  - 检查响应头是否包含：
    ```http
    Access-Control-Allow-Origin: *
    Access-Control-Allow-Methods: GET, HEAD
    ```
  - 如果没有，说明 OSS 未正确配置 CORS。

### **解决方案**
在阿里云 OSS 控制台，为 Bucket 添加 CORS 规则：
```json
[
  {
    "AllowedOrigin": ["*"],
    "AllowedMethod": ["GET", "HEAD"],
    "AllowedHeader": ["*"],
    "ExposeHeader": [],
    "MaxAgeSeconds": 3600
  }
]
```
保存后，等待几分钟生效，然后刷新页面测试。

---

## **2. MIME 类型不正确**
如果 OSS 返回的 `Content-Type` 不是 `video/mp4`，浏览器可能拒绝播放。

### **检查方法**
- 在 Chrome DevTools 的 **Network** 选项卡查看视频请求的响应头：
  ```http
  Content-Type: video/mp4
  ```
  - 如果不是 `video/mp4`（例如 `application/octet-stream`），需要修正。

### **解决方案**
在阿里云 OSS 控制台：
1. 找到该视频文件，进入 **文件管理**。
2. 设置 **HTTP 头**，手动指定 `Content-Type: video/mp4`。

---

## **3. 视频编码格式问题**
某些浏览器对 MP4 的编码格式（如 H.264、H.265）有要求，如果视频编码不兼容，可能导致无法播放。

### **检查方法**
- 使用 `ffprobe`（FFmpeg 工具）检查视频编码：
  ```bash
  ffprobe -v error -show_format -show_streams "视频文件.mp4"
  ```
  - 检查 `codec_name` 是否是 `h264`（兼容性最好）。

### **解决方案**
如果视频编码不是 H.264，可以用 FFmpeg 转码：
```bash
ffmpeg -i input.mp4 -c:v libx264 -c:a aac output.mp4
```
然后重新上传到 OSS。

---

## **4. 浏览器缓存问题**
有时浏览器缓存了错误的响应，导致 `<video>` 无法加载。

### **解决方案**
- **强制刷新**（Ctrl + F5）测试。
- **使用无痕模式**（排除插件干扰）。
- **在 `<video>` 标签的 URL 后加随机参数**，避免缓存：
  ```html
  <video controls>
    <source src="https://your-video-url.mp4?t=123456" type="video/mp4">
  </video>
  ```

---

## **5. `<video>` 标签写法问题**
确保 `<video>` 标签正确使用 `controls` 和 `<source>`：
```html
<video controls width="600">
  <source src="https://your-video-url.mp4" type="video/mp4">
  您的浏览器不支持 HTML5 视频
</video>
```
如果仍然不行，可以尝试：
```html
<video src="https://your-video-url.mp4" controls></video>
```

---

## **6. HTTPS 混合内容问题**
如果网页是 HTTPS，但视频是 HTTP，浏览器会阻止加载。

### **解决方案**
确保视频 URL 也是 HTTPS：
```html
<video src="https://your-video-url.mp4" controls></video>
```

---

## **7. 防盗链问题**
如果 OSS 启用了 **Referer 防盗链**，可能导致 `<video>` 无法加载。

### **解决方案**
在 OSS 控制台检查 **Bucket 防盗链** 设置：
- 确保 **空 Referer** 允许访问。
- 或者添加你的网站域名到白名单。

---

## **8. 测试方法**
### **（1）直接访问视频 URL**
在浏览器地址栏输入视频 URL，看是否能播放：
- ✅ 能播放 → 可能是 CORS 或 `<video>` 标签问题。
- ❌ 不能播放 → 可能是 OSS 权限、文件损坏或 URL 错误。

### **（2）用 `curl` 检查响应头**
```bash
curl -I "https://your-video-url.mp4"
```
检查：
- `HTTP/2 200`（状态码）
- `Access-Control-Allow-Origin: *`（CORS）
- `Content-Type: video/mp4`（MIME 类型）

---

## **总结**
| 问题 | 检查方法 | 解决方案 |
|------|---------|---------|
| **CORS 问题** | DevTools 看 `Access-Control-Allow-Origin` | 在 OSS 设置 CORS |
| **MIME 类型错误** | DevTools 看 `Content-Type` | 在 OSS 手动设置 `video/mp4` |
| **视频编码不兼容** | `ffprobe` 检查编码 | 转码为 H.264 |
| **浏览器缓存** | 无痕模式测试 | 加随机参数 `?t=123` |
| **HTTPS 混合内容** | 检查 URL 协议 | 确保视频是 HTTPS |
| **防盗链问题** | 直接访问测试 | 调整 OSS 防盗链设置 |

如果仍然无法解决，可以提供：
- **浏览器控制台错误截图**
- **`curl -I "视频URL"` 的输出**
- **视频编码信息（`ffprobe` 结果）**

这样能更精准定位问题！ 🚀


# 终极修改
下载ffmpeg,操作转化格式
```
ffmpeg -i 1728898660108-P10PROMAX.mp4 -vcodec libx264 -acodec aac outfile.mp4
```


# 参考链接
- [x] [iOS 音视频(一) - 基础知识](https://www.jianshu.com/p/80a4348982c8)
