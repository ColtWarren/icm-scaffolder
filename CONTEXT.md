# Current Project

## What we are building

A workspace that scaffolds other ICM workspaces. Given a described workflow,
it produces the folder tree, the CONTEXT.md files, and the reference docs
that make that workflow runnable by an agent.

Secondary use: authoring standalone markdown that follows ICM conventions
(specs, protocols, reference docs) when no full workspace is needed.

## What good looks like

- **The structure is obvious without explanation.** Someone opening the
  folder cold can tell what each stage does and in what order.
- **Every file has one job.** A file that holds both rules and working
  material gets split.
- **Inputs are named, not implied.** Each stage contract says which files
  and which sections to load. "Read the previous stage" is not an input.
- **Line caps hold.** CONTEXT.md under 80 lines, reference files under 200.
  Hitting the cap is a signal to split, not to shrink the font.
- **Placeholders are gone.** A scaffold ships filled in. Bracketed
  placeholders left in a file mean the scaffold is not finished.
- **Nothing is duplicated.** One home per fact; other files point at it.

## What to avoid

- **Stage inflation.** Four real stages beat eight ceremonial ones. If two
  stages always run together and nobody reviews between them, they are one
  stage.
- **Pipelining a loop.** ICM handles sequential, reviewable, repeatable
  work. Debugging and training adaptation are loops. If the workflow is a
  loop, say so instead of forcing stages onto it.
- **Reference bloat.** Reference material is constraints the model should
  internalize. If it is background reading, it does not belong in Layer 3.
- **Learning from outputs.** Scaffolds derive from the conventions, never
  from earlier scaffolds this workspace produced. Early outputs are the
  worst outputs.
- **Inventing conventions.** The 15 patterns come from ICM. If a situation
  is not covered, flag it as uncovered rather than filling the gap silently.

## Open questions

These are unresolved and should be treated as unresolved, not guessed at:

1. Does the sequential-pipeline shape fit software engineering work, or
   only the front half of it (research, spec, scaffold) with debugging
   sitting outside?
2. Do the 80/200 line caps hold for engineering reference material, or are
   they tuned to content production?
3. Where does a real codebase sit? It is Layer 4 by function but far too
   large to load. ICM does not answer this.

## Known overlap

The ICM repo ships a `workspace-builder` that does much of this. This
workspace is deliberately hand-built so the conventions get learned rather
than generated. Once the builder has been run and understood, revisit
whether this workspace still earns its place.
