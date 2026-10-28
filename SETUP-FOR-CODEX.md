# Prompt: set up Codex on my laptop from this repo

Paste everything below the line into the Codex CLI (`codex` in a terminal on your
laptop, not chatgpt.com or Codex cloud, which can't see your files). If `codex`
isn't installed yet, run the one line in the README's "Start here" first; it
installs Codex.

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
8. If `gh auth status` fails, tell me a browser window is about to open and may
   land behind the terminal, run `gh auth login --web -h github.com -p https`,
   show me the code, and wait for me to finish in the browser. Then accept any
   pending invites from calebnewtonusc yourself with
   `gh api user/repository_invitations` and `gh api -X PATCH user/repository_invitations/<id>`.
   Never send me to a browser for something `gh` can do.
9. If `~/code/anchored` doesn't exist, run `gh repo clone calebnewtonusc/anchored ~/code/anchored`.
   In it, run `git config core.hooksPath .githooks` and then `agent-check --no-tsc`
   once to prove the checks run.
10. Finish with two short lists: logins I still need, with the exact step for
    each, and anything that failed, with the error.
11. Write a PDF to `~/Downloads/anthony-codex-setup snags.pdf` listing every snag
    we hit, in order: what I saw, what caused it, what fixed it. I'll send it to Caleb.

Tell me to restart Codex at the end so it loads the skills, AGENTS.md and the hook,
and to trust the new hook when Codex asks. Never put a token or password in a file.
