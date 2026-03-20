[English](./cursor.en.md) | **中文**

# Cursor 速查表

> 快捷键、核心功能、使用技巧一页搞定。

## 核心快捷键

| 快捷键 (Mac) | 快捷键 (Win/Linux) | 说明 |
|--------------|-------------------|------|
| `Cmd+K` | `Ctrl+K` | 内联编辑——选中代码后直接让 AI 修改 |
| `Cmd+L` | `Ctrl+L` | 打开 AI Chat 面板 |
| `Cmd+I` | `Ctrl+I` | 打开 Composer（多文件编辑模式） |
| `Cmd+Shift+K` | `Ctrl+Shift+K` | 终端中的 AI 命令生成 |
| `Tab` | `Tab` | 接受 AI 补全建议 |
| `Esc` | `Esc` | 拒绝 AI 补全建议 |
| `Cmd+Shift+L` | `Ctrl+Shift+L` | 将选中代码添加到 Chat 上下文 |

## Agent 模式（推荐）

自 2025 年起，**Agent 模式**已成为 Cursor 的主要高级工作流。在 Chat 面板中选择 "Agent" 模式，AI 将自动读取文件、执行终端命令、跨文件编辑，并迭代修复错误——无需手动逐步引导。对于复杂任务，Agent 模式比手动使用 Cmd+K / Composer 效率更高。

## 三种基础交互模式

### 1. Tab 补全

自动触发，无需操作。Cursor 在你输入时实时预测下一段代码。

**技巧**：
- 写好函数签名和注释后暂停，让 AI 补全函数体
- 如果建议不好，继续输入几个字符，AI 会重新预测

### 2. Cmd+K 内联编辑

选中代码 → `Cmd+K` → 输入指令 → AI 直接在编辑器中修改。

```
# 使用示例
选中一个函数 → Cmd+K → "添加错误处理和输入验证"
选中 CSS → Cmd+K → "改为 dark mode 配色"
选中 SQL → Cmd+K → "优化查询性能，添加索引提示"
```

### 3. Chat / Composer

- **Chat**（`Cmd+L`）：对话式交互，适合提问、分析、生成新代码
- **Composer**（`Cmd+I`）：跨文件编辑模式，适合涉及多个文件的修改

## @ 引用系统

在 Chat 和 Composer 中使用 `@` 来引用上下文：

| 引用 | 说明 |
|------|------|
| `@filename` | 引用特定文件 |
| `@folder` | 引用整个文件夹 |
| `@codebase` | 搜索整个代码库 |
| `@web` | 搜索网络获取最新信息 |
| `@docs` | 引用已索引的文档 |
| `@git` | 引用 git 历史和 diff |

## .cursorrules 快速配置

> **注意**：`.cursorrules` 是旧版格式，仍然有效。Cursor 新版推荐使用 `.cursor/rules/` 目录，支持多个规则文件。

在项目根目录创建 `.cursorrules` 文件：

```
You are an expert in [your tech stack].

Key rules:
- [Rule 1: coding standard]
- [Rule 2: naming convention]
- [Rule 3: architecture pattern]

When generating code:
- Always include error handling
- Always add TypeScript types
- Follow existing patterns in the codebase
```

## 常用操作

### 快速修 Bug

```
选中报错的代码 → Cmd+K → "修复这个 TypeError，输入可能为 null"
```

### 生成组件

```
Chat: 创建一个 React 表格组件，支持排序、分页、搜索过滤，
使用 TypeScript 和 Tailwind CSS
```

### 重构代码

```
选中代码块 → Cmd+K → "将这个 switch-case 重构为策略模式"
```

### 写测试

```
选中函数 → Cmd+L → "为这个函数写完整的单元测试，覆盖边界情况"
```

### 理解代码

```
选中代码 → Cmd+L → "解释这段代码的逻辑，特别是这个正则表达式的作用"
```

## 效率技巧

1. **善用 Composer**：涉及多文件改动时，Composer 比 Chat 效率更高
2. **精确引用**：用 `@filename` 给 AI 提供准确的上下文，避免它猜测
3. **渐进式编辑**：先用 Chat 讨论方案，确认后再用 Cmd+K 执行修改
4. **保存常用指令**：将常用的 prompt 保存在 `.cursorrules` 中
5. **结合终端**：Cursor 的终端也支持 AI——用 `Cmd+Shift+K` 生成命令

---

更多项目配置详见 [项目配置篇](../guides/04-project-setup.md)
