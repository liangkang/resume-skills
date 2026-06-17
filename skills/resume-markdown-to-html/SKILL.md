---
name: resume-markdown-to-html
description: Use when user asks to generate HTML from resume markdown, convert resume to HTML, or explicitly invokes this skill - requires resume.md to exist in a variant directory
---

# Resume Markdown to HTML

## Overview

Converts `<variant>/resume.md` to `<variant>/resume.html` using pandoc. The skill bundles the shared `template.html` and `style.css`; each company-specific directory only needs `resume.md`.

## When to Use

Use when:
- User says "generate HTML from my resume"
- User says "convert resume to HTML"
- User says "create HTML version of resume"
- User explicitly calls this skill
- User finishes resume and wants HTML output

Do NOT use when:
- User only wants PDF (generate HTML first, then PDF separately)
- User wants to check/validate resume content (use update-resume skill)
- User asks about how to convert (explain, don't execute)

## Skill Assets

This skill includes the HTML template and stylesheet:

```
resume-markdown-to-html/
├── SKILL.md
├── template.html     ← Pandoc HTML template (bundled)
└── style.css         ← Stylesheet (copied into variant dir on build)
```

Resolve the skill directory in this order:
1. `.claude/skills/resume-markdown-to-html/` (after Claude Code install)
2. `skills/resume-markdown-to-html/` (repo layout)

## Required Files

Before conversion, verify:

```
deepseek/             ← example variant directory
└── resume.md         ← Source (REQUIRED)

skills/resume-markdown-to-html/   ← or .claude/skills/resume-markdown-to-html/
├── template.html
└── style.css
```

The variant directory name is flexible (`deepseek/`, `google/`, etc.) — use whichever folder the user is working in.

## Implementation

### Step 1: Resolve Paths

Set variables for the target variant and skill directory:

```bash
VARIANT=deepseek   # change to the active resume directory

if [ -d .claude/skills/resume-markdown-to-html ]; then
  SKILL_DIR=.claude/skills/resume-markdown-to-html
else
  SKILL_DIR=skills/resume-markdown-to-html
fi
```

### Step 2: Verify Files Exist

```bash
ls -la "$VARIANT/resume.md" "$SKILL_DIR/template.html" "$SKILL_DIR/style.css"
```

**If any file missing:**
- `resume.md` missing → **ERROR**: "resume.md not found in $VARIANT. Please create your resume first."
- Skill assets missing → **ERROR**: "template.html or style.css not found in $SKILL_DIR. Reinstall the skill."

### Step 3: Copy Stylesheet and Run Pandoc

Copy `style.css` into the variant directory so the generated HTML can load it locally, then convert:

```bash
cp "$SKILL_DIR/style.css" "$VARIANT/"
cd "$VARIANT" && pandoc resume.md \
  --template="../$SKILL_DIR/template.html" \
  -o resume.html
```

**Important:**
- Run pandoc from inside the variant directory
- Template path is relative to the variant directory
- `style.css` must sit beside `resume.html` for browser preview and PDF export

### Step 4: Verify Success

```bash
ls -lh "$VARIANT/resume.html" "$VARIANT/style.css"
```

**Success indicators:**
- `resume.html` exists and size > 0 bytes
- `style.css` was copied into the variant directory

### Step 5: Report to User

**Success message:**
```
✓ HTML generated successfully!

Location: deepseek/resume.html

Next steps:
- View: Open resume.html in your browser
- Export to PDF: Open in Chrome, press Cmd+P (macOS) or Ctrl+P (Windows), save as PDF
```

**Failure message:**
```
✗ HTML generation failed

Error: [specific error message]

Please check:
- resume.md exists and is valid Markdown
- skill assets exist in skills/resume-markdown-to-html/ or .claude/skills/resume-markdown-to-html/
- pandoc is installed (run: brew install pandoc)
```

## Common Mistakes

### ❌ Looking for template.html in the variant directory
```bash
# Wrong - template no longer lives in deepseek/
cd deepseek && pandoc resume.md --template=template.html -o resume.html
```

```bash
# Correct - use bundled skill assets
cp ../skills/resume-markdown-to-html/style.css .
cd deepseek && pandoc resume.md \
  --template=../skills/resume-markdown-to-html/template.html \
  -o resume.html
```

### ❌ Forgetting to copy style.css
```bash
# Wrong - HTML renders without styles
cd deepseek && pandoc resume.md --template=../skills/resume-markdown-to-html/template.html -o resume.html
```

```bash
# Correct - copy stylesheet first
cp ../skills/resume-markdown-to-html/style.css deepseek/
cd deepseek && pandoc resume.md --template=../skills/resume-markdown-to-html/template.html -o resume.html
```

### ❌ Running pandoc from repo root with wrong relative paths
```bash
# Wrong - template path breaks
pandoc deepseek/resume.md --template=skills/resume-markdown-to-html/template.html -o deepseek/resume.html
```

```bash
# Correct - cd into variant dir, use ../SKILL_DIR/template.html
cp skills/resume-markdown-to-html/style.css deepseek/
cd deepseek && pandoc resume.md --template=../skills/resume-markdown-to-html/template.html -o resume.html
```

## Error Handling

| Error | Cause | Solution |
|-------|-------|----------|
| `resume.md: No such file` | File doesn't exist | User must create resume first |
| `template.html: No such file` | Skill not installed or incomplete | Copy skills into `.claude/skills/` |
| `pandoc: command not found` | Pandoc not installed | Run `brew install pandoc` |
| `parse error at line X` | Invalid Markdown syntax | Check resume.md for syntax errors |
| HTML loads without styles | style.css not copied | Copy from skill dir before or after pandoc |

## Validation Checklist

Before reporting success:
- [ ] `resume.md` exists in the target variant directory
- [ ] Skill assets exist in `skills/resume-markdown-to-html/` or `.claude/skills/resume-markdown-to-html/`
- [ ] `style.css` copied into the variant directory
- [ ] Pandoc command executed without errors
- [ ] `resume.html` was created with content (size > 0 bytes)

## Real-World Impact

Centralizes HTML layout and styling in the skill so every company-specific resume directory stays content-only, while still producing a locally viewable HTML file with working CSS.
