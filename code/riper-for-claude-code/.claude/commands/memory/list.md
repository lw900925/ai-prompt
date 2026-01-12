---
description: 列出所有分支的记忆记录
---

# 记忆库概览

## ⚠️ 记忆库位置要求

**关键路径策略**：
- 记忆库必须位于仓库根目录：使用 `git rev-parse --show-toplevel` 查找根目录，然后定位到 `[根目录]/.claude/memory-bank/`
- 切勿创建包级别的记忆库：`packages/*/.claude/memory-bank/` ❌
- 在单体仓库中：根目录的一个记忆库服务于整个项目

### 记忆列表的正确与错误路径示例
✅ **正确**：`[根目录]/.claude/memory-bank/main/`（其中根目录 = `git rev-parse --show-toplevel`）
❌ **错误**：`[根目录]/packages/react/.claude/memory-bank/main/`
❌ **错误**：`packages/react/.claude/memory-bank/main/`

## 当前分支的记忆记录
**分支**：`git branch --show-current`

`ls -la $(git rev-parse --show-toplevel)/.claude/memory-bank/$(git branch --show-current)/ 2>/dev/null || echo "当前分支无记忆记录"`

## 所有分支的记忆记录
`find $(git rev-parse --show-toplevel)/.claude/memory-bank -type f -name "*.md" 2>/dev/null | head -20 || echo "未找到记忆记录"`

## 记忆库组织结构

```
[根目录]/.claude/memory-bank/ (其中根目录 = git rev-parse --show-toplevel)
├── main/
│   ├── 20250108-session.md
│   └── plans/
│       └── main-20250108-feature.md
├── feature-branch/
│   ├── 20250107-session.md
│   └── reviews/
│       └── feature-branch-20250107-review.md
└── experiment-riper5/
    └── 20250108-session.md
```

## 使用提示
- 记忆记录按分支组织，以防止冲突
- 使用 `/memory:save` 保存重要上下文
- 使用 `/memory:recall` 检索特定记忆
- 计划和评审报告由RIPER模式自动存储