# Minimal AI engineering baseline

Version 1.0.

A small set of instruction templates for projects worked on by AI coding agents such as Claude Code
and Codex. It aims to improve correctness and maintainability with minimal recurring overhead,
without replacing the review process a project already has. It is not an orchestration framework.

## Quick start

The kit is read by people, not loaded by agents. You copy the templates into your project, and your
agents then load those copies on their own: Codex reads `AGENTS.md`, and Claude Code reads
`CLAUDE.md`, which imports `AGENTS.md`, so both follow one file. The `.template` suffix keeps the
files in this folder from being loaded where they are.

1. Read this README, at least [Operating model](#operating-model) and [Adoption](#adoption). For a
   project that already has agent instructions, start with the read-only assessment there.
2. Copy [templates/AGENTS.md.template](templates/AGENTS.md.template) to `AGENTS.md` at your
   project root. Fill in or remove every `<placeholder>`, in the header and under "Project facts",
   and record any change you make to the engineering policy under "Local deviations".
3. If you use Claude Code, copy [templates/CLAUDE.md.template](templates/CLAUDE.md.template) to
   `CLAUDE.md` beside it.
4. If the project has financially or operationally consequential behavior, copy
   [templates/high-integrity.md.template](templates/high-integrity.md.template) into the project
   (for example as `docs/high-integrity.md`), fill it in, and name it under "Conditional
   references" in `AGENTS.md`.
5. Start a fresh session of each agent you use and check that it loaded the instructions.

## Contents

| File | Use |
| --- | --- |
| [templates/AGENTS.md.template](templates/AGENTS.md.template) | Shared project instructions, read by Codex and (through the bridge) Claude |
| [templates/CLAUDE.md.template](templates/CLAUDE.md.template) | Claude bridge that imports `AGENTS.md` |
| [templates/high-integrity.md.template](templates/high-integrity.md.template) | Domain guide for financially or operationally consequential behavior |
| [LICENSE](LICENSE) | CC0 1.0 Universal public domain dedication |

## Version and ownership

- Source templates are inert: the `.template` suffix keeps tools from loading them. Copy and adapt
  them deliberately; fill or remove every `<placeholder>` before committing an adoption.
- Each project maintains its own deployed project facts.
- Each adopted `AGENTS.md` records the baseline version and any deliberate local deviations.
- Updating a project compares three things: the old source, the new source, and the local
  adaptation.
- There is no automatic synchronization.
- Keep your own standard answers (review process, remote-write policy, local conventions) in a
  separate personal profile, not in these templates. Fill them in at adoption.

## Operating model

- One lead implementation agent by default.
- Use the project's existing tools and review process.
- Version 1 adds no custom agents, skills, or hooks.
- Routine work needs no extra planning document or declared tier.

## Verification levels

Choose the level by consequences, uncertainty, detectability, and recoverability. No level waives
a project's existing review or repository requirements.

| Level | When | Add |
| --- | --- | --- |
| Routine | Localized, understood, reversible, limited consequence | Relevant checks and meaningful regression evidence |
| Structural | Changed interfaces, persistence, ownership, integration, or substantial uncertainty | Brief acceptance criteria, compatibility considerations, affected integration checks |
| High integrity | Plausible financial loss, authoritative data corruption, security compromise, or consequential external action | Explicit invariants, independent expected outcomes, failure/replay evidence, release and recovery requirements |

## Delegation

- Delegate only bounded work with a concrete benefit.
- Give the delegate: objective, paths/interfaces, source revision, constraints, permissions,
  acceptance criteria, expected outputs, and stop conditions.
- State essential constraints explicitly; do not assume the delegate inherits them.
- Research delegates default to read-only capabilities.
- Only the lead authorizes further delegation.
- Parallel implementation needs separate worktrees, clear ownership, isolated mutable test
  resources, and integrated verification afterwards.
- Worktrees do not isolate credentials or external services.
- Agreement between agents is not evidence of correctness.

## Verification

- Use the repository's actual commands, with working directory and prerequisites.
- Distinguish behavioral, integration, regression, and architectural checks.
- Establish independent expected results for consequential calculations.
- Record what ran, its result, the relevant revision/environment, and what was omitted.
- Do not weaken tests or silently accept new snapshots to obtain a pass.
- Do not add blanket full-suite, coverage, type-checking, or tool requirements.

## Access controls

- Safe local work that is already authorized should proceed without repeated prompts.
- Consequential external actions require the applicable authorization.
- Keep production credentials and services out of development environments.
- Review hooks, skills, MCP servers, and setup scripts before trusting them.
- Command-deny rules and prompts are not complete isolation.
- Validate effective boundaries with harmless, disposable targets. Never test a denial by attempting
  a real trade, a live mutation, or a remote push.
- Mark each control as verified, failed, or unverified.
- Do not describe an agent's shell execution as sandboxed unless a supported, independently
  established isolation mechanism is in place. For example, Claude Code's sandbox runs on macOS,
  Linux, and WSL2 only; on native Windows it runs commands unsandboxed.
- Repository-specific policies remain authoritative. A local commit never authorizes publishing.

## Review integration

If the project already has a review process (a second agent, a review document format, CI review
rules), the baseline fits into it rather than replacing it.

- Preserve the review process's formats, states, ownership, and protected content.
- Put baseline content into the matching parts of the existing review format: requirements and
  acceptance criteria with the change description, invariants and boundaries with constraints,
  uncertainties and failure scenarios with what the reviewer should examine, executed checks and
  results with verification.
- In the narrative, distinguish defects, unverified risks, architecture concerns, and optional
  suggestions. Do not invent machine-readable fields.
- Do not edit files or blocks owned by the review tooling during ordinary adoption.

## Adoption

- **New project:** fill project facts, identify safe commands and basic checks, then adopt
  `AGENTS.md` and the Claude bridge.
- **Existing project:** start with a read-only assessment. Merge prospectively and preserve useful
  instructions and review-tooling material. Place additions outside protected blocks.
- **High-integrity project:** also instantiate the domain guide, identify independent reference
  cases, and verify operational boundaries.
- No broad cleanup or architecture rewrite.
- When adapting an existing `CLAUDE.md`, keep meaningful Claude-specific instructions and remove
  duplicated shared policy deliberately.
- Inspect ancestor instructions, overrides, imports, and tool settings.
- Check loading in fresh sessions of every agent you use. A loading check is not an enforcement
  check.
- Do not rely on globally configured fallback filenames or symlinks.
- Write anything every agent must follow into `AGENTS.md` itself. Claude expands `@path` imports;
  do not assume other agents do.
- Keep the `@AGENTS.md` import bridge as the compatible default. Whether Claude reads `AGENTS.md`
  natively depends on its version (2.1.277 or later), whether that support is enabled, and the
  effective **Project instructions** setting. Under the documented default, a `CLAUDE.md`,
  `.claude/CLAUDE.md`, or `CLAUDE.local.md` in the working directory or any ancestor directory
  prevents automatic `AGENTS.md` loading. Upgrading alone does not make the bridge unnecessary;
  remove it only after verifying in fresh sessions that `AGENTS.md` loads without it.

## Architecture continuity

- Reuse existing architecture documentation.
- Create a small architecture map only when navigation or boundaries need it. Capture
  responsibilities, flows, authoritative state, dependencies, and consequential decisions.
- Update affected facts in the same change.
- Keep unfinished task state where the existing review process keeps it.
- No generated repository inventories or mandatory ADRs.

## Trial before relying on it

The baseline has no demonstrated benefit until you measure one.

- Compare paired tasks with and without the baseline, from the same starting revisions, models,
  environments, requirements, and checks. Randomize the order and isolate session memories.
- Keep existing safety controls and review in both conditions.
- Define independent acceptance cases before development starts.
- Record correctness, regressions, confirmed review findings, human correction time, total time,
  cost, and unnecessary code in one small, manually maintained table.
- Treat results as directional; equal outcomes favor the simpler process.
- Remove components that cause friction without demonstrated benefit.

## Compatibility sources

Checked on 8 October 2026:

- [Claude Code instruction loading](https://code.claude.com/docs/en/memory): `CLAUDE.md` and
  `CLAUDE.local.md` load from the working directory and every ancestor; `@path` imports. Native
  `AGENTS.md` loading needs v2.1.277 or later, enabled support, and a permitting **Project
  instructions** setting. By default, a `CLAUDE.md`, `.claude/CLAUDE.md`, or `CLAUDE.local.md` in
  the working directory or an ancestor prevents it.
- [Claude Code sandboxing](https://code.claude.com/docs/en/sandboxing): macOS, Linux, and WSL2
  only; unsandboxed on native Windows
- [Claude Code permissions](https://code.claude.com/docs/en/permissions)
- [Codex AGENTS.md instructions](https://learn.chatgpt.com/docs/agent-configuration/agents-md):
  global, then project root to working directory, closer files take priority, byte limit
- [Codex Windows sandbox](https://learn.chatgpt.com/docs/windows/windows-sandbox)

## License

The kit is dedicated to the public domain under [CC0 1.0 Universal](LICENSE). You may copy, adapt,
and redistribute the README and templates, including into your own projects' instruction files,
without asking permission or giving attribution. CC0 waives copyright and related rights only: it
grants no trademark or patent rights and comes with no warranty.
