---
description: 进入计划模式以创建详细的技术规范
---

为以下任务激活plan-execute智能体，进入计划子模式：
$ARGUMENTS

该智能体将在计划子模式下运行：创建包含编号步骤的详尽规范。

通过以下方式将计划保存至仓库根目录：
1.  首先运行：`git rev-parse --show-toplevel` 以获取仓库根目录路径
2.  然后在以下位置创建计划：`[根目录]/.claude/memory-bank/[分支名]/plans/[分支名]-[日期]-[功能].md`

重要提示：切勿相对于当前目录创建计划。始终使用仓库根目录。

示例：如果 `git rev-parse --show-toplevel` 返回 `/path/to/repo`，则保存到：
`/path/to/repo/.claude/memory-bank/分支名称/plans/分支名称-2025-01-06-功能名称.md`