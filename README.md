# 韦秋萍个人展示站

这是一个面向面试和老板查看的个人展示网站，使用 Vue 3 + Vite 构建，重点展示知识 IP 增长、商业转化、团队 SOP、讲师和主播能力。

## 先读这个

- 页面入口：`src/App.vue`
- 样式入口：`src/style.css`
- 核心素材：`public/content/core-work/`
- 轻量展示图：`public/content/optimized/`
- 简历文件：`public/content/resume/wei-qiuping-resume.pdf`

## 本地运行

```bash
npm install
npm run dev
```

打开终端显示的本地地址，一般是 `http://localhost:5173`。

## Vercel 部署

这个项目是静态前端站，部署到 Vercel 使用默认 Vite 配置即可：

- Build Command：`npm run build`
- Output Directory：`dist`
- Install Command：`npm install`

不需要配置 GitHub Pages 的 `/qp-agent/` 路径。
