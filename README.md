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

你不需要写服务端。这个项目是静态网站，可以直接用 GitHub Pages：

1. 打开 GitHub 仓库 `joker-ssh/qp-agent`
2. 进入 `Settings` → `Pages`
3. `Build and deployment` 的 `Source` 选择 `GitHub Actions`
4. 以后每次推送 `main` 分支，GitHub 会自动运行 `.github/workflows/deploy.yml`
5. 部署成功后的公网地址是 `https://joker-ssh.github.io/qp-agent/`

GitHub Pages 部署的是 `npm run build` 生成的 `dist` 静态文件。

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
