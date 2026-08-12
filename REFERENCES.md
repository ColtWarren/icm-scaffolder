# References

Source: Interpretable Context Methodology, Van Clief & McDermott,
arXiv:2603.16021 (CC BY 4.0). Protocol repo MIT licensed:
github.com/RinDig/Interpretable-Context-Methodology

Everything below is a constraint to apply, not background to read.

---

## The five layers

| Layer | File | Question | Budget |
|---|---|---|---|
| 0 | `CLAUDE.md` | Where am I? | ~800 tok |
| 1 | `CONTEXT.md` | Where do I go? | ~300 tok |
| 2 | Stage `CONTEXT.md` | What do I do? | 200–500 tok |
| 3 | Reference material | What rules apply? | 500–2k tok |
| 4 | Working artifacts | What am I working with? | varies |

Layers 0–2 are structural routing. Layers 3–4 are content.

**Layer 3 vs Layer 4 is the distinction that matters most:**

| | Layer 3 | Layer 4 |
|---|---|---|
| Changes between runs | No | Yes |
| Model should | Internalize as constraints | Process as input |
| Lives in | `references/`, `_config/`, `shared/` | `output/` |
| Analogy | The recipe | The ingredients |

Mixing them forces the model to sort rules from material on its own.

---

## Workspace shape

```
workspace/
  CLAUDE.md              # Layer 0
  CONTEXT.md             # Layer 1: routing
  stages/
    01-<name>/
      CONTEXT.md         # Layer 2: stage contract
      references/        # Layer 3
      output/            # Layer 4: handoff point
    02-<name>/
      ...
  _config/               # Layer 3: standing config
  shared/                # Layer 3: cross-stage
  setup/
    questionnaire.md     # one-time onboarding
```

Numbering encodes execution order. Stage N's `output/` is stage N+1's input.
A human edit to that folder is picked up by the next stage.

---

## Stage contract template

Every stage CONTEXT.md has exactly three required sections.

```markdown
## Inputs
| Source | File/Location | Section/Scope | Why |
|---|---|---|---|
| Previous stage | ../01-<name>/output/ | Full file | Source material |
| Conventions | ../../_config/rules.md | Naming section | Applies to output |

## Process
1. <step>
2. <step>
3. Run audit
4. Save to output/

## Outputs
| Artifact | Location | Format |
|---|---|---|
| <name> | output/<slug>.md | Markdown |
```

Two optional sections, for stages where the model makes judgment calls:

- **Checkpoints** — agent pauses mid-stage, presents options, human steers
  before the next unit of work begins.
- **Audits** — checklist the agent runs *before* writing output. Every check
  needs an unambiguous pass condition. "Is it good?" is not a check.

Linear stages (extraction, rendering, file moves) usually need neither.

---

## The conventions

**Architecture**

- *Stage contracts.* Inputs, Process, Outputs. Always all three.
- *Stage handoffs.* Output folders connect stages. Edits are picked up.
- *One-way references.* If A points at B, B does not point back at A.
- *Selective section routing.* Name the section, not the whole file.
- *Canonical sources.* One home per fact. Duplicated rules drift.

**Quality**

- *Specs are contracts.* A spec says WHAT and WHEN, never HOW. The build
  stage keeps freedom above the quality floor.
- *Checkpoints.* Creative stages pause for steering.
- *Stage audits.* Unambiguous pass conditions, run before output is written.
- *Value validation.* Content stages declare what value the output delivers
  before drafting starts.
- *Docs over outputs.* Agents learn patterns from reference docs, never from
  previous outputs. Early outputs are the worst outputs; learning from them
  means quality never improves.

**Onboarding**

- *Questionnaire design.* Flat, all at once, system-level only. Configure
  the factory, not the product.
- *Shared constants.* Code-producing workspaces define constants once and
  import everywhere.

---

## Hard limits

- CONTEXT.md files: under 80 lines
- Reference files: under 200 lines
- No stage outputs committed to git (`.gitkeep` only)
- No circular dependencies between stages
- Creative stages: at least one checkpoint and one audit

---

## Where ICM does not apply

Stop and say so if the workflow is any of these:

- **Tight agent loops.** File handoffs are too slow for real-time exchange.
- **High concurrency.** ICM is local-first. No queueing, no state isolation.
- **Automated mid-pipeline branching.** A human can branch between stages.
  Automating it drags ICM back toward being a framework.

Evidence caveat worth remembering: the paper reports no controlled
comparison against monolithic prompting, and all testing was on one model
family. The structure is well-argued, not measured.
