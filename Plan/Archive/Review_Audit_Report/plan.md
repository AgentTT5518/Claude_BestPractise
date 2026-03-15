# Plan: Review_Audit_Report

**Status:** Complete
**Created:** 2026-03-15
**Feature Branch:** `feature/Review_Audit_Report`

---

## Goal / Problem Statement

Address all issues identified in the audit report for the Claude Code Project Template repo. The audit flagged critical security/CI gaps, moderate documentation and configuration issues, and minor inconsistencies.

## Proposed Approach

Work through each issue tier (critical → moderate → minor) and apply targeted fixes. No new features — only corrections to existing files and creation of missing required files.

## Files to Create / Modify

| Action | File Path | Description |
|--------|-----------|-------------|
| Modify | `.gitignore` | Add `node_modules/`, `.env*`/`!.env.example`, `tests/test-results/`, build output dirs |
| Modify | `.github/workflows/cd.yml` | Add `node_check` conditional (same as ci.yml); comment out `cache: 'npm'` |
| Modify | `.github/workflows/ci.yml` | Expand secret scan to all of `.`; add `*.yaml`/`*.yml`; exclude `.git/` |
| Modify | `ARCHITECTURE.md` | Fix "Last updated" date from 2026-03-12 to 2026-03-13 |
| Modify | `CLAUDE.md` | Add template note explaining unchecked items and `[placeholder]`/`[pm]` tokens are intentional |
| Modify | `README.md` | Fix Quick Start step 3 — ARCHITECTURE.md already exists, no need to "create" it |
| Create | `.env.example` | Placeholder env vars file required by Rule 1 and Setup Checklist |
| Create | `docs/decisions/.gitkeep` | Create missing `docs/decisions/` directory referenced in CLAUDE.md and ARCHITECTURE.md |

## Open Questions

- None remaining.

## Decisions Made

- `docs/decisions/` created with `.gitkeep` so git tracks the empty directory; it will be populated as features complete
- `.env.example` created with commented-out example vars so it's useful as a starter without containing real values
- CD pipeline kept as a reference deploy template (Vercel) but now skips all steps when no `package.json` is present, matching CI behavior
- Secret scan now scans all of `.` with `*.yaml`/`*.yml` included to catch secrets in workflow files; `.git/` excluded to avoid false positives

## Comments / Review Notes

- Audit report also noted `settings.local.json` has absolute paths and is gitignored via `.claude/*` — no action needed, behavior is correct
- `src/` and `tests/` directories don't exist (template repo) — no action needed, CI handles this gracefully with the `node_check` conditional
- `docs/requirements/` has one file (`project-setup-decision-system.md`) — not a gap, just sparse; no action needed
