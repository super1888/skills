# Skills

本项目用于把指定内容沉淀成可复用的 Codex Skills。核心能力是通过 `content-to-skill/` 对用户提供的技术博客、文章、文档链接、长文本或本地资料进行拆解、萃取和重组，生成一个结构完整、触发精准、可直接集成到本项目的好用 skill。

## 项目核心

`content-to-skill/` 是本项目的核心 skill。它负责把原始内容转换成成熟技能，而不是简单摘要文章。

它会重点处理：

- 识别内容适配的任务场景和触发条件。
- 提炼原文里的设计思路、架构逻辑、解题方法和实操步骤。
- 生成规范的 `SKILL.md`、`agents/openai.yaml` 和 `references/` 溯源资料。
- 保持主技能正文精简，把原文知识点、案例、清单和深度拆解放到 `references/`。
- 校验生成结果是否满足触发精准、输出稳定、溯源可查、上下文精简和易维护。

## 生成 Skill 的基本流程

1. 提供目标内容：文章链接、技术博客、产品文档、设计文档、本地文件或粘贴文本。
2. 使用 `content-to-skill/` 拆解内容：识别主题、边界、核心方法、风险点和可复用规则。
3. 生成新 skill 目录：包含 `SKILL.md`、可选 `agents/openai.yaml` 和必要的 `references/*.md`。
4. 将新 skill 集成到本项目：放在根目录下，并在 README 的技能列表中简单登记。
5. 后续维护时优先更新对应 skill 的 `references/`，只有核心流程变化时才修改 `SKILL.md`。

## 好 Skill 的判断标准

- 触发精准：用户不需要手动指定 skill，也能在相关任务中自动命中。
- 输出稳定：不同任务能产出结构一致、可落地的结果。
- 溯源可查：原始知识点、设计思路和实操方法能在 `references/` 中找到。
- 上下文精简：`SKILL.md` 只保留核心逻辑、执行步骤和输出格式。
- 易于维护：新增案例、补充规则或优化知识点时，可单独归入参考文件。

## 推荐 Skill 结构

```text
skill-name/
├── SKILL.md
├── agents/
│   └── openai.yaml
└── references/
    ├── source-map.md
    ├── extraction-notes.md
    ├── workflow-checklist.md
    └── examples.md
```

## 当前 Skills

- `content-to-skill/`：核心生成技能，根据指定内容生成完整可用的 Codex Skill，并负责溯源、质检、触发验证与维护规则。
- `ecommerce-design/`：电商系统设计技能，覆盖商品、交易、订单、支付、库存、营销、售后等领域设计。
- `insurance-system-design/`：保险系统设计技能，覆盖保险产品、保单、理赔、渠道、计费对账与风控。

## 维护约定

- 新增内容型 skill 时，优先用 `content-to-skill/` 生成，再按项目结构集成。
- 除 `content-to-skill/` 外，其他 skill 都是对不同内容或领域知识的总结沉淀，README 只需简单说明功能。
- 大段来源资料、案例、表格和扩展清单默认放入 `references/`。
- 不把原文长篇内容直接堆进 `SKILL.md`，避免增加上下文成本。
- 更新 skill 时保持主流程稳定，优先通过新增或修改参考文件完成迭代。
