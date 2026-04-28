# Skill Registry

**Delegator use only.** Any agent that launches sub-agents reads this registry to resolve compact rules, then injects them directly into sub-agent prompts. Sub-agents do NOT read this registry or individual SKILL.md files.

See `_shared/skill-resolver.md` for the full resolution protocol.

## User Skills

| Trigger | Skill | Path |
|---------|-------|------|
| When creating a GitHub issue, reporting a bug, or requesting a feature. | issue-creation | /Users/milooo_003/.config/opencode/skills/issue-creation/SKILL.md |
| When creating a pull request, opening a PR, or preparing changes for review. | branch-pr | /Users/milooo_003/.config/opencode/skills/branch-pr/SKILL.md |
| When user asks to create a new skill, add agent instructions, or document patterns for AI. | skill-creator | /Users/milooo_003/.config/opencode/skills/skill-creator/SKILL.md |
| When writing Go tests, using teatest, or adding test coverage. | go-testing | /Users/milooo_003/.config/opencode/skills/go-testing/SKILL.md |
| When user says "judgment day", "judgment-day", "review adversarial", "dual review", "doble review", "juzgar", "que lo juzguen". | judgment-day | /Users/milooo_003/.config/opencode/skills/judgment-day/SKILL.md |
| Analyze Stitch projects and synthesize a semantic design system into DESIGN.md files | design-md | /Users/milooo_003/Desktop/Web Dev/Works/mpg-caps/.agents/skills/design-md/SKILL.md |
| Teaches agents to iteratively build websites using Stitch with an autonomous baton-passing loop pattern | stitch-loop | /Users/milooo_003/Desktop/Web Dev/Works/mpg-caps/.agents/skills/stitch-loop/SKILL.md |
| Unified entry point for Stitch design work. Handles prompt enhancement, design system synthesis, and high-fidelity screen generation/editing via Stitch MCP. | stitch-design | /Users/milooo_003/Desktop/Web Dev/Works/mpg-caps/.agents/skills/stitch-design/SKILL.md |
| Use when building or styling web UI, pages, components, artifacts, or applications. | frontend-design | /Users/milooo_003/Desktop/Web Dev/Works/mpg-caps/.agents/skills/frontend-design/SKILL.md |

## Compact Rules

Pre-digested rules per skill. Delegators copy matching blocks into sub-agent prompts as `## Project Standards (auto-resolved)`.

### issue-creation
- Always search existing issues before creating a new one.
- Never create blank issues; use the repo template only.
- Questions go to Discussions, not Issues.
- New issues start as `status:needs-review`; no PR before `status:approved`.
- Bug reports must include repro steps, expected vs actual behavior, OS, agent/client, and shell.
- Feature requests must state the problem, proposed solution, and affected area.

### branch-pr
- Every PR must link exactly one approved issue with `Closes/Fixes/Resolves #N`.
- Use branch names `type/description` matching `^(feat|fix|chore|docs|style|refactor|perf|test|build|ci|revert)/[a-z0-9._-]+$`.
- Use conventional commits only; never add `Co-Authored-By` trailers.
- PRs must have exactly one `type:*` label.
- Run `shellcheck` on modified shell scripts before opening the PR.
- PR body must include linked issue, summary bullets, changes table, and test plan.

### skill-creator
- Create a skill only for reusable, non-trivial patterns; avoid one-off documentation.
- Use `skills/{skill-name}/SKILL.md` with lowercase hyphenated names.
- Frontmatter must include `name`, `description` with trigger text, `license`, and metadata.
- Put strict rules in Critical Patterns; keep examples minimal and focused.
- Use `assets/` for templates/schemas and `references/` only for local docs.
- Register the new skill in `AGENTS.md` after creating it.

### go-testing
- Prefer table-driven tests for pure logic and multiple scenarios.
- Test Bubbletea state transitions by calling `Model.Update()` directly.
- Use `teatest.NewTestModel()` for full interactive TUI flows.
- Use golden files for visual output verification and `t.TempDir()` for filesystem work.
- Test success and error paths explicitly; mock side effects behind interfaces.
- Break complex logic into smaller testable units instead of overgrown integration tests.

### judgment-day
- Before launching judges, resolve project standards from Engram or `.atl/skill-registry.md`.
- Launch two blind judges in parallel with identical scope and standards.
- Classify findings as `CRITICAL`, `WARNING (real)`, `WARNING (theoretical)`, or `SUGGESTION`.
- Only confirmed issues from both judges are high-confidence fixes.
- Ask the user before fixing confirmed issues after round 1.
- Re-judge after critical fixes; do not loop forever on theoretical warnings or minor suggestions.

### design-md
- Use Stitch project and screen metadata plus downloaded HTML/CSS as the source of truth.
- Translate technical tokens into semantic design language, not raw implementation jargon.
- Name colors descriptively and always include exact hex codes with functional roles.
- Describe geometry, depth, and layout in human design terms.
- Generate `DESIGN.md` in the prescribed structure and keep terminology consistent.
- Explain the atmosphere and intent, not just the literal styles.

### stitch-loop
- Always read `.stitch/next-prompt.md`, `.stitch/SITE.md`, and `.stitch/DESIGN.md` before generating.
- The baton frontmatter `page` field determines the output filename.
- Persist Stitch identifiers in `.stitch/metadata.json` after creating or updating screens.
- Download generated HTML/PNG into `.stitch/designs/`, then integrate HTML into `site/public/`.
- Update navigation, sitemap, roadmap, and consumed ideas after each page integration.
- You MUST rewrite `.stitch/next-prompt.md` before finishing so the loop continues.

### stitch-design
- Always enhance the user prompt before calling any Stitch generation or edit tool.
- Reuse the existing `projectId` and incorporate `.stitch/DESIGN.md` when available.
- Replace vague UI wording with precise design-system and UX terminology.
- Structure prompts with vibe, required design system, and explicit page sections.
- Prefer targeted `edit_screens` refinements over full regeneration when possible.
- Always surface Stitch `outputComponents` insights back to the user.

### frontend-design
- Start by defining purpose, audience, constraints, and one bold aesthetic direction.
- Build real production-grade UI; do not stop at pretty mockup code.
- Avoid generic AI aesthetics, predictable layouts, and overused fonts like Inter/Arial/Roboto.
- Use strong typography, deliberate color systems, and motion that serves high-impact moments.
- Match implementation complexity to the chosen aesthetic; restraint matters as much as flourish.
- Make the interface memorable through intentional composition, texture, depth, and detail.

## Project Conventions

| File | Path | Notes |
|------|------|-------|
| — | — | No project-level convention files found at the repository root (`AGENTS.md`, `CLAUDE.md`, `.cursorrules`, `GEMINI.md`, `copilot-instructions.md`). |

Read the convention files listed above for project-specific patterns and rules. All referenced paths have been extracted — no need to read index files to discover more.
