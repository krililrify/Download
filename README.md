# KRI Download Web

静态 HTML 文件分发页面，可直接部署到 Cloudflare Pages。

## 使用

1. 把本仓库连接到 Cloudflare Pages（无需构建命令，输出目录 `/`）。
2. 在 `index.html` 修改 `CONFIG.workerApi` 和 `CONFIG.turnstileSiteKey`。
3. 在 Cloudflare Turnstile 的允许域名中添加 Pages 正式域名。
4. Worker 接口约定：`POST /authorize`，请求 JSON `{ "file": "karing_android.apk", "turnstileToken": "..." }`，响应 `{ "url": "https://..." }`。
5. Worker 必须服务端调用 Turnstile Siteverify 校验 Token，核对 hostname，校验文件白名单，生成十分钟有效的签名下载地址。VPS 也必须校验签名。

注意：本仓库只有前端，Worker 与 VPS 下载接口未部署前，按钮不能实际下载。不得在前端放置 Turnstile Secret 或下载签名密钥。
