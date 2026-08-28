# 苏打的blog

Hugo + PaperMod,部署在 GitHub Pages。

## 日常三件事

**① 写一篇新文章**

在 `content/posts/` 下建一个 `.md` 文件,开头加这段(front matter):

```yaml
---
title: "文章标题"
date: 2026-08-31
tags: ["流体仿真", "GPU"]
math: true        # 需要数学公式时加这行,不需要可以删
draft: false      # 改成 true 就是草稿,不会发布
---
```

下面正常写 Markdown。

**② 本地预览**

```bash
cd D:\Blog
hugo server -D          # -D 表示连草稿一起看
```

浏览器打开 http://localhost:1313 ,改文件会自动刷新。

**③ 发布**

```bash
git add -A
git commit -m "新文章:xxx"
git push
```

推上去之后 GitHub Actions 自动构建部署,一两分钟后网站更新。

---

## 数学公式

front matter 里写了 `math: true` 就能用:

- 行内:`$\nabla \cdot \mathbf{u} = 0$`
- 独立成行:`$$\nabla^2 p = \frac{\nabla \cdot \mathbf{u}^{*}}{\Delta t}$$`

## 代码块

用三个反引号 + 语言名:

````
```cpp
float dt = 1.0f / 60.0f;
```
````

支持 cpp / csharp / hlsl / python / bash / yaml 等等。

## 图片和视频

图片放 `static/images/`,文章里写 `![说明](/images/xxx.png)`。

视频建议传 B 站,然后嵌入 iframe(直接放仓库会让仓库变得很大)。

---

## 首次部署(只需做一次)

1. 在 GitHub 建一个仓库,名字必须是 **`sodappm.github.io`**,公开;
2. 本地关联并推送:
   ```bash
   cd D:\Blog
   git remote add origin https://github.com/sodappm/sodappm.github.io.git
   git branch -M main
   git push -u origin main
   ```
3. 仓库页面 → **Settings → Pages → Build and deployment → Source 选 "GitHub Actions"**;
4. 等 Actions 跑完(仓库页 Actions 标签能看进度),访问 https://sodappm.github.io

## 结构

```
content/posts/     文章都放这里
static/            图片等静态文件
layouts/partials/  extend_head.html 里配了 KaTeX
themes/PaperMod/   主题(git submodule,别手动改)
hugo.yaml          站点配置(标题、菜单、社交链接)
.github/workflows/ 自动部署
```
