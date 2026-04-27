# CLAUDE.md

This file provides guidance to Claude Code when working in this repository.

## Purpose of this repo

This is a **Product Management Operating System** — a portable collection of skills, prompts, and harness configuration that supports a PM's day-to-day work (discovery, prioritization, sprint planning, PRDs, roadmapping, stakeholder updates, etc.).

The repo is designed to be **plug-and-play across companies**. Skills and configuration here must remain free of any specific company, customer, product, or stakeholder content so this OS travels with the user.

## Where business context lives

**Not here.** All business, project, customer, and stakeholder content lives in external tools (Notion, Slack, Jira, Gmail, Google Calendar, etc.). The repo holds only the *machinery* that operates on that external content.

Concretely, do not write the following into local files in this repo:
- Company, customer, lawyer, insurer, partner, or stakeholder names
- Initiative names, PRDs, roadmaps, sprint plans, OKRs, or strategy docs
- Meeting notes, interview transcripts, or research findings
- Internal decisions, blockers, or action items

When a skill needs to capture or read business content, it must do so via the appropriate external tool. If a skill is about to write business content into the working directory, that's a bug — fix the skill.

## Tool preference: CLI over MCP

**Always prefer a command-line tool over an MCP server when both can do the job.** CLIs are faster, cheaper on context, scriptable, easier to chain with `grep`/`jq`/pipes, and produce outputs that are stable and easy to inspect.

Order of preference:
1. **Native CLI** for the service (e.g., `gh` for GitHub, `gcalcli` for Google Calendar, `jira` for Jira, `gcloud` / `aws` / etc.)
2. **Authenticated HTTP via `curl`** when no CLI exists but a REST API does, and credentials are available locally
3. **MCP tools** only when no CLI or HTTP path is practical, or when the MCP genuinely offers something the CLI cannot (e.g., rich block-level Notion editing)

Skills should be written with this preference in mind. If a skill currently uses MCP for something a CLI can do, that's worth refactoring.

If a needed CLI isn't installed, suggest the install command and ask the user before installing.

## Skills

Skills live under `.claude/skills/<skill-name>/SKILL.md`. Each skill is a self-contained, portable workflow. When editing a skill:

- Keep it free of company/product/customer specifics — use placeholders (`<initiative>`, `<channel>`, `<team>`) instead of real names
- State the trigger phrases explicitly in the frontmatter `description`
- Prefer CLI invocations in the skill body over MCP calls

## Conventions

- This repo is not a software project — there are no build, test, or lint commands. It's configuration and prompts.
- Keep markdown clean and skimmable. Avoid emojis unless the user asks.
- Today's date and the user's email are injected at session start; rely on those rather than hardcoding.
