---
name: qp-agent-site
description: Maintain and deploy the qp-agent Vue/Vite personal website for 韦秋萍. Use when working in the joker-ssh/qp-agent repository, changing site content, updating public assets, fixing deployment paths, or preparing GitHub Pages deployment.
---

# QP Agent Site

## Project Map

- Treat `src/App.vue` as the main user-facing content entry.
- Treat `src/style.css` as the main visual styling entry.
- Treat `public/resume.pdf` and `public/*` as static files copied directly into production.
- Treat `vite.config.js` as deployment-sensitive configuration.
- Keep `dist/` generated and untracked.

## Deployment Rules

- For GitHub Pages at `https://joker-ssh.github.io/qp-agent/`, keep `base: '/qp-agent/'` in `vite.config.js`.
- For root-domain hosts such as Vercel, remove the custom `base` value so built assets load from `/assets/...`.
- Use `.github/workflows/deploy.yml` for GitHub Pages deployment with `npm ci`, `npm run build`, and uploaded `dist`.
- After deployment-path changes, run `npm run build` and inspect `dist/index.html` asset URLs before pushing.

## Working Style

- Keep edits minimal and focused; this is a small static website, not an app platform.
- Prefer local preview with `npm run dev` for page and style iteration.
- Do not run `npm run build` for every small content or style change unless deployment config, dependencies, or production paths changed.
- When organizing docs or assets, keep user-facing entry files obvious and separate internal reference material from public-facing files.

## Common Tasks

### Update site content

1. Edit `src/App.vue`.
2. Update matching styles in `src/style.css` only when needed.
3. Preview locally with `npm run dev`.

### Add public images or documents

1. Put public static assets under `public/`.
2. Reference them with paths compatible with `import.meta.env.BASE_URL` when used from Vue.
3. Avoid committing raw source material unless it belongs in the public site.

### Prepare GitHub Pages deployment

1. Confirm `vite.config.js` includes `base: '/qp-agent/'`.
2. Confirm `.github/workflows/deploy.yml` exists.
3. Run `npm run build`.
4. Confirm `dist/index.html` points assets at `/qp-agent/assets/...`.
5. Commit and push to `main`.
