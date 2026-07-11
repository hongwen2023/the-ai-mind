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
| Current sprint | Book I Prelude and Act I rewrite |
| Current chapter | Chapter 9 Design Brief |
| Last completed content | Chapter 8 canonical v1.0 and Learning Package |
| Architecture | Frozen for v1.0 |
| Next release target | v0.2 · Book I Chapter 11-20 |

## Current Learning Focus

```text
Prelude: complete v1.0
  ↓
Chapter 1: complete v1.0
  ↓
Chapter 2: canonical v1.0
  ↓
Chapter 3: Design Brief
  ↓
Chapter 3: canonical v1.0
  ↓
Chapter 4: Design Brief
  ↓
Chapter 4: canonical v1.0
  ↓
Chapter 5: Design Brief
  ↓
Chapter 5: canonical v1.0
  ↓
Chapter 6: Design Brief
  ↓
Chapter 6: canonical v1.0
  ↓
Chapter 7: Design Brief
  ↓
Chapter 7: canonical v1.0
  ↓
Chapter 8: canonical v1.0
  → Chapter 9: Design Brief
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
- [reviews/](reviews/README.md): permanent editorial reviews and review templates.

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
- [ ] Review file created or explicitly deferred.
- [ ] Git commit created.
- [ ] GitHub pushed.

## Bootstrap Protocol

If you are a new AI assistant or contributor taking over this project:

1. Read this `MANIFEST.md`.
2. Read [STATUS.md](STATUS.md).
3. Read [CONSTITUTION.md](CONSTITUTION.md).
4. Read [DECISIONS.md](DECISIONS.md).
5. Read [ARCHITECTURE.md](ARCHITECTURE.md).
6. Read [AI_COLLABORATION.md](AI_COLLABORATION.md).
7. Read [docs/bootstrap/CODEX_PROMPT.md](docs/bootstrap/CODEX_PROMPT.md).
8. Read [docs/author-bible/AUTHOR_BIBLE.md](docs/author-bible/AUTHOR_BIBLE.md).
9. Locate the current book and chapter from this manifest.
10. Continue from the current chapter.
11. Do not redesign the curriculum unless explicitly requested.
12. Produce one complete chapter at a time.
13. Commit after each completed chapter.
14. Update `STATUS.md` before moving to the next chapter.

## Resume Prompt

Use this prompt when starting a new ChatGPT/Codex conversation:

```text
Continue The AI Mind project.

Repository:
https://github.com/hongwen2023/the-ai-mind

Please first read MANIFEST.md, STATUS.md, CONSTITUTION.md, and DECISIONS.md.
Also read ARCHITECTURE.md and AI_COLLABORATION.md.
Then read docs/bootstrap/CODEX_PROMPT.md and docs/author-bible/AUTHOR_BIBLE.md.
Continue from the Current Chapter.
Do not redesign the architecture.
Produce one complete chapter at a time.
Commit after every completed chapter and update STATUS.md.
```

## Next Action

Create the Chapter 9 Design Brief as a Book I-level Understanding Audit. It
must reconstruct the relationship map from Chapters 1-8 rather than introduce
a new concept. Do not draft Chapter 9 until the Design Brief is approved.
