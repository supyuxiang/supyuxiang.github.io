# Yuxiang Feng 个人主页

英文个人学术主页，版式参考 [shanhe321.github.io](https://shanhe321.github.io/)。

- 线上地址：https://supyuxiang.github.io/
- 仓库：https://github.com/supyuxiang/supyuxiang.github.io
- GitHub 用户名：`supyuxiang`（短地址必须是 `https://用户名.github.io/`，因此仓库名必须是 `supyuxiang.github.io`）

这是静态站点，没有构建步骤。改完 `index.html` 或 `images/` 后推到 `main`，GitHub Pages 大约 1 分钟后更新。

## 文件结构

```
index.html          # 整站内容与样式都在这里
images/
  profile.jpg       # 侧栏头像
  sjtu.png          # 交大校徽
  dlut.png          # 大工校徽
  fudan.png         # 复旦校徽
  pku.png           # 北大校徽
.nojekyll           # 不要删，让 Pages 按纯静态文件发布
README.md           # 本说明
```

不要新增 `CNAME`。加了自定义域名后，GitHub 会把站点从 `supyuxiang.github.io` 跳走。

## 改哪里

所有可见文字都在 `index.html`。按 `id` 搜对应段落：

| 要改的内容 | 搜索 |
| --- | --- |
| 页面标题、canonical | `<title>`、`rel="canonical"`、`og:url` |
| 侧栏姓名、身份、邮箱、微信、GitHub | `class="sidebar"` |
| 简介三段 | `id="about-me"` 后面的 Biography |
| 教育 | `id="education"` |
| News | `id="news"` |
| 论文 | `id="publications"` |
| 实习 | `id="experience"` |
| 奖项 | `id="honors"` |
| 页脚更新日期 | `<footer>` |

正文保持英文。中文名写在英文名后面，用英文括号：

```html
Hi! I am <strong>Yuxiang Feng (冯羽翔)</strong>, ...
```

不要用全角括号 `（）`，间距会偏大。

### 加一条 News

复制现有 `<li>`，改年份和一句话：

```html
<li><em>2026</em>: 🎉 <strong>Paper-Name</strong> is accepted by <strong>Venue</strong>.</li>
```

### 加一篇论文

在 `id="publications"` 下复制一整块 `paper-box`。从新到旧排列。模板：

```html
<div class="paper-box">
  <div class="paper-box-image">
    <div class="badge">Venue 2027</div>
    <div class="venue-card">Under review</div>
  </div>
  <div class="paper-box-text">
    <p><strong>Paper Title</strong></p>
    <p><strong>Yuxiang Feng</strong> et al. &nbsp;|&nbsp; <em>Under review at Venue 2027</em></p>
    <p><strong>TL;DR:</strong> <em>One or two sentences.</em></p>
  </div>
</div>
```

录用后把 `badge` / `venue-card` 改成 `Accepted` 或 `Oral`。有 PDF / arXiv / code 时，加在标题下面：

```html
<p>
  <a href="PAPER.pdf">Paper</a> /
  <a href="https://arxiv.org/abs/xxxx.xxxxx">arXiv</a> /
  <a href="https://github.com/supyuxiang/repo">Code</a>
</p>
```

### 换头像或校徽

把新图放到 `images/`，文件名与 `index.html` 里的 `src` 一致。校徽地址带了 `?v=2`（例如 `images/dlut.png?v=2`），换图后把数字加 1，避免浏览器缓存旧图。

头像用接近正方形的照片，页面会裁成圆。

## 本地预览

在仓库根目录：

```bash
python3 -m http.server 8877 --directory . --bind 127.0.0.1
```

浏览器打开 http://127.0.0.1:8877/ 。改完刷新即可，不必重启。

## 发布到 GitHub Pages

1. 确认在仓库根目录，分支是 `main`：

   ```bash
   cd /root/yxfeng.github.io   # 或你的本地克隆路径
   git status
   ```

2. 本机如果访问 GitHub 很慢或 `git push` 在 HTTP/2 报错，先开代理：

   ```bash
   source /etc/network_turbo
   ```

3. 提交并推送（不要把 token 写进文件或 `git remote`）：

   ```bash
   git add index.html images README.md
   git commit -m "Update homepage"
   git push origin main
   ```

4. 约 1 分钟后打开 https://supyuxiang.github.io/ 并强制刷新（Ctrl+Shift+R）。  
   构建状态：仓库 → Settings → Pages，或 https://github.com/supyuxiang/supyuxiang.github.io/settings/pages

推送如果被拒绝（`fetch first`），先拉再推，不要 `push --force`：

```bash
git pull --rebase origin main
git push origin main
```

## 权限与安全

Fine-grained PAT 至少需要：

- Repository：`supyuxiang/supyuxiang.github.io`（或 All repositories）
- **Contents: Read and write**（才能 `git push`）
- 改仓库名 / Pages 设置时还要 **Administration** 和 **Pages** 的写权限

Token 只放环境变量，用完到 [Fine-grained tokens](https://github.com/settings/personal-access-tokens) 撤销。不要贴到聊天、README 或 commit 里。

## 不要做的事

- 不要把仓库改回 `yxfeng.github.io`。那会变成项目站 `https://supyuxiang.github.io/yxfeng.github.io/`，不再是根域名。
- 不要加 `CNAME`（例如 `www.yxfeng.com`），除非 DNS 已经指到 GitHub Pages。
- 不要提交 `.env`、token、私钥。
- 用户名 `yxfeng` 已被占用，无法使用 `https://yxfeng.github.io/`。
