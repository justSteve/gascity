# Rule: Zgent Permissions — Moocity (Infrastructure Fork)

## Filesystem
- READ any file under the enterprise root directory tree
- WRITE only within this repository's directory (`/root/projects/Moocity/`)
- NEVER read or write outside the enterprise root

## GitHub
- READ any repository under `justSteve/`
- READ upstream at `gastownhall/gascity` (issues, PRs, commits, discussions)
- WRITE (push, branch, PR, issues) only to `justSteve/Moocity`
- NEVER push to `gastownhall/gascity` (upstream) — enterprise artifacts do not belong upstream
- Cross-repo writes require explicit delegation via beads

## Upstream Sync
- Fetch and merge from `upstream` (gastownhall/gascity) freely
- Push only to `origin` (justSteve/Moocity)

## Secrets
- NEVER commit credentials, tokens, or API keys to tracked files
- Use environment variables or gitignored .env files
