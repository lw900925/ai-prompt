# [您的项目名称] - 项目信息

## 项目概述
[在此处添加您的项目描述]

## 基本命令

### 开发

```bash
# 在此处添加您项目的常用命令
# 例如：
# npm install
# npm run dev
# npm run build
# npm test
```

## 目录结构

```text
您的项目/
├── src/          # 请根据您的实际结构调整
├── tests/        # 您的测试目录
├── docs/         # 您的文档目录
└── .claude/      # RIPER工作流程配置
```

## 技术栈
- [在此处添加您的技术栈]
- [例如：React, Node.js, Python 等]

## RIPER 工作流程

本项目采用RIPER开发流程，以实现结构化、上下文高效的开发。

### 可用命令
- `/riper:strict` - 启用严格的RIPER协议执行
- `/riper:research` - 研究模式，用于信息收集
- `/riper:innovate` - 创新模式，用于头脑风暴（可选）
- `/riper:plan` - 计划模式，用于制定规范
- `/riper:execute` - 执行模式，用于实现
- `/riper:execute` <子步骤> - 执行计划中的特定子步骤
- `/riper:review` - 评审模式，用于验证
- `/memory:save` - 将上下文保存至记忆库
- `/memory:recall` - 从记忆库检索信息
- `/memory:list` - 列出所有记忆记录

### 工作流程阶段

- **研究与创新** - 理解并探索代码库与需求
- **计划** - 创建详细的技术规范并保存至记忆库
- **执行** - 严格按照已批准的计划进行实现
- **评审** - 根据计划验证实现结果

### 使用工作流程

1. 从 `/riper:strict` 开始以启用严格模式
2. 使用 `/riper:research` 调研代码库
3. （可选）使用 `/riper:innovate` 进行头脑风暴和方法探索
4. 使用 `/riper:plan` 创建计划
5. 使用 `/riper:execute` 执行（或使用 `/riper:execute 1.2` 执行特定步骤）
6. 使用 `/riper:review` 进行验证

## 记忆库策略

### **⚠️ 关键**：仓库级记忆库

- 记忆库位置：使用 `git rev-parse --show-toplevel` 查找根目录，然后定位到 `[根目录]/.claude/memory-bank/`
- 切勿在子目录或包中创建记忆库
- 所有记忆记录均支持分支感知并按日期组织
- 记忆记录跨会话持久保存，可与团队共享

### 记忆库结构

```text
.claude/memory-bank/
├── [分支名称]/
│   ├── plans/      # 技术规范
│   ├── reviews/    # 代码评审报告
│   └── sessions/   # 会话上下文
```

## 开发指南

- [在此处添加您项目特定的开发指南]
- 遵循现有代码模式
- 为新功能编写测试
- 为复杂逻辑编写文档