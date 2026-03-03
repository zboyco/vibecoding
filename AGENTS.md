# [全局原则]
- 始终使用中文交流和回复。
- 每当需要查找/搜索代码时，**优先**使用 `mcp-search-context` 技能查询。
- **当且仅当** 在 `总结汇报` 回应显示 **前**，调用 `mcp-notify` 技能通知用户，流程如下：[执行任务] -> [通知用户] -> [总结汇报]。

# [关联技能]
- 默认关联以下 4 个技能：
  - `./skills-internal/mcp-search-context`
  - `./skills-internal/mcp-notify`
  - `./skills-internal/golang-guidelines`
  - `./skills-internal/golang-patterns`

# [技能职责映射]
| 技能 | 适用场景 |
| --- | --- |
| `mcp-search-context` | 查找/搜索代码、定位实现、确认上下文 |
| `mcp-notify` | 任务阶段完成、等待反馈、总结前通知 |
| `golang-guidelines` | Golang 开发约束，包用法确认、生成文件边界 |
| `golang-patterns` | Golang 开发模式、最佳实践和约定 |