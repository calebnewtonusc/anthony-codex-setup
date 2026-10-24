# anthony-codex-setup

A Codex CLI setup for a Linux laptop, so Codex writes code and copy that pass the
same checks as the rest of the team: no em dashes, no AI-sounding prose, no
narration comments, typecheck green before every commit. It merges into whatever
`~/.codex` you already have and never overwrites your files. No sudo.

## Install

```bash
mkdir -p ~/code/anthony-codex-setup && curl -fsSL https://codeload.github.com/calebnewtonusc/anthony-codex-setup/tar.gz/HEAD | tar xz -C ~/code/anthony-codex-setup --strip-components 1 && cd ~/code/anthony-codex-setup && ./install.sh
```

Or paste [SETUP-FOR-CODEX.md](SETUP-FOR-CODEX.md) into Codex and it does every step.
`./install.sh --dry-run` previews. Running it twice adds nothing the second time.

## What you get

- **Skills** in `~/.agents/skills`, which Codex picks up on its own: debugging,
  reviewing-changes, shipping, interface (UI that doesn't look generated),
  deep-research, repo-health, hackathon (the day's rules and a build plan),
  stack-rules, grilling, openspec, reflect, skill-forge, graph-engineering,
  clone-site. Writing editors: no-ai-slop, avoid-ai-writing, humanizer, and deslop
  for code. Plus pdf, docx, xlsx, webapp-testing, mcp-builder and skill-creator
  from Anthropic's skills repo.
- **Checks** in `~/.local/bin`, runnable from any shell:
  - `agent-check`: `tsc --noEmit` plus the slop checks on staged files. Exit 1 on failure.
  - `slop-check <file.md> --issues`: structural AI tells in prose, 0 to 100.
  - `ai-scan <file-or-dir>`: vocabulary tells (needs the avoid-ai-writing skill, installed here).
  - `code-slop --issues`: AI-authorship tells in the working-tree diff.
  - `agent-hook-init`: adds a pre-commit hook running `agent-check` to the current repo.
- **AGENTS.md**: the team's working rules, written as one marked block in
  `~/.codex/AGENTS.md`. Your own text above and below it stays.
- **A Codex hook**: after every `apply_patch`, the edited files are scored and the
  findings go back to Codex so it fixes them on the next step. Codex asks you to
  trust a new hook before it runs, so approve it on first launch.
- **MCP servers**, each registered with an absolute command: context7 (current
  library docs), sequential-thinking, playwright and chrome-devtools (headless
  browser), fetch, git, and github (reads the token from `gh` at startup, so no
  token is ever written to a file).
- **Tools**, from official releases into `~/.local/bin`: node 22, codex, gh, jq,
  ripgrep, uv. Anything you already have is left alone.

## Flags

`--no-prereqs`, `--no-skills`, `--no-mcp`, `--no-config`, `--dry-run`.
`tests/smoke.sh` runs the installer in an empty home folder, twice, and checks the
second run adds nothing.

## What it never touches

- A skill, MCP server or command whose name you already have.
- Your AGENTS.md text, hooks or config values. Each gets backed up to
  `~/.local/share/anthony-codex-setup/backups/<timestamp>/` first.
- Any repo's git hooks. `agent-hook-init` adds one only when you run it, and only
  when the repo has none.

## Uninstall

- Delete `~/.local/share/anthony-codex-setup` and the links pointing into it from
  `~/.agents/skills` and `~/.local/bin`.
- Delete the block between the `anthony-codex-setup` markers in `~/.codex/AGENTS.md`
  and the `slop-after-edit.py` entry in `~/.codex/hooks.json`.

## Sources

- [petergyang/no-ai-slop](https://github.com/petergyang/no-ai-slop), [conorbronsdon/avoid-ai-writing](https://github.com/conorbronsdon/avoid-ai-writing), [blader/humanizer](https://github.com/blader/humanizer)
- [31Carlton7/skills](https://github.com/31Carlton7/skills): deslop, whose rules `code-slop` runs deterministically
- [anthropics/skills](https://github.com/anthropics/skills): document and dev skills
- The `skills/` folder and `bin/` checks here: ported from Caleb Newton's own kit

All glory to God!
