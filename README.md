# skills

此仓库用于存放“skills”（技能/模板/流程），目标是把 AI 的零散输出转成结构化、可学习、可验证、可维护的教学材料。

当前状态（简要）
- 仓库：https://github.com/okwillbe/skills
- 目前我们将专注于一个核心 skill：generate-learning-material（用于生成高质量、可维护的学习资料）。

设计原则（本仓库遵循）
- 可复现：每个自动生成的文档包含前置元数据（来源、生成器、模型、prompt SHA、时间戳、相关 commit）。
- 可审计：每次生成/更新写入生成日志（generation-log.json 或单文档 log），便于回溯与人工审核。
- 不直接覆盖：自动化生成产物默认通过 PR 提交，人工 review 后合并（CI 做基础校验）。
- 可扩展：后续可加入更多 skills（例如：design-skills、research-skills），但当前只实现并改进一个 skill 以解决当前需求。

如何使用（目前流程）
1. 我将把“增强版 generate-learning-material skill”写成一个 Markdown 文件放到 `skills/` 目录下，文件名建议：
   - `skills/generate-learning-material-advanced.md`
2. 该 skill 定义：输入、输出、元数据 frontmatter、生成日志格式、sources snapshot 策略、CI 验证规则、再生成策略等。
3. 当需要为某个主题（例如 pydantic）生成文档时：
   - 通过一个生成脚本（tools/generate.py）或手动把 prompt 发给 LLM，得到草稿后将其作为 PR 提交到 `content/` 下；
   - PR 会包含 generation-log（JSON）并由 CI 运行基础校验（frontmatter、示例数量、练习数量、代码块存在性）;
   - 人工 reviewer 确认内容后合并；如果 sources 发生变化，CI/定时任务会自动提出再生成的 PR。

放置位置（约定）
- skill 文档（模板/流程）： `skills/` 目录（如 `skills/generate-learning-material-advanced.md`）
- prompt 模板： `prompt-templates/` 目录
- 生成的学习资料： `content/{category}/{topic}/{YYYYMMDD}-{slug}.md`
- 来源快照： `content/snapshots/{sha256}.txt`
- 全局生成日志： `logs/generation-log.json`（或每文档单独 log 文件）

我接下来的两步建议（请选择其一）
- A) 我现在把“增强版 generate-learning-material”skill（含 frontmatter 模板、generation-log 示例和 CI 检查示例）直接提交到 `skills/generate-learning-material-advanced.md`，并在 `content/` 下创建一个占位的 pydantic 文档与 logs 示例（推荐，用于立刻跑 CI 检查）；
- B) 我先把增强版 skill 的完整 Markdown 内容贴到这里，你审阅并确认后我再提交到仓库（适合需要先修改细节的场景）。

备注
- 目前我们仅实现并维护一个 skill，以便把流程打通并修正细节，之后再把经验复制到更多 skill 类型。若你同意，我会直接提交 A（会写入主分支 main）；如果你希望先 review，请选 B。

请回复 “A” 或 “B”。若选择 A，可同时指定是否要创建一个新分支（例如 `feature/generate-skill`），否则我会直接提交到 `main`。