# RIPER 工作流程 - Claude Code 版

**R**esearch（研究） • **I**nnovate（创新） • **P**lan（规划） • **E**xecute（执行） • **R**eview（审查）

一个结构化的、上下文高效的开发工作流程，用于 [Claude Code](https://github.com/anthropics/claude-code/)，使用 [自定义斜杠命令](https://docs.anthropic.com/en/docs/claude-code/slash-commands#custom-slash-commands) 和 [子代理](https://docs.anthropic.com/en/docs/claude-code/sub-agents)。

## 🎯 概览

RIPER 创建了一个受控的、引导式的流程，强制在研究、规划和执行阶段之间进行分离。这有助于：

- 通过专门的代理减少上下文使用
- 防止在理解之前进行过早实现
- 维护清晰的决策文档记录
- 启用可重复的开发流程

## 🚀 快速开始

### 安装

1. 将 `.claude` 目录复制到你的项目根目录：
```bash
cp -r .claude /path/to/your/project/
```

2. 用你的项目详情更新 `.claude/project-info.md`

3. 使用你的技术栈和路径自定义 `.claude/riper-config.json`

4. 可选：将 `.claude/memory-bank/` 添加到 `.gitignore` 以保持计划和审查的隐私性：

   ```bash
   echo ".claude/memory-bank/" >> .gitignore
   ```

   或有选择性地仅忽略计划和审查，同时保留记忆库结构：

   ```bash
   echo ".claude/memory-bank/*/plans/" >> .gitignore
   ```

   ```bash
   echo ".claude/memory-bank/*/reviews/" >> .gitignore
   ```

   注意：如果你不小心提交了这些文件，在合并前删除它们：

   ```bash
   git rebase -i HEAD~n  # 其中 n 是要查看的提交数
   ```

### 基本用法

启动引导式 RIPER 会话：

```
/riper:strict
```

然后使用工作流命令：

1. **研究** - 调查代码库

   ```
   /riper:research analyze authentication system
   ```

2. **规划** - 创建技术规格说明书

   ```
   /riper:plan add OAuth2 support
   ```

3. **执行** - 实现批准的计划

   ```
   /riper:execute
   ```

   或执行特定的子步骤：

   ```
   /riper:execute 2.3
   ```

4. **审查** - 验证实现
   ```
   /riper:review
   ```

## 📚 命令参考

### RIPER 工作流命令

| 命令                     | 描述                     | 模式限制         |
| ----------------------- | ------------------------ | --------------- |
| `/riper:strict`         | 启用严格协议强制           | 无               |
| `/riper:research`       | 进入研究模式（只读）        | 只读             |
| `/riper:innovate`       | 头脑风暴方法（可选）        | 只读             |
| `/riper:plan`           | 创建技术规格说明书          | 读 + 写入记忆库   |
| `/riper:execute`        | 实现批准的计划             | 完全访问          |
| `/riper:execute <step>` | 执行特定的计划步骤          | 完全访问         |
| `/riper:review`         | 根据计划进行验证            | 读 + 测试执行    |
| `/riper:workflow`       | 完整引导式工作流            | 因阶段而异       |

### 记忆库命令

| 命令                      | 描述                   |
| ------------------------ | ---------------------- |
| `/memory:save <context>` | 保存重要的上下文         |
| `/memory:recall <topic>` | 检索保存的上下文         |
| `/memory:list`           | 列出所有记忆            |

## 🏗️ 架构

### 代理

RIPER 为了提高效率使用 3 个合并代理：

1. **research-innovate** - 处理研究和头脑风暴阶段
2. **plan-execute** - 管理规划和实现
3. **review** - 验证实现是否符合规格说明书

### 记忆库结构

```
.claude/memory-bank/
├── main/                  # 主分支记忆
│   ├── plans/            # 技术规格说明书
│   ├── reviews/          # 代码审查报告
│   └── sessions/         # 会话上下文
└── [feature-branch]/     # 功能分支记忆
    └── ...
```

### 模式能力

| 模式     | 读 | 写 | 执行 | 规划 | 验证 |
| -------- | ---- | ----- | ------- | ---- | -------- |
| RESEARCH | ✅   | ❌    | ❌      | ❌   | ❌       |
| INNOVATE | ✅   | ❌    | ❌      | ❌   | ❌       |
| PLAN     | ✅   | 📄\*  | ❌      | ✅   | ❌       |
| EXECUTE  | ✅   | ✅    | ✅      | ❌   | ❌       |
| REVIEW   | ✅   | 📄\*  | ✅\*\*  | ❌   | ✅       |

\* 仅限记忆库
\*\* 仅限测试执行

## 🔧 配置

### project-info.md

更新你的项目详情：

- 项目名称和描述
- 常见命令
- 目录结构
- 技术栈
- 开发指南

### riper-config.json

自定义工作流程设置：

- 重要路径
- 技术栈模式
- 记忆库配置
- 代理模型

### settings.json

Claude Code 项目设置：

- 项目名称
- 描述
- 自定义指令

## 💡 提示与最佳实践

### 何时使用 RIPER

✅ **适合于：**

- 复杂的多步骤功能
- 重构关键代码
- 实施架构更改
- 需要仔细规划的任务

❌ **跳过以下情况：**

- 简单的错误修复
- 次要的文本更改
- 直接的更新
- 探索性编码

### 工作流提示

1. **始终从研究开始** - 在编码前理解可以防止浪费精力
2. **使用记忆库** - 保存重要上下文以供未来会话使用
3. **在计划中要具体** - 详细的规格说明书导致准确的实现
4. **无情地审查** - 尽早发现偏差
5. **在子步骤上迭代** - 使用 `/riper:execute 2.3` 来修复特定部分

### 上下文效率

- 研究阶段使用更便宜的、聚焦的工具
- 计划保存到记忆库，减少重复
- 执行阶段拥有来自批准计划的完整上下文
- 审查验证而无需重新实现

## 🤝 贡献

欢迎改进！重点领域：

- 其他工作流命令
- 更好的记忆管理
- 增强的代理能力
- 集成示例

## 📜 致谢

此实现基于由匿名贡献者 ([robotlovehuman](https://forum.cursor.com/u/robotlovehuman/)) 在 [Cursor Forums](https://forum.cursor.com/t/i-created-an-amazing-mode-called-riper-5-mode-fixes-claude-3-7-drastically/65516)上创建的 RIPER-5 工作流程。

## 📄 许可证

MIT - 可在你的项目中自由使用

---

## 示例会话

启动严格模式（始终）：

```bash
/riper:strict
```

研究现有代码：

```bash
/riper:research analyze current API structure
```

创建计划：

```bash
/riper:plan add rate limiting to API endpoints
```

在 `.claude/memory-bank/main/plans/` 中查看生成的计划：

```bash
/riper:execute
```

或执行特定步骤

```bash
/riper:execute 1.2
```

```bash
/riper:execute 2
```

验证实现：

```bash
/riper:review
```

## 故障排除

**问：命令不起作用？**  
答：确保 `.claude` 目录在项目根目录中

**问：记忆库没有保存？**  
答：检查 `.claude/memory-bank/` 上的写入权限

**问：代理出错？**  
答：验证 `riper-config.json` 是否为有效的 JSON

**问：如何为我的项目自定义？**  
答：从 `project-info.md` 和 `riper-config.json` 开始

## 致敬

[![Mentioned in Awesome Claude Code](https://awesome.re/mentioned-badge.svg)](https://github.com/hesreallyhim/awesome-claude-code)