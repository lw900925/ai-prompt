---
description: 将上下文保存至支持分支感知的记忆库
---

# 保存至记忆库

## ⚠️ 记忆库位置要求

**关键路径策略**：
- 记忆库必须位于仓库根目录：使用 `git rev-parse --show-toplevel` 查找根目录，然后定位到 `[根目录]/.claude/memory-bank/`
- 切勿创建包级别的记忆库：`packages/*/.claude/memory-bank/` ❌
- 在单体仓库中：根目录的一个记忆库服务于整个项目

### 正确与错误路径示例
✅ **正确**：`[根目录]/.claude/memory-bank/main/session.md`（其中根目录 = `git rev-parse --show-toplevel`）
❌ **错误**：`[根目录]/packages/react/.claude/memory-bank/main/session.md`
❌ **错误**：`packages/react/.claude/memory-bank/main/session.md`

我将把以下信息保存至支持分支感知的记忆库：

## 上下文信息
- **日期**：!`date +%Y-%m-%d`
- **时间**：!`date +%H:%M:%S`
- **分支**：!`git branch --show-current`
- **最新提交**：!`git log -1 --oneline`
- **工作目录状态**：!`git status --short`

## 记忆内容
$ARGUMENTS

## 存储位置
记忆将保存至：
1. 首先运行：`git rev-parse --show-toplevel` 以获取仓库根目录
2. 保存到：`[根目录]/.claude/memory-bank/!`git branch --show-current`/!`date +%Y%m%d`-session.md`

这确保了记忆记录：
- 具有分支特异性（切换分支时不会冲突）
- 按日期组织（便于查找近期工作）
- 跨会话持久保存
- 可与团队共享（如需可提交至版本控制）