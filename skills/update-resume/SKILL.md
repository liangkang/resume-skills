---
name: update-resume
description: Use when user wants to create or update their resume - validates completeness of standard resume sections and prompts for missing information
---

# Update Resume

## Overview

Validates resume completeness by checking standard sections against a reference structure. Prompts user for missing information unless explicitly stated as unavailable.

## When to Use

Use when:
- User asks to "update my resume" or "check my resume"
- User wants to "create a resume"
- User says "is my resume complete?"

Do NOT use when:
- User asks only to export/generate PDF (use export-pdf skill)
- User asks to edit specific content without validation

## Core Pattern

```markdown
# Standard Resume Sections (Chinese)
Based on demo_resume.md structure:
1. 姓名和联系方式 (Name & Contact): 姓名, 电话, 邮箱
2. 工作经历 (Work Experience)
   - 公司名称
   - 时间段 (YYYY年MM月 - YYYY年MM月 或 至今)
   - 职位名称 部门名称
   - 负责业务
   - 主要职责
   - 业务价值
3. 教育经历 (Education)
   - 学校名称
   - 时间段
   - 专业名称 学历 学院名称 全日制
   - 专业排名
   - 编程技能
4. 荣誉奖项 (Awards/Honors) - optional
   - 奖项名称 | 赛事/活动 | 成绩
5. 开源项目 (Open Source) - optional
   - 项目名称, GitHub链接
6. 项目经历 (Project Experience)
   - 项目名称
   - 时间段
   - 角色/职位 部门名称
   - 工作内容
   - 项目
   - 最终效果
```

## Implementation

### Step 1: Locate Resume File

Look for resume.md in these locations:
1. `deepseek/resume.md` (primary)
2. `resume.md` (root)
3. Ask user for path if not found

### Step 2: Read and Parse

Read the file and identify all level-2 headings (`##`). These are the actual sections present.

### Step 3: Validate Against Standard Sections

Compare found sections against demo_resume.md structure:

**Required Sections:**
- 姓名和联系方式: 姓名, (+86) 电话, 邮箱
- 工作经历: 公司, 时间, 职位/部门, 负责业务, 主要职责, 业务价值
- 教育经历: 学校, 时间, 专业/学历/学院/全日制, 专业排名, 编程技能
- 项目经历: 项目名称, 时间, 角色/部门, 工作内容, 项目, 最终效果

**Optional Sections:**
- 荣誉奖项: 奖项名称 | 赛事/活动 | 成绩
- 开源项目: 项目名称, GitHub链接

| Standard Section | Status | Action |
|------------------|--------|--------|
| 姓名和联系方式 | Present + has all fields | ✓ |
| 姓名和联系方式 | Present but missing fields | Ask user to provide missing fields |
| 工作经历 | Missing any sub-field | Ask for complete structure |
| 荣誉奖项 (optional) | Missing | Ask once, accept "I don't have" |

### Step 4: Report Findings

**Format:**
```
## Resume Completeness Check

✓ Complete Sections:
- 工作经历: 2 companies listed with full details (负责业务, 主要职责, 业务价值)
- 教育经历: 清华大学, with 专业排名 and 编程技能

⚠️ Incomplete Sections:
- 姓名和联系方式: Missing email address
- 项目经历: Missing 工作内容 or 最终效果 details

❌ Missing Sections:
- 项目经历: This section is recommended

Optional sections not present:
- 荣誉奖项
- 开源项目
```

### Step 5: Prompt for Missing Info

**Essential sections (work, education, contact):**
```markdown
Your resume is missing the following essential information:

1. **Email address** - Required for employers to contact you
2. **工作经历 details** - Current entry lacks:
   - 负责业务 (Business responsibilities)
   - 主要职责 (Main duties)
   - 业务价值 (Business value)
3. **项目经历** - Missing:
   - 工作内容 (Work content)
   - 项目 (Project details)
   - 最终效果 (Final results)

Please provide these details, or let me know if you don't have this information.
```

**Optional sections (awards, open source):**
```markdown
Optional sections that could strengthen your resume:
- 荣誉奖项 (Awards)
- 开源项目 (Open Source projects)

Do you have any of these to add? It's fine if you don't.
```

## Handling User Responses

| User Response | Action |
|---------------|--------|
| "I don't have awards" | Accept and skip that section |
| "I graduated in 2020" | Add to education section |
| "None" or "No" for optional sections | Accept and don't ask again |
| Provides partial info | Validate what's provided, ask for remaining required fields |

## Common Mistakes

### ❌ Forcing Optional Sections
```markdown
❌ "You MUST add awards section"
✅ "Awards section is optional - do you have any to add?"
```

### ❌ Accepting Incomplete Required Sections
```markdown
❌ User: "I don't want to add my education"
    You: "OK, skipping education"
✅ User: "I don't want to add my education"
    You: "Education is a standard required section for most resumes. 
         Without it, your resume may be incomplete for job applications.
         Are you sure you want to proceed without education history?"
```

### ❌ Not Checking Content Depth
```markdown
❌ Section exists → assume complete
✅ Section exists → check if has meaningful content (not just header)
```

## Validation Checklist

Before reporting resume as "complete":
- [ ] All required sections present (姓名和联系方式, 工作经历, 教育经历, 项目经历)
- [ ] Required sections have actual content (not empty)
- [ ] Contact info includes: 姓名, (+86) 电话, 邮箱
- [ ] Work experience has complete structure: 公司, 时间, 职位/部门, 负责业务, 主要职责, 业务价值
- [ ] Education has: 学校, 时间, 专业/学历/学院/全日制, 专业排名, 编程技能
- [ ] Project experience has: 项目名称, 时间, 角色/部门, 工作内容, 项目, 最终效果
- [ ] Asked about optional sections (荣誉奖项, 开源项目) at least once

## Edge Cases

**Fresh Graduate (no work experience):**
- Education and project experience become critical sections
- Education must include: 专业排名, 编程技能
- Projects/coursework can substitute for work experience
- Still require complete project structure: 工作内容, 项目, 最终效果
- Accept lack of work experience explicitly

**Career Changer:**
- May have unconventional structure
- Validate for completeness of their chosen format
- Standard sections still serve as checklist

**Minimal Resume:**
- If user explicitly says "I only want name, phone, job"
- Warn that minimal resume may be insufficient for applications
- Accept only after explicit confirmation

## Real-World Impact

Ensures users don't submit incomplete resumes while respecting their explicit choices about optional content.
