# The AI Mind Constitution

This constitution defines the non-negotiable writing and teaching rules for The AI Mind.

It exists so that the project can survive across time, contributors, tools, and AI assistants without losing its identity.

## Rule 1: Why Before What

Never begin a core concept with a dictionary definition.

Do not start with:

> What is gradient?

Start with:

> Why does a machine need gradient?

Every chapter must first establish the problem that makes the concept necessary.

## Rule 2: Intuition Before Precision

Every difficult idea must first be made visible through intuition:

- story
- analogy
- geometry
- mental model
- small example

Only after intuition is established should formal mathematics appear.

## Rule 3: Story Before Mathematics

Mathematics should feel inevitable, not decorative.

The reader should feel:

> Of course we need this formula.

If a formula appears before the need for it is clear, rewrite the section.

## Rule 4: Mathematics Must Answer a Question

Every equation must answer:

- What problem does it solve?
- What does each symbol mean?
- What would fail without it?
- Where will it appear later in AI?

Equations that do not serve understanding should be removed.

## Rule 5: Code Must Reveal an Idea

Code is not included to look practical. Code must reveal structure.

Every code block should answer:

- Why do we need this?
- What concept does this make concrete?
- What does the framework usually hide?

## Rule 6: Connect to Engineering

Every core concept should eventually connect to real AI engineering:

- PyTorch
- autograd
- optimization
- transformers
- LLM training
- inference
- evaluation
- agents

The project is not only about knowing; it is about building.

## Rule 7: Teach Failure Modes

Every chapter must explain when the concept fails or becomes insufficient.

Examples:

- When do linear models fail?
- When does gradient descent struggle?
- When does attention become expensive?
- When does a loss function optimize the wrong thing?

Research thinking begins when learners understand limits.

## Rule 8: Teach Back

Every chapter must include a Teach Back prompt.

The learner should be able to explain the idea:

- to a 12-year-old
- to a peer
- to an engineer
- to an interviewer

If the learner cannot teach it, the learner does not own it yet.

## Rule 9: Research Corner

Every chapter must include a Research Corner with questions such as:

- What remains unsolved?
- Why are current methods imperfect?
- What papers or research directions connect here?
- If we were researchers, what would we try next?

The goal is not only to train users, but to grow researchers.

## Rule 10: Everything Connects

No concept should live alone.

Every chapter should connect backward and forward:

```text
Loss
  ↓
Optimization
  ↓
Backpropagation
  ↓
Autograd
  ↓
micrograd
  ↓
Transformer training
  ↓
RLHF / DPO / reward modeling
```

The project should gradually become a knowledge graph, not a pile of notes.

## Rule 11: Stable Knowledge in the Main Text

The main text should prioritize ideas that remain useful for years:

- vectors
- matrices
- probability
- optimization
- gradients
- backpropagation
- attention
- scaling
- evaluation

Fast-changing tools and model versions should be placed in update notes or appendices.

## Rule 12: Finance Is a First-Class Application

This curriculum is designed with AI research and finance in mind.

Where relevant, chapters should connect ideas to:

- company representation
- factor models
- risk
- financial statements
- industry research
- portfolio reasoning
- AI hedge fund research systems

The final learner should be able to use AI to build better research workflows.

## Rule 13: One Complete Chapter at a Time

Long-term drafts should be avoided.

Preferred workflow:

```text
ChapterXX.md
  ↓
Review
  ↓
Commit
  ↓
STATUS update
  ↓
Next chapter
```

The repository should remain readable and shippable at all times.

## Rule 14: Do Not Redesign During Production

The v1.0 architecture is frozen.

New structural ideas should go into `DECISIONS.md` or a future v2.0 backlog, not interrupt active writing.

## Rule 15: The Final Test

Every chapter should pass five tests:

1. A curious beginner can understand the opening.
2. A serious student can follow the reasoning.
3. An engineer can implement the core idea.
4. A researcher can see the open questions.
5. The chapter remains useful years later.

If a chapter fails these tests, revise it before calling it complete.
