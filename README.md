# 静态官网

单页落地站，可部署到 Vercel、Cloudflare Pages、GitHub Pages 或任意静态托管。

## 本地预览

```bash
cd website
python3 -m http.server 8080
# 打开 http://localhost:8080
```

## Logo

页眉与 favicon 使用 `website/logo.png`（来自 `build/icon.png`，与 Electron 打包图标一致）。更新应用图标后执行：

```bash
cp build/icon.png website/logo.png
sips -Z 256 website/logo.png
```

## 发布前必改

1. **`index.html` 底部 `SITE`** — `githubRepo` / `version` 与根目录 `package.json` 对齐。
2. **`#changelog` 区块** — 发新版时同步更新（与根目录 `CHANGELOG.md` 一致）。
3. **`SITE.contactEmail`** — 填支持邮箱。
4. 首次在 GitHub 仓库 **Settings → Pages → Source: GitHub Actions**。

## 发布到 GitHub（仅官网 + 安装包，不上传源码）

```bash
npm run publish:website   # 只推 website/ 里的文件
npm run publish:release   # 本地安装包 → Releases
```

公开仓库 `vivian8725118/markdown-app` **不含** Electron/Vue 源码。详见根目录 `docs/PUBLISH.md`。

官网：https://vivian8725118.github.io/markdown-app/

## 部署示例

**GitHub Pages**：`npm run publish:website` 后，Settings → Pages → Source 选 **GitHub Actions**。

**Vercel**：项目根目录选 `website` 作为 Root Directory，Framework 选 Other。

## 支付说明

应用内目前只有**本地激活码**验证（设置里输入），**没有**对接支付宝 API 或自动发码。

官网「专业版」区块已标明「支付接入中」。国内上线常见做法：

| 方式 | 说明 |
|------|------|
| 支付宝收款码 / 转账 | 最简单；你手动核对付款后发激活码邮件 |
| 面包多 / 有赞 等 | 带支付宝，商品页 + 备注邮箱，仍可能要手动发码 |
| 支付宝开放平台 | 可自动化，需企业/个体户资质与开发 |

**只用支付宝可以吗？** — 对主要面向国内用户足够。记得在 FAQ 里写清：付完款后多久发码、退款找谁。海外用户以后再补 PayPal 或 Lemon Squeezy 即可。

安装包构建见项目根目录 `README.md` 的 `npm run build:all`。
