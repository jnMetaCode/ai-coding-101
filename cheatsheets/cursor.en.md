**English** | [中文](./cursor.md)

# Cursor Cheatsheet

> Keyboard shortcuts, core features, and tips at a glance.

## Core Keyboard Shortcuts

| Shortcut (Mac) | Shortcut (Win/Linux) | Description |
|----------------|---------------------|-------------|
| `Cmd+K` | `Ctrl+K` | Inline edit — select code and let AI modify it |
| `Cmd+L` | `Ctrl+L` | Open AI Chat panel |
| `Cmd+I` | `Ctrl+I` | Open Composer (multi-file editing mode) |
| `Cmd+Shift+K` | `Ctrl+Shift+K` | AI command generation in terminal |
| `Tab` | `Tab` | Accept AI completion suggestion |
| `Esc` | `Esc` | Reject AI completion suggestion |
| `Cmd+Shift+L` | `Ctrl+Shift+L` | Add selected code to Chat context |

## Agent Mode (Recommended)

Since 2025, **Agent mode** has become the primary power-user workflow in Cursor. Select "Agent" in the Chat panel, and the AI will automatically read files, run terminal commands, edit across files, and iteratively fix errors — no manual step-by-step guidance needed. For complex tasks, Agent mode is significantly more efficient than manual Cmd+K / Composer usage.

## Three Basic Interaction Modes

### 1. Tab Completion

Triggers automatically as you type. Cursor predicts the next code block in real time.

**Tips**:
- Write a function signature and comment, then pause — let AI complete the body
- If the suggestion is poor, type a few more characters and AI will re-predict

### 2. Cmd+K Inline Edit

Select code → `Cmd+K` → type instruction → AI modifies directly in the editor.

```
# Examples
Select a function → Cmd+K → "Add error handling and input validation"
Select CSS → Cmd+K → "Convert to dark mode color scheme"
Select SQL → Cmd+K → "Optimize query performance, add index hints"
```

### 3. Chat / Composer

- **Chat** (`Cmd+L`): Conversational interaction for questions, analysis, and generating new code
- **Composer** (`Cmd+I`): Cross-file editing mode for changes spanning multiple files

## @ Reference System

Use `@` in Chat and Composer to provide context:

| Reference | Description |
|-----------|-------------|
| `@filename` | Reference a specific file |
| `@folder` | Reference an entire folder |
| `@codebase` | Search the entire codebase |
| `@web` | Search the web for up-to-date information |
| `@docs` | Reference indexed documentation |
| `@git` | Reference git history and diffs |

## Quick .cursorrules Setup

> **Note**: `.cursorrules` is the legacy format and still works. Modern Cursor uses the `.cursor/rules/` directory, supporting multiple rule files.

Create a `.cursorrules` file in your project root:

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

## Common Operations

### Quick Bug Fix

```
Select buggy code → Cmd+K → "Fix this TypeError, input may be null"
```

### Generate a Component

```
Chat: Create a React table component with sorting, pagination,
and search filtering. Use TypeScript and Tailwind CSS.
```

### Refactor Code

```
Select code block → Cmd+K → "Refactor this switch-case into a strategy pattern"
```

### Write Tests

```
Select function → Cmd+L → "Write comprehensive unit tests for this function, cover edge cases"
```

### Understand Code

```
Select code → Cmd+L → "Explain the logic, especially what this regex does"
```

## Efficiency Tips

1. **Use Composer**: For multi-file changes, Composer is more efficient than Chat
2. **Precise references**: Use `@filename` to give AI accurate context instead of letting it guess
3. **Progressive editing**: Discuss the approach in Chat first, then use Cmd+K to execute
4. **Save common instructions**: Put frequently used prompts in `.cursorrules`
5. **Use the terminal**: Cursor's terminal also supports AI — use `Cmd+Shift+K` to generate commands

---

For project configuration details, see [Project Setup](../guides/04-project-setup.en.md)
