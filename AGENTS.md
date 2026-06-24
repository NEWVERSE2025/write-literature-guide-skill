# Agent 使用说明

本仓库提供一个用于中文文献导读写作和格式修订的 agent skill。

当用户要求生成、检查或修改中文文献导读时，请先读取：

```text
skills/write-literature-guide/SKILL.md
```

如果 `SKILL.md` 要求读取参考规则，请继续读取：

```text
skills/write-literature-guide/references/guide-rules.md
```

执行任务时，应以 `SKILL.md` 和 `guide-rules.md` 为准。`README.md` 只说明安装和使用方法，不替代 skill 规则。

对于不支持 Codex skill 机制的 agent，可将 `SKILL.md` 和 `guide-rules.md` 作为普通任务上下文使用，并按其中规则生成或修改文献导读。
