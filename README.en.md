# 🧑‍🏭 Artisan Dev Flow (artisan-dev-flow)

> Give your AI coding assistant a proven development workflow: evaluate reusable open-source solutions before you start, get design approval before you code, verify every step, and complete quality checks before release.

[中文版](README.md)

Artisan is a Skill for AI coding assistants (Codex, Claude Code, OpenCode, and others) — think of it as an executable development-process guide. Once installed, your AI follows a proven workflow instead of coding by impulse. It takes 10 seconds to install and weighs in at just over 300 lines, with zero configuration required for beginners.

## Why does this exist?

If you regularly ask AI to build features, you have probably hit one of these:

**1. Wasted effort.** The AI happily writes a pile of code, and later you discover GitHub already had a project doing almost exactly the same thing. Adapting existing code takes half the time of building from scratch.

**2. Wrong direction, discovered too late.** The AI starts coding without clarifying what you want, or dumps five questions on you at once. Halfway through, you realize the direction was wrong.

**3. Everything at once, nothing works.** The AI spreads across ten modules and looks impressively fast — until integration day, when the main flow does not work at all and every module is a castle in the air.

**4. "Build succeeded" is not "it works".** The AI says "all tests pass", but the tests are superficial, and the moment you actually run the program it crashes.

**5. Release incidents.** Secrets written into code, temp files committed, debug settings left on — discovered only after shipping.

**6. The same bug, forever.** The AI keeps guessing at the same issue, fixing one break and causing another, never stopping to find the root cause.

Artisan exists to solve exactly these problems. It turns the habits of a reliable engineer into a workflow the AI can follow.

## Core philosophy

Today's large language models are powerful enough to build an entire codebase on their own — and powerful enough to "conveniently" reinvent the wheel. They are confident enough to write secrets straight into code and push `.env` files all the way to GitHub.

What they lack is not capability, but checkpoints at critical moments: has an open-source solution been evaluated before starting? Has the design spec passed review before coding? Has a minimal working slice been proven before full-scale development? Is the acceptance evidence sufficient before declaring completion? Have sensitive data and temporary artifacts been cleaned before release?

Artisan is that gatekeeper. It does not teach the AI how to write code — that needs no teaching. It simply makes the AI pause for a second at the points where things most often go wrong: reuse first, approve first, verify first, check first.

| Critical moment | Gatekeeping question | Corresponding gate |
| --- | --- | --- |
| Before starting | Has an open-source solution been evaluated? | Reuse decision |
| Before coding | Has the design spec passed review? | Design approval |
| Before full-scale work | Has a minimal working slice been proven? | Vertical slice |
| Before claiming done | Is the acceptance evidence sufficient? | Acceptance evidence |
| Before release | Are sensitive data and temp artifacts cleaned? | Release check |

## What it is

There are already heavyweight AI development methodologies (Superpowers, Spec Kit, Trellis, etc.). Artisan differs:

- **It is an orchestrator**, not a new set of wheels. It owns the sequence, the decision gates, and the quality bar; the actual work is delegated to capabilities you already have.
- **It is tiny**: just 4 files and 300+ lines. Copy it in, no dependencies, no changes to your toolchain, 10-second install.
- **It is beginner-friendly**: zero configuration, no framework knowledge required. It explains each step in plain language, and you only answer one or two questions it asks.
- **It is tool-agnostic**: with or without Trellis, with or without CodeGraph — it works either way, degrading to a simplified flow when a capability is missing.

The name: a craftsman's way of working — evaluate materials first (reusable open-source options), measure before cutting (analyze the current state), proceed only after design review (design approval), verify as you go (layered verification), and complete checks before delivery (release check).

## How it works

### Step one: classify the task

Not every task needs the full workflow. Artisan uses three tracks:

| Track | Tasks | Handling |
| --- | --- | --- |
| 🐇 Fast path | Typo fixes, small local edits | Do it directly, no ceremony |
| 🏗️ Standard path | New projects, features, cross-module changes | Full workflow |
| 🚨 High-risk path | Money, accounts, privacy, external writes, deployments, industrial equipment | Full workflow + extra safeguards (dry run, rollback, small canary first) |

### Step two: the eight-step workflow

1. **Open-source evaluation** (GitHub reuse gate) — search the ecosystem first and assess whether a mature implementation can be adopted or extended, instead of starting from zero. When a closely matching project exists, recommend adopting it directly.
2. **Current-state analysis** (code archaeology) — analyze the structure, data flow, and existing engineering conventions. Suggest a code index (CodeGraph) when useful, only with your consent.
3. **Design review** (design approval) — define goals, non-goals, acceptance criteria, and module boundaries in a design spec. **No coding until the design passes review.**
4. **Verification plan** — before coding, define how "works" will be proven: layers and evidence requirements for static checks, automated tests, and real-run verification.
5. **Minimal vertical slice** — first build one minimal end-to-end path through the real system (e.g., launch → user action → persistence → result display). **No full-scale rollout until the slice passes.**
6. **Controlled parallelism** — complete core contracts and integration paths serially by default; parallelize only independent tasks, usually at most 2–3 workstreams, integrating after each batch.
7. **Acceptance and debugging** — verify the main flow first, then boundaries and failure paths; acceptance requires evidence (command output, logs, screenshots). Two consecutive failed fixes on the same path means stop guessing and dig into root cause.
8. **Release and learning** — check for sensitive data and temp artifacts, document what is verified vs. unverified and the rollback path; only capture lessons worth reusing.

### Five gates

1. No reuse decision → no custom building.
2. No design approval → no code.
3. No proven vertical slice → no expanded parallelism.
4. No acceptance evidence → no "done".
5. No security and release check → no shipping.

### Lines it holds

- Secrets are read from environment variables only, never written into code, logs, or chat.
- If the user says "read-only, don't touch files", not a single file is created.
- Without explicit user consent, nothing is committed, pushed, or released.

## What problems does it solve?

| Pain point | How Artisan addresses it | Mechanism |
| --- | --- | --- |
| Wasted effort | Mandatory GitHub search before building; recommend adopting existing projects | Step 1 + Gate 1 |
| Wrong direction found late | Design review before coding; one key question at a time | Step 3 + Gate 2 |
| Everything at once, nothing works | Prove a minimal vertical slice before controlled parallelism | Steps 5–6 + Gate 3 |
| Fake tests, fake completion | Demand real-run evidence; distinguish mocks from real verification | Steps 4, 7 + Gate 4 |
| Release incidents | Pre-release checks for secrets, temp files, debug configs | Step 8 + Gate 5 |
| The same bug forever | Two failed fixes → root-cause analysis, no guessing | Step 7 |
| Overconfident AI | Completion report must separate "verified / partially verified / unverified" | Step 8 |

## Real case: what it prevented

**A user wanted an RSS reader and wrote zero lines of code.**
The request: "A Windows-local RSS reader: multi-source subscription, keyword filtering, scheduled refresh, one-click install." Instead of coding immediately, Artisan searched GitHub first — RSS Guard covered all four requirements natively, was actively maintained, and shipped official Windows installers. Recommendation: adopt it directly. Result: zero code, requirement met the same day. That is "reuse first" in action.

More input → output examples in [examples/](examples/).

## Quick start

**Install (Codex)**: copy the `artisan-dev-flow` folder into `~/.codex/skills/` and restart Codex; it is discovered automatically.

**Install (Claude Code / OpenCode)**: copy `SKILL.md` and `references/` into the corresponding skills directory (`agents/openai.yaml` is Codex UI metadata only and can be ignored elsewhere).

**Usage**: say "按我的开发流程推进 XXX" or simply describe a new project, feature, or high-risk fix — Artisan triggers automatically.

**Optional dependencies**: brainstorming, verification-planning, Trellis, CodeGraph, etc. The best experience comes with them installed; without them, Artisan degrades gracefully to a simplified flow.

## Who is it for?

- Developers who use AI for coding but want it to be more reliable.
- Solo maintainers juggling several projects who do not want to reinvent wheels.
- Anyone whose projects touch real devices, real accounts, or real data and cannot afford "good enough".
- Beginners who want to build good habits from day one.

## Relationship to existing methodologies

Artisan does not replace Superpowers, Spec Kit, or Trellis — it sits above them, deciding when to use which capability and when to stop and ask. It plays the role of workflow orchestration and quality gating, not a specific implementation tool.

## License

MIT License. See [LICENSE](LICENSE).
