# img-cdn

固定 URL 图片托管仓库。用途：给 HTML / 文档提供**永久不变**的公网图片地址，同时允许随时替换图片内容。

## 核心机制

**URL 只取决于「用户名 / 仓库 / 分支 / 文件路径」，与文件内容无关。**
所以只要**覆盖同名文件**（老图被新图顶替），URL 永远不变，引用它的页面无需改动。

## 访问地址

| 方式 | URL 模板 | 特性 |
|---|---|---|
| jsDelivr CDN（推荐） | `https://cdn.jsdelivr.net/gh/MuchA533753/img-cdn@main/<path>` | 全球 CDN，带 CORS 头，可主动刷缓存 |
| GitHub Pages | `https://MuchA533753.github.io/img-cdn/<path>` | 覆盖后约 10 分钟内生效 |
| GitHub raw | `https://raw.githubusercontent.com/MuchA533753/img-cdn/main/<path>` | 有速率限制，不建议用于正式页面 |

## 已有资源

| 路径 | jsDelivr 直链 | 说明 |
|---|---|---|
| `qr/coolhunter-cli.png` | `https://cdn.jsdelivr.net/gh/MuchA533753/img-cdn@main/qr/coolhunter-cli.png` | 酷家乐 CLI 使用与反馈交流群 二维码，1080×1080，有效期 7 天，需每周覆盖更新 |

## 更新流程（URL 不变）

```bash
cd /path/to/img-cdn
cp <新图片> qr/coolhunter-cli.png     # 同名覆盖
git add -A && git commit -m "update qr/coolhunter-cli.png"
git push
curl "https://purge.jsdelivr.net/gh/MuchA533753/img-cdn@main/qr/coolhunter-cli.png"
```

最后一行是刷新 jsDelivr 边缘缓存。不刷的话，CDN 最长可能保留约 12 小时旧图。

## HTML 引用

```html
<img src="https://cdn.jsdelivr.net/gh/MuchA533753/img-cdn@main/qr/coolhunter-cli.png"
     alt="酷家乐 CLI 使用与反馈交流群" width="240" height="240">
```

## 注意

- 本仓库为**公开**仓库，仓库内所有图片均可被任何人访问。不要放含个人隐私、身份证件、内部资料的图。
- 文件名建议用 ASCII（`coolhunter-cli.png`），中文文件名会被 URL 编码，个别老旧系统处理不佳。
- 单文件建议小于 20 MB（jsDelivr 限制）。
