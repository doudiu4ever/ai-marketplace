# AI Marketplace

个人常用 skill 集合，支持 Claude Code、Codex 和 Antigravity (agy) 插件安装。

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

### Antigravity (agy)

Antigravity 支持直接从 GitHub 仓库安装插件，无需单独注册 marketplace：

```bash
# 安装仓库内的全部插件（自动扫描 plugins/ 目录）
agy plugin install https://github.com/doudiu4ever/ai-marketplace

# 或仅安装单个插件
agy plugin install https://github.com/doudiu4ever/ai-marketplace/tree/main/plugins/dev-tool
```

安装到 `~/.gemini/config/plugins/`，在 Antigravity CLI 和 App 之间自动同步。

## 更新

已按上述方式安装后，在终端刷新或重新安装插件。

### Claude Code

```bash
claude plugin marketplace update ai-marketplace
claude plugin update dev-tool@ai-marketplace
```

更新后重启 Claude Code。

### Codex

```bash
codex plugin marketplace upgrade ai-marketplace
codex plugin add dev-tool@ai-marketplace
```

`upgrade` 刷新 marketplace 的 Git 快照，再用 `add` 安装其中的新版插件。更新后开启新会话。

### Antigravity (agy)

重新执行安装命令即可覆盖为最新版本：

```bash
# 更新仓库内的全部插件
agy plugin install https://github.com/doudiu4ever/ai-marketplace

# 或仅更新单个插件
agy plugin install https://github.com/doudiu4ever/ai-marketplace/tree/main/plugins/dev-tool
```

更新后开启新会话。

## 组件

### dev-tool

开发流程与协作文档工具，包含以下 skill：

- **requirements-to-review**：先讨论并确认需求，再按 checklist 实现。逐步模式每项完成后循环审核与修复，等待用户确认才继续下一项；全量模式全部实现后统一循环审核与修复，交由人工验收。
- **multi-agent-docs**：规范多个 AI agent 协作时的文档组织，保持入口文档同步、共享文档中立，避免工具专属规则混入通用说明。来自 [multi-agent-docs](https://github.com/doudiu4ever/multi-agent-docs)。

安装后可直接要求“使用 requirements-to-review 流程”或“使用 multi-agent-docs 整理文档”。Claude Code 和 Antigravity (agy) 也可输入 `/dev-tool:requirements-to-review` 或 `/dev-tool:multi-agent-docs`。

`requirements-to-review` 默认使用当前客户端可用的独立审核能力：Claude Code 可使用只读 reviewer，Codex 可使用 review 功能，Antigravity (agy) 默认自动使用只读子代理（或可委派独立只读 reviewer 的已安装 skill），也可按约定使用外部审核工具或手动审核方式。
