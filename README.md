# 折纸工坊 Paper Fold Workshop

上传照片 + 写一句话 → AI 自动抠图做封面 → 生成一个「折纸展开」动效网页（单文件 HTML，可保存分享）。

**在线体验**：GitHub Pages 部署后访问 `https://<用户名>.github.io/paper-fold-workshop/`

## 它是怎么工作的

- 纯前端实现，**无需后端、无需数据库**；
- 抠图模型 **RMBG-1.4**（约 44MB）通过 [transformers.js](https://github.com/huggingface/transformers.js) 在**用户浏览器里**推理（模型走 hf-mirror.com 镜像），照片不上传到任何服务器；
- 前端合成白边贴纸封面（凸包轮廓 + 底弧收口），连同纸纹、文字一起 base64 注入 `paper-fold-template.html` 的占位符，产出自包含成品 HTML；
- 成品内嵌 three.js（CDN）播放折纸展开动画。

## 部署

静态站点，任意托管皆可：

```bash
python3 -m http.server 3000   # 本地预览
```

GitHub Pages：仓库 Settings → Pages → Source 选 `main` 分支 `/ (root)`。

## 文件

| 文件 | 说明 |
|---|---|
| `index.html` | 折纸工坊页面（上传 / 输入 / 生成） |
| `paper-fold-template.html` | 折纸动效模板（生成品的骨架） |
| `paper_texture.jpg` | 纸纹贴图 |

## 已知限制

- 用户首次生成需下载约 44MB 模型（之后浏览器缓存）；
- 特写照片抠图效果最好；大场景合影可能偏松；
- 成品中的书法字体（霞鹜文楷）走 CDN，断网时回退系统楷体。
