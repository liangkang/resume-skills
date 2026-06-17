# 简历

本仓库包含 Markdown 格式的简历，以及将其转换为 HTML 和 PDF 所需的文件。

每个顶层目录对应**一家公司/场景的简历版本**——构建流程相同，内容和侧重点按该投递目标调整。例如，`deepseek/` 是面向 DeepSeek 投递的版本。

## 项目结构

```
deepseek/           # 面向 DeepSeek 的简历版本
├── resume.md       # 简历源文件（Markdown）
└── resume.html     # 生成的 HTML 文件

skills/             # Agent Skills（需安装到 .claude/skills）
├── update-resume/
└── resume-markdown-to-html/
    ├── template.html   # 共享 Pandoc HTML 模板
    └── style.css       # 共享样式表
```

## Agent Skills（Claude Code）

本仓库提供用于编辑简历和生成 HTML 的 [Agent Skills](https://docs.anthropic.com/en/docs/claude-code/skills)。在 **Claude Code** 中使用，需将 skills 复制到项目下的 `.claude/skills` 目录：

```bash
mkdir -p .claude/skills
cp -r skills/* .claude/skills/
```

安装后，Claude Code 会自动识别并使用这些 skills：

| Skill | 说明 |
| --- | --- |
| `update-resume` | 检查简历完整性，提示补全缺失章节 |
| `resume-markdown-to-html` | 通过 Pandoc 将 `resume.md` 转换为 `resume.html`（含 `template.html` 和 `style.css`） |

之后可以直接对 Claude 说「更新我的简历」或「把简历转成 HTML」，它会自动调用对应的 skill。

## 构建步骤

### 1. 安装 Pandoc

[Pandoc](https://pandoc.org/) 是一款通用文档转换工具，请先完成安装。

**macOS（Homebrew）：**

```bash
brew install pandoc
```

**Windows（Chocolatey）：**

```bash
choco install pandoc
```

**Linux（Debian/Ubuntu）：**

```bash
sudo apt install pandoc
```

其他平台的安装方式请参阅 [Pandoc 官方安装指南](https://pandoc.org/installing.html)。

### 2. 将 Markdown 转换为 HTML

HTML 模板和样式表位于 `resume-markdown-to-html` skill 中，不在各版本目录里。先将 `style.css` 复制到版本目录，再在该目录下运行 pandoc：

```bash
VARIANT=deepseek

cp skills/resume-markdown-to-html/style.css "$VARIANT/"
cd "$VARIANT" && pandoc resume.md \
  --template=../skills/resume-markdown-to-html/template.html \
  -o resume.html
```

若 skills 已安装到 Claude Code，将路径 `skills/resume-markdown-to-html/` 替换为 `.claude/skills/resume-markdown-to-html/` 即可。

该命令读取 `resume.md`，套用共享模板，将样式表复制到输出目录旁，并生成 `resume.html`。

### 3. 导出为 PDF

在 Google Chrome（或其他基于 Chromium 的浏览器）中打开 `resume.html`：

1. 打开文件：将 `resume.html` 拖入 Chrome 窗口，或使用 **文件 → 打开文件**。
2. 打印为 PDF：按 `Cmd + P`（macOS）或 `Ctrl + P`（Windows/Linux）。
3. 将 **目标打印机** 设置为 **另存为 PDF**。
4. 点击 **保存**，选择 PDF 的保存位置。

## 编辑简历

修改 `deepseek/resume.md` 后，重复步骤 2 和 3 即可重新生成 HTML 和 PDF。
