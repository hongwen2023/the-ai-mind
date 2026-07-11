# Workflow

The AI Mind uses a publisher-style Author / Editor workflow.

## Standard Chapter Flow

```text
Draft chapter (Codex / Author)
  ↓
Commit draft
  ↓
Editorial review (ChatGPT / Editor)
  ↓
Save review under reviews/bookX/
  ↓
Revision (Codex / Author)
  ↓
Technical approval
  ↓
Update glossary / STATUS / roadmap
  ↓
Commit and push
```

## Review Files

Use:

```text
reviews/REVIEW_TEMPLATE.md
```

Store Book I reviews under:

```text
reviews/book1/
```

## Rule

Do not bypass review for major revisions. GitHub is the single source of truth.
