# 文献导读撰写 Skill
这是一个用于生成和修改中文文献导读的 agent skill。它适用于学术论文 PDF、中文翻译稿、已有文献导读模板和待修改的 Word 文档，可帮助 agent 按固定结构、中文表达习惯、Word 字体版式和引用格式生成 `.docx` 文献导读。


本仓库的核心 skill 位于：

```text
skills/write-literature-guide/
```

## 用途

该 skill 用于让 agent 完成以下任务：

- 阅读英文或中文学术论文，提取论文信息、摘要、研究背景、研究方法、结果和结论。
- 根据已有模板数据库的写法，生成中文文献导读。
- 将导读保存为 Word `.docx` 文件。
- 按模板修正文献导读的标题、正文、编号、图表、引用、超链接和段落格式。
- 从原 PDF 中截取必要的标题页、摘要、作者信息和关键图表，插入到导读文档中。

## 文件结构

```text
write-literature-guide-skill/
├─ README.md
└─ skills/
   └─ write-literature-guide/
      ├─ SKILL.md
      ├─ agents/
      │  └─ openai.yaml
      └─ references/
         └─ guide-rules.md
```

说明：

- `SKILL.md` 是 skill 的入口说明，agent 应先读取它。
- `references/guide-rules.md` 保存详细的写作规则、格式规则和质量检查清单。
- `agents/openai.yaml` 提供给支持 OpenAI/Codex 风格 skill 元数据的 agent 使用。
- `README.md` 只用于说明安装和使用方法，不应被当成写作规则的唯一来源。

## 安装到 Codex

### 用户级安装

适合希望在所有项目中都能调用此 skill 的情况。

Windows PowerShell：

```powershell
git clone https://github.com/NEWVERSE2025/write-literature-guide-skill.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -Recurse -Force ".\write-literature-guide-skill\skills\write-literature-guide" "$env:USERPROFILE\.codex\skills\write-literature-guide"
```

macOS 或 Linux：

```bash
git clone https://github.com/NEWVERSE2025/write-literature-guide-skill.git
mkdir -p ~/.codex/skills
cp -R write-literature-guide-skill/skills/write-literature-guide ~/.codex/skills/
```

### 项目级安装

适合只希望在某个项目中启用此 skill 的情况。

Windows PowerShell：

```powershell
git clone https://github.com/NEWVERSE2025/write-literature-guide-skill.git
New-Item -ItemType Directory -Force ".\.codex\skills" | Out-Null
Copy-Item -Recurse -Force ".\write-literature-guide-skill\skills\write-literature-guide" ".\.codex\skills\write-literature-guide"
```

macOS 或 Linux：

```bash
git clone https://github.com/NEWVERSE2025/write-literature-guide-skill.git
mkdir -p .codex/skills
cp -R write-literature-guide-skill/skills/write-literature-guide .codex/skills/
```

安装后重新打开 Codex 会话，或让 agent 重新加载 skill 列表。

## 在 Codex 中使用

安装后，可以用 `$write-literature-guide` 明确调用：

```text
使用 $write-literature-guide 根据这篇 PDF 生成一份中文文献导读，保存为 docx。
```

```text
使用 $write-literature-guide 检查这份文献导读，将格式、字体版式、编号、图表和引用按模板进行修改。
```

```text
使用 $write-literature-guide 根据当前文件夹中的论文和导读模板，生成同风格的中文文献导读。
```

## 兼容其它 agent 的使用方法

这个仓库尽量保持通用：skill 的规则写在 Markdown 文件中，没有依赖固定的本机路径，也没有要求只能由 Codex 使用。其它 agent 可以按自身能力选择以下方式接入。

### 支持 Codex 风格 skill 的 agent

将下面这个文件夹复制到该 agent 的 skill 目录：

```text
skills/write-literature-guide/
```

然后用 skill 名称调用：

```text
使用 write-literature-guide 生成中文文献导读。
```

或：

```text
使用 $write-literature-guide 生成中文文献导读。
```

### 支持仓库指令文件的 agent

打开你正在用的 agent（Claude Code、Codex、Cursor、OpenClaw、Hermes、CodeBuddy、Workbuddy、Gemini CLI、OpenCode 等），告诉它：
帮我安装这个 skill：https://github.com/NEWVERSE2025/write-literature-guide-skill

### 没有 skill 系统的 agent

把以下两个文件作为上下文提供给 agent：

```text
skills/write-literature-guide/SKILL.md
skills/write-literature-guide/references/guide-rules.md
```

然后用自然语言要求它执行任务，例如：

```text
请严格按照 SKILL.md 和 guide-rules.md 的规则，根据这篇论文 PDF 生成中文文献导读，并保存为 docx。
```

这种情况下，`$write-literature-guide` 只是一个方便识别的调用名称，不是必须语法。

