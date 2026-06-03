# FundCanvas Deploy Package

这是 FundCanvas 原型的可部署静态交付包，用于给开发人员完成后续上线改造。

## 快速启动

```powershell
cd C:\Users\86137\Downloads\fundcanvas-deploy-20260531-200245
npx serve .
```

也可以直接用 nginx、OSS 静态站点、S3/CloudFront 或任意静态文件服务托管本目录。

## 目录

```text
index.html
assets/
  reference/
    fundcanvas_reference_dataset.js
  vendor/
    html2canvas.min.js
  h5-demo/
    long_poster_function_cuts/
    guangfa_hengrong_section_cuts/
docs/
  DEV_HANDOFF.md
  DEPLOYMENT.md
```

## 当前交付内容

- 单文件前端原型：参考图库、AI 需求助手、基础配置、文字预览、画布预览、导出。
- id69 广发基金 / 蚂蚁财富号 / H5 长图 / 产品推介 demo。
- H5 demo 支持参考图功能区切分、逐区生图结果展示、最终拼接、单区重绘示意。
- 所有 demo 资源已改为相对路径，不依赖本机 Downloads 路径。

## 给开发人员的入口文档

- `docs/DEV_HANDOFF.md`：业务流程、关键函数、API 接入建议。
- `docs/DEPLOYMENT.md`：静态部署、路径检查、上线校验清单。
