# skills

这是一个存放可复用 "skills"（技能/模板/流程）的仓库。每个 skill 都是一个可复用的模板、提示词或流程，用来把零散知识、文档或 AI 输出整理成可学习、可维护、可验证的知识产物。

当前状态
- 仓库：https://github.com/okwillbe/skills
- 当前聚焦的第一个 skill：`learning/generate-learning-material`
- 它用于解决“AI 生成的学习资料结构混乱、缺来源、缺解释、缺审计和更新策略”的问题。

仓库结构
- `README.md` — 仓库级说明
- `skills/learning/generate-learning-material/generate-learning-material.md` — 第一个 skill（当前重点）
- `prompt-templates/` — 可直接复用的 prompt 模板
- `content/` — 生成的学习资料
- `content/snapshots/` — 引用资源的来源快照（建议保存）
- `logs/` — 生成日志（生成时间、模型、来源、质量检查等）
- `tools/` — 校验脚本和辅助工具
- `.github/workflows/` — CI 校验工作流

当前重点
- 这个仓库目前只实现并维护一个 skill：`generate-learning-material`
- 后续可以依照同样模式扩展更多 skill（如 `research`, `design`, `problem-solving` 等）

开始使用
1. 阅读 `skills/learning/generate-learning-material/generate-learning-material.md`
2. 按 skill 中的流程生成学习资料草稿
3. 将输出保存到 `content/` 下，附上生成日志
4. 通过 PR 提交，后续可由 CI 校验前置元数据和基本质量要求
