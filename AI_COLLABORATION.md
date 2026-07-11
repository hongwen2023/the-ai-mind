# AI Collaboration Protocol

This protocol applies to ChatGPT, Codex, Claude, Gemini and future AI
assistants.

## Role Split

The project uses a publisher-style Author / Editor workflow.

| Role | Owner | Responsibility |
|---|---|---|
| Author | Codex | Draft chapters, notebooks, figures, glossary updates, commits |
| Editor-in-Chief | ChatGPT / human editor | Technical review, pedagogy, narrative, math, AI correctness, finance, research |
| Source of Truth | GitHub | Canonical files, review history, revisions, releases |

## Read Order

Always read:

1.  MANIFEST.md
2.  STATUS.md
3.  CONSTITUTION.md
4.  DECISIONS.md
5.  ARCHITECTURE.md
6.  [docs/author-bible/AUTHOR_BIBLE.md](docs/author-bible/AUTHOR_BIBLE.md)

before modifying any content.

## Files Requiring Extra Care

Do not modify without explicit approval:

-   MANIFEST.md
-   CONSTITUTION.md
-   ARCHITECTURE.md
-   AI_COLLABORATION.md
-   DECISIONS.md

Normal content files (chapters, notebooks, glossary) may be updated
following project standards.

## Contribution Rules

-   Produce one complete chapter at a time.
-   Follow [docs/bootstrap/CHAPTER_TEMPLATE.md](docs/bootstrap/CHAPTER_TEMPLATE.md).
-   Keep terminology consistent.
-   Update STATUS.md after completing a chapter.
-   Do not redesign project architecture unless explicitly requested.
-   Do not overwrite an editor review; preserve it under `reviews/`.
-   Treat review reports as project history, not temporary notes.

## Editorial Workflow

Each substantial chapter should follow:

```text
Design Brief (Author)
  ↓
Design Review (Editor)
  ↓
Draft (Author)
  ↓
Editorial Review (Editor)
  ↓
Revision (Author)
  ↓
Approval (Editor)
  ↓
Merge / publish
```

Review files live under:

```text
reviews/book1/chapterXX_review.md
```

Use [reviews/REVIEW_TEMPLATE.md](reviews/REVIEW_TEMPLATE.md) for new reviews.

Chapter Design Briefs live beside their book under `designs/`. A full chapter
draft begins only after the Editor-in-Chief approves its Design Brief.

## Commit Discipline

Use logical commits that preserve the publication trail:

```text
docs(book1): draft chapterXX
docs(review): editorial review chapterXX
docs(book1): revise chapterXX
docs(book1): approve chapterXX
```

For small chapters or early v1.0 work, one complete chapter commit is acceptable, but the review process becomes mandatory once an editor review exists.

## Consistency Checklist

-   Story before abstraction.
-   Intuition before mathematics.
-   Mathematics before code.
-   Include Engineering Perspective.
-   Include AI × Finance when appropriate.
-   Include Research Corner.
-   Include Teach Back.
