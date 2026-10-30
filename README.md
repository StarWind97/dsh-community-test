# 我的主页（DSH 社区）

这个仓库就是你在 **DeepSeek Harness · GitHub 社区插件** 里的个人主页。

- 仓库里的 `posts/*.md` 就是你的帖子；
- 每次提交（commit）就是一次发布；
- `feed.json` 是所有帖子的索引，关注你的人只需要它，不必逐条扫描仓库；
- `profile.json` 是你的主页资料；
- `following.json` 是你公开的订阅列表（可选，相当于博客时代的 blogroll）。

## 发布一篇新帖子

### 方式一：在 DSH 里发（推荐）

在 DeepSeek Harness 中安装社区插件，配置好本机 Git 认证并连接目标仓库，然后明确对 Agent 说：

> 把这条对话整理成一篇帖子发布，标题《……》

插件会生成 `posts/<日期>-<slug>-<完整ID>.md`、更新 `feed.json`，并**一次提交**推送。编辑保留原 ID 和路径。连接可读不代表推送权限已经验证；API 高级模式另行保存凭据，完全空仓库须先初始化分支。

### 方式二：直接在 GitHub 网页/手机上发

1. 在 `posts/` 下新建 `2026-10-28-hello.md`；
2. 文件开头写 frontmatter：

```md
---
id: 01JABCDEF0123456789ABCDEFG
title: 你好，世界
publishedAt: 2026-10-28T09:00:00Z
tags: [dsh, hello]
---

正文写在这里，支持 Markdown。
```

3. 提交。仓库自带的 GitHub Action 配置会调用索引脚本，必要时另作一次提交；实际执行和耗时需要在你的仓库核验，本项目尚未完成真实 Action 验收。

> `id` 建议用 ULID（插件会生成；手写时随机字符串也可以，只要全局唯一）。
> `publishedAt` 省略时索引脚本回退到该文件最近一次 Git 提交时间。

## 关注别人

在插件的「社区」页粘贴对方的仓库地址即可，例如 `alice/blog`。
本地订阅列表默认只保存在你自己的电脑上；如果你想让别人通过你发现更多博主，可以把订阅列表公开到 `following.json`。

## 目录约定（schema v1）

| 文件 | 作用 |
|---|---|
| `profile.json` | 主页资料：昵称、简介、头像、链接、语言 |
| `posts/<slug>.md` | 单篇帖子，YAML frontmatter + Markdown 正文 |
| `feed.json` | 帖子索引，由插件或 Action 维护，读者只拉这个文件 |
| `following.json` | 可选：公开的订阅列表（blogroll） |

## 隐私

- 当前插件只支持 GitHub；内容保存在你的仓库，读取可能经过 GitHub/CDN；
- 默认 Git 由本机处理认证；API 凭据不会随静态读取发送到 CDN；
- 订阅关系默认只存本地；公开 `following.json` 是你的主动选择；
- 删除当前帖子不会清除 Git 历史、CDN 和其他副本；有效索引快照会更新读者缓存，索引移除也可能只是容量截断。
