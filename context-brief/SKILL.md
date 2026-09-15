---
name: context-brief
description: Maintain a compact handoff brief for long-running work across Agent products. Use when opening a new conversation, continuing prior work, summarizing progress, completing work, handing off to another agent, or deciding whether project context should be updated.
---

# Context Brief

Use this skill to keep a short continuity brief for long-running work across Agent products. The brief helps the next agent or tool environment understand the project direction without rereading the full conversation or every source file.

When using this skill, tell the user that `context-brief` is being used, will be used, or may be useful for review, summary, handoff, or context update work. If the update is optional, ask briefly whether they want the brief updated before writing it. This applies in Codex, DSH, Cursor, Claude Code, Harness-style products, and other Agent environments that can read project rules or workflow instructions.

## Use cases

Use this skill in these situations:

- Start of work: when the user opens a new conversation, continues prior work, asks to resume, or refers to existing project context. Read the brief first, then choose the smallest useful set of source files for the current request.
- Explicit close or handoff: when the user asks to summarize, complete, wrap up, hand off, continue later, or move work to a new conversation. Update or create the handoff brief before finishing.
- Useful end-of-turn reminder: when the work reaches a natural stopping point and decisions, files, architecture, role boundaries, or next steps changed. Ask whether the user wants the brief updated.
- User-requested context update: update when the user confirms the brief should be changed.

Do not update the brief for small wording edits, one-off explanations, or routine answers that do not affect future work. Avoid forcing an update after every conversation; update only when it improves continuity.

## Product compatibility

This skill is platform-neutral. In Codex, it can be installed as a normal Skill. In Cursor, Claude Code, DSH, Harness-style products, 龙虾, or similar Agent products, use the `SKILL.md` content as project rules, system prompt material, workflow instructions, or shared knowledge. The required behavior is the same: read the brief before continuing work, update it only when it improves future continuity, and keep formal project details in their source documents.

## Handoff brief

Prefer one handoff Markdown file per project. If the user names a file, use that file. If no file exists, create a concise Markdown file with a clear name such as `context-brief.md` or `context-brief_project-handoff.md` in the project’s planning or docs directory.

The brief should help a future agent decide what to read next. It should not replace formal project documents, specifications, or decision records.

## What to include

Keep only information that changes future work:

- Current background and project direction.
- Decisions the user has confirmed.
- Terms, role boundaries, architecture assumptions, and naming that must stay consistent.
- A small file-routing table: user task -> files to read.
- Likely next work.
- Risks, mistakes to avoid, and user preferences that affect output quality.

Do not copy full conversation history, detailed arguments, long examples, or content that already lives in a linked source document. Link to the source instead.

## Size rule

Target 60-90 lines. If the brief exceeds 100 lines, compress before adding more. Keep one fact in one place. Prefer replacing stale text over appending.

## Reading rule for future conversations

The brief should instruct future agents to read it first, then choose the smallest useful set of source files for the user's current task. Do not tell future agents to read all linked documents by default.

## Writing style

Use direct working-note language. Preserve names, dates, links, role boundaries, approvals, and decisions. Remove filler, promotional language, chatbot residue, repeated conclusions, and unsupported claims.

For non-English project notes, preserve the user's preferred language and tone. If the workspace has a writing or style rule, apply it before delivery.

## Finish check

Before reporting completion, verify:

- Important links resolve or are clearly marked as local/project-relative.
- The brief still points to the right entry files.
- It does not duplicate detailed source content.
- It stays within the target length, or the overage is justified.
- It contains no TODO/TBD placeholders or stale decisions.
