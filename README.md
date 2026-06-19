# Process-AI-Skills-Repo

> 制造工艺 AI 提示词/技能库 — 基于 LangGPT 结构化模板的高级工艺工程师 AI 助手

## 📋 项目简介

本仓库提供一套 **LangGPT 结构化 System Prompt 模板**，用于训练 AI 成为一名资深制造工艺工程师，能够根据用户输入的工艺信息，自动生成符合工业标准的 **URS（用户需求规格书）**、**SOP（标准作业指导书）** 和 **PFMEA（过程失效模式与影响分析）** 文档。

## 🏭 支持的工艺类型

| 序号 | 工艺名称 | 英文名称 | 文档 |
|------|----------|----------|------|
| 01 | 压装工艺 | Servo Press-fit | [工艺文档](工艺文档-01-压装工艺.md) |
| 02 | 拧紧工艺 | Servo Tightening | [工艺文档](工艺文档-02-拧紧工艺.md) |
| 03 | 激光焊接 | Laser Welding | [工艺文档](工艺文档-03-激光焊接.md) |
| 04 | 动平衡测试 | Dynamic Balancing Test | [工艺文档](工艺文档-04-动平衡测试.md) |
| 05 | 气密测试 | Air Tightness Test | [工艺文档](工艺文档-05-气密测试.md) |
| 06 | 点胶工艺 | Dispensing | [工艺文档](工艺文档-06-点胶工艺.md) |
| 07 | 锡线焊接工艺 | Tin Wire Soldering | [工艺文档](工艺文档-07-锡线焊接工艺.md) |
| 08 | 旋转关节模组性能测试 | Rotary Joint Module Performance Test | [工艺文档](工艺文档-08-旋转关节模组性能测试.md) |
| 09 | 电机定子性能测试 | Motor Stator Performance Test | [工艺文档](工艺文档-09-电机定子性能测试.md) |

## 📂 文件结构

```
Process-AI-Skills-Repo/
├── langppt-process-engineer.md          # V2.0 LangGPT System Prompt 模板（核心）
├── 工艺文档-01-压装工艺.md               # URS / SOP / PFMEA
├── 工艺文档-02-拧紧工艺.md
├── 工艺文档-03-激光焊接.md
├── 工艺文档-04-动平衡测试.md
├── 工艺文档-05-气密测试.md
├── 工艺文档-06-点胶工艺.md
├── 工艺文档-07-锡线焊接工艺.md
├── 工艺文档-08-旋转关节模组性能测试.md
├── 工艺文档-09-电机定子性能测试.md
└── README.md
```

## 🚀 快速开始

### 1. 使用 LangGPT 模板

复制 `langppt-process-engineer.md` 中的 System Prompt 到你的 AI 助手（如 ChatGPT、Claude 等）中，即可开始生成工艺文档。

### 2. 交互流程

```
用户 → "请帮我生成一份拧紧工艺的 URS"
  ↓
AI → 确认文档类型：URS ✅
  ↓
AI → 确认工艺类型：拧紧工艺 ✅
  ↓
AI → 根据知识库生成完整 URS 文档
```

## 📊 文档标准

每份 V2.0 文档包含：

### URS（用户需求规格书）
- 项目概况与总体要求
- 核心工艺技术参数（硬件要求）
- 控制策略与防错逻辑（软件要求）
- 工业控制、MES 与数据追溯
- EHS（环境、健康与安全）
- 设备验收标准（FAT / SAT）

### SOP（标准作业指导书）
- 准备工作与 5S 要求
- PPE 个人防护装备
- 首件检验规范
- 标准操作步骤（Step-by-Step）
- 异常处理与升级流程（Escalation）
- 条码追溯操作

### PFMEA（过程失效模式与影响分析）
- 基于 AIAG-VDA 统一标准格式
- 失效模式 / 影响 / 原因分析
- 预防控制 / 探测控制
- RPN 风险优先级评估
- 建议优化措施

## 🔧 工业标准

- **制程能力**: Cpk ≥ 1.67
- **测量系统**: GR&R ≤ 10%
- **PFMEA 格式**: AIAG-VDA 统一标准
- **数据追溯**: OPC UA / MES 集成
- **安全标准**: EHS 合规

## 📝 许可证

MIT License

## 🤝 贡献

欢迎提交 Issue 和 Pull Request 来改进本项目。

---

**维护者**: [OpenAiShcool](https://github.com/y2y94578kv-create)
