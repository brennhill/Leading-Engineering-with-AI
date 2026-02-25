# Docs Index for Humans and LLMs

This folder exists to make the repo easy to navigate and reason about.

The goal is simple: every feature has one canonical doc that links to its design, code, and tests in the header so humans and coding agents can find the right context fast.

## How to use this folder
1. Start at `docs/index.md` (create it if missing) as the table of contents.
2. For each feature, create one file from `docs/templates/feature-context-template.md`.
3. Keep the header links current whenever code paths or tests move.

## Required header fields (for feature docs)
Every feature doc should include these fields in front matter:
- `feature`
- `status`
- `spec`
- `code_paths`
- `tests`
- `owner`
- `last_updated`

Optional but recommended:
- `related_docs`
- `runbook`
- `risk_tier`
- `feature_flag`

## Quality rules
- One feature, one canonical doc.
- Link to source of truth; do not duplicate long specs.
- Keep docs short and high signal.
- Add concrete paths, not vague descriptions.
- Update `last_updated` whenever behavior changes.
- If a doc is stale, mark it stale at the top.

## Why this helps LLM quality
A clean docs map reduces search drift, lowers context bloat, and improves first-pass correctness.

If you are using coding agents, this structure is often the difference between "mostly right" and "production ready."
