# AGENTS.md

本文件是 Agent 的最小启动与导航协议，不重复完整规则。

## 开始工作

1. 先读 `README.md`，了解仓库定位、职责边界和入口。本仓库主要保存研究知识与协作状态，不是源代码仓库；具体实现和测试在对应代码仓库进行。
2. 根据任务读取适用规则，不要无差别加载全部规则：
   - 修改文档：先读 `rules/documentation.md`。
   - 推进研究：读 `rules/workflows/research.md`，并按需读取相关专题文档。
   - 修改或审查规则：读 `rules/meta.md`。
   - 涉及 Draft：读 `rules/drafts.md`。
   - 日常巡检或跨仓库同步：读 `rules/workflows/daily-maintenance.md`。
   - 使用 Discussions、Issues 或 Docs 协作：读 `rules/research-collaboration.md`。
   - 涉及代码维护：读 `rules/code-maintenance.md`，并在对应代码仓库操作。
3. 涉及当前项目方向或约束时，先查 `docs/decisions-and-views.md` 及相关专题文档。

## 工作原则

- `rules/` 定义协作约定，`docs/` 保存当前有效知识；本文件只负责导航。具体问题以适用规则和已确认决策为准。
- 区分背景、已确认决策、证据、假设与暂用假设；不得把推断静默升级为事实或用户决策。
- 只维护当前有效状态，历史由 Git 保存；删除或调整内容时，按文档约定清理失效描述和引用。
- `rules/` 主要由人审视和调整；除非用户明确要求或任务本身是规范审查，不要自行修改规则。
- 低风险普通文档维护按适用流程执行；代码变更、破坏性操作和重大取舍不会因整理任务自动获得授权。
- 完成后简要报告改动范围、验证情况及仍待决定事项。
