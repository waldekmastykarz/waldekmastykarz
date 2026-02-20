# Project Curation Criteria

Rules for deciding which repos belong in the Projects section and which to skip.

## Include a repo when ALL of these are true

1. **Has a meaningful description** — The repo has a non-empty GitHub description that explains what it does
2. **Is a standalone tool or product** — Something people can install, use, or depend on. CLIs, libraries, apps, VS Code extensions, services
3. **Has original purpose** — Not a fork used only to submit PRs, not a config dump, not a one-off experiment

## Exclude a repo when ANY of these are true

1. **Demo or sample** — Conference demos, tutorials, sample apps built to illustrate a concept (names often contain `demo`, `sample`, `example`, `101`)
2. **Test or playground** — Repos for testing tools, CI, or reproducing bugs (`test-repo`, `playground`, `repro`)
3. **No description** — Empty description usually signals a scratch repo
4. **Config or dotfiles** — Personal configuration, themes, blog config
5. **Archived or inactive fork** — Forks with no meaningful original work
6. **Profile repo** — The `waldekmastykarz/waldekmastykarz` repo itself
7. **One-off scripts** — Small utility scripts not intended for reuse by others
8. **Internal tooling** — Stats dashboards, automation scripts for personal workflow (e.g., `devproxy-stats`, `latest-devproxy-version`)

## Edge cases

When a repo is borderline (e.g., it has a description but could be a demo), ask the user rather than guessing.
