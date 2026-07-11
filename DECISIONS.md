# The AI Mind Decisions

This file records major project decisions using an Architecture Decision Record (ADR) style.

Do not rewrite accepted decisions casually. Append new decisions instead.

## ADR-0001: Treat The AI Mind as a Living Curriculum

**Date:** 2026-07-11
**Status:** Accepted

### Decision

The AI Mind is not only a book. It is a living, open curriculum composed of books, notebooks, labs, figures, exercises, research notes, and projects.

### Rationale

The long-term goal is to train AI engineers and researchers, not merely publish static notes. A curriculum structure supports iteration, contribution, and multiple output formats such as Markdown, website, PDF, and notebooks.

## ADR-0002: GitHub Repository as Single Source of Truth

**Date:** 2026-07-11
**Status:** Accepted

### Decision

The GitHub repository is the single source of truth. Chat history is not the project memory.

### Rationale

Long conversations are fragile. A multi-year project needs version control, commit history, file-level ownership, and recoverable state.

## ADR-0003: Add MANIFEST.md as Bootstrap File

**Date:** 2026-07-11
**Status:** Accepted

### Decision

`MANIFEST.md` is the primary bootstrap file for humans and AI assistants.

### Rationale

Any future assistant or contributor should be able to resume the project by reading a small set of root files. `MANIFEST.md` records identity, current state, rules, bootstrap protocol, and next action.

## ADR-0004: Add CONSTITUTION.md as Writing Law

**Date:** 2026-07-11
**Status:** Accepted

### Decision

`CONSTITUTION.md` defines non-negotiable teaching and writing principles.

### Rationale

The project must maintain a consistent style across many chapters, books, tools, and contributors.

## ADR-0005: Freeze v1.0 Architecture

**Date:** 2026-07-11
**Status:** Accepted

### Decision

The v1.0 architecture is frozen. New structural ideas should be deferred to future revisions unless explicitly requested.

### Rationale

Continuous redesign prevents shipping. The first major objective is to complete a coherent v1.0, then refine.

## ADR-0006: One Complete Chapter Per Delivery Unit

**Date:** 2026-07-11
**Status:** Accepted

### Decision

Each completed chapter should be delivered as one canonical `chapter-XX.md` file.

### Rationale

Long-lived draft fragments make maintenance difficult. Drafting can happen during the writing process, but the repository should prefer canonical chapter files.

## ADR-0007: Commit After Each Completed Chapter

**Date:** 2026-07-11
**Status:** Accepted

### Decision

After each completed chapter, update status files and commit.

### Rationale

This keeps the repository always shippable and makes progress recoverable.

## ADR-0008: Book I Act II Is the Current Sprint

**Date:** 2026-07-11
**Status:** Accepted

### Decision

The current sprint is Book I Act II, covering the chain from vectors to backpropagation.

### Rationale

This material creates the bridge to Karpathy's `micrograd` and the later deep learning implementation track.
