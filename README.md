# context-brief Skill

`context-brief` 是一个用于长期任务续接的通用 Agent Skill。它维护一份简短的交接说明，让新窗口、新 Agent 或新的工具环境快速了解项目背景、关键决策、重要文件和下一步方向，避免每次都重新阅读完整对话和所有文档。

这个 Skill 不绑定某一个产品。它可以用于 Codex、DSH、Cursor、龙虾、Claude Code、Harness，以及其他支持自定义规则、项目说明、system prompt、agent skill 或知识文件的 Agent 产品。

## 核心思路

`context-brief` 只做一件事：用一份短文档承接上下文。

Agent 开始工作时，先读取这份交接说明，再按当前任务读取必要文件。任务结束时，如果用户明确要求总结、交接、下次继续，或者本轮对话产生了关键变化，Agent 再更新交接说明。普通问答、小范围改写、一次性解释不需要更新。

## 它解决什么问题

- 长任务换窗口后，新 Agent 不知道前因后果。
- 项目文件越来越多，每次都读全量文档会浪费 token。
- 多个 Agent 或多个产品协作时，容易重复判断、遗漏约定或使用过期口径。
- 用户在多轮讨论中确认过的决策，没有沉淀成可复用的上下文。
- 同一项目在 Codex、Cursor、Claude Code、DSH、Harness 等工具之间切换时，缺少统一的上下文入口。

## 适合哪些 Agent 产品

| 产品或环境 | 推荐用法 |
|---|---|
| Codex | 放入 `~/.codex/skills` 或项目 `.agents/skills`，作为可触发的 Skill 使用。 |
| Cursor | 将 `SKILL.md` 的规则放入项目规则、Agent rules 或团队约定文档中，并把交接说明放在项目 docs 目录。 |
| Claude Code | 将 `SKILL.md` 作为项目级工作规则或上下文说明使用，交接说明作为每次续接前的入口文档。 |
| DSH / DeepSeek Harness | 将 `SKILL.md` 注册为 Harness 的任务前置规则或 Agent 工作流说明，交接说明作为任务路由前的上下文输入。 |
| Harness 类产品 | 将该 Skill 接入任务编排入口，在分发给具体 Agent 前先读取交接说明。 |
| 龙虾或其他 Agent 产品 | 如果产品支持自定义提示词、项目知识库或工作流说明，可直接引用 `SKILL.md`，并指定固定交接文档路径。 |

不同产品的 Skill 目录和触发机制可能不同。只要能做到两件事，就可以使用 `context-brief`：第一，Agent 开工前能读到规则；第二，Agent 能读取和更新项目交接说明。

## 适合什么时候用

- 新窗口继续旧任务时，先读取交接说明。
- 用户说“总结”“完成”“收尾”“交接”“下次继续”时，更新交接说明。
- 本轮对话产生了关键决策、重要文件、架构变化、角色边界变化或下一步调整时，询问用户是否需要更新。
- 项目需要多人、多 Agent 或多工具协作，希望统一上下文入口时。

## 交接说明应该写什么

交接说明只保留会影响后续工作的内容：

- 当前背景和项目方向。
- 用户已经确认的决策。
- 必须保持一致的术语、角色边界、架构假设和命名。
- 文件路由：什么任务应该读取哪些文件。
- 可能的下一步工作。
- 需要避免的错误、风险和用户偏好。

不要把完整聊天记录、详细推理过程、长示例或正式文档正文复制进去。已有内容应链接到源文件。

## 建议的文档长度

交接说明建议控制在 60-90 行。超过 100 行时，先压缩旧内容，再补充新内容。优先替换过期信息，不要一直追加。

## 在 Codex 中安装

把 `context-brief` 文件夹复制到本地 Codex skills 目录：

```bash
mkdir -p ~/.codex/skills
cp -R context-brief ~/.codex/skills/
```

如果希望同一个项目里的 Agent 都使用这套续接规则，可以放到项目目录：

```bash
mkdir -p .agents/skills
cp -R context-brief .agents/skills/
```

## 在其他 Agent 产品中使用

如果目标产品没有 Codex Skill 目录，可以采用通用接入方式：

1. 把 `context-brief/SKILL.md` 作为项目规则、Agent rules、system prompt 或工作流说明。
2. 在项目中创建一个固定的交接文档，例如 `context-brief.md`。
3. 要求 Agent 在续接任务时先读 `context-brief.md`，再按任务读取相关文件。
4. 要求 Agent 在用户明确要求总结/交接，或关键上下文变化后，经用户确认再更新 `context-brief.md`。

## 目录结构

```text
context-brief/
├── SKILL.md
└── agents/
    └── openai.yaml
```

`SKILL.md` 是 Skill 的主体说明，包含触发场景、交接说明的写法和检查规则。`agents/openai.yaml` 是 Codex 的展示信息，其他 Agent 产品可以忽略。

## 一句话介绍

`context-brief` 用一份短交接文档承接长期任务，让新窗口、新 Agent 或新的工具环境先掌握项目全貌，再按需读取相关文件，减少重复沟通和 token 消耗。
