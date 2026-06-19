# langppt-process-engineer - Work Plan

## TL;DR (For humans)
**What you'll get:** 一份完整的 LangGPT System Prompt（系统提示词），让 AI 扮演"高级制造工艺专家"，能根据用户输入的工艺类型自动生成 URS/SOP/PFMEA 文档。模板包含 7 大模块，内嵌压装/拧紧/激光焊三种工艺的专业知识字典。

**Why this approach:** LangGPT 结构是目前工业级提示词工程的最佳实践——模块化设计让角色设定、知识库、工作流和约束条件各归其位，确保 LLM 输出专业、一致且可控。

**What it will NOT do:** 不会包含实际的 URS/SOP/PFMEA 文件生成（那是模板运行后的结果）；不会包含 3 种工艺之外的工艺知识；不会包含自动化工装或 API 代码。

**Effort:** Short（一个文本交付物，4 个构建步骤）
**Risk:** Low - 需求清晰，结构明确，已在草案 + Metis 审查中处理了所有 gap

**Decisions to sanity-check:**
- 模块标题用英文（Role, Profile 等），内容用中文
- "Constrains" 纠正为 LangGPT 标准拼写 "Constraints"
- Constrains 中包含输出语言约束和反幻觉保护

Your next move: approve this plan, and I'll start writing the template.

---

> TL;DR (machine): short; low-risk; one deliverable (LangGPT System Prompt); 5 sequential todos; no code changes.

## Scope
### Must have
- [MH1] LangGPT 标准 7 模块结构 (Role, Profile, Goals, Constraints, Skills, Workflow, Initialization)
- [MH2] Skills 模块嵌入 3 种工艺 YAML 知识字典（压装/拧紧/激光焊）
- [MH3] Workflow 实现 3 步交互 + 未知工艺回退 + 输入不完整处理
- [MH4] Constraints 包含输出语言约束（简体中文）和反幻觉保护
- [MH5] Initialization 包含专业问候语及功能说明
- [MH6] 输出为可读 Markdown 格式

### Must NOT have (guardrails, anti-slop, scope boundaries)
- [MN1] 不包含独立于 System Prompt 的模板文件或代码脚本
- [MN2] 不包含除 3 种工艺外的其他工艺知识（防 LLM 编造）
- [MN3] 不包含实际运行 LLM 生成文档（那是模板的使用阶段）
- [MN4] 不使用除 Markdown 外的输出格式

## Verification strategy
> 提示词模板的验证不同于代码——需通过结构化审查确认各模块完整性和准确性。
- **Test decision:** 结构化审查 (manual review with checklist) + 可选 LLM 试运行
- **Evidence:** `.omo/evidence/task-langppt-process-engineer.md`

验证方法：
1. **结构审查**: 逐项对照 LangGPT 7 模块清单，确认全部存在且结构正确
2. **知识完整性审查**: 核对 Skills 中 3 个 YAML 块是否完整无遗漏
3. **约束一致性审查**: 确认 Constraints 包含语言约束和反幻觉保护
4. **Workflow 逻辑审查**: 模拟用户对话（正常 + 异常路径）验证工作流逻辑

## Execution strategy
### Parallel execution waves
> 由于是单一文本交付物，所有 todo 串行执行。

### Dependency matrix
| Todo | Depends on | Blocks | Can parallelize with |
| --- | --- | --- | --- |
| 1. 基础模块 | — | 2 | — |
| 2. Skills 模块 | 1 | 3 | — |
| 3. Workflow 模块 | 1 | 4 | — |
| 4. 完整组装+验证 | 2, 3 | — | — |

## Todos
> 每个 todo 构建一个模块，串行执行。最终 todo 做完整组装和验证。
<!-- APPEND TASK BATCHES BELOW THIS LINE WITH edit/apply_patch - never rewrite the headers above. -->
- [ ] 1. 编写 LangGPT 基础结构模块（Role, Profile, Goals, Constraints, Initialization）
  What to do / Must NOT do:
  - 编写 `# Role`: 高级制造工艺专家 (Senior Process Engineer)
  - 编写 `# Profile`: 包含作者、版本、语言、描述等元信息
  - 编写 `# Goals`: 核心目标——根据输入自动生成 URS/SOP/PFMEA
  - 编写 `# Constraints`: 包含输出语言（简体中文）、反幻觉保护（未知工艺回退引导）、知识范围限制、输出格式要求
  - 编写 `# Initialization`: 专业中文问候语 + 功能说明 + 引导用户输入
  - 不得在此 to-do 中编写 Skills 或 Workflow 模块内容
  - 模块标题使用英文（LangGPT 标准），但 Constraints 中的 Language 字段值可注明"Chinese/中文"
  
  Parallelization: Wave 1 | Blocked by: — | Blocks: 2, 3
  References (executor has NO interview context - be exhaustive):
  - `.omo/drafts/langppt-process-engineer.md` — 草案中的 Decisions、Scope IN/OUT、Metis 处理记录
  - LangGPT 标准结构: Role / Profile / Goals / Constraints / Skills / Workflow / Initialization
  - 用户需求: 角色 = 高级制造工艺专家，核心任务 = 生成 URS/SOP/PFMEA
  - Metis 决定: 使用 "Constraints"（纠正用户拼写 "Constrains"）
  - Metis 决定: Constraints 中必须包含简体中文输出语言约束
  - Metis 决定: Constraints 中必须包含反幻觉保护——未知工艺不得编造参数，需引导用户选择支持的工艺
  - Metis 决定: Initialization 包含「您好！我是高级制造工艺专家。我可以帮助您生成 URS、SOP 或 PFMEA 文档。请告诉我您需要哪种文档类型？」

  Acceptance criteria (agent-executable):
  - 文本中包含 `# Role` `# Profile` `# Goals` `# Constraints` `# Initialization` 5 个模块标题
  - Constraints 中包含语言约束、反幻觉保护、知识范围限制三项内容
  - Initialization 包含问候语+功能引导

  QA scenarios (name the exact tool + invocation): happy + failure, Evidence `.omo/evidence/task-1-langppt-process-engineer.md`
  - Happy: 逐项确认 5 个模块存在且内容完整 (使用 Read 工具读取输出文件)
  - Failure: 确认不存在 Skills 和 Workflow 模块（应在此 todo 中不出现）
  
  Commit: Y | feat(langppt): add base LangGPT modules (Role, Profile, Goals, Constraints, Initialization)

- [ ] 2. 编写 Skills 模块 - 嵌入工艺知识字典
  What to do / Must NOT do:
  - 编写 `# Skills` 模块，嵌入 3 种工艺的 YAML 格式知识字典
  - 每种工艺包含：关键参数 / 控制策略 / 质量评价 / 常见失效(PFMEA素材)
  - 工艺 1: 压装工艺 (Press-fitting) — 压装速度、目标压力、目标位移、保压时间、恒力/恒位移控制、力-位移曲线包络线监控、最终停止力、推出力测试、卡涩/划伤/压装不到位/过压变形
  - 工艺 2: 拧紧工艺 (Tightening) — 贴合扭矩、目标扭矩、目标转角、扭矩控制-转角监控、屈服点控制、静态扭矩复检、扭矩衰减率、浮高/未贴合/滑牙/错牙/漏装
  - 工艺 3: 激光焊接 (Laser Welding) — 激光功率、焊接速度、离焦量、保护气流量、焦点位置实时追踪、熔池形貌监控、金相切片分析、拉拔力测试、气孔/裂纹/虚焊/咬边
  - YAML 格式使用代码块 ```yaml ... ``` 包裹
  - 不得在此 todo 中修改基础模块内容
  - 不得自行添加 3 种工艺之外的其他工艺知识
  
  Parallelization: Wave 2 | Blocked by: Todo 1 | Blocks: 4
  References (executor has NO interview context - be exhaustive):
  - 用户需求中的 3 个工艺字典（全部内容，参数/控制/评价/失效要完整无遗漏）
  - `.omo/drafts/langppt-process-engineer.md` — Scope IN 明确 Skills 包含 3 种工艺 YAML
  - 格式要求: ```yaml ... ``` 代码块 + 中文说明

  Acceptance criteria (agent-executable):
  - Skills 模块包含 3 个 YAML 代码块，分别对应压装/拧紧/激光焊
  - 每个工艺 YAML 包含 4 个字段: key_parameters / control_strategy / quality_evaluation / pfmea_failure_modes
  - 参数值与用户提供的完全一致，无遗漏无多余

  QA scenarios (name the exact tool + invocation): happy + failure, Evidence `.omo/evidence/task-2-langppt-process-engineer.md`
  - Happy: 逐项核对 3 个 YAML 块的字段和参数值与用户需求一致 (使用 grep 搜索关键参数名)
  - Failure: 确认不存在第 4 种工艺的 YAML 块（如焊接变体、胶接等）
  
  Commit: Y | feat(langppt): embed 3 process knowledge dictionaries in Skills

- [ ] 3. 编写 Workflow 模块 - 设计交互流程
  What to do / Must NOT do:
  - 编写 `# Workflow` 模块，定义 3 步交互逻辑
  - 步骤 1: 询问用户需要编写哪种工艺文档（URS / SOP / PFMEA）
  - 步骤 2: 询问用户针对哪一种具体工艺（压装 / 拧紧 / 激光焊）
  - 步骤 3: 根据用户选择的文档类型+工艺类型，调用 Skills 中对应的工艺知识，生成 Markdown 文档
  - 增加异常处理分支：
    - 如果用户选择的文档类型不在 [URS, SOP, PFMEA] 中 → 提示用户从列表中选择
    - 如果用户选择的工艺不在 [压装, 拧紧, 激光焊] 中 → 说明知识库限制，建议从支持的工艺中选择
    - 如果用户输入信息不完整 → 引导用户补充必要信息
  - 不得在此 todo 中修改 Skills 模块内容
  - 不得增加第 4 步或改变交互顺序
  
  Parallelization: Wave 2 | Blocked by: Todo 1 | Blocks: 4
  References (executor has NO interview context - be exhaustive):
  - 用户需求中的 Workflow 设计: 3 步交互（文档类型 → 工艺类型 → 生成输出）
  - `.omo/drafts/langppt-process-engineer.md` — 决定 8（错误处理回退逻辑）
  - Metis 建议: 需要处理未知工艺、输入不完整等异常情况

  Acceptance criteria (agent-executable):
  - Workflow 包含明确的 3 步编号流程
  - 包含至少 2 个异常处理分支（未知文档类型、未知工艺）
  - 每一步的描述包含具体交互说明（问什么、怎么问）

  QA scenarios (name the exact tool + invocation): happy + failure, Evidence `.omo/evidence/task-3-langppt-process-engineer.md`
  - Happy: 确认 3 步逻辑完整清晰（人工阅读 Workflow 模块）
  - Failure: 用 "非法输入" 测试——确认 Workflow 包含对未知工艺和未知文档类型的处理
  
  Commit: Y | feat(langppt): add Workflow with 3-step interaction and error handling

- [ ] 4. 完整组装 + 输出文档指南 + 最终验证
  What to do / Must NOT do:
  - 将所有模块按标准 LangGPT 顺序组装为一份完整的 System Prompt
  - 补充 C4: 在 Skills 或独立区域中，为 URS/SOP/PFMEA 三种文档各提供一份简要的结构指南（描述文档应包含的章节，而非完整的文档模板）
    - URS 结构示例：1. 设备概述 2. 技术参数 3. 功能要求 4. 安全和环境要求 5. 验收标准
    - SOP 结构示例：1. 适用范围 2. 参考文件 3. 操作步骤 4. 关键控制点 5. 异常处理
    - PFMEA 结构示例：1. 过程功能 2. 失效模式 3. 失效影响 4. 严重度 5. 频度 6. 探测度 7. 建议措施
  - 最终输出必须全部为简体中文（模块标题除外）
  - 执行最终验证：结构审查 + 知识完整性审查 + 约束一致性审查 + 工作流逻辑审查
  - 不得增加超出 Scope 的内容
  - 不得改写用户提供的 YAML 参数内容
  
  Parallelization: Wave 3 | Blocked by: 2, 3 | Blocks: —
  References (executor has NO interview context - be exhaustive):
  - LangGPT 模块标准顺序: Role → Profile → Goals → Constraints → Skills → Workflow → Initialization
  - `.omo/drafts/langppt-process-engineer.md` — 全部决定和范围定义
  - Todos 1-3 的输出（需合并这三个模块的输出）
  - 用户需求中的 URS/SOP/PFMEA 概念

  Acceptance criteria (agent-executable):
  - 最终文件包含全部 7 个 LangGPT 模块，顺序正确
  - Skills 中包含 3 个完整 YAML 知识块
  - Constraints 中包含语言约束和反幻觉保护
  - Workflow 包含 3 步交互 + 异常处理
  - 整个文件为 Markdown 格式
  - 全部内容为简体中文（模块标题除外）

  QA scenarios (name the exact tool + invocation): happy + failure, Evidence `.omo/evidence/task-4-langppt-process-engineer.md`
  - Happy: 
    1. 结构审查: Read 工具逐模块检查 7 个模块是否存在 (Read 读取最终文件)
    2. 知识审查: grep 检查 3 个工艺的关键参数名是否完整
    3. 约束审查: grep 检查 "未知工艺"、"简体中文" 等约束关键字是否存在
    4. Workflow 审查: grep 检查 "步骤 1"、"步骤 2"、"步骤 3" 是否存在
  - Failure: 
    1. 确认没有多余工艺知识（grep 排除 "超声波"、"胶接" 等外来工艺名）
    2. 确认输出中没有英文文档内容（read 检查文档部分）

  Commit: Y | feat(langppt): complete LangGPT template with assembly and validation

## Final verification wave
> Runs in parallel after ALL todos. ALL must APPROVE. Surface results and wait for the user's explicit okay before declaring complete.
- [ ] F1. 结构合规性: 验证全部 7 个 LangGPT 模块存在且顺序正确 (Read 读取最终文件)
- [ ] F2. 知识完整性: 验证 3 个 YAML 工艺字典完整无遗漏 (grep 所有关键参数名)
- [ ] F3. 约束一致性: 验证 Constraints 包含语言约束 + 反幻觉保护 + 知识范围限制 (grep 关键字)
- [ ] F4. 试运行逻辑审查: 手动模拟用户对话路径，确认 Workflow 逻辑自洽

## Commit strategy
- 本交付物为单个文本文件，在一次提交中完成所有模块的写入
- 由于内容相关性强，Merge 策略为 squash merge
- 提交信息使用 Conventional Commits 格式

## Success criteria
1. System Prompt 包含全部 7 个 LangGPT 模块，无遗漏
2. Skills 模块包含 3 个工艺 YAML 知识块，参数与用户提供完全一致
3. Constraints 包含输出语言约束 + 反幻觉保护 + 知识范围限制
4. Workflow 定义了明确的 3 步交互 + 异常处理分支
5. Initialization 包含问候语和功能引导
6. 最终输出格式为 Markdown，内容主要为简体中文
7. 最终验证 F1-F4 全部通过
