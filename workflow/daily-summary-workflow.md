# Daily Summary Workflow

这个工作流用于每天整理 AI 学习和实操记录，并把结果更新到 GitHub。

## Daily Input

每天学习或实操后，在 `daily/` 目录新增一篇记录：

```text
daily/YYYY-MM-DD.md
```

可以直接复制：

```text
daily/template.md
```

记录不需要写成长文，但要尽量包含：

- 今天学习了什么
- 今天动手做了什么
- 使用了哪些 AI 工具
- 遇到了什么问题
- 产生了什么产品思考
- 哪些内容可以沉淀到作品集
- 明天准备做什么

## Daily Automation

每天晚上，自动任务会做这些事：

1. 读取当天的 `daily/YYYY-MM-DD.md`。
2. 如果当天没有记录，就不创建当天总结，也不要提交空内容。
3. 如果当天记录存在，生成或更新 `summaries/daily/YYYY-MM-DD.md`。
4. 根据最近记录更新 README 中的当前进展。
5. 提交改动。
6. 尝试推送到 GitHub。

## Summary Standard

每日总结应包含：

- 学习主题
- 实操成果
- 工具使用体感
- 产品经理视角的收获
- 可沉淀到作品集的内容
- 下一步计划

## GitHub Token Rule

不要把 GitHub token 写入：

- README
- 脚本
- 自动化 prompt
- Git remote URL
- 任何会提交到仓库的文件

自动推送应使用本机安全凭证，例如 GitHub Desktop、系统 Keychain 或 Git credential helper。
