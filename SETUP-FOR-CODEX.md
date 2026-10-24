# Prompt: set up Codex on my laptop from this repo

Paste everything below the line into Codex.

---

Set up my Codex CLI from https://github.com/calebnewtonusc/anthony-codex-setup.
I'm on Linux. Do every step yourself and only stop for things that need my hands
(a browser sign-in, my sudo password).

1. Download it: `mkdir -p ~/code/anthony-codex-setup && curl -fsSL https://codeload.github.com/calebnewtonusc/anthony-codex-setup/tar.gz/HEAD | tar xz -C ~/code/anthony-codex-setup --strip-components 1`
2. Read `README.md` and `install.sh` in full so you know what each step does.
3. Run `./install.sh --dry-run` from that folder and tell me in a few lines what it adds.
4. Run `./install.sh`. If it says git, python3 or curl is missing, tell me the
   exact `sudo apt install` line and wait for me.
5. Run `./install.sh` again and confirm it reports nothing new.
6. Check, with a pass or fail line each: `ls -L ~/.agents/skills` resolves every
   skill, `codex mcp list` shows the servers in README.md, `agent-check --help`,
   `slop-check --help` and `code-slop --help` run, `~/.codex/hooks.json` is valid
   JSON, and `~/.codex/AGENTS.md` has the anthony-codex-setup block.
7. Run `bash tests/smoke.sh` and show me its last line.
8. If `gh auth status` fails, run `gh auth login --web` and wait for me to finish in
   the browser.
9. In the hackathon repo (`~/code/anchored` or wherever I cloned it), run
   `git config core.hooksPath .githooks` and then `agent-check --no-tsc` once to
   prove the checks run.
10. Finish with two short lists: logins I still need, with the exact step for
    each, and anything that failed, with the error.

Tell me to restart Codex at the end so it loads the skills, AGENTS.md and the hook,
and to trust the new hook when Codex asks. Never put a token or password in a file.
