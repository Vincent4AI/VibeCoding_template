# VibeCoding Template

**SDD (Spec-Driven Development) + Claude Code 项目初始化模板**

一个为 Claude Code vibecoding 工作流设计的项目模板。新建项目时，使用初始化 prompt 一键生成完整的开发框架：规范驱动开发体系、进度追踪、跨会话记忆。

## 为什么需要这个模板？

Vibecoding 很爽，但项目一大就容易失控：

- Claude Code 每次对话都是"失忆"的，上下文丢失
- 没有规范约束，生成的代码风格不统一
- 改了东西不知道改到哪了，进度追踪靠脑子
- 模块之间接口没对齐，联调时到处是坑

**这个模板用 SDD 流程 + 自动化进度追踪解决这些问题。**

## 核心理念

```
先写规范 → 再写代码 → 自动追踪
```

| 机制 | 解决什么问题 |
|------|-------------|
| `CLAUDE.md` | 统一编码约定、接口定义、禁止操作 |
| `TODO.md` | 功能路线图，完成即自动打勾 |
| `docs/sdd/STATUS.md` | 模块状态矩阵，一目了然 |
| `docs/sdd/specs/` | 模块规范，约束代码生成 |
| `MEMORY.md` | 跨会话记忆，不再重复解释上下文 |

## 快速开始

### 1. 新建项目目录

```bash
mkdir my-project && cd my-project
```

### 2. 打开 Claude Code

```bash
claude
```

### 3. 粘贴初始化 Prompt

复制 [`init-prompt.md`](./init-prompt.md) 的内容，填好 6 个项目信息字段：

```
- 项目名称: my-awesome-app
- 一句话描述: 一个做 XX 的工具
- 语言/技术栈: TypeScript + Node.js
- 构建工具: npm
- 测试框架: Jest
- 数据库: PostgreSQL
```

粘贴到 Claude Code 发送，**一次性自动生成所有文件**。

### 4. 开始开发

生成的文件结构：

```
my-project/
├── CLAUDE.md                          # 项目约定 (Claude Code 自动读取)
├── TODO.md                            # 开发路线图
├── docs/
│   └── sdd/
│       ├── README.md                  # SDD 流程说明
│       ├── STATUS.md                  # 模块状态矩阵
│       ├── templates/
│       │   └── module-spec.tmpl.md    # 模块规范模板
│       ├── specs/                     # 各模块的规范文档
│       └── adr/                       # 架构决策记录
│           ├── README.md
│           └── template.md
└── .claude/projects/.../memory/
    └── MEMORY.md                      # 跨会话记忆
```

## SDD 开发流程

```
┌─────────┐    ┌─────────┐    ┌──────────┐    ┌─────────┐    ┌──────────┐
│  Draft  │───▶│ Review  │───▶│ Approved │───▶│  Impl   │───▶│ Verified │
└─────────┘    └─────────┘    └──────────┘    └─────────┘    └──────────┘
  写规范        评审规范        规范通过        编写代码       测试通过
```

**每完成一个模块，Claude Code 自动更新：**
1. `TODO.md` — 打勾 `[x]`
2. `docs/sdd/STATUS.md` — 更新状态矩阵
3. `MEMORY.md` — 更新跨会话记忆

## 自动进度追踪

这是模板的核心特性。在 `CLAUDE.md` 中内置了强制指令：

> 完成任何模块或功能的实现后，Claude Code **必须** 自动更新 TODO.md、STATUS.md、MEMORY.md，无需用户提醒。

你不需要手动维护进度，专注写需求就好。

## 模板文件说明

| 文件 | 作用 |
|------|------|
| `init-prompt.md` | 初始化 prompt，新项目时复制粘贴使用 |
| `README.md` | 本说明文件 |

## 适用场景

- 个人项目的 vibecoding 开发
- 需要 Claude Code 长期维护的项目
- 多模块、需要接口对齐的中大型项目
- 任何想让 AI 编码更可控的场景

## License

MIT
