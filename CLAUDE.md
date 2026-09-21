# Repository Guidelines

## 项目定位

这是个人 plugin marketplace，收录自己常用的 skill。同时支持 Claude Code 和 Codex 通过各自的 plugin 安装机制使用，共用同一份 skill 内容。

## 目录结构

- `plugins/<plugin-name>/`：独立插件，当前有 `dev-tool`。
- `plugins/<plugin-name>/skills/<skill-name>/SKILL.md`：skill 定义与执行说明。
- `.agents/plugins/marketplace.json`、`.claude-plugin/marketplace.json`：两端 marketplace 索引。
- 插件内的 `.codex-plugin/plugin.json`、`.claude-plugin/plugin.json`：两端插件清单。
- `README.md`：面向用户，仅包含安装说明和组件简介。

## 维护约定

- 新增或调整插件时，同时考虑 Claude Code 和 Codex 的发现、安装及加载方式；平台配置分别维护，skill 正文保持单一来源。
- 两端 marketplace 条目同步维护；插件清单中的名称、版本、描述和作者保持一致。
- 插件和 skill 目录使用小写连字符命名；`SKILL.md` 保留 `name`、`description` front matter，名称与目录一致。
- 说明文档以中文为主，指令简短、可执行；JSON 使用两空格缩进。
- `AGENTS.md` 与 `CLAUDE.md` 保持相同的项目规则。详细用法和安装步骤放在共享文档中，分别说明两个平台的操作。
- 修改聚焦当前需求，保留已有工作，不引入无关基础设施。

## 验证与交付

- 当前无构建流程或自动化测试。修改清单后使用 `python3 -m json.tool <文件路径>` 检查 JSON，并核对引用路径与名称。
- 修改安装配置后，分别验证两个平台；未实际验证的部分明确说明。
- 提交前检查 `git status --short` 和 `git diff --check`；未跟踪文件需单独查看。
- 提交说明简短描述目的；交付时说明变更、验证结果及尚未完成的事项。仅在用户授权后执行 commit 或 push。
