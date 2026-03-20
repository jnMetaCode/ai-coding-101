**English** | [中文](./05-advanced-techniques.md)

# 05 - Advanced Techniques: Unlock the Full Potential of AI Coding

> Multi-agent workflows, git worktree isolation, parallel execution, MCP extensions, and custom skills.

## Multi-Agent Workflows

When a task is complex enough, a single AI session may not suffice. Multi-agent mode lets you run multiple AI instances simultaneously, each handling a different subtask.

**Use cases**:

- Developing frontend and backend in parallel
- One agent writes code while another writes tests
- One agent works on the main task while another reviews

```bash
# Terminal 1: Agent A handles the backend API
cd backend && claude
> Implement user registration API with email verification

# Terminal 2: Agent B handles the frontend
cd frontend && claude
> Create a registration page that submits to POST /api/auth/register
```

**Key principles**:

- Define the interface contract (API schema) upfront so both agents work from the same spec
- Use CLAUDE.md to describe the full project architecture so each agent has global context

More agent patterns and industry applications: [agency-agents-zh](https://github.com/jnMetaCode/agency-agents-zh)

## Git Worktree Isolation

Git Worktree lets you have multiple working directories from the same repository, each on a different branch. This is the infrastructure for parallel AI tasks.

```bash
# Create worktrees
git worktree add ../project-feature-auth feature/auth
git worktree add ../project-fix-bug fix/critical-bug

# Start AI in different worktrees
cd ../project-feature-auth && claude
cd ../project-fix-bug && claude

# Clean up when done
git worktree remove ../project-feature-auth
```

**Benefits**:

- Each task has an isolated filesystem — no interference
- AI cannot accidentally modify files from other tasks
- Multiple AI instances can run without conflicts

## Parallel Task Execution

Combine worktrees and multi-agent for true parallel development:

```bash
# Script to launch three parallel tasks
for branch in feature/auth feature/payment feature/notification; do
  dir="../worktree-$(echo $branch | tr '/' '-')"
  git worktree add "$dir" "$branch"
  (cd "$dir" && claude -p "Complete the tasks for this branch per TODO.md") &
done
wait
```

**Caveats**:

- Parallel tasks should be as independent as possible to minimize merge conflicts
- Each worktree consumes one API session quota
- Manual conflict review is still needed when merging

## MCP Servers and Tool Extensions

MCP (Model Context Protocol) lets AI tools connect to external services — databases, APIs, anything beyond the filesystem.

```json
// Claude Code MCP config example (.mcp.json)
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

**Popular MCP Servers**:

| Server | Purpose |
|--------|---------|
| postgres | Query databases directly |
| github | Manage GitHub Issues/PRs |
| filesystem | Access files outside the sandbox |
| fetch | Fetch web content |
| memory | Cross-session memory |

## Custom Skills Development

Skills are reusable workflow templates. You can create custom skills for your team's common operations.

```markdown
<!-- .claude/skills/create-api-endpoint.md -->
# Skill: Create API Endpoint

## Input
- Endpoint path and HTTP method
- Request/response format

## Steps
1. Create route file in src/routes/
2. Create controller in src/controllers/
3. Create input validator in src/validators/
4. Create test file in src/tests/
5. Register the route in src/routes/index.ts
6. Run tests to verify
```

**Tips**:

- Encode your team's best practices as skills
- Skills are composable — chain multiple skills for complex tasks
- Version-control skill files alongside your project

---

Previous: [Project Setup](./04-project-setup.en.md) | Next: [Team Practices](./06-team-practices.en.md)

Related cheatsheet: [Claude Code](../cheatsheets/claude-code.en.md)
