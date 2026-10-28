# anthony-codex-setup

A Codex CLI setup for a Linux laptop, so Codex writes code and copy that pass the
same checks as the rest of the team: no em dashes, no AI-sounding prose, no
narration comments, typecheck green before every commit. It merges into whatever
`~/.codex` you already have and never overwrites your files. No sudo.

## Start here: where you type

This is for the Codex CLI in a terminal on your Linux laptop (Ctrl+Alt+T opens one
on Ubuntu). Not chatgpt.com, and not Codex cloud at chatgpt.com/codex: both run on
OpenAI's servers, can't see your laptop's files or `~/.codex`, and will send you to
connect GitHub instead. You don't need that.

Paste this into the terminal. It downloads this repo and runs the whole setup,
including installing Codex itself, so you don't need Codex first:

```bash
mkdir -p ~/code/anthony-codex-setup && curl -fsSL https://codeload.github.com/calebnewtonusc/anthony-codex-setup/tar.gz/HEAD | tar xz -C ~/code/anthony-codex-setup --strip-components 1 && cd ~/code/anthony-codex-setup && ./install.sh
```

It stops for you in two places, and each one opens a browser window that can land
behind the terminal. If nothing seems to happen, Alt-Tab to the browser.

- **GitHub sign-in.** It shows a code like `ABCD-1234`. Copy it, press Enter, sign
  in to github.com in the browser if it asks, paste the code, click Authorize.
  With no desktop browser, open https://github.com/login/device on your phone.
  Once you're signed in, it accepts any pending GitHub invites from Caleb for you.
- **Codex sign-in**, the first time you run `codex`. Pick Sign in with ChatGPT and
  finish in the browser tab it opens.

Then run `codex` in the terminal, and when it asks whether to trust the new
anthony-codex-setup hook, say yes. If the setup stopped partway or printed anything
under "Problems", paste [SETUP-FOR-CODEX.md](SETUP-FOR-CODEX.md) into `codex` and it
finishes the job, then writes a PDF of every snag to `~/Downloads` for you to send
to Caleb.

## Install

The line under "Start here" is the whole install. `./install.sh --dry-run`
previews. Running it twice adds nothing the second time.

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
