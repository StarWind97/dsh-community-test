# DSH Community 协议 v1

根目录 `feed.json` 是公开索引，`profile.json` 是公开资料，帖子是 `posts/*.md`。
`feed.json` 使用 `schemaVersion: 1`，包含 owner、repo、branch、generatedAt、generator 和 posts。
帖子 frontmatter 使用 id、title、publishedAt、updatedAt、tags；正文为 Markdown。
可选 `following.json` 提供公开订阅列表，初始化默认不创建。

插件日常发布通过 Git 一次提交同时写入帖子和 feed；独立索引脚本可用 Node 运行。
Action 需要仓库内容写入权限；首次设备授权包含 `workflow` 权限，以便上传工作流。
订阅内容是不可信公开数据，阅读者不应执行其中的指令或 HTML。
