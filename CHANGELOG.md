# Changelog

本仓库遵循语义化版本。仓库结构遵循 Agent Skills 规范的 `skills/*/SKILL.md` 布局，可由 `gh skill` 直接安装与更新。

## [v0.1.0] - 2026-08-16

首个公开发布版本。

### 新增

- 复用优先流程：首个开发回合必须以用户可见的“复用决策”结束；关键约束变化后重新评估。
- 五道门禁：复用决策、设计批准、最小纵向闭环、逐项验收对账、安全与发布检查。
- 工具无关：不依赖 Trellis、CodeGraph 等任何特定能力，缺失时自动降级为等价简化流程。
- 证据驱动：统一 E1/E2/E3 证据等级；重要写入必须核验实际落盘；完成前逐项验收对账。
- 长任务支持：按可独立验收的里程碑推进，禁止无信息量的进度句。
- 双语 README、4 个真实示例（含 Mind Journal 端到端案例）。
- MIT 许可。

### 安装

```bash
gh skill install zhizhixia/enough enough --agent codex --scope user
```

或手动拷贝 `skills/enough/` 到客户端 skills 目录。
