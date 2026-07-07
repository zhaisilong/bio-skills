# Bio Skills

Portable Codex skills for recurring repository and bioinformatics workflows.

## Quick Start

Clone the public skills repository and inspect available skills:

```bash
git clone https://github.com/zhaisilong/bio-skills.git
cd bio-skills
find .codex/skills -maxdepth 2 -name SKILL.md -print
```

## Layout

- `.codex/skills/<skill-name>/SKILL.md` contains the Codex skill entrypoint.
- Keep each skill self-contained and avoid machine-specific absolute paths.
- Add `scripts/`, `references/`, or `assets/` inside a skill only when the
  resource is required by that skill.

## Install One Skill Into A Project

Copy a skill directory into the target repository's Codex skills directory:

```bash
mkdir -p <target-repo>/.codex/skills
cp -R .codex/skills/change-steward <target-repo>/.codex/skills/
```

## Install All Skills Into A Project

Copy every skill in this repository into a target project:

```bash
mkdir -p <target-repo>/.codex/skills
cp -R .codex/skills/* <target-repo>/.codex/skills/
```

## Install As Personal Codex Skills

Copy a skill into the personal Codex skills directory:

```bash
mkdir -p "${CODEX_HOME:-$HOME/.codex}/skills"
cp -R .codex/skills/change-steward "${CODEX_HOME:-$HOME/.codex}/skills/"
```

After installation, start Codex in the target repository and reference the skill
by name, for example `$change-steward`.

## Claude Code

These skills use `SKILL.md`-centered directories. When needed, adapt the same
skill directories under `.claude/skills/` and review any platform-specific
instructions before relying on them in Claude Code.
