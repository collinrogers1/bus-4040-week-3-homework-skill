# bus-4040-week-3-homework-skill

## What does the skill do?
This is a Claude Skill called **sql-debugger**. It automatically activates whenever I share a broken or misbehaving SQL query and ask what's wrong with it. Instead of just fixing the query silently, it identifies the specific bug, explains the root cause in plain English, provides the corrected query, and confirms why the fix works.

## How does the skill work?
The skill lives in a `SKILL.md` file with two parts:
- **Frontmatter** — a `name` and a `description` that tells Claude Code *when* to use the skill (trigger phrases like "why isn't this query working" or "debug this query").
- **Instructions** — a step-by-step process: identify the bug, explain the cause, provide the corrected query, confirm the fix. It also includes rules, like asking which SQL dialect is being used if it's not specified, since syntax varies across Postgres, MySQL, SQL Server, etc.

For Claude Code to actually discover and load the skill, a copy has to live in `.claude/skills/sql-debugger/SKILL.md` — skills are only auto-loaded from that folder at the start of a session. I kept a second copy at the repo root (`sql-debugger/`) so the skill is easy to find just by browsing the repo.

I tested it with a query that had two real bugs: an `INNER JOIN` that silently dropped customers with zero orders, and a `GROUP BY` clause missing a selected column. The skill correctly caught both, explained why the `INNER JOIN` was the cause, and rewrote it using a `LEFT JOIN` — along with a note about why the `GROUP BY` behavior differs between MySQL and other databases.

## Why did I create this skill?
I'm currently taking BIA 4530, where a lot of the coursework involves writing SQL queries that need to return exact, correct results — but the hardest bugs are the ones that don't throw an error, they just quietly return the wrong rows (a JOIN that drops records, a GROUP BY that doesn't group what you meant it to). I wanted a tool that catches that specific class of mistake and explains *why* it happened, not just what to change.

This also would have saved real time during my internship this summer at Micron, where I was writing and troubleshooting SQL queries to pull and analyze production/manufacturing data for reports. When a query silently returned incomplete or duplicated data, I'd usually have to manually trace through the joins and filters myself to find the issue. Having something that immediately flags the root cause — like an INNER JOIN dropping unmatched rows — would have cut that debugging time down significantly.

## How can this skill be useful later?
Any time I'm working with SQL — in a class project, a future internship, or a job — I'll run into queries that return wrong results without throwing an error, which are the hardest bugs to catch. This skill turns Claude into a quick second pair of eyes for that specific problem, and because it's just a text file, I can drop it into any repo or project going forward and reuse it immediately.
