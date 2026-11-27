# 审核记录分层与平级审核方式

状态：已完成
需求确认依据：用户在当前会话中明确确认需求边界、过程细节严格置于 git 仓库目录之外、全量执行模式及宿主内置只读 `research` 子代理审核方式
执行模式：全量
当前实现范围：本次需求全部 checklist 项
审核范围：全部未提交变更（已暂存、未暂存及未跟踪内容）
审核方式：宿主内置只读 `research` 子代理（同宿主、带完整上下文、无外部代码外发；用户显式选择）

## 需求与范围

- **目标**：调整 `requirements-to-review` skill 的文档落盘分层与独立审核方式定位，使“审核循环收敛”、“忽略项长期可追溯”与“不污染 git 提交”同时成立。
- **核心边界**：
  1. **git 工作区内（随任务提交进 git）**：主体需求文档必须放在项目 git 工作区内，包含需求/范围/验收、概括性的验证与审核记录（审出了什么、修复了什么、忽略了什么；修复项已有代码与需求文档变更，只做简要记录）以及专门的 `## 审核忽略区`（留作长期追溯，并让无显式上下文的独立 reviewer 仅读取未提交变更即可识别已裁定边界）。
  2. **git 仓库目录之外（严格不进 git 仓库）**：每轮独立审核的原始细节记录/核查流水，以及修复过程中的详细测试数据与过程日志，严格保存在 git 仓库目录之外，不纳入 git 追踪、不污染仓库提交。
  3. **独立审核方式平级可选**：审核仍由 skill 发起，显式注入上下文的独立审核（如宿主内置只读子代理、`codex review -` 等）与不带显式上下文、直接审核未提交变更的独立审核（如 `codex review --uncommitted`）调整为平级选项，由用户自由选择；外部工具需经用户选定/授权的安全底线保持不变。
  4. **无上下文审核自洽**：在 `## 审核忽略区` 与简要审核记录模板中提供简短自说明，明确忽略区为已裁定边界、细节流水在仓库目录之外，避免 reviewer 重复提示已覆盖项或对忽略区文案本身发散挑刺。
- **非目标**：不改变 `requirements-to-review` 的触发规则、逐步/全量执行模式语义、次生发散自检与收敛退出条件，不新增固定任务文档目录名约定，不改动其他 skill。

## 验收条件

- [SKILL.md](../plugins/dev-tool/skills/requirements-to-review/SKILL.md) 明确规定主体需求文档（含简要审核记录与专门的审核忽略区）在 git 工作区内并随任务提交，过程细节记录与详细测试数据严格放在 git 仓库目录之外，且前后章节（文档落盘、验证证据、调用审核、处理每轮结果、交付提交）口径一致无矛盾。
- [SKILL.md](../plugins/dev-tool/skills/requirements-to-review/SKILL.md)、[review-invocation.md](../plugins/dev-tool/skills/requirements-to-review/references/review-invocation.md) 与 [README.md](../README.md) 将“显式注入上下文审核”与“不带显式上下文的未提交变更审核（如 `codex review --uncommitted`）”列为平级选项，移除将 `codex review --uncommitted` 降级为仅作补充检查或默认偏重单一方式的表述，同时保留外部工具授权底线。
- 三端 `plugin.json` 版本号同步递增为 `0.2.10` 且 JSON 校验、`agy plugin validate ./plugins/dev-tool` 与 `git diff --check` 全部通过。
- 独立只读 `research` 子代理审核全部未提交变更后明确报告无问题。

## 实现 checklist

- [x] 更新 [SKILL.md](../plugins/dev-tool/skills/requirements-to-review/SKILL.md) 的第 2、3、4、5 节及模板，落地文档分层、简要记录、审核忽略区自说明与平级审核方式。
- [x] 更新 [review-invocation.md](../plugins/dev-tool/skills/requirements-to-review/references/review-invocation.md) 与 [README.md](../README.md)，将 `codex review --uncommitted` 与显式注入上下文方式调整为平级选项，并同步复审和仓外记录约定。
- [x] 同步递增三端 `plugin.json` 版本号至 `0.2.10`，完成 JSON、`agy plugin validate` 与 `git diff --check` 校验。
- [x] 使用宿主内置只读 `research` 子代理完成全部未提交变更的独立审核修复循环。

## 验证与审核记录

- **本地校验通过**：`SKILL.md` 23907 字节；5 份 JSON 清单语法与两空格缩进、`agy plugin validate ./plugins/dev-tool --strict`（0 error / 0 warning）及 `git diff --check` 全部通过。
- **独立审核通过（1 轮收敛）**：宿主内置只读 `research` 子代理审核全部 7 个未提交文件及关联约定文档，结论为“本轮无问题”（审出 0 项、修复 0 项、忽略 0 项）。逐轮审核原始记录与校验日志严格保存在 git 仓库目录之外。
- **未验证部分**：未在 Claude Code、Codex、Antigravity 三端实际执行插件安装/更新及新会话端到端运行验证（本次未修改安装配置与 marketplace 索引结构）。

## 审核忽略区

本区记录已裁定暂缓/忽略的问题与边界，随任务提交进 git 供长期追溯；独立审核仅在新改动或新证据表明存在超出下列边界的实质影响时重开，不对忽略区记录本身做次生审查。

暂无。

## 人工审核与交付

人工审核通过；用户已授权执行 `git commit` 与 `git push`，随本次提交完成交付。
