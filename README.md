# AI Marketplace

个人常用 skill 集合，支持 Claude Code 和 Codex 插件安装。

## 安装

通过 Git 仓库安装，无需提前克隆。在终端执行对应命令，安装后开启新会话。

### Claude Code

```bash
claude plugin marketplace add https://github.com/doudiu4ever/ai-marketplace.git
claude plugin install dev-tool@ai-marketplace
```

### Codex

```bash
codex plugin marketplace add https://github.com/doudiu4ever/ai-marketplace.git
codex plugin add dev-tool@ai-marketplace
```

## 组件

### dev-tool

开发流程与协作文档工具，包含以下 skill：

- **requirements-to-review**：先讨论并确认需求，再按 checklist 实现。逐步模式每项完成后循环审核与修复，等待用户确认才继续下一项；全量模式全部实现后统一循环审核与修复，交由人工验收。
- **multi-agent-docs**：规范多个 AI agent 协作时的文档组织，保持入口文档同步、共享文档中立，避免工具专属规则混入通用说明。来自 [multi-agent-docs](https://github.com/doudiu4ever/multi-agent-docs)。

安装后可直接要求“使用 requirements-to-review 流程”或“使用 multi-agent-docs 整理文档”。Claude Code 也可输入 `/dev-tool:requirements-to-review` 或 `/dev-tool:multi-agent-docs`。

`requirements-to-review` 的自动审核需要安装并配置 Codex CLI，包括在 Claude Code 中使用时。
