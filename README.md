# CV / Resume

This repository contains Markdown resumes and the files needed to convert them to HTML and PDF.

Each top-level directory is a **company-specific resume variant** — the same build pipeline, with content and emphasis tailored to that application. For example, `deepseek/` is the version prepared for DeepSeek.

## Project Structure

```
deepseek/           # Resume variant for DeepSeek
├── resume.md       # Resume source (Markdown)
└── resume.html     # Generated HTML output

skills/             # Agent skills (install into .claude/skills)
├── update-resume/
└── resume-markdown-to-html/
    ├── template.html   # Shared Pandoc HTML template
    └── style.css       # Shared stylesheet
```

## Agent Skills (Claude Code)

This repo includes [Agent Skills](https://docs.anthropic.com/en/docs/claude-code/skills) for resume editing and HTML generation. To use them with **Claude Code**, copy the skills into your project's `.claude/skills` directory:

```bash
mkdir -p .claude/skills
cp -r skills/* .claude/skills/
```

After installation, Claude Code will automatically discover and use these skills:

| Skill | Description |
| --- | --- |
| `update-resume` | Validate resume completeness and prompt for missing sections |
| `resume-markdown-to-html` | Convert `resume.md` to `resume.html` via Pandoc (includes `template.html` and `style.css`) |

You can then ask Claude to "update my resume" or "convert resume to HTML" and it will invoke the matching skill.

## How to Build

### 1. Install Pandoc

[Pandoc](https://pandoc.org/) is a universal document converter. Install it before proceeding.

**macOS (Homebrew):**

```bash
brew install pandoc
```

**Windows (Chocolatey):**

```bash
choco install pandoc
```

**Linux (Debian/Ubuntu):**

```bash
sudo apt install pandoc
```

For other platforms and installation methods, see the [official Pandoc installation guide](https://pandoc.org/installing.html).

### 2. Convert Markdown to HTML

The HTML template and stylesheet live in the `resume-markdown-to-html` skill, not in each variant directory. Copy `style.css` into the variant folder, then run pandoc from there:

```bash
VARIANT=deepseek

cp skills/resume-markdown-to-html/style.css "$VARIANT/"
cd "$VARIANT" && pandoc resume.md \
  --template=../skills/resume-markdown-to-html/template.html \
  -o resume.html
```

If skills are installed for Claude Code, use `.claude/skills/resume-markdown-to-html/` instead of `skills/resume-markdown-to-html/`.

This reads `resume.md`, applies the shared template, copies the stylesheet beside the output, and writes `resume.html`.

### 3. Export to PDF

Open `resume.html` in Google Chrome (or another Chromium-based browser):

1. Open the file: drag `resume.html` into a Chrome window, or use **File → Open File**.
2. Print to PDF: press `Cmd + P` (macOS) or `Ctrl + P` (Windows/Linux).
3. Set **Destination** to **Save as PDF**.
4. Click **Save** and choose where to save the PDF.

## Editing the Resume

Edit `deepseek/resume.md`, then repeat steps 2 and 3 to regenerate the HTML and PDF.
