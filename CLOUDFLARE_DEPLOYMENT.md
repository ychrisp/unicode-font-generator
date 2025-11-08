# Cloudflare Pages 部署指南

本项目可通过 Git 集成部署到 Cloudflare Pages。

## 部署步骤

### 1. 准备 Git 仓库
确保代码已推送到 GitHub/GitLab：
```bash
git add .
git commit -m "Prepare for Cloudflare Pages deployment"
git push
```

### 2. 在 Cloudflare Dashboard 创建项目

1. 登录 [Cloudflare Dashboard](https://dash.cloudflare.com/)
2. 选择你的账户：**Sead@difft.com's Account**
3. 进入 **Workers & Pages** → **Pages**
4. 点击 **Create application**
5. 选择 **Connect to Git**

### 3. 连接 Git 仓库

1. 授权 Cloudflare 访问你的 GitHub/GitLab
2. 选择 `font-generator` 仓库
3. 点击 **Begin setup**

### 4. 配置构建设置

在构建配置页面填写以下信息：

**项目名称：** `font-generator`

**生产分支：** `main` （或你的主分支名称）

**构建设置：**
- **Framework preset:** Next.js
- **Build command:** `npm run build`
- **Build output directory:** `.vercel/output/static`

**环境变量（如果需要）：**
```
NODE_VERSION=18
```

### 5. 高级设置（可选）

点击 **Environment variables** 添加任何需要的环境变量。

### 6. 部署

点击 **Save and Deploy**

Cloudflare Pages 将会：
1. 从 Git 拉取代码
2. 安装依赖（npm install）
3. 运行构建命令
4. 部署到全球 CDN

### 7. 访问网站

部署完成后，你会得到一个 URL：
- 生产环境：`https://font-generator.pages.dev`
- 预览环境：每次 PR 都会生成独立的预览 URL

## 自定义域名（可选）

部署成功后，可以添加自定义域名：

1. 在项目页面点击 **Custom domains**
2. 点击 **Set up a custom domain**
3. 输入你的域名（如 `www.fontgenerator.dev`）
4. 按照指示配置 DNS

## 自动部署

配置完成后，每次推送到主分支都会自动触发部署：

```bash
git add .
git commit -m "Update content"
git push
```

## 故障排除

### 构建失败

1. 检查构建日志
2. 确保 `package.json` 中所有依赖都已列出
3. 检查 Node.js 版本兼容性

### 页面显示 404

检查 `pages_build_output_dir` 配置是否正确

### 静态资源加载失败

确保 Next.js 配置中的 `assetPrefix` 设置正确

## 注意事项

1. **Edge Runtime：** 本项目使用 Cloudflare Workers Edge Runtime
2. **环境变量：** 敏感信息请在 Dashboard 中配置，不要提交到 Git
3. **构建时间：** 首次部署可能需要 3-5 分钟
4. **函数限制：** 注意 Cloudflare Pages Functions 的限制（CPU 时间、内存等）

## 参考文档

- [Cloudflare Pages Documentation](https://developers.cloudflare.com/pages/)
- [Next.js on Cloudflare Pages](https://developers.cloudflare.com/pages/framework-guides/nextjs/)
- [Pages Functions](https://developers.cloudflare.com/pages/functions/)
