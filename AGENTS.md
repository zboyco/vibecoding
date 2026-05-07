# [全局原则]
- 始终使用中文交流和回复。
- 每当需要查找/搜索代码时，**优先**使用 `mcp-search-context` 技能查询。
- **当且仅当** 在 `总结汇报` 回应显示 **前**，调用 `mcp-notify` 技能通知用户，流程如下：[执行任务] -> [通知用户] -> [总结汇报]。

# [关联技能]
- 默认关联以下 5 个技能（相对当前文件路径）：
  - `./skills-internal/mcp-search-context`
  - `./skills-internal/mcp-notify`
  - `./skills-internal/golang-guidelines`
  - `./skills-internal/golang-patterns`
  - `./skills-internal/api-design`

# [技能职责映射]
| 技能 | 适用场景 |
| --- | --- |
| `mcp-search-context` | 查找/搜索代码、定位实现、确认上下文 |
| `mcp-notify` | 任务阶段完成、等待反馈、总结前通知 |
| `golang-guidelines` | Golang 开发约束，包用法确认、生成文件边界 |
| `golang-patterns` | Golang 开发模式、最佳实践和约定 |
| `api-design` | API 设计模式、最佳实践和约定 |

# [MCP 工具使用提示]
## gopls
- `gopls` MCP 工具用于 Go 语言服务级别的结构化理解、诊断、符号查询、引用分析、包 API 确认和重命名操作。
- 当目标文件、包、类型、函数或方法尚不明确时，先使用 `mcp-search-context` 定位业务上下文；当已经明确 Go 文件、包或符号后，再使用 `gopls` 做精确分析。
- 不要用 `gopls` 替代普通全文检索、非 Go 文件搜索或业务语义定位；这类场景仍优先使用 `mcp-search-context` 或 `rg`。

### 使用顺序
- 需要了解当前 Go 工作区整体情况时，先使用 `go_workspace`。
- 已知大致符号名、类型名、函数名或方法名，但不确定精确位置时，使用 `go_search`。
- 已经定位到具体 Go 文件，并准备理解或修改它时，使用 `go_file_context`。
- 涉及跨包调用、导出类型、接口、公共函数或包级 API 兼容性时，使用 `go_package_api`。
- 已经定位到具体符号，并需要确认调用点、影响范围或重构风险时，使用 `go_symbol_references`。
- 需要重命名 Go 符号时，必须优先使用 `go_rename_symbol` 生成跨工作区重命名编辑，避免手工替换遗漏引用。
- 修改 Go 代码后，应使用 `go_diagnostics` 检查解析、类型和构建诊断。
- 只有在涉及依赖安全、漏洞排查、依赖升级风险确认时，才使用 `go_vulncheck`；普通功能修改不默认运行。

### 工具职责
- `go_workspace`：总结 Go 工作区结构、模块和包概览，适合作为 Go 任务的全局入口。
- `go_diagnostics`：检查 Go 工作区解析、类型和构建错误；不能替代单元测试或集成测试。
- `go_file_context`：总结指定 Go 文件的跨文件依赖、相关符号和调用关系。
- `go_package_api`：总结一个或多个 Go 包的对外 API，包括导出类型、函数、方法和接口。
- `go_search`：在 Go 工作区内按符号名做模糊搜索；不要用于普通文本内容搜索。
- `go_symbol_references`：查找指定 Go 符号的引用位置，用于影响范围评估和重构前确认。
- `go_rename_symbol`：执行 Go 符号跨工作区重命名，优先于手工编辑。
- `go_vulncheck`：检查 Go 依赖漏洞和安全风险，仅在安全或依赖相关任务中使用。
