# 韦秋萍个人网站

这是一个用于展示运营总监个人经历与项目亮点的 Vue3 + Vite 静态网站模板。

## 先读这个

- 用户入口：`src/App.vue`
- 样式入口：`src/style.css`
- 简历文件：`public/resume.pdf`

## 本地运行

```bash
npm install
npm run dev
```

打开终端显示的本地地址，一般是 `http://localhost:5173`。

## 部署到公网

你不需要写服务端。这个项目是静态网站，最简单推荐用 Vercel：

1. 把代码推送到 GitHub 仓库 `joker-ssh/qp-agent.git`
2. 打开 Vercel，选择 `Import Git Repository`
3. 选择这个仓库
4. Framework Preset 选择 `Vite`
5. Build Command 填 `npm run build`
6. Output Directory 填 `dist`
7. 点击 Deploy

部署完成后，Vercel 会给你一个公网 URL，别人可以直接访问。

## 推送到 GitHub

```bash
git init
git add .
git commit -m "init personal website"
git branch -M main
git remote add origin https://github.com/joker-ssh/qp-agent.git
git push -u origin main
```

如果远端仓库已经有内容，先告诉我，我可以帮你处理同步和冲突。
