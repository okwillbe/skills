# Skill: generate-learning-material-advanced

类别: learning
摘要: 用 AI 生成高质量、可学习、可维护的学习资料，并记录来源、生成日志、版本信息、更新策略与质量检查要求。

目标
- 解决当前痛点：AI 生成的学习资料常见问题包括：
  - 缺少介绍与用途说明；
  - 直接给示例，不解释原理；
  - 缺少来源与可验证信息；
  - 内容乱、前后不一致；
  - 不知道文档该放在哪里，也没有更新/再生成策略。

适用场景
- 想学习新技术或库（例如：pydantic、FastAPI、React Hooks、AI Agent、MCP 等）
- 需要将零散材料整理成一个结构化教程
- 需要把 AI 输出变成可审计、可维护、可复用的教学材料

目标受众
- 有 Python / JS / Java 等基础的工程师
- 课程作者、内容设计师、技术博主
- 想用 AI 生成学习资料但怕内容杂乱的人

前置要求
- 指定主题（例如：pydantic）
- 指定目标受众（例如：有 Python 基础的初学者）
- 指定学习目标（例如：1 小时速成 / 能在项目里使用）
- 产出可选择：Markdown / HTML / 复习卡片 / 文档站（可选）

输入（必填）
- topic: 主题名称
- audience: 目标读者
- goal: 学习目标
- references: 参考来源（URL / 文档 / 代码 / 实验输出）
- output_style: markdown / notebook / article / lesson-plan

输出（必须包含）
1. 一句话概览：主题是什么、解决什么问题、适合谁
2. 2 个现实应用场景
3. 前置知识与版本依赖说明
4. 章节目录（TOC）
5. 核心概念分解（每个概念 1-3 段，含类比）
6. 3 个可运行示例（由浅入深，逐行/逐块解释）
7. 常见坑与排查建议（至少 6 条）
8. 2 个练习题（含提示和参考答案）
9. 5 条复习卡片（Q/A）
10. 速查表（类/函数/参数）
11. 参考资源（按入门 → 进阶排序）
12. 固定元数据字段（见下）
13. 生成日志（见下）

文档存放规范
- 生成物统一目录：
  - `content/{category}/{topic}/{YYYYMMDD}-{slug}.md`
  - 示例：`content/learning/pydantic/20261014-pydantic-quickstart.md`
- 生成物对应日志：
  - `logs/{category}/{topic}/{YYYYMMDD}-{slug}.json`
  - 或全局日志：`logs/generation-log.json`
- 来源快照（可选，但强烈建议）：
  - `content/snapshots/{sha256}.txt`

文档头部元数据��frontmatter）
必须在每个生成文档顶部添加 YAML frontmatter：

```yaml
---
title: "Pydantic 速成（1 小时）"
slug: "pydantic-quickstart"
category: "learning"
topic: "pydantic"
target_audience: "有 Python 基础的初学者"
runtime_env: "Python 3.10, pydantic==2.0"
references:
  - url: "https://docs.pydantic.dev/"
    title: "Pydantic 官方文档"
  - url: "https://fastapi.tiangolo.com/"
    title: "FastAPI 官方文档"
generated_at: "2026-10-14T10:12:00Z"
generator:
  name: "generate-learning-material-advanced"
  version: "0.1.0"
  model: "gpt-4o"
  prompt_sha256: "<sha256 of prompt template>"
  prompt_path: "prompt-templates/pydantic_learning_prompt.md"
  generation_id: "gen-20261014-abcdef123456"
quality_checks:
  toc_present: true
  examples_count: 3
  exercises_count: 2
  issues: []
---
```

说明：
- `references` 是关键字段，必须至少有 1-3 个官方/权威链接；
- `generation_id` 用于定位对应日志；
- `quality_checks` 用于记录检查结果；
- 若有不确定结论，应写成：`需要验证` 或 `需人工确认`。

生成日志格式（JSON）
每次生成或更新时，必须写入日志，推荐结构如下：

```json
{
  "generation_id": "gen-20261014-abcdef123456",
  "document": "content/learning/pydantic/20261014-pydantic-quickstart.md",
  "generated_at": "2026-10-14T10:12:00Z",
  "generator": {
    "name": "generate-learning-material-advanced",
    "version": "0.1.0",
    "model": "gpt-4o",
    "prompt_path": "prompt-templates/pydantic_learning_prompt.md",
    "prompt_sha256": "<sha256>",
    "model_params": {
      "temperature": 0.2,
      "max_tokens": 4000
    }
  },
  "input": {
    "topic": "pydantic",
    "audience": "有 Python 基础的初学者",
    "goal": "1 小时速成，能做基本数据验证"
  },
  "references": [
    {
      "url": "https://docs.pydantic.dev/",
      "title": "Pydantic 官方文档",
      "fetched_at": "2026-10-14T09:50:00Z",
      "sha256": "<snapshot-sha>"
    }
  ],
  "quality_checks": {
    "toc_present": true,
    "examples_count": 3,
    "exercises_count": 2,
    "issues": []
  },
  "warnings": [
    "v1/v2 差异需人工确认"
  ],
  "commit_sha": "<latest commit or generated commit>"
}
```

说明：
- 日志便于审计、回溯、更新和复现；
- source snapshot 的 sha256 可用于判断文档是否已经过期；
- 任何可能的“未验证结论”都必须在 `warnings` 中记录。

来源（reference）管理
- 每个参考来源必须保留：URL、title、获取时间、可选的 snapshot sha256。
- 如果参考内容有更新，系统应该给出 `stale` 或 `update_required` 标记。
- 强烈建议保存源内容快照：`content/snapshots/{sha256}.txt`，方便后续追溯和比对。

更新与再生成策略
- 若参考来源发生变化，或用户要求重写，生成器必须重新编译文档；
- 生成新版本时需要更新：
  - `generated_at`
  - `generation_id`
  - `commit_sha`
  - `logs/generation-log.json`
- 生成新版本不能直接覆盖旧版本，建议：
  - 现有版本保留历史；
  - 新版本通过 PR 或新文件提交；
  - 旧内容在 git 历史中保留（审计）。

生成流程（推荐）
1. 解析主题与输入（topic/audience/goal/references）。
2. 从参考材料中提取保留规则：可验证事实、示例、版本差异。
3. 生成 TOC，并让人确认是否符合目标。 
4. 生成文档草稿；文档必须遵循：概览 → 概念 → 示例 → 练习 → 复习卡片 → ��考资源。
5. 生成 `frontmatter` 和对应 `generation-log.json`。
6. 运行基础质量校验：
   - 是否有 TOC
   - 是否有代码块
   - 是否 ≥ 3 个示例
   - 是否 ≥ 2 个练习
   - 是否有 references
7. 如果校验失败，改成 `quality_checks.issues` 列出问题并重新执行。
8. 创建 PR 或记录生成历史后再合并。

质量校验清单（必须通过）
- [ ] 文档有标题与一句话概览
- [ ] 有 2 个真实场景
- [ ] 有前置知识与版本说明
- [ ] 有 TOC
- [ ] 至少 3 个可运行例子
- [ ] 至少 2 个练习，且有答案/提示
- [ ] 至少 5 条复习卡片
- [ ] 有参考来源列表
- [ ] 有 generation-log 与 frontmatter 元数据
- [ ] 所有可能不确定的结论都已标记为 `需要验证`

自动化建议（CI / GitHub Actions）
- `.github/workflows/validate-generated-docs.yml`
- 检查项：
  - frontmatter 是否存在
  - `references` 是否非空
  - `quality_checks.examples_count` 是否 ≥ 3
  - `quality_checks.exercises_count` 是否 ≥ 2
  - 是否有 `generation_id` 和 `generated_at`
  - 代码块语法基础检查（可选）
- 失败时输出完整问题列表到 PR summary

示例 prompt（给 AI）

```text
请以面向【{target_audience}】的方式生成关于【{topic}】的学习资料，学习目标为【{goal}】。必须遵循以下要求：
1. 先给一句话概览 + 2 个真实场景；
2. 给出前置知识和版本说明；
3. 生成 TOC；
4. 解释核心概念（每个概念 1-3 段，含类比）；
5. 提供 3 个可运行示例，逐行或逐块解释；
6. 列出至少 6 个常见坑与排查建议；
7. 给 2 个练习，并附提示/参考答案；
8. 给 5 条复习卡片（Q/A）；
9. 给出速查表；
10. 按“入门 → 进阶”列出参考资源；
11. 在文档顶部附上 YAML frontmatter 和所有要求字段；
12. 不要只给代码，必须解释为什么这么写；
13. 若某个结论存在不确定性，请在该结论后写“需要验证”。
```

附带说明
- 以上 skill 解决的是：我现在需求的“学一个新知识时，AI 总是给不完整、不结构化、没有来源、不易维护、不能更新”的问题。
- 这不是单纯“prompt 提示词”，而是一整套对“学习资料生成器”的规范与约束。
- 后续可以扩展到更多 skill 类型（例如 design-skill、research-skill、course-structure-skill），但当前优先解决这一类核心需求。

这个 skill 的最重要价值：
- 让生成文档不再只是“文章”，而是“可以被审计、被复用、被持续更新的知识资产”。
