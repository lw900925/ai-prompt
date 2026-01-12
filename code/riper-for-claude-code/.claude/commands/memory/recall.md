---
description: 从当前分支的记忆库中检索记忆记录
---

# 从记忆库检索记忆

我将从支持分支感知的记忆库中检索记忆记录。

## ⚠️ 记忆库位置要求

**关键路径策略**：
- 记忆库必须位于仓库根目录：使用 `git rev-parse --show-toplevel` 查找根目录，然后定位到 `[根目录]/.claude/memory-bank/`
- 切勿创建包级别的记忆库：`packages/*/.claude/memory-bank/` ❌
- 在单体仓库中：根目录的一个记忆库服务于整个项目

### 检索记忆的正确与错误路径示例
✅ **正确**：`[根目录]/.claude/memory-bank/main/session.md`（其中根目录 = `git rev-parse --show-toplevel`）
❌ **错误**：`[根目录]/packages/react/.claude/memory-bank/main/session.md`
❌ **错误**：`packages/react/.claude/memory-bank/main/session.md`

## 当前上下文
- **分支**：!`git branch --show-current`
- **日期**：!`date +%Y-%m-%d`

## 自上次会话以来的Git历史记录

显示自上次记忆保存以来的提交记录：
```bash
last_memory=$(ls -t $(git rev-parse --show-toplevel)/.claude/memory-bank/$(git branch --show-current)/sessions/*.md 2>/dev/null | head -1)
if [ -n "$last_memory" ]; then
    last_date=$(stat -c %y "$last_memory" | cut -d' ' -f1)
    git log -n 10 --oneline --since="$last_date"
fi
```

显示记忆库的近期更改：
```bash
git log -n 5 -p -- .claude/memory-bank/
```

## 搜索范围
正在以下位置查找记忆记录：`[根目录]/.claude/memory-bank/!`git branch --show-current`/`（其中根目录 = `git rev-parse --show-toplevel`）

## 搜索查询
$ARGUMENTS

## 可用的记忆记录

`!ls -la $(git rev-parse --show-toplevel)/.claude/memory-bank/$(git branch --show-current)/ 2>/dev/null || echo "当前分支未找到记忆记录"`

我将根据您的查询搜索并显示相关的记忆记录，同时提供自上次会话以来的Git历史上下文。