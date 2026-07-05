# White AI PM

这是一个面向 AI 产品经理方向的学习与实践仓库。

我目前是一名云厂商 CDN 产品经理，正在系统补齐 AI Agent、MCP、CLI、API 设计和开发者工具相关能力。本仓库会记录我的学习路径、动手项目、产品分析和实验复盘，用来沉淀面向 AI 产品经理岗位的作品集。

## Why This Repo

AI 产品经理，尤其是 Agent、开发者工具、AI Infra 方向的产品经理，不能只停留在概念理解或 PRD 输出上。这个方向更看重：

- 是否能从开发者视角理解工具链和 API 设计
- 是否真实使用过 AI Coding / Agent 工具完成任务
- 是否能判断一个业务系统如何改造成 Agent Friendly
- 是否能动手做出 CLI、MCP Server、Agent Demo 或插件
- 是否能持续跟踪模型、工具和生态变化，并形成自己的判断

这个仓库的目标是把这些能力转化为可验证的实践成果。

## Focus Areas

### 1. AI Agent

关注 Agent 的核心机制：

- 模型如何理解任务和规划步骤
- Tool Calling 如何工作
- 上下文、记忆、状态如何管理
- Agent 如何处理失败、重试和人类确认
- Agent 在真实业务场景中的能力边界

### 2. MCP

关注 Model Context Protocol 在开发者工具和企业系统中的应用：

- MCP Server / Client 的基本结构
- Tool、Resource、Prompt 的设计方式
- 如何把内部系统能力暴露给 AI Agent
- 如何设计权限、审计、确认和高风险操作保护

### 3. CLI & Developer Tools

通过 CLI 练习开发者产品思维：

- 命令设计是否直觉
- 参数是否清晰
- 输出是否结构化
- 错误提示是否可行动
- 是否适合被人和 AI Agent 同时使用

### 4. Agent Friendly API Design

结合云产品和 CDN 背景，研究什么样的 API 更适合 AI Agent 调用：

- 明确的语义和边界
- 强类型参数与结构化返回
- 可观察、可追踪、可恢复
- 支持 dry-run、幂等、回滚和权限分级
- 面向诊断、配置、运维等高频场景优化

## Projects

### CDN Doctor CLI

一个面向 CDN 故障诊断的命令行工具。

计划能力：

- 解析 CDN 访问日志
- 识别 4xx / 5xx / 回源异常 / 缓存命中率下降等问题
- 调用 LLM 生成诊断摘要
- 输出结构化排查报告
- 给出下一步排查建议

目标不是做一个完整的商业系统，而是验证 AI Agent 如何辅助云产品运维诊断。

### CDN MCP Server

一个模拟 CDN 管理和诊断能力的 MCP Server。

计划提供的 tools：

- `query_cdn_logs`
- `get_cache_hit_rate`
- `explain_error_code`
- `purge_cache`
- `generate_incident_report`

重点关注：

- 工具命名和参数设计
- 只读操作与高风险操作的边界
- Agent 调用工具时的安全确认机制
- 结构化返回和错误处理

### Agent Friendly CDN Console

一个产品分析与设计项目，探索如何把传统 CDN 控制台改造成 Agent Friendly 工作台。

关注问题：

- 哪些 CDN 场景最适合 Agent 介入
- 控制台、API、CLI、MCP 应该如何协同
- 如何让 Agent 帮助用户诊断问题，而不是只生成一段泛泛建议
- 如何设计面向企业客户的权限、审计和风险控制

## Notes

仓库中会持续沉淀以下内容：

- AI 工具使用记录
- 模型能力边界观察
- Agent 产品案例分析
- MCP 学习笔记
- API 设计反思
- 项目复盘文章

## Daily Workflow

为了把学习过程持续沉淀为作品集，本仓库会维护一套每日记录和总结工作流。

- 每日原始记录：`daily/YYYY-MM-DD.md`
- 每日总结沉淀：`summaries/daily/YYYY-MM-DD.md`
- 记录模板：`daily/template.md`
- 工作流说明：`workflow/daily-summary-workflow.md`

每日记录关注“学了什么、做了什么、用了什么工具、遇到什么问题、产生什么产品思考”。每日总结会把这些内容整理成更适合复盘和展示的版本。

## Learning Roadmap

### Stage 1: Tool Usage

- 深度使用 Claude Code / Codex / Cursor 等 AI Coding 工具
- 用 AI 完成真实代码阅读、修改、调试和文档生成任务
- 记录工具在哪些场景有效，在哪些场景容易失败

### Stage 2: Build Small Tools

- 开发一个简单 CLI
- 接入 LLM API
- 练习结构化输出和错误处理
- 用 README、示例和测试提升项目完成度

### Stage 3: Build MCP Server

- 实现一个可被 Agent 调用的 MCP Server
- 设计多个真实业务工具
- 区分查询、诊断、变更类操作
- 增加权限、确认和审计思考

### Stage 4: Product Thinking

- 总结 Agent Friendly API 设计原则
- 拆解优秀 AI Developer Tools
- 输出面向 AI 产品经理岗位的项目复盘
- 形成自己的产品判断框架

## Current Status

This repo is in progress.

Next steps:

- [x] Create the GitHub repo and README
- [x] Build the daily learning log workflow
- [x] Add the first ReAct Agent learning sample
- [x] Generate daily learning summaries for recorded learning days
- [ ] Create the first CLI prototype
- [ ] Add sample CDN logs
- [ ] Generate structured diagnosis reports
- [ ] Build a mock CDN MCP Server
- [ ] Write the first product case study

## About Me

Hello，我是White，目前是一名云计算行业的产品经理。我主要负责 BytePlus CDN 的基础产品功能设计和规划，面向ToB企业级客户售卖。

我正在从云产品经验出发，探索 AI Agent、MCP、CLI 和开发者工具方向，希望通过真实项目提升自己对 AI 产品、开发者体验和 Agent Friendly 系统设计的理解。
