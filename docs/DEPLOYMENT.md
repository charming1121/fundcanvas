# FundCanvas 部署说明

## 部署方式

本交付包是静态站点，可以直接部署整个目录。

本地预览：

```powershell
cd C:\Users\86137\Downloads\fundcanvas-deploy-20260531-200245
npx serve .
```

nginx 示例：

```nginx
server {
  listen 80;
  server_name fundcanvas.example.com;

  root /var/www/fundcanvas-deploy;
  index index.html;

  location / {
    try_files $uri $uri/ /index.html;
  }

  location /assets/ {
    try_files $uri =404;
    expires 7d;
  }
}
```

## 静态资源要求

`index.html` 依赖以下相对路径，部署时必须保持目录结构不变：

```text
./assets/reference/fundcanvas_reference_dataset.js
./assets/vendor/html2canvas.min.js
./assets/h5-demo/long_poster_function_cuts/
./assets/h5-demo/guangfa_hengrong_section_cuts/
```

若资源改放 CDN 或对象存储，需要同步修改 `index.html` 中这些常量：

- `H5_DEMO_CUT_BASE`
- `H5_DEMO_GENERATED_SECTION_BASE`
- 参考数据 `<script src="./assets/reference/fundcanvas_reference_dataset.js"></script>`
- html2canvas `<script src="./assets/vendor/html2canvas.min.js"></script>`

## 上线前检查

- 页面能打开，控制台没有 404 和脚本错误。
- 参考图库能看到 id69 广发基金参考帖。
- 应用参考后，基础配置识别为财富号、单图、H5 海报、产品推介。
- 点击确认文案并生图后，右侧出现 5 个功能区。
- 5 个生图后功能区图片都能加载。
- 最终拼接长图可以显示。
- 每个功能区详情页可以打开。
- 单区重绘按钮能触发示意状态。
- 导出图片功能可用。

## 安全与后端接入

当前包用于前端 demo 和开发交接，不应直接在公网版本中写入模型 API Key。

生产环境建议：

- 前端只调用业务后端接口。
- 后端保存和调用模型 API Key。
- 后端对图片上传、生成任务和用户身份做鉴权。
- 大图与生成结果落对象存储，通过签名 URL 或 CDN 访问。
- 对基金营销内容增加合规审核、敏感词检查和免责声明校验。

## 常见问题

### 图片 404

检查部署后 `assets/h5-demo` 是否完整上传，尤其是中文文件名是否被服务器正确保留。

### 导出失败

确认 `assets/vendor/html2canvas.min.js` 存在并可访问。若存在跨域图片，服务器需要正确配置 CORS。

### 参考图库为空

确认 `assets/reference/fundcanvas_reference_dataset.js` 可访问，并且脚本执行后存在 `window.FUNDCANVAS_REF_DATA`。
