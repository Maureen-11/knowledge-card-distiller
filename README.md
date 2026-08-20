# Knowledge Card Distiller

`knowledge-card-distiller` 是一个 Codex Skill，用于把用户粘贴的文章或本地 Markdown/TXT 文档提炼为简洁、忠于原文的知识卡片。

## 项目解决的问题

长文章通常包含重复说明、背景铺垫和多个相互关联的观点，不便于快速复习。这个 Skill 会识别其中最重要的知识，合并重复内容，并将其整理成单点卡片，帮助用户学习、复习和自测，同时避免添加原文没有的信息。

## 主要功能

- 处理用户粘贴的文章，以及本地 `.md`、`.markdown`、`.txt` 文件。
- 通常输出 5–8 张卡片；原文不足以支持 5 个独立知识点时宁可少输出，也不凑数。
- 每张卡片只讲一个知识点，包含标题、核心知识、简明解释，以及原文例子或自测题。
- 提取中心观点、定义、机制、区别或行动原则，合并重叠内容并删除重复信息。
- 保留原文中的限定条件、不确定性和适用范围，不编造事实、解释、例子或引文。
- 默认使用用户要求的语言；没有指定时跟随原文语言。
- 不生成图片、可执行代码、PDF 或交互界面。

## 安装方法

将 [`skills/knowledge-card-distiller`](skills/knowledge-card-distiller/) 文件夹复制到 Codex 的 Skills 目录中。

Windows 默认安装位置：

```text
C:\Users\<用户名>\.codex\skills\knowledge-card-distiller
```

也可以在本项目根目录运行 PowerShell：

```powershell
New-Item -ItemType Directory -Force -Path "$env:USERPROFILE\.codex\skills" | Out-Null
Copy-Item -Recurse -Force -LiteralPath ".\skills\knowledge-card-distiller" -Destination "$env:USERPROFILE\.codex\skills"
```

如果设置了自定义 `CODEX_HOME`，应改为复制到该目录下的 `skills` 文件夹。安装后确认目标目录中存在 `SKILL.md` 和 `agents/openai.yaml`。

## 使用方法

在 Codex 中调用 `$knowledge-card-distiller`，然后粘贴文章正文：

```text
使用 $knowledge-card-distiller，把下面的文章整理成中文知识卡片：

复利是收益继续参与后续收益计算的过程……
```

也可以提供本地文件路径：

```text
使用 $knowledge-card-distiller，把 D:\notes\article.md 转成中文知识卡片。
```

如果没有指定输出语言，Skill 会跟随原文语言。除非用户明确要求外，它不会联网补充资料。

## 输入输出示例

输入：

```text
主动回忆是指在不查看答案的情况下，主动尝试从记忆中提取信息。相比反复阅读，它更能检验学习者是否真正掌握内容。练习应间隔进行，因为适度遗忘会增加提取难度。题目太难时可以提供提示，但提示不应直接暴露答案。
```

输出节选：

```markdown
## 知识卡片

### 1. 主动回忆依靠主动提取信息
- **核心知识：** 主动回忆要求学习者在不查看答案时尝试从记忆中提取信息。
- **简明解释：** 它直接检验能否想起内容，而不只是再次接触内容。
- **自测：** 主动回忆与反复阅读的关键差别是什么？

### 2. 间隔练习利用适度遗忘
- **核心知识：** 将练习分散到不同时间进行，可以利用适度遗忘增加提取难度。
- **简明解释：** 原文把适度的提取难度视为间隔练习的一部分。
- **自测：** 为什么练习不应全部集中在同一时间？
```

## 许可证

本项目采用 [MIT License](LICENSE)。

