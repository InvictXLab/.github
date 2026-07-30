# Pull Request Standard

本规范适用于 InvictXLab 组织中的所有 Pull Request（PR），无论作者是人、Agent 还是自动化。

## 标题

标题使用 Conventional Commits 语法：

```text
<type>(<optional-scope>)!: <summary>
```

- `type` 必须是 `feat`、`fix`、`docs`、`refactor`、`test`、`build`、`ci`、`chore`、`perf` 或 `revert`。
- `scope` 可选，使用小写 ASCII 字母、数字、点、斜杠、下划线或连字符。
- `!` 表示 breaking change。
- `type`、`scope` 和代码标识符使用英文；`summary` 默认使用简体中文。

## 正文

每个 PR 必须包含以下四个二级标题，且每节都要提供有意义的内容：

```md
## Why

## What changed

## Validation

## Risk and rollback
```

不适用时说明原因，不能只写 `N/A`。Issue、Spec、ADR、截图、部署说明和跨仓依赖按需补充，不作为所有 PR 的固定区块。

`Validation` 必须记录实际执行的证据。测试命令、硬件检查、文档校对、截图和人工验证都可以；具体要求以目标仓库的 `AGENTS.md` 和工具链为准。

## Draft 与 Ready

- Agent 创建 PR 时先开 Draft。
- 人可以直接创建 Ready PR，但必须已经完成实现、自查和 Validation，并确保正文与最新 diff 一致。
- Ready 表示现在值得占用 reviewer 时间，不表示“先开出来再说”。

## Review

- Ready PR 应获得至少一个非作者 approval。
- 新 commit 改变 diff 后，旧 approval 视为失效，需要针对最新 diff 重新审批。
- 合并前应解决所有 review conversations。
- `dishonoreded` 可以在没有非作者 approval 时合并，但仍须满足本规范的其他要求。该例外不允许直接 push 默认分支，也不允许绕过检查或未解决评论。

## 跨仓改动

一项跨仓结果应拆成每仓一个独立 PR，组成一个 Change Series。每个 PR：

- 链接同一个 Issue、Spec 或变更记录；
- 写明依赖关系、推荐合并顺序和暂时不兼容窗口；
- 独立提供 Validation 与 Risk and rollback；
- 使用兼容设计处理无法原子合并的过渡期。

## 合并

- 只使用 Squash Merge。
- squash commit 标题使用已校验的 PR 标题。
- 合并后删除远端 head branch。
- 未收到明确合并请求时，Agent 不得自行 merge。

## 当前执行方式

PR Standard workflow 会把标题或正文结构不合规显示为失败。当前检查是 Advisory Check，不是 GitHub Merge Gate；即使 GitHub 仍显示 Merge 按钮，贡献者也应先修复失败项。
