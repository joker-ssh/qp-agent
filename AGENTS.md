# Global User Preferences

## Markdown preference

When the user asks to open, read, view, summarize, or organize a Markdown (`.md`) file:

- Default to presenting it as a preview-style rendered document, not as raw Markdown source.
- Prefer a clean reading view with headings, sections, and the final visible structure.
- Only show raw Markdown syntax when the user explicitly asks for source, formatting, or file editing details.

## Working style

- The user prefers minimal entry points and low visual clutter.
- Prefer showing which file to read first.
- Separate "user-facing entry files" from "internal reference files" whenever organizing folders.

--- project-doc ---

# Project Preferences

## Validation

- 不要每次修改后都自动运行 `npm run build`，除非用户明确要求，或改动涉及构建配置、依赖、部署问题。
- 日常样式和页面迭代优先使用本地开发服务预览。
