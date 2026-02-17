---
name: lesson-sync
description: Use when starting a session and lessons need syncing to CLAUDE.md, when last sync was more than 24 hours ago, or when user says "/lesson sync"
---

# Lesson Sync

## Overview

Sync top-10 lessons from YAML database to CLAUDE.md for persistent visibility.

**REQUIRED SUB-SKILL:** superpowers:lesson-add (defines YAML schema)

**Core principle:** High-frequency lessons must be visible in every conversation.

## When to Use

- First conversation of the day (check `last_sync` in `.claude/superpowers-lessons.yaml`)
- `last_sync` > 24 hours ago
- User manually requests `/lesson sync`
- After bulk lesson-add operations

## The Process

1. **Read** `.claude/superpowers-lessons.yaml`
   - If file missing or empty → inform user, skip sync
2. **Sort** lessons by `count DESC`
3. **Take top-10**
4. **Generate** Markdown block:

```markdown
<!-- LESSONS:START — superpowers:lesson-sync 自动更新，勿手动编辑 -->
## 教训区

> 上次同步：{date} | 条目总数：{total} | 显示 top-10

| # | 教训 | 次数 | 修复方案 |
|---|------|:----:|----------|
| 1 | {title} | {count} | {fix} |
...
<!-- LESSONS:END -->
```

5. **Replace** content between `LESSONS:START` and `LESSONS:END` in project CLAUDE.md
   - If markers not found → append entire block to end of CLAUDE.md
6. **Update** `last_sync` in YAML file to current timestamp
7. **Report**: Which lessons entered/exited top-10, total count

## Rules

- ONLY modify content between `LESSONS:START` and `LESSONS:END` markers
- Never touch any other part of CLAUDE.md
- Always update `last_sync` even if top-10 unchanged
- Use project CLAUDE.md (not global `~/.claude/CLAUDE.md`)
