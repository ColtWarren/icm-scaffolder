# icm-scaffolder

An ICM workspace whose job is designing other ICM workspaces.

Built while working through Jake Van Clief's free
[Clief Notes](https://www.skool.com/cliefnotes) course, alongside the
lessons rather than after them. Public so the process is visible,
including the parts that aren't finished.

## What ICM is

The [Interpretable Context Methodology](https://arxiv.org/abs/2603.16021)
(Van Clief & McDermott, 2026) argues that for workflows that are
sequential, human-reviewed, and repeatable, folder structure can do the
job usually handed to an agent framework. Numbered folders encode
sequence. Each stage declares its inputs, process, and outputs in a
`CONTEXT.md`. One stage's `output/` is the next stage's input, and a human
can edit anything in between.

Protocol and reference implementation:
[RinDig/Interpretable-Context-Methodology](https://github.com/RinDig/Interpretable-Context-Methodology)
(MIT).

## What's here

| File | Layer | Purpose |
|---|---|---|
| `CLAUDE.md` | 0 | Identity and behavioral constraints |
| `CONTEXT.md` | 1 | What this workspace builds, what good looks like |
| `REFERENCES.md` | 3 | ICM conventions as enforced constraints |
| `proposals/` | — | Workspace designs produced here, not yet built |

No stages yet. This is a context bundle, not a pipeline — which is exactly
what Lesson 1.2 of the course builds. Stages come later.

## Status

Early. Three test runs against real requests, all of which ended in a
proposal rather than a build. That was the intended behavior, not a
failure to produce: `CLAUDE.md` asks the agent to confirm a shape before
generating a folder tree.

Two things testing surfaced that the published conventions don't cover:

**No defined input point.** Every stage gets an `output/` because stage
N+1 reads stage N. Stage 01 has nothing upstream, and nothing in the
conventions says where raw source material enters. A root-level
`brief.md` — a human-provided seed — resolves this without breaking the
handoff rule, since a seed isn't a stage output.

**Where fetched sources live.** Primary documents pulled mid-pipeline are
per-run by position but durable by nature. Putting them in a stage
`output/` means the no-outputs-in-git rule forces a refetch every run.
Unresolved.

## Caveats

The ICM paper is a preprint and states plainly that no controlled
comparison against monolithic prompting was run, that its practitioner
data is self-reported from a small self-selected group, and that all
testing was on a single model family. The structure is well-argued rather
than measured. Treated here as a promising method under test, not a
proven one.

## Credit

Interpretable Context Methodology by Jake Van Clief, paper co-authored
with David McDermott. arXiv:2603.16021, CC BY 4.0. Protocol MIT licensed.
Everything in this repo is my own work built on those conventions.
