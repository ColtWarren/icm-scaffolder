# Workspace Proposal — `research-findings`

**Status:** PROPOSED, NOT BUILT
**Proposed:** 2026-08-13
**Shape approved:** yes. **Build authorized:** no.
**Held pending:** Clief Notes course, stages material (Section 3).
**Proposed location:** `~/projects/research-findings/`

Approving a shape is not authorizing a build. This file exists so the proposal
survives the chat log it was made in.

Scope note: this document is about **one workspace**. It is not about ICM as a
method — that lives in `icm-findings.md`, and this file points at it rather
than repeating it.

---

## 1. The workflow being scaffolded

One run, already executed by hand: start from a name and a claim that can't be
evaluated, search broadly, separate verified from unverified by checking claims
against primary sources, then write up findings with evidence quality stated
plainly.

The two parts that made the output worth keeping were the verification step and
the explicit account of what could not be confirmed. A structured document
without those would have been confident and wrong.

---

## 2. Proposed tree

```
research-findings/
  CLAUDE.md                          # Layer 0
  CONTEXT.md                         # Layer 1: routing
  brief.md                           # the seed: name + claim to evaluate
  stages/
    01-survey/
      CONTEXT.md
      references/source-types.md
      output/                        # source inventory
    02-verify/
      CONTEXT.md
      references/verification-rules.md
      output/                        # claim ledger + fetched primaries
    03-findings/
      CONTEXT.md
      references/findings-format.md
      output/                        # the doc
  shared/
    claim-status.md                  # status vocabulary, canonical
  setup/
    questionnaire.md
```

---

## 3. Three stages, and why not more

The hand-run had four steps. Four steps are not four stages.

Step 1 is an input, not a stage. A name and a claim is a `brief.md` — a
human-provided seed, sitting at root. Because a seed is not a stage output, it
violates no handoff convention; it is simply where the pipeline starts.

Steps 3 and 4 each get a stage because each carried the value.

Step 2 gets its own stage because "have I found enough to start verifying" is a
real decision a human makes before anyone spends effort fetching primary
documents. That decision point is the boundary.

Nothing else earns a stage. Splitting outlining from drafting inside step 4
would be ceremonial — nobody reviews between them.

### Uneven rigidity

The stages are deliberately not uniform:

| Stage | Contract | Checkpoint | Audit |
|---|---|---|---|
| 01-survey | thin | no | no |
| 02-verify | tight | yes | yes, hard |
| 03-findings | thin | yes | light |

One run tells us the verification step worked. It does not tell us what
"searched broadly enough" means, or what the right findings structure is. Those
two stages stay loose so they break in use and tell us something.

Uniform structure applied to non-uniform confidence produces ceremony around
the one stage doing real work.

---

## 4. `02-verify` audit — pass conditions

Pass conditions, not process steps. Each is checkable without judgment:

1. Every claim carries exactly one status from `shared/claim-status.md`. No
   blanks, no compound statuses.
2. Every claim marked `verified-primary` names a URL, DOI, or commit hash that
   was fetched during this run. A summary of a source is not that source.
3. No claim's status exceeds what its named source can support. A secondary
   source cannot yield `verified-primary`, structurally.
4. Claim count in equals claim count out. Anything unresolved appears in the
   unverified list rather than disappearing.
5. The source's own stated limitations are recorded as claims in the ledger.

Condition 5 is a placement argument. "What this source admits it hasn't proven"
reads like a write-up task, but it is a reading of the primary document and
belongs where the document is still open. By stage 03 the source is closed and
that section becomes reconstruction.

### Checkpoint

`02-verify` pauses when a claim will not resolve against a primary source. The
human chooses: drop it, keep it as unverified, or go find another source.

---

## 5. `shared/claim-status.md` — canonical vocabulary

Four statuses, one home. Both `02-verify` and `03-findings` point at this file;
neither restates it. The moment the vocabulary lives in two places it drifts.

| Status | Meaning |
|---|---|
| `verified-primary` | Confirmed against the source document itself, fetched this run |
| `verified-secondary` | Supported only by a source describing another source |
| `unverified` | Could not be resolved; carried forward explicitly |
| `contradicted` | A primary source contradicts the claim |

---

## 6. Unresolved — where fetched primaries live

Fetched papers and repos are Layer 4 but durable across runs. Putting them in a
stage `output/` means the no-outputs-in-git rule forces a refetch every run; a
committed top-level `sources/` folder may be the better home.

This is the open sub-question already tracked as **Finding 1 in
`icm-findings.md`**. Not restated here — that file is its home. This proposal
assumes `02-verify/output/` as the interim placement and will follow whatever
Finding 1 resolves to.

---

## 7. Rejected — the backward-edge fix

**Proposed:** the "go find another source" checkpoint resolution creates an edge
from `02-verify` back to `01-survey`. Reading that as a circular dependency, the
fix was to let `02-verify` do its own searching so the edge stayed inside the
stage — at the cost of muddying the boundary between the two stages.

**Rejected.** The fix solves a problem that doesn't exist. The hard limit
forbids circular dependencies between stages, which is about stage contracts
pointing at each other. A person deciding "this needs more sources" and
re-running `01-survey` is not a contract — it is a human branching between
stages, which the conventions explicitly permit. What they forbid is automating
that branch, because automating it drags ICM back toward being a framework.

Keep the clean boundary. Keep the loop manual.

Recorded as Finding 5 in `icm-findings.md`.

---

## 8. Evidence backing this proposal

One hand-run, not a proven pattern. Deliberately thin. The expectation is that
using it reveals what is missing faster than designing it further would.
