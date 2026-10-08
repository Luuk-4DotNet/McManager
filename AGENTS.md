# Agent Instructions

Canonical, tool-agnostic instructions for any AI coding agent (GitHub Copilot, Claude Code, Gemini CLI, Mistral Vibe, ...). `CLAUDE.md`, `GEMINI.md` and `.github/copilot-instructions.md` point here; edit this file only.

McManager is a "Windows Task Manager for macOS" app, built with .NET. The solution lives in `McManager/McManager.slnx`.

Update this file with build, test (including single-test invocation) and lint commands, and the high-level architecture, once they are settled.

## Project Conventions

- Use .NET MAUI.
- Use functional programming as much as possible, with expression-bodied members.
- Every project has a corresponding test project.
- Separate the layers of the app (e.g. UI, Core, Persistence).

### Testing

- Every class has a unit test class named `<ClassName>Tests`.
- Tests are named `<MethodToTest>_When<TestCase>_Expect<ExpectedResult>` and contain Arrange, Act and Assert sections.

### Indentation

- 1 tab is fine, 2 tabs is okay, 3 tabs is not done.
- Prevent deep nesting with inverted ifs / guard clauses and method extraction.

## Version Control

- Collaborate using GitHub Flow: work on branches and merge through pull requests.
- Create atomic commits (one logical change each).
- Features: branch `feature/<YYYYMMDD>-<FeatureInPascalCase>` (e.g. `feature/20261008-ProcessList`).
- Bugs: branch `fix/<YYYYMMDD>-<BugInPascalCase>` (e.g. `fix/20261008-CrashOnStartup`).

## Agent Assets Layout

Single source of truth is `.agents/`; tool-specific folders are symlinks to it.

- `.agents/skills/<name>/SKILL.md`: skills (open Agent Skills format: `name` + `description` frontmatter).
- `.agents/agents/<name>.agent.md`: sub-agents / personas. Frontmatter is limited to the portable `name` (lowercase, hyphens) and `description`. Do not add tool-specific keys (`tools`, `model`, `handoffs`, ...); tool names and model IDs differ per vendor.
- Symlinks: `.github/{skills,agents}`, `.claude/{skills,agents}`, `.gemini/{skills,agents}`, `.vibe/skills` → `../.agents/...`.
- Write instructions in vendor-neutral terms ("search the codebase", "edit files"), never vendor tool names or product names.
- Mistral Vibe defines agents in its own TOML format and cannot load `.agent.md` files; it reads `AGENTS.md` and the skills.
