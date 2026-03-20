[English](./05-advanced-techniques.en.md) | **中文**

# 05 - 进阶篇：释放 AI 编程的全部潜力

> 多 Agent 协作、Git Worktree 隔离、并行任务、MCP 扩展、自定义 Skills。

## 多 Agent 工作流

当任务足够复杂时，单个 AI 会话可能不够用。多 Agent 模式让你同时运行多个 AI 实例，各自负责不同的子任务。

**适用场景**：

- 前后端同时开发
- 一个 Agent 写代码，另一个写测试
- 一个 Agent 做主任务，另一个做 Code Review

```bash
# 终端 1：Agent A 负责后端 API
cd backend && claude
> 实现用户注册 API，包含邮箱验证

# 终端 2：Agent B 负责前端页面
cd frontend && claude
> 创建注册页面，表单提交到 POST /api/auth/register
```

**关键原则**：

- 提前定义好接口契约（API schema），让两个 Agent 基于同一契约工作
- 用 CLAUDE.md 描述完整的项目架构，确保每个 Agent 都了解全局

更多 Agent 模式和行业应用：[agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh)

## Git Worktree 隔离

Git Worktree 让你在同一个仓库中同时拥有多个工作目录，每个目录在不同分支上。这是并行 AI 任务的基础设施。

```bash
# 创建 worktree
git worktree add ../project-feature-auth feature/auth
git worktree add ../project-fix-bug fix/critical-bug

# 在不同 worktree 中启动 AI
cd ../project-feature-auth && claude
cd ../project-fix-bug && claude

# 完成后清理
git worktree remove ../project-feature-auth
```

**优势**：

- 每个任务在独立的文件系统中，互不干扰
- AI 不会意外修改其他任务的文件
- 可以同时运行多个 AI 实例而不冲突

## 并行任务执行

结合 Worktree 和多 Agent，你可以实现真正的并行开发：

```bash
# 一个脚本启动三个并行任务
for branch in feature/auth feature/payment feature/notification; do
  dir="../worktree-$(echo $branch | tr '/' '-')"
  git worktree add "$dir" "$branch"
  (cd "$dir" && claude -p "完成这个分支的待办任务，参考 TODO.md") &
done
wait
```

**注意事项**：

- 并行任务应该尽量独立，减少文件冲突
- 每个 worktree 消耗一个 API 会话的配额
- 合并时仍需人工审查冲突

## MCP Servers 和工具扩展

MCP（Model Context Protocol）让 AI 工具连接外部服务——数据库、API、文件系统之外的任何工具。

```json
// Claude Code MCP 配置示例（.mcp.json）
{
  "mcpServers": {
    "postgres": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-postgres"],
      "env": {
        "DATABASE_URL": "postgresql://localhost:5432/mydb"
      }
    },
    "github": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-github"],
      "env": {
        "GITHUB_TOKEN": "${GITHUB_TOKEN}"
      }
    }
  }
}
```

**常用 MCP Server**：

| Server | 用途 |
|--------|------|
| postgres | 直接查询数据库 |
| github | 操作 GitHub Issues/PR |
| filesystem | 访问沙箱外的文件 |
| fetch | 抓取网页内容 |
| memory | 跨会话记忆 |

## 自定义 Skills 开发

Skills 是可复用的工作流模板。你可以为团队常见操作创建自定义 Skills。

```markdown
<!-- .claude/skills/create-api-endpoint.md -->
# Skill: 创建 API 端点

## 输入
- 端点路径和方法
- 请求/响应格式

## 步骤
1. 在 src/routes/ 创建路由文件
2. 在 src/controllers/ 创建控制器
3. 在 src/validators/ 创建输入验证
4. 在 src/tests/ 创建测试文件
5. 更新 src/routes/index.ts 注册路由
6. 运行测试确保通过
```

**技巧**：

- 将团队的最佳实践编码为 Skills
- Skills 可以组合使用——一个复杂任务由多个 Skills 串联完成
- 版本控制 Skills 文件，随项目一起维护

---

上一篇：[项目配置篇](./04-project-setup.md) | 下一篇：[团队协作篇](./06-team-practices.md)

相关速查表：[Claude Code 速查](../cheatsheets/claude-code.md)
