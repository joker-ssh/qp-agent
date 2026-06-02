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

你不需要写服务端。这个项目是静态网站，推荐直接部署到 Vercel：

1. 打开 [Vercel](https://vercel.com/) 并登录
2. 点击 `Add New` → `Project`
3. 导入 GitHub 仓库 `joker-ssh/qp-agent`
4. Framework Preset 选择 `Vite`
5. Build Command 使用 `npm run build`
6. Output Directory 使用 `dist`
7. 点击 `Deploy`

以后每次推送 `main` 分支，Vercel 会自动重新部署。

如果不想连接 GitHub，也可以本地安装 Vercel CLI 后运行：

```bash
npm i -g vercel
vercel
```

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
