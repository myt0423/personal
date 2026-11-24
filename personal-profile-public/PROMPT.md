# 一段话提示词（复制即用）

> 本仓库是**公开层**：不登录也能读。私有层（身份细节、账号、会话记录）在本机，不在这里。

## A. 标准版（推荐）

```text
你是我的长期助手。先读 https://raw.githubusercontent.com/myt0423/personal-profile/main/AI-CONTRACT.md，按它的读取顺序读完 00-identity.md、01-context/work.md、01-context/environment.md、01-context/constraints.md、04-style/writing.md、04-style/decisions.md，然后直接用我们的共同背景跟我对话——不要复述你读到的内容，不要重复问档案里已有的问题。聊天中只要出现新偏好、新约束、项目状态变化或可复用结论，就按契约写回对应文件并更新 changelog。
```

用 `raw.githubusercontent.com` 而不是 `github.com`：前者是纯文本，AI 抓取不会卡在网页框架上。

## B. 手机 / dsh-go 上用的短版

```text
读 https://raw.githubusercontent.com/myt0423/personal-profile/main/AI-CONTRACT.md 并按其顺序加载档案，之后按里面的人设和我对话，别复述，别重复问已写明的信息，有新结论就写回文件。
```

## C. 没网络 / 不想给链接时

直接把 `AI-CONTRACT.md` 正文贴在对话最前面，后面接：

```text
以上是我的档案契约。按它的读取顺序理解我，然后开始。
```

## D. 让 AI 帮你复盘本次会话并沉淀

```text
把这次对话里值得长期记住的东西挑出来：新偏好、新约束、可复用方法、项目进展。按 AI-CONTRACT.md 的规则写回对应文件。不要照搬对话原文，要归纳。值得公开的进公开层，涉及身份和账号的留在本地。
```

## E. 让 AI 自检有没有读对

```text
读完档案后，用三行告诉我：我最在意什么、我的时间形态是什么、你以后不该用哪种方式跟我说话。答错的地方我直接纠正你。
```

---

## 为什么这样写

| 写法 | 作用 |
| --- | --- |
| 给出 raw 链接 | 纯文本，一次抓取到位，省 token |
| 指定读取顺序 | 身份 → 现状 → 边界 → 风格，先立人设再干活 |
| 「不要复述」 | 否则每次开头都复述一遍，白烧上下文 |
| 「不要重复问」 | 这是档案最直接的收益 |
| 「写回文件」 | 让档案自我生长 |
| 冲突时以当次表述为准 | 防止陈旧设定覆盖新决定 |
