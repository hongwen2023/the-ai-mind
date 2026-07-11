# The AI Mind Manifest

**Version:** 0.1
**Repository:** https://github.com/hongwen2023/the-ai-mind
**Status:** Active living curriculum
**Single source of truth:** This repository

## Identity

The AI Mind is an open curriculum for learning artificial intelligence from first principles.

It is not only a book. It is a living education project that combines:

- Books
- Notebooks
- Labs
- Figures
- Exercises
- Research notes
- Capstone projects

## Mission

Help curious learners grow through four stages:

```text
AI Learner
  ↓
AI Engineer
  ↓
AI Researcher
  ↓
AI Builder
```

The long-term goal is to help a serious learner reach the level of a strong AI master's graduate: able to explain, derive, implement, evaluate, and create AI systems.

## Current State

| Field | Value |
|---|---|
| Current version | v0.1 |
| Current stage | Book I v1.0 drafting |
| Current book | Book I · Discovering Intelligence |
| Current sprint | Sprint 1 · Book I Act II |
| Current chapter | Chapter 17 |
| Last completed content | Chapter 16 complete v1.0 |
| Architecture | Frozen for v1.0 |
| Next release target | v0.2 · Book I Chapter 11-20 |

## Current Learning Focus

```text
Vector
  ↓
Matrix
  ↓
Linear Transformation
  ↓
Nonlinearity
  ↓
Loss Function
  ↓
Optimization
  ↓
Chain Rule
  ↓
Backpropagation
  ↓
Autograd / micrograd
```

## Constitution Summary

The full rules live in [CONSTITUTION.md](CONSTITUTION.md). The short version:

- Why before What.
- Intuition before precision.
- Story before mathematics.
- Mathematics before code.
- Code before engineering.
- Engineering before research.
- Every chapter must explain failure modes.
- Every chapter must include Teach Back.
- Every chapter must include Research Corner.
- Every chapter should connect to the knowledge graph.

## Documentation Map

Project support documents live under [docs/](docs/README.md):

- [docs/bootstrap/](docs/bootstrap/): Codex bootstrap and resume files.
- [docs/author-bible/](docs/author-bible/): editorial and content quality standards.
- [docs/operations/](docs/operations/): project operations, release, review, and maintenance notes.
- [docs/handoff/](docs/handoff/): structured handoff notes for new work sessions.

## Definition of Done

A chapter is not considered complete until these are done:

- [ ] Markdown chapter completed.
- [ ] Learning objectives included.
- [ ] Feynman explanation included.
- [ ] Mathematics section included where appropriate.
- [ ] Coding lab included or explicitly deferred.
- [ ] Engineering perspective included.
- [ ] AI x Finance section included where relevant.
- [ ] Failure modes included.
- [ ] Research Corner included.
- [ ] Exercises included.
- [ ] Glossary terms updated.
- [ ] STATUS.md updated.
- [ ] Git commit created.
- [ ] GitHub pushed.

## Bootstrap Protocol

If you are a new AI assistant or contributor taking over this project:

1. Read this `MANIFEST.md`.
2. Read [STATUS.md](STATUS.md).
3. Read [CONSTITUTION.md](CONSTITUTION.md).
4. Read [DECISIONS.md](DECISIONS.md).
5. Read [docs/bootstrap/CODEX_PROMPT.md](docs/bootstrap/CODEX_PROMPT.md).
6. Read [docs/author-bible/AUTHOR_BIBLE.md](docs/author-bible/AUTHOR_BIBLE.md).
7. Locate the current book and chapter from this manifest.
8. Continue from the current chapter.
9. Do not redesign the curriculum unless explicitly requested.
10. Produce one complete chapter at a time.
11. Commit after each completed chapter.
12. Update `STATUS.md` before moving to the next chapter.

## Resume Prompt

Use this prompt when starting a new ChatGPT/Codex conversation:

```text
Continue The AI Mind project.

Repository:
https://github.com/hongwen2023/the-ai-mind

Please first read MANIFEST.md, STATUS.md, CONSTITUTION.md, and DECISIONS.md.
Then read docs/bootstrap/CODEX_PROMPT.md and docs/author-bible/AUTHOR_BIBLE.md.
Continue from the Current Chapter.
Do not redesign the architecture.
Produce one complete chapter at a time.
Commit after every completed chapter and update STATUS.md.
```

## Next Action

Complete `books/book-1-discovering-intelligence/chapters/chapter-17.md`:

> Chapter 17: 为什么优化能够让模型越来越好？

Then update `STATUS.md` and continue to Chapter 18.
