# 量化标准参考

本文档提供岗位JD各要素的量化标准参考，用于生成可量化的匹配条件。

---

## 一、学历量化标准

### 学历层级

| 层级 | 标准表述 | 适用场景 | AI匹配规则 |
|------|----------|----------|------------|
| 中专/高中 | 中专及以上 | 生产操作工 | 学历≥中专 |
| 大专 | 大专及以上 | 技工、基础职能 | 学历≥大专 |
| 本科 | 本科及以上 | 研发、管理、核心职能 | 学历≥本科 |
| 硕士 | 硕士优先 | 高级技术、专家岗 | 学历≥本科(硕士优先) |
| 博士 | 博士优先 | CTO、技术带头人 | 学历≥硕士(博士优先) |

### 学历匹配JSON格式

```json
{
  "education": {
    "required": "本科",
    "minimum": "大专",
    "strict": true,
    "note": "若候选人学历为大专，需有8年以上相关经验方可破格"
  }
}
```

### 制造业学历建议

| 岗位类别 | 建议学历 | 说明 |
|----------|----------|------|
| 生产操作 | 中专/大专 | 操作技能为主，学历门槛适当降低 |
| 生产技术 | 大专/本科 | 需要一定专业知识 |
| 研发工程 | 本科/硕士 | 专业深度要求高 |
| 质量管理 | 大专/本科 | 体系知识+实践经验 |
| 职能管理 | 本科 | 管理+专业双重能力 |

---

## 二、经验年限量化标准

### 年限层级

| 年限 | 标准表述 | 适用场景 | AI匹配规则 |
|------|----------|----------|------------|
| 应届/不限 | 不限 | 基层岗位、培训生 | 无年限要求 |
| 1-2年 | 1年以上 | 初级专员 | 经验≥1年 |
| 3年 | 3年及以上 | 中级专员 | 经验≥3年 |
| 5年 | 5年及以上 | 高级专员/主管 | 经验≥5年 |
| 8年 | 8年及以上 | 经理级 | 经验≥8年 |
| 10年+ | 10年及以上 | 高级经理/总监 | 经验≥10年 |

### 经验匹配JSON格式

```json
{
  "experience_years": {
    "required": 3,
    "unit": "年",
    "scope": "相关工作经验",
    "strict": true,
    "calculation": "累计同行业/同岗位经验"
  }
}
```

### 经验类型细分

| 经验类型 | 表述示例 | AI匹配关键词 |
|----------|----------|--------------|
| 行业经验 | 制造业经验 | 制造业、工厂、生产 |
| 岗位经验 | 同岗位经验 | 研发工程师、生产主管 |
| 项目经验 | 主导过XX项目 | 项目经理、组长 |
| 管理经验 | 带团队X人 | 管理X人、下属X人 |

---

## 三、技能/证书量化标准

### 技能层级

| 层级 | 表述示例 | 含义 | AI匹配 |
|------|----------|------|--------|
| 掌握 | 掌握XX | 了解基础概念 | 关键词匹配 |
| 熟悉 | 熟悉XX | 能实际应用 | 关键词+场景 |
| 熟练 | 熟练使用XX | 能独立操作 | 项目经验验证 |
| 精通 | 精通XX | 专家水平 | 能指导他人 |

### 技能分类量化

#### 工具软件类

```json
{
  "skills": {
    "design": ["SolidWorks", "AutoCAD", "Pro/E", "UG"],
    "analysis": ["MATLAB", "Python", "R"],
    "office": ["Excel", "PPT", "Word"],
    "erp": ["SAP", "用友", "金蝶"],
    "project": ["Project", "Visio"]
  }
}
```

#### 管理体系类

```json
{
  "certificates": {
    "quality": ["ISO9001", "IATF16949", "ISO14001"],
    "safety": ["ISO45001", "安全生产证"],
    "project": ["PMP", "PRINCE2"],
    "quality_tool": ["六西格玛绿带", "六西格玛黑带"]
  }
}
```

### 证书匹配JSON格式

```json
{
  "certificates": {
    "required": ["初级会计师"],
    "preferred": ["中级会计师", "CPA"],
    "verification": "证书名称或实际能力验证"
  }
}
```

---

## 四、制造业专项量化

### 研发类

```json
{
  "RD": {
    "must_match": {
      "education": "本科",
      "experience_years": 3,
      "skills": ["SolidWorks", "AutoCAD"],
      "knowledge": ["APQP", "PPAP", "FMEA"]
    },
    "bonus_points": {
      "skills": ["Pro/E", "ANSYS", "MATLAB"],
      "experience": ["制造业研发", "新产品导入"],
      "certificates": ["专利代理人"]
    }
  }
}
```

### 生产类

```json
{
  "production": {
    "must_match": {
      "education": "大专",
      "experience_years": 5,
      "skills": ["现场管理", "生产计划"],
      "knowledge": ["5S", "精益生产基础"]
    },
    "bonus_points": {
      "skills": ["JIT", "TPM"],
      "experience": ["精益改善项目", "产能提升"],
      "certificates": ["精益工程师认证"]
    }
  }
}
```

### 质量类

```json
{
  "quality": {
    "must_match": {
      "education": "本科",
      "experience_years": 3,
      "skills": ["SPC", "MSA", "FMEA"],
      "knowledge": ["ISO9001体系"]
    },
    "bonus_points": {
      "skills": ["六西格玛", "QFD"],
      "experience": ["供应商质量管理", "客诉处理"],
      "certificates": ["六西格玛绿带", "IATF16949内审员"]
    }
  }
}
```

### 供应链类

```json
{
  "supply_chain": {
    "must_match": {
      "education": "本科",
      "experience_years": 3,
      "skills": ["采购流程", "库存管理"],
      "tools": ["ERP系统"]
    },
    "bonus_points": {
      "skills": ["供应商开发", "成本分析"],
      "experience": ["战略采购", "供应链优化"],
      "certificates": ["CPSM"]
    }
  }
}
```

---

## 五、匹配度评估规则

### 硬性匹配（必须项）

```
if (candidate.education < required.education) → 硬性不匹配
if (candidate.experience < required.experience) → 硬性不匹配
if (candidate.missing_required_skill) → 硬性不匹配
```

### 加分项评估

```
base_score = 60  // 基础分
if (has_bonus_skill) → +10分
if (has_bonus_experience) → +15分
if (has_bonus_certificate) → +10分
if (exceed_education) → +5分
if (exceed_experience) → +5分
final_score = min(base_score + bonuses, 100)
```

### 匹配度等级

| 等级 | 分值 | 说明 | 建议 |
|------|------|------|------|
| A | 90-100 | 完全符合或超出 | 直接推荐 |
| B | 75-89 | 基本符合，有加分项 | 重点推荐 |
| C | 60-74 | 勉强符合 | 备选考虑 |
| D | <60 | 不符合 | 不推荐 |

---

## 六、JSON量化标准模板

```json
{
  "position": {
    "name": "岗位名称",
    "department": "部门"
  },
  "must_match": {
    "education": {
      "level": "本科",
      "minimum": "大专",
      "strict": true
    },
    "experience_years": {
      "required": 3,
      "scope": "相关工作经验",
      "strict": true
    },
    "skills": {
      "must_have": ["技能1", "技能2"],
      "verification": "面试考察"
    },
    "knowledge": {
      "must_have": ["知识1", "知识2"]
    },
    "certificates": {
      "required": [],
      "must_have_verifiable": false
    }
  },
  "bonus_points": {
    "skills": {
      "nice_to_have": ["加分技能列表"],
      "weight": 10
    },
    "experience": {
      "nice_to_have": ["加分经验列表"],
      "weight": 15
    },
    "certificates": {
      "nice_to_have": ["加分证书列表"],
      "weight": 10
    },
    "education": {
      "extra": "超出要求学历可加分",
      "weight": 5
    }
  },
  "matching_rules": {
    "strict_threshold": "必须项全部满足",
    "score_formula": "60 + sum(bonus_points)",
    "recommendation": {
      "A": {"score": "90-100", "action": "直接推荐"},
      "B": {"score": "75-89", "action": "重点推荐"},
      "C": {"score": "60-74", "action": "备选考虑"},
      "D": {"score": "<60", "action": "不推荐"}
    }
  }
}
```

---

## 七、快速提取清单

生成JD时，请确保以下要素都已量化：

### 基础信息
- [ ] 学历要求：具体到层级（大专/本科/硕士）
- [ ] 经验要求：具体到年限（X年）
- [ ] 专业要求：具体到专业大类

### 技能要求
- [ ] 工具软件：列出具体软件名称
- [ ] 管理体系：列出具体体系名称
- [ ] 认证证书：列出具体证书名称

### 加分项
- [ ] 稀缺经验：明确加分条件
- [ ] 额外技能：列出加分技能
- [ ] 认证加分：列出加分证书

---

*本文档为jd-writer-skill的量化标准参考，用于生成可供AI评估简历的标准化匹配条件。*
