---
name: grill-with-docs
description: 一场持续的采访，用于打磨计划或设计，同时随着进展创建文档（ADR 和词汇表）。（副作用：读写仓库 CONTEXT.md/ADR）
disable-model-invocation: true
---

## ⚠️ 副作用与边界（市场审核披露）

- **文件**：读写仓库 CONTEXT.md、ADR
- **网络**：不直接访问外部网络
- **命令**：不直接执行命令
- **凭据/敏感数据**：不接触凭据或敏感数据
- **人工确认**：所有高影响操作均由用户确认后执行。


调用 Skill 工具两次，分别是 "grilling" 和 "domain-modeling"。
