[English](./07-tools-comparison.en.md) | **中文**

# 07 - 工具对比篇：六大 AI 编程工具深度对比

> Claude Code、Cursor、GitHub Copilot、Codex CLI、Gemini CLI、Windsurf——逐一分析优劣。

## 总览对比

| 维度 | Claude Code | Cursor | GitHub Copilot | Codex CLI | Gemini CLI | Windsurf |
|------|-------------|--------|----------------|-----------|------------|----------|
| 类型 | 终端 Agent | IDE | IDE 插件 | 终端 Agent | 终端 Agent | IDE |
| 开发商 | Anthropic | Anysphere | GitHub/Microsoft | OpenAI | Google | Codeium |
| 模型 | Claude 系列 | 多模型 | GPT-4o/Claude | codex-mini/GPT-5 | Gemini 2.5 | 多模型 |
| 上下文范围 | 整个项目 | 文件级 + 引用 | 文件级 + 引用 | 整个项目 | 整个项目 | 文件级 + 引用 |
| 多文件编辑 | 原生支持 | Composer 模式 | 有限 | 原生支持 | 原生支持 | Cascade 模式 |
| 学习曲线 | 中等 | 低 | 极低 | 中等 | 中等 | 低 |

## 各工具详解

### Claude Code

**优势**：
- 深度理解整个项目上下文，适合复杂的跨文件任务
- 终端原生，与 git、shell 工具链无缝集成
- 支持 MCP 协议扩展能力
- 长上下文窗口（200K tokens）

**劣势**：
- 需要终端操作经验
- 无可视化 IDE 界面
- API 按量付费（Sonnet ~$3/$15 per M tokens）或 Max 订阅 $100/月起

**最适合**：资深开发者、复杂重构、多文件协作任务

### Cursor

**优势**：
- VS Code 体验，迁移成本极低
- 内联编辑 + Chat + Composer 多种交互方式
- 支持多个 AI 模型切换
- Tab 补全速度快

**劣势**：
- 大项目上下文理解不如终端 Agent
- 月费模式，重度用户可能触及限额

**最适合**：日常开发、快速原型、VS Code 用户

### GitHub Copilot

**优势**：
- 与 VS Code/JetBrains 深度集成
- 行级补全体验成熟流畅
- Copilot Chat 支持对话式交互
- Agent 模式逐步增强中

**劣势**：
- 复杂任务能力弱于专业 Agent
- 对项目全局上下文理解有限

**最适合**：入门用户、轻量辅助、已有 GitHub 生态的团队

### Codex CLI

**优势**：
- OpenAI 生态整合
- 支持沙箱执行，安全隔离
- 可批量自动化任务

**劣势**：
- 需要 OpenAI API key 或 ChatGPT 订阅
- 生态和插件还在早期

**最适合**：OpenAI 生态用户、自动化脚本任务

### Gemini CLI

**优势**：
- 免费使用（有配额限制）
- Google 生态集成（Firebase、GCP 等）
- 100 万 token 上下文窗口

**劣势**：
- 代码生成质量不稳定
- 工具生态不如竞品成熟

**最适合**：Google 技术栈用户、预算有限的个人开发者

### Windsurf

**优势**：
- Cascade 模式提供类 Agent 体验
- 界面友好，上手简单
- 有免费套餐

**劣势**：
- 社区和文档相对较少
- 高级功能不如 Cursor 丰富

**最适合**：想要 IDE Agent 体验的新手

## 定价对比

| 工具 | 价格 |
|------|-------|
| Claude Code | API 按量付费（Sonnet ~$3/$15 per M tokens）; Max 订阅 $100/月起 |
| Cursor | $20/月 Pro, $60/月 Pro+, $200/月 Ultra, $40/人/月 Teams（积分制） |
| GitHub Copilot | 免费版可用, $10/月 Pro, $39/月 Pro+, $19/人/月 Business |
| Codex CLI | 免费（受限）; ChatGPT Plus $20/月, Pro $200/月 |
| Gemini CLI | 免费（受限）; AI Pro $19.99/月 |
| Windsurf | $15/月 Pro, $30/人/月 Team |
| Kiro | 免费预览版（2025年推出） |
| Trae | 免费（字节跳动推出） |

## 工具迁移

### 从 Copilot 迁移到 Claude Code

1. 安装 Claude Code：`npm install -g @anthropic-ai/claude-code`
2. 为项目创建 `CLAUDE.md`（将你习惯的 Copilot 指令转化为项目配置）
3. 从简单任务开始适应终端交互
4. 逐步将复杂任务交给 Claude Code

### 从 Cursor 迁移到 Claude Code

1. 将 `.cursorrules` 的内容迁移到 `CLAUDE.md`
2. 习惯在终端而非 IDE 中与 AI 交互
3. 利用 Claude Code 的项目级上下文优势处理大型任务

## 组合使用

很多开发者不是只用一个工具，而是组合使用：

| 组合方案 | 适用场景 |
|----------|----------|
| Copilot + Claude Code | 日常补全用 Copilot，复杂任务用 Claude Code |
| Cursor + Claude Code | Cursor 做 UI 开发，Claude Code 做后端和重构 |
| Copilot + Gemini CLI | 编码用 Copilot，Google 相关部署用 Gemini |

**建议**：先精通一个工具，再尝试组合。不要同时学习太多工具。

---

上一篇：[团队协作篇](./06-team-practices.md) | 返回：[目录](../README.md)

相关速查表：[Claude Code 速查](../cheatsheets/claude-code.md) | [Cursor 速查](../cheatsheets/cursor.md) | [提示词模板](../cheatsheets/prompts.md)
