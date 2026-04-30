# JD Writer Skill - 岗位JD撰写助手

一款专为制造业HR设计的岗位JD撰写Agent Skill，帮助快速生成专业、结构化的职位描述。

## 功能特点

- **引导式交互**：通过提问引导，快速获取岗位关键信息
- **标准结构输出**：生成统一格式的Markdown JD文档
- **量化标签**：附带[必须]/[加分]标签，便于AI评估简历匹配度
- **全岗位覆盖**：支持研发、生产、运营、职能、销售等各类岗位
- **JSON量化标准**：自动生成匹配度评估的JSON结构

## 安装方法

### 通用安装（推荐）

复制技能文件夹到通用技能目录：

```bash
mkdir -p ~/.agents/skills/jd-writer-skill
cp -r jd-writer-skill/* ~/.agents/skills/jd-writer-skill/
```

### Claude Code / VS Code Copilot

```bash
mkdir -p ~/.claude/skills/jd-writer-skill
cp -r jd-writer-skill/* ~/.claude/skills/jd-writer-skill/
```

### Cursor

```bash
mkdir -p .cursor/rules/jd-writer-skill
cp -r jd-writer-skill/* .cursor/rules/jd-writer-skill/
```

### Windsurf

```bash
mkdir -p .windsurf/rules/jd-writer-skill
cp -r jd-writer-skill/* .windsurf/rules/jd-writer-skill/
```

## 快速开始

### 方式一：直接命令

```
/jd-writer-skill 帮我写一个产品研发工程师的JD
```

### 方式二：详细描述

```
/jd-writer-skill
我需要招聘一位生产主管，要求：
- 部门：生产部
- 地点：东莞
- 学历：大专及以上
- 经验：5年以上
```

### 方式三：引导式

输入 `/jd-writer-skill` 后，Skill会通过提问引导你补充岗位信息。

## 输出示例

```markdown
# 产品研发工程师

## 基础信息
- **部门**：研发中心
- **岗位类别**：研发
- **工作地点**：深圳
- **薪资范围**：15-25K

## 岗位职责
1. 负责新产品设计开发
2. 主导技术方案制定
3. 跟进试产导入

## 任职要求

### 必须项 [必须]
- **学历**：本科及以上 [必须]
- **经验**：3年以上 [必须]
- **技能**：SolidWorks [必须]

### 加分项 [加分]
- APQP流程经验 [加分]
- 专利撰写能力 [加分]

## 量化匹配标准（供AI评估用）
```json
{
  "must_match": {
    "education": "本科",
    "experience_years": 3,
    "skills": ["SolidWorks"]
  },
  "bonus_points": {
    "skills": ["APQP", "专利撰写"]
  }
}
```
```

## JD结构说明

| 模块 | 说明 |
|------|------|
| 基础信息 | 部门、地点、薪资等基本信息 |
| 岗位职责 | 3-5条核心工作职责 |
| 任职要求 | 分为必须项和加分项 |
| 岗位亮点 | 薪酬福利、发展空间等吸引力 |
| 量化标准 | JSON格式的匹配条件 |

## 标签含义

| 标签 | 含义 | 简历筛选规则 |
|------|------|--------------|
| `[必须]` | 硬性要求 | 不满足直接淘汰 |
| `[加分]` | 软性优势 | 满足则加分 |

## 适用岗位类型

- **研发类**：产品工程师、工艺工程师、电气工程师
- **生产类**：生产主管、班组长、设备工程师
- **质量类**：质量工程师、SQE、质量主管
- **运营类**：采购工程师、仓库主管、物流专员
- **职能类**：人事专员、财务会计、行政专员
- **销售类**：销售工程师、销售主管、市场专员

## 常见问题

### Q: 信息不全怎么办？

A: 提供你知道的信息即可，Skill会引导补充缺失的关键要素。

### Q: 如何调整学历/经验要求？

A: 直接告诉Skill你的要求，如"学历放宽到大专"、"经验要求5年以上"。

### Q: 加分项写多少合适？

A: 建议3-5条，与必须项形成差异化。

### Q: 量化标准有什么用？

A: JSON格式的量化标准可直接用于AI简历解析系统的匹配度评估。

## 文件结构

```
jd-writer-skill/
├── SKILL.md                    # 主文件（技能定义）
├── references/
│   ├── jd-modules.md          # JD模块详细说明
│   ├── quant-standards.md     # 量化标准参考
│   └── examples.md            # 完整示例
└── README.md                  # 本文档
```

## 参考文档

- [JD模块说明](references/jd-modules.md) - 各模块撰写规范
- [量化标准参考](references/quant-standards.md) - 量化条件模板
- [完整示例](references/examples.md) - 各类岗位JD示例

## 版本信息

- **版本**：1.0.0
- **更新日期**：2026-04-30
- **适用场景**：制造业工贸一体公司

---

*本Skill专注于岗位JD撰写，为简历解析和匹配度评估提供结构化信息输入。*
