---
slug: langppt-process-engineer
status: drafting
intent: clear
pending-action: write .omo/plans/langppt-process-engineer.md
approach: 生成一份完整的 LangGPT 结构 System Prompt，包含 Role / Profile / Goals / Constrains / Skills / Workflow / Initialization 七大模块，其中 Skills 模块嵌入压装/拧紧/激光焊三种工艺的结构化知识字典，Workflow 模块实现 3 步交互逻辑（问文档类型 → 问工艺类型 → 调用知识生成输出）。
---

# Draft: langppt-process-engineer

## Components (topology ledger)
| id | outcome (one line) | status |
|----|-------------------|--------|
| C1 | LangGPT 标准结构骨架 (Role, Profile, Goals, Constrains, Skills, Workflow, Initialization) | active |
| C2 | 工艺知识字典集成 — 将压装/拧紧/激光焊 3 个 YAML 知识块融入 Skills 模块 | active |
| C3 | 交互工作流设计 — 3 步询问（文档类型 → 工艺类型 → 生成输出） | active |
| C4 | 输出文档模板骨架 — URS / SOP / PFMEA 三种文档的 Markdown 结构 | active |

## Open assumptions (announced defaults)
| assumption | adopted default | rationale | reversible? |
|-----------|----------------|-----------|-------------|
| 模板语言 | 模块标题用英文（Role, Profile 等），说明和内容用中文 | 用户素材中术语中英混杂；保留 LangGPT 标准模块名 + 中文内容符合工业文档习惯 | 是，可改为全中文 |
| 输出格式 | Markdown | 用户明确要求 | 否 |
| Skills 模块内知识格式 | 以 YAML 代码块形式嵌入，附中文说明 | 用户提供的本就是 YAML 格式，保持原样可读性最好 | 是 |

## Findings (cited - path:lines)
- 用户需求完整明确，所有工艺参数（压装/拧紧/激光焊）已提供
- LangGPT 标准结构包含 Role, Profile, Goals, Constrains, Skills, Workflow, Initialization
- Workflow 3 步交互逻辑已明确定义

## Decisions (with rationale)
1. **模块标题保留英文** — LangGPT 社区标准做法，模块标题英文便于跨语言识别
2. **工艺知识以 YAML 代码块嵌入 Skills** — 保持用户提供的原始结构，不重写为自然语言
3. **输出文档模板仅定义结构描述** — C4 指嵌入在 System Prompt 中的文档结构指南（如"URS 包含：1. 设备概述 2. 技术参数 3. ..."），而非独立模板文件
4. **拼写纠正：使用 Constraints** — 用户写的是 "Constrains"（拼写错误），LangGPT 社区标准为 "Constraints"，纠正之
5. **System Prompt 中增加输出语言约束** — 在 Constrains 中明确：输出文档全部使用简体中文，仅保留英文技术术语
6. **增加反幻觉保护** — 在 Constrains 中明确：若用户选择的工艺不在已知 3 种之列，不得编造参数，必须引导用户选择支持的工艺
7. **Initialization 内容** — 提供专业中文问候语 + 功能说明
8. **错误处理** — 在 Workflow 中增加输入不完整/未知工艺时的回退逻辑

## Scope IN
- 一份完整的 LangGPT System Prompt，覆盖 7 个模块
- Skills 模块包含 3 种工艺的结构化知识（YAML 代码块）
- Workflow 实现 3 步交互逻辑 + 错误处理分支
- Constrains 包含：输出语言约束、反幻觉保护、知识范围限制
- Initialization 包含问候语和功能说明
- 最终输出为 Markdown 格式

## Scope OUT (Must NOT have)
- 不包含实际 URS/SOP/PFMEA 文件内容生成（这是模板运行后的结果）
- 不包含代码实现（如自动化脚本、API 调用等）
- 不包含除 3 种工艺外的其他工艺知识
- 不包含独立于 System Prompt 的模板文件

## Open questions
- 无 — 所有信息已由用户完整提供，Metis 发现的 gap 已通过决定 4-8 解决

## Metis 反馈处理记录
| # | 反馈 | 处理 |
|---|------|------|
| 1 | 计划文件为空 | 待填充（下方进行） |
| 2 | 无验证策略 | 在 Verification strategy 中定义 |
| 3 | 无错误处理/反幻觉 | 决定 8 + 决定 6 已处理 |
| 4 | C4 范围模糊 | 决定 3 已处理 |
| 5 | 输出语言未约束 | 决定 5 已处理 |
| 6 | Constrains 拼写 | 决定 4 已处理 |
| 7 | 反幻觉保护 | 决定 6 已处理 |
| 8 | Initialization 未定义 | 决定 7 已处理 |
| 9 | 工艺数据充分性 | 保留：标注为 "SOP 质量取决于用户提供的信息量" |
| 10 | 草案声称无未决问题 | 已更新，增加 Metis 处理记录 |
| 11 | 无验收标准 | 在计划 Success criteria 中定义 |
| 12 | 模板残留 | 清理计划文件模板

## Approval gate
status: approved
user-reply: "继续" (2026-06-19)
pending-action: write .omo/plans/langppt-process-engineer.md
