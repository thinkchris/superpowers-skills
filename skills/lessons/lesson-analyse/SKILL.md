---
name: lesson-analyse
description: Use when completing tasks that had errors, repeated attempts, time-consuming debugging, or unexpected issues - post-task reflection to identify what went wrong
---

# Lesson Analyse

## Overview

Post-task reflection: identify what went wrong, why, and how to prevent it next time.

**Core principle:** Every mistake is a learning opportunity, but only if captured immediately.

## When to Use

- Task completed but had errors, retries, or wasted effort
- Debugging took longer than expected
- Had to backtrack or change approach mid-task
- Made a mistake that an existing rule/skill should have prevented

**When NOT to use:**
- Task completed smoothly with no issues
- Trivial tasks (typo fixes, simple questions)

## The Process

1. **Identify**: What specific things went wrong in this session?
2. **Categorize**: process / config / architecture / testing / deployment
3. **Root cause**: Why did it happen? (forgot rule? didn't know? skipped step?)
4. **Fix**: What should be done differently next time? (one sentence, actionable)
5. **Related skill**: Is there an existing superpowers skill that should have prevented this?
6. **Output**: Present lesson draft to user:

```
教训草案：
- title: [一句话描述]
- category: [process/config/architecture/testing/deployment]
- description: [具体错误场景]
- fix: [下次怎么做]
- related_skill: [关联 skill，如有]

是否录入？→ superpowers:lesson-add
```

7. **Prompt**: Ask user whether to record via `superpowers:lesson-add`

## Red Flags

- Skipping reflection because "it was just a small mistake" — small mistakes recur
- Writing vague fixes ("be more careful") — insist on actionable steps
- Attributing errors only to external factors — examine own process first
- Listing too many lessons at once — focus on the 1-2 most impactful
