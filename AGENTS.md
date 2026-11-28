# Notes for coding agents

This repository gathers the hdslave synths, drum machines and effects for MPC Sample, SP-16, macOS and Windows. The plug-in submodules follow their `main` branches. The hdslaveOS submodule follows its `hdslave` branch.

The README indexes them. Every project's own repository is the source of truth. This repository only records which commit of each one belongs together.

## Read the workspace guide first

On the author's machine, this repository sits in one folder beside the projects' own checkouts. That folder's `../AGENTS.md` and `../Workflow/release-and-card.md` hold the shared workflow and the hub's place in a release. Read them before you change anything here.

## How the hub is kept

- **Change a project in its own checkout**, not in the submodule folder here. Commit and push there, then move the pin here. Commits made inside these folders bypass the checkouts that other agents build from.
- **Move one pin** (the usual case: only the project just released):
  1. In the folder, `git fetch origin`, then `git checkout --detach origin/main` (`origin/hdslave` for hdslaveOS).
  2. `git add <Folder>`, then commit, for example "Pin Anvil 0.5.4 (a4b5c76)".
- **Move every pin.** `tools/update.sh` moves every folder to its branch's newest commit, commits, then runs `git submodule update --recursive`, so hdslaveOS's own submodules stay where hdslaveOS pins them.
  - Never run `git submodule update --remote --recursive`: it would move hdslaveOS's `base` to the wrong branch.
- **Add a project:**
  1. `git submodule add -b main <url> <Folder>`. Folder names have no spaces (`Cortex-Filter`).
  2. Set the commit identity inside the new submodule.
  3. Add a README entry in its section. Use labeled previews from published interfaces and link each preview to its full-size image. For an SP-16 release, include its wide panel and platform download.
  4. Update the collection and platform counts in the README.
- **Commits** are made as `hdslave <111106843+hdslave@users.noreply.github.com>`. Other agents push here too, so run `git pull --rebase` before you start. Never push without the owner's word.
- **Names in the README.** Trademarked names appear only as "in the style of" in the README, with the trademark notice kept current.
