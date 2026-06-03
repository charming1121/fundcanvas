# FundCanvas 开发交接说明

## 项目概览

本交付包是 FundCanvas 基金营销生图平台的静态原型版本。当前重点演示 id69 广发基金参考帖的完整 H5 长图流程：从参考图库识别配置，到文案预览，再到按功能区切分、逐区生成、最终拼接和单区重绘。

当前版本没有后端服务，API 调用相关函数已保留在前端代码中，开发上线时应迁移到后端代理或业务服务。

## 核心文件

- `index.html`：主应用，包含 HTML、CSS 和业务 JS。
- `assets/reference/fundcanvas_reference_dataset.js`：参考图库数据，提供 `window.FUNDCANVAS_REF_DATA`。
- `assets/h5-demo/long_poster_function_cuts/`：id69 原参考长图的功能切片。
- `assets/h5-demo/guangfa_hengrong_section_cuts/`：用户提供的生图后 5 个功能区结果。
- `assets/vendor/html2canvas.min.js`：本地化的导出依赖。

## id69 Demo 流程

1. 从参考图库选择 id69 广发基金财富号 H5 参考帖。
2. 系统识别基础配置：财富号、单图、H5 海报、产品推介。
3. AI 需求助手根据参考帖填充适合 H5 产品推介的需求建议。
4. 用户确认文字预览后点击生图。
5. 系统先展示参考长图按功能区切分的结果。
6. 逐区注入 5 个生图后结果：头图区、数据解读区、策略背书区、产品要素区、风险提示区。
7. 所有功能区确认后拼接成最终 H5 长图。
8. 每个功能区可单独查看详情，并支持单区重绘示意。

## 关键状态与函数

- `state.canvasPreviewMode`：控制 `reference`、`module`、`result` 三种预览状态。
- `state.h5DemoGeneratedSections`：保存 5 个功能区的生图后结果。
- `state.h5DemoCollapsedSections`：控制功能区折叠状态。
- `state.h5DemoExpandedSection`：控制当前展开的功能区。
- `isGuangfaWealthProductH5DemoItem(post)`：判断是否命中 id69 H5 demo。
- `buildAssistantDraft(userText)`：AI 需求助手建议生成。
- `getH5DemoSectionList()`：定义 5 个业务功能区。
- `startGuangfaProductH5CutDemo()`：启动切分、逐区生图、拼接的 demo 流程。
- `buildGuangfaProductH5CutStitchData(forceRebuild)`：构建最终拼接长图数据。
- `simulateH5SectionRedraw(sectionKey)`：单功能区重绘示意。
- `openCanvasReferenceDetail(mode, sectionKey, partId)`：打开整图、参考区或生图区详情。

## API 接入建议

前端中保留了这些 API 相关函数，适合开发时改造成后端代理调用：

- `buildSysPrompt(...)`：组装大模型系统提示词和用户需求。
- `callLLM(...)`：调用文本模型，生成结构化文案和配置。
- `callImgAPI(...)`：调用文生图接口。
- `callImgEditAPI(...)`：调用图生图或局部编辑接口。

上线时不建议在浏览器里暴露任何模型 API Key。建议新增后端接口，例如：

- `POST /api/assistant/draft`：根据用户需求和参考帖返回配置与文案草稿。
- `POST /api/generation/image`：生成单张图或功能区图片。
- `POST /api/generation/edit-section`：对指定功能区做局部重绘。
- `POST /api/assets/upload`：上传参考图和生成结果，返回站内资源 URL。

## 生产化 TODO

- 将单文件原型拆成组件化前端工程，例如 Vite + React 或 Vue。
- 将本地 mock/demo 资源接入正式素材库、对象存储或 CDN。
- 将 `fundcanvas_reference_dataset.js` 替换为后端接口返回。
- 将模型调用迁移到服务端，统一鉴权、限流、审计和错误处理。
- 为生图任务增加异步队列、任务状态、失败重试和结果持久化。
- 为 H5 长图拼接接入真实图像处理服务，避免只在前端做视觉示意。
- 增加基金合规审核流，尤其是收益、风险、业绩、免责声明相关内容。
- 增加浏览器兼容测试和移动端适配测试。
