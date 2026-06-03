# Package Manifest

## Included

- `index.html`：FundCanvas 静态原型入口。
- `README.md`：交付包快速说明。
- `docs/DEV_HANDOFF.md`：开发交接说明。
- `docs/DEPLOYMENT.md`：部署说明和上线检查。
- `assets/reference/fundcanvas_reference_dataset.js`：参考图库数据。
- `assets/vendor/html2canvas.min.js`：前端导出依赖。
- `assets/h5-demo/long_poster_function_cuts/`：原始 H5 长图功能区参考切片。
- `assets/h5-demo/guangfa_hengrong_section_cuts/`：生图后 5 个功能区切片。

## Not Included

- 后端服务。
- 数据库。
- 模型 API Key。
- 正式用户鉴权。
- 正式素材库或对象存储配置。

## Packaging Notes

- 交付包已移除本机 `C:\Users\86137\Downloads` 绝对路径依赖。
- 交付包已移除 H5 demo 静态资源中的 `file:///` 引用。
- CDN 依赖已改为本地 `assets/vendor/html2canvas.min.js`。
