---
name: update-projects
description: This skill should be used when the user asks to "update projects", "refresh the project list", "sync projects with GitHub", "add new repos to the README", "sort projects by activity", or mentions updating the Projects section of the profile README.
---

# Update Projects List

Synchronize the Projects section in README.md with public GitHub repos. Fetch repos, identify missing projects worth listing, assign emojis, and sort by recent activity.

## Workflow

STOP — Read `references/curation-criteria.md` before proceeding. It defines which repos qualify as projects and which to skip.

### Step 1: Read the current README

Read README.md and extract the current list of projects from the `### Projects` section. Note each project name and its GitHub URL.

### Step 2: Fetch public repos

Run:

```sh
GH_PAGER=cat gh repo list waldekmastykarz --source --no-archived --limit 100 \
  --json name,description,pushedAt,url \
  --jq 'sort_by(.pushedAt) | reverse | .[] | [.pushedAt, .name, .description // "", .url] | @tsv'
```

For org repos already in the list (e.g. `dotnet/dev-proxy`, `pnp/cli-microsoft365`), fetch their `pushedAt` separately:

```sh
GH_PAGER=cat gh repo view <owner/repo> --json pushedAt --jq '.pushedAt'
```

### Step 3: Identify missing projects

Compare the fetched repos against the current project list. Apply the curation criteria from `references/curation-criteria.md` to decide which missing repos to add. When unsure whether a repo qualifies, ask.

### Step 4: Update the project list

For each new project:

1. Pick a single emoji that represents the project's domain or function (see Emoji Guidelines below)
2. Use the repo description as the project description — clean up trailing periods and adjust phrasing for consistency with existing entries

Combine new and existing projects, then sort the entire list by `pushedAt` date (most recent first).

### Step 5: Write back to README

Replace the `### Projects` section in README.md with the updated, sorted list. Preserve the format:

```markdown
- <emoji> [Project Name](https://github.com/owner/repo) — Short description
```

### Step 6: Summarize changes

Report:
- Which projects were added (if any)
- Which projects changed position due to re-sorting
- Total project count

## Emoji Guidelines

Choose one emoji per project that reflects its primary function:

| Domain | Emoji examples |
|---|---|
| Security/protection | 🛡️ |
| CLI tools | ⚙️, 🏃, 🌍 |
| AI/agents | 🤖 |
| Download/package | 📦 |
| VS Code extensions | 🪟 |
| Privacy | 🙈 |
| Monitoring/status | 📡 |
| Auth/tokens | 🔑 |
| Testing/mocks | 🧪 |
| Comparison/eval | ⚖️, 🦙 |
| Counting/metrics | 🔢 |
| Validation | ✅ |
| Templates | 📐 |
| Search | 🔍 |
| Notebooks | ⚖️ |

Avoid reusing the same emoji for different projects. If no obvious match exists, pick something visually distinctive and thematically close.

## Additional Resources

### Reference Files

- **`references/curation-criteria.md`** — Rules for deciding which repos belong in the project list and which to skip
