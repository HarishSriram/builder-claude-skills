---
name: audit-docs
description: Audits all markdown files in the repository for repetition, stale content, factual inconsistencies, organisational issues, and token efficiency. Use when reviewing docs, checking doc quality, or after major changes.
---

# Repo Documentation Audit

Perform a strict audit of all markdown files in this repository. This is a quality control exercise — be critical, not generous.

## Step 1: Inventory

Find ALL .md files (excluding node_modules, .next, .venv, __pycache__, .git). For each file, note:
- File path and approximate line count
- 1-sentence summary of what it contains
- Which category it belongs to (spec, doc, config, content, agent, archive, design)

## Step 2: Repetition Analysis

Cross-reference every file against every other file. Look for:
- **Identical information** in multiple files (tech stack, project structure, scoring config, phase status, etc.)
- **Summaries that became copies** — overview files that duplicate detailed specs instead of linking to them
- **Internal repetition** — the same concept described twice within one file
- Count exact duplicated concepts and which files they appear in. Be specific — "tech stack appears in X, Y, Z" not "some overlap exists."

For every duplicated concept, identify the **canonical source** (the master file where that concept should be defined and maintained). The fix is always:
1. **Update the canonical source** to be accurate and complete
2. **Replace duplicates in other files** with a brief summary (1-2 lines max) + a link to the canonical source — never a full copy

Present duplications in a table with columns: Concept | Canonical source | Files that duplicate it | Recommended action (update master / replace with link / delete).

## Step 3: Stale Content

Check for:
- **History masquerading as current state** — post-mortems, retrospectives, or analysis sections in files whose purpose is "current state"
- **Done items in active lists** — completed backlog items, finished roadmap phases still in active planning docs
- **Spec drift** — specs that describe old behaviour after the code has changed (check version numbers, config values, thresholds, weights, metric counts)
- **Orphan references** — links to files that have been moved or renamed

## Step 4: Factual Inconsistencies

Cross-check numbers and config values across files:
- Test counts
- Scoring thresholds, weights, penalty values, lens tier assignments
- Phase completion status
- File paths and references
- API shapes and endpoint names

Flag every disagreement with the specific values and file locations.

## Step 5: Organisational Issues

Check for:
- Files in the wrong directory (e.g., internal planning docs in a content/ folder meant for blog posts)
- Naming that doesn't communicate purpose (e.g., "MASTER.md" for a legacy file)
- Missing index/README files in directories with 3+ files
- Archive candidates — completed work still in active directories

## Step 6: Token Efficiency & Merge Candidates

Every .md file costs tokens when loaded into agent context. Evaluate each file for:

- **Unreferenced files** — files not referenced by CLAUDE.md, README.md, any agent file, or any other .md file. If nothing points to a file, it's either orphaned or missing a reference. Flag it.
- **Low-value token spend** — files with high line counts but low information density (verbose prose that could be a table, repeated boilerplate, excessive formatting). Estimate token cost (lines × ~4 tokens/line) and flag files where the cost/value ratio is poor.
- **Merge candidates** — pairs (or groups) of files where:
  - Content overlaps significantly (>30% shared concepts)
  - Both files serve the same audience and purpose
  - Merging would reduce total tokens without losing information
  - The merged file would still have a clear, single responsibility

For each merge candidate, present: Files to merge | Shared content % | Proposed merged filename | What gets kept vs dropped | Estimated token savings.

**Do NOT recommend merging files that serve genuinely different purposes** (e.g., a spec vs its history log, a current design system vs its legacy predecessor). The goal is fewer files with less redundancy, not fewer files at any cost.

## Step 7: Report

Present findings in this structure:
1. **Repetition** — table of duplicated concepts with all file locations
2. **Stale content** — specific sections to trim, move, or delete (with line numbers)
3. **Factual inconsistencies** — table of disagreements with exact values from each file
4. **Organisational issues** — files to move, rename, or add
5. **Token efficiency** — unreferenced files, low-density files with estimated token cost, merge candidate table
6. **Recommended actions** — prioritised list (high/medium/low) with estimated effort. Merge recommendations should include before/after token estimates.

Be strict. "Intentional overlap for different audiences" is acceptable ONLY if the content genuinely differs (e.g., README is user-facing quick start vs CLAUDE.md is agent context). If two files contain the same table with the same data, that's duplication regardless of audience.

Do NOT make any changes. Report only. Wait for the user to approve actions before editing.
