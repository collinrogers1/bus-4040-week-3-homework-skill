---
name: sql-debugger
description: Use this skill whenever the user shares a SQL query that is erroring, returning wrong/unexpected results, or that they want checked for bugs. Trigger on phrases like "why isn't this query working," "what's wrong with this SQL," "debug this query," or any pasted SQL query paired with a problem description.
---

# SQL Debugger

When the user shares a broken or misbehaving SQL query, follow these steps:

1. **Identify the bug.** Read the query carefully and pinpoint the specific clause or line causing the problem (syntax error, wrong join type, missing GROUP BY, incorrect filter, off-by-one in date ranges, etc.).
2. **Explain the root cause in plain English.** One or two sentences — why the query produces the wrong result or fails, not just what's wrong syntactically.
3. **Provide the corrected query.** Show the full fixed query, not just the changed fragment, so it's easy to copy and run.
4. **Confirm the fix.** Briefly state why the correction resolves the issue.

## Rules
- If the SQL dialect isn't specified or obvious (Postgres, MySQL, SQL Server, SQLite, BigQuery), ask before assuming — syntax for dates, limits, and window functions varies.
- Don't change the query's intent — only fix what's actually broken.
- If there are multiple bugs, list them all rather than stopping at the first one found.
