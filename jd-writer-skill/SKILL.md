---
name: jd-writer-skill
description: Generate structured job descriptions for AI resume matching. Input: natural language job requirements. Output: structured JD with keywords for resume evaluation.
version: 5.0.0
---

# JD Writer Skill (AI-only)

## Input Types
- A: Natural language with partial requirements
- B: Only responsibilities, no requirements
- C: Minimal (just job title/abbreviation)
- D: Copy-pasted from job sites

## Processing Rules

### Rule 1: Extract Keywords
Extract: job title, education, experience_years, major, skills, certificates, industry, location, salary

### Rule 2: Remove Soft Skills
Remove any soft skill descriptions (communication, teamwork, learning ability, responsibility). Do NOT output them.

### Rule 3: Standardize Terms
- "大专" = "专科", "高职"
- "本科" = "学士", "大学本科"
- "硕士" = "研究生"
- "SolidWorks" = "SW", "三维建模"
- "Pro/E" = "ProE", "Creo"

### Rule 4: Deduplicate
Remove duplicate requirements.

## Output Format

```markdown
# {JOB_TITLE}

## Basic Info
- Category: {R&D/Production/Quality/SupplyChain/Admin/Sales}
- Location: {CITY}
- Salary: {RANGE}

## Requirements

### Must-Have [must]
| Dimension | Requirement | Resume Keywords |
|-----------|-------------|----------------|
| Education | {TEXT} | {KEYWORDS} |
| Experience | {TEXT} | {KEYWORDS} |
| Major | {TEXT} | {KEYWORDS} |
| Skills | {TEXT} | {KEYWORDS} |
| Certificates | {TEXT} | {KEYWORDS} |

### Preferred [preferred]
| Dimension | Requirement | Resume Keywords |
|-----------|-------------|----------------|
| Industry | {TEXT} | {KEYWORDS} |
| Project | {TEXT} | {KEYWORDS} |
| Skills | {TEXT} | {KEYWORDS} |
| Certificates | {TEXT} | {KEYWORDS} |

## Matching Criteria
```json
{
  "position": "{JOB_TITLE}",
  "must_match": {
    "education": {"min_level": "{LEVEL}", "keywords": ["{KW}"]},
    "experience": {"min_years": {NUM}, "keywords": ["{KW}"]},
    "major": {"keywords": ["{KW}"]},
    "skills": {"required": ["{KW}"]},
    "certificates": {"required": ["{KW}"]}
  },
  "preferred": {
    "industry": ["{KW}"],
    "project": ["{KW}"],
    "skills": ["{KW}"],
    "certificates": ["{KW}"]
  }
}
```
```

## Mapping Rules (Responsibility → Skill)

### R&D
- 设计 → SolidWorks, Pro/E, Creo
- 量产导入 → APQP, PPAP, NPI
- 模具 → 模具设计, 注塑
- 专利 → 专利撰写

### Production
- 现场管理 → 5S, Lean, TPM
- 体系 → ISO9001, IATF16949

### Quality
- SPC → SPC, Minitab
- FMEA → FMEA, DFMEA
- 体系 → ISO9001, IATF16949, 内审员

### SupplyChain
- 采购 → 供应商管理, ERP
- 计划 → PMC, ERP, Excel

## Preset Options

### Education
- 大专及以上
- 本科及以上
- 硕士及以上

### Experience
- 1-2年
- 3-5年
- 5年以上
- 应届生可接受

### Skills by Category

**R&D:**
- SolidWorks, Pro/E/Creo, UG/NX, AutoCAD, CATIA, ANSYS

**Production/Quality:**
- Excel Advanced, SPC/Minitab, MSA/FMEA

**SupplyChain:**
- SAP/ERP, Excel Advanced, WMS/MES

## Example Output

```markdown
# Product R&D Engineer

## Basic Info
- Category: R&D
- Location: Shenzhen
- Salary: 18-25K

## Requirements

### Must-Have [must]
| Dimension | Requirement | Resume Keywords |
|-----------|-------------|----------------|
| Education | Bachelor or above | Bachelor, Master, PhD |
| Experience | 3-5 years R&D | R&D Engineer, Product Design |
| Major | Mechanical/Materials | Mechanical Engineering, Materials |
| Skills | SolidWorks/Pro/E | SolidWorks, Pro/E, Creo |
| Certificates | None | - |

### Preferred [preferred]
| Dimension | Requirement | Resume Keywords |
|-----------|-------------|----------------|
| Industry | Consumer Electronics | Consumer Electronics |
| Project | APQP/PPAP | APQP, PPAP, NPI |
| Skills | Patent Writing | Patent, Invention Patent |
| Certificates | Mechanical Engineer | Mechanical Engineer |

## Matching Criteria
```json
{
  "position": "Product R&D Engineer",
  "must_match": {
    "education": {"min_level": "Bachelor", "keywords": ["Bachelor", "Master", "PhD"]},
    "experience": {"min_years": 3, "keywords": ["R&D Engineer", "Product Design"]},
    "major": {"keywords": ["Mechanical Engineering", "Materials"]},
    "skills": {"required": ["SolidWorks", "Pro/E"]},
    "certificates": {"required": []}
  },
  "preferred": {
    "industry": ["Consumer Electronics"],
    "project": ["APQP", "PPAP", "NPI"],
    "skills": ["Patent Writing"],
    "certificates": ["Mechanical Engineer"]
  }
}
```
```
