# context-brief Skill

`context-brief` is a lightweight agent skill for long-running projects. It keeps a compact handoff brief so a future conversation or another agent can understand the project direction without reading the whole chat history or every source document.

Use it when work spans multiple conversations, multiple agents, or several documents. The skill is designed to reduce context cost: it reads or updates one short brief first, then routes the agent to only the files needed for the current task.

## What it does

- Creates or updates a concise project handoff Markdown file.
- Records confirmed decisions, file routes, role boundaries, next steps, and risks.
- Avoids copying full chat history or duplicating formal documents.
- Reminds the agent to ask before optional updates, instead of rewriting the brief after every turn.
- Tells the user when the skill is being used for review, summary, handoff, or context update work.

## Recommended use

Use `context-brief` at the start of a new conversation when the user wants to continue previous work. The agent should read the brief first, then open only the source files needed for the current request.

Use it at the end of work when the user asks to summarize, wrap up, complete, hand off, or continue later. If the conversation changed important decisions, files, architecture, role boundaries, or next steps, the agent can ask whether the brief should be updated.

Routine answers, small wording edits, and one-off explanations usually do not need an update.

## Install locally in Codex

Copy the `context-brief` folder into your Codex skills directory:

```bash
mkdir -p ~/.codex/skills
cp -R context-brief ~/.codex/skills/
```

Restart Codex if the skill does not appear automatically.

## Install for a project

For a repository or shared workspace, copy the skill into the project skills directory:

```bash
mkdir -p .agents/skills
cp -R context-brief .agents/skills/
```

Project-level installation is useful when all agents working in the same repository should share the same continuity workflow.

## Structure

```text
context-brief/
├── SKILL.md
└── agents/
    └── openai.yaml
```

`SKILL.md` contains the skill instructions and trigger description. `agents/openai.yaml` provides optional UI metadata for Codex.
