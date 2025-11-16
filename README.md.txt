# AI ID Photo - Demo (Static, frontend-only)

这是一个**演示版静态网站**，用于向投资人展示产品流程：用户上传自拍 → 选择尺寸/背景 → 生成证件照 PDF → 生成打印提取码（演示）。  
演示版不调用付费AI API，所有图像处理在浏览器上完成（裁剪+背景覆盖），用于展示流程与 UX。

## 功能（Demo）
- 中/日/英 三种语言切换
- 上传照片、选择尺寸（30×40 / 35×45 / 40×50）
- 预览与高分辨率 PDF 下载
- 生成随机打印提取码（演示）

## 如何部署到 GitHub Pages
1. 在 GitHub 上新建一个仓库，例如 `ai-idphoto-mvp`。
2. 将本项目文件 (index.html, styles.css, app.js, README.md, assets/) 推送到该仓库。
3. 在仓库 Settings → Pages 中选择 `main` 分支，/ 根目录 (/) 并保存。
4. 等待几分钟，GitHub Pages 将生成一个 `https://<your-username>.github.io/<repo>/` 的演示地址。

## 如何把 Demo 替换为“真实后端 + AI”版本（要点）
**不要在前端保存 API Key！** 实际上需要一个后端来调用 remove.bg / PhotoRoom 等服务并返回处理后图像或 PDF。

流程建议：
1. 用户上传图片（前端上传到你的后端或直接上传到临时存储，如 S3）。
2. 后端将图片发给 remove.bg / PhotoRoom（需 API Key），得到透明背景或抠图结果。
3. 后端使用图像库（Pillow / OpenCV）合成背景、调整头部比例并生成高分辨率 JPG/PDF。
4. 后端把文件存到云端（S3 / Cloudinary）并返回下载链接或调用便利店 API 上传并获取打印码。
5. 前端显示下载链接或打印提取码给用户。

## 进一步建议与注意事项
- 生产环境要实现「用户图片的自动删除策略（例如 24 小时后删除）」。  
- 需准备好隐私政策、利用規約（法律合规）。  
- 若要对接便利店（NetPrint / PrintSmash），请先与相关系统提供商或便利店总部确认文件格式、API 使用方式与费用。  
- 若后端使用 Node/Python，我可以帮你提供示例代码（如何安全调用 remove.bg 并生成 PDF）。

## 联系
如果需要我帮你把 demo 上线到 GitHub Pages，或帮助写后端示例代码（Node / Python）来对接 remove.bg / PhotoRoom，请联系: email@example.com
