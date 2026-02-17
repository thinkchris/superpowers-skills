---
name: lesson-add
description: Use when a lesson has been identified from errors or mistakes and needs to be recorded, or when user says "记录教训", "record lesson", or "/lesson add"
---

# Lesson Add

## Overview

Record a lesson to the project's lesson database. This skill owns the YAML schema definition.

**Core principle:** Every recorded lesson makes the next session smarter.

## YAML Schema (Authoritative)

**File**: `{project}/.claude/superpowers-lessons.yaml`

```yaml
version: 1
last_sync: "2026-02-17T10:30:00+11:00"
lessons:
  - id: "kebab-case-unique-id"
    title: "一句话描述教训"
    count: 1
    category: "process"          # process | config | architecture | testing | deployment
    first_seen: "2026-02-17"
    last_seen: "2026-02-17"
    description: "具体错误场景"
    fix: "下次该怎么做（一句话，可执行）"
    related_skill: ""            # optional: superpowers:skill-name
```

**Field rules:**

| Field | Required | Rule |
|-------|:--------:|------|
| `id` | yes | kebab-case, unique, derived from title |
| `title` | yes | One sentence, specific |
| `count` | yes | Integer, starts at 1 |
| `category` | yes | One of: process, config, architecture, testing, deployment |
| `first_seen` | yes | ISO date of first occurrence |
| `last_seen` | yes | ISO date of most recent occurrence |
| `description` | yes | Specific error scenario |
| `fix` | yes | Actionable — not "be more careful" |
| `related_skill` | no | `superpowers:skill-name` if applicable |

## The Process

1. **Read** `.claude/superpowers-lessons.yaml` (create with `version: 1, last_sync: null, lessons: []` if missing)
2. **Deduplicate**: Check existing lessons by `id` and `title` semantic similarity
   - Match found → `count++`, update `last_seen`, merge description if new info
   - No match → create new entry with `count: 1`
3. **Write** updated YAML back to file
4. **Prune**: If total > 100 → sort by `count ASC, last_seen ASC` → delete tail until ≤ 100
5. **Confirm**: Output `✅ Recorded: {title} (count: {n}) | Total: {total} lessons`

## Red Flags

- Recording vague lessons ("注意一下") — insist on specific, actionable fix
- Duplicate lessons with different wording — always deduplicate by semantic similarity
- Forgetting to update `last_seen` on count increment
