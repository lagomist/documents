# AGENTS.md

## Repository Overview

This is a **personal documentation/knowledge repository** (`lagomist/documents`) containing Markdown and text notes on Linux/Ubuntu administration, embedded development, software tools, and computer science topics. Content is primarily in **Chinese** with English technical terms.

## Directory Structure

```
├── README.md                    # Minimal readme
├── issue.md                     # Troubleshooting notes (WSL1, Ubuntu, arm64)
├── Memorandum.md                # Large memo/reference file
├── Memorandum.html              # HTML version of memorandum
├── record/                      # Technology reference notes (Markdown)
│   ├── cmake.md                 # CMake guide
│   ├── conda.md                 # Conda/Miniconda notes
│   ├── docker.md                # Docker commands & containers
│   ├── esp-idf.md               # ESP-IDF (Espressif IoT) notes
│   ├── git.md                   # Git command reference
│   ├── opencv.md                # OpenCV notes
│   ├── regularExpression.md     # Regex reference
│   └── yocto.md                 # Yocto Project notes
├── legacyRecord/                # Older notes (plain text)
│   └── *.txt                    # Vim, Ubuntu, Raspberry Pi, Orange Pi, etc.
├── dataStructure/               # CS notes (binary trees, etc.)
└── SoftwareRecord/              # Software tool documentation
    └── softwareToolList.md      # Comprehensive tool list
```

## Build / Lint / Test

**None.** This is a static documentation repository with no build system, no CI/CD, no package manager, and no test framework.

### Adding new notes

1. Place Markdown files in `record/` (tech references) or `SoftwareRecord/` (software tools)
2. Place plain text files in `legacyRecord/`
3. Commit with descriptive messages: `git commit -m "add <topic> notes"`

## Code Style Guidelines

### File Format

- **New files**: Use `.md` (Markdown) extension, UTF-8 encoding
- **Legacy files**: `.txt` files in `legacyRecord/` — preserve as-is
- **Line endings**: LF (Unix-style)

### Markdown Conventions

- **Headings**: Use `#` for top-level, `##` for sections, `###` for subsections
- **Section separators**: Use `---` between major sections
- **Code blocks**: Use fenced code blocks with language identifiers:

  ````markdown
  ``` bash
  sudo apt install <package>
  ```
  ````

- **Inline code**: Wrap commands and filenames in backticks: `git status`
- **Tables**: Use for structured metadata (e.g., tool descriptions):

  ```markdown
  | 描述 | 内容          |
  |----|-------------|
  | 功能 | Markdown编辑器 |
  | 说明 | 图形界面使用      |
  ```

- **Numbered lists**: Use for step-by-step instructions
- **Bold**: Use `**text**` for emphasis on section labels like **一.描述**, **二.安装**, **三.用法**

### Naming Conventions

- **Filenames**: `kebab-case.md` (e.g., `regularExpression.md`, `softwareToolList.md`)
- **Avoid spaces and special characters** in filenames
- **Categories**: Match directory names to content type (`record/` for tech refs, `SoftwareRecord/` for tools)

### Language

- **Primary language**: Chinese (Simplified)
- **Technical terms**: Keep in English (e.g., Docker, CMake, ESP-IDF, Git)
- **Code/comments**: English is acceptable; follow existing file conventions

### Content Structure (for new tool/reference docs)

Follow the three-section pattern used in `SoftwareRecord/softwareToolList.md`:

1. **一.描述** (Description) — table with 功能 (function) and 说明 (notes)
2. **二.安装** (Installation) — step-by-step commands
3. **三.用法** (Usage) — how to use the tool

### Git Conventions

- **Remote**: `https://github.com/lagomist/documents.git`
- **Branch**: `master`
- **User**: `lagomist` / `g3325035035137@gmail.com`
- **Commit messages**: Descriptive, in Chinese or English (match existing style)
- Example: `git commit -m "add docker container management notes"`

## Cursor / Copilot Rules

No `.cursorrules`, `.cursor/rules/`, or `.github/copilot-instructions.md` files exist in this repository.
