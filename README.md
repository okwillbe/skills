# skills

这是一个存放可复用 "skills"（技能/模板/流程）的仓库。每个 skill 都是可复用的模板、提示词和流程，用来把零散的知识或 AI 输出组织成可学习、可维护的知识产物。

当前状态
- 仓库主页: https://github.com/okwillbe/skills
- 本仓库以中文为主文档语言（可双语贡献）。
- 当前只实现并维护第一个 skill：learning/generate-learning-material（用于生成结构化学习资料）。

目录结构（简要）
- skills/                    ← skill 模板与具体 skill 的所在目录
  - learning/                ← learning 类 skill 的集合
    - generate-learning-material/ ← 第一个 skill 的目录
      - generate-learning-material.md ← skill 文件（详述输入/输出/流程/质量检查/示例 prompt）
- prompt-templates/          ← 可直接复用的 prompt 模板
- content/                   ← 生成的学习资料（由 skill 产出，放在此处）
- content/snapshots/         ← 引用来源的快照（可选，但建议保存以便审计）
- logs/                      ← 生成日志（记录每次生成的元数据）
- tools/                     ← 校验脚本与辅助工具（如 snapshot fetcher）

使用说明
1. 查阅 `skills/learning/generate-learning-material/generate-learning-material.md` 了解第一个 skill 的输入/输出与使用流程；
2. 使用 prompt 模板（位于 `prompt-templates/`）调用 LLM 生成文档草稿；
3. 将生成的文档放入 `content/` 后提交 PR；CI 会验证 frontmatter 与质量检查项；
4. 审核通过后合并，生成日志会写入 `logs/generation-log.json` 以便追溯。

贡献
- 欢迎以 PR 形式提交新的 skill 或改进现有 skill。请确保每个 skill 文件遵循 `skills/skill-template.md` 中的 frontmatter 规范。

