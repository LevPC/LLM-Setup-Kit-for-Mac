# LLM Setup Kit for Mac

## Project
Full Mac migration and disaster recovery kit for LLM development environments on Apple Silicon.

## Repository
- **GitHub**: `parsamivehchi/llm-setup-kit-for-mac` (private)
- **Local**: `~/Desktop/DEV/mac-setup/`
- **GitHub Pages**: https://parsamivehchi.github.io/llm-setup-kit-for-mac/
- **Pages source**: `docs/` folder on `main` branch

## Key Scripts
| Script | Purpose | Flags |
|--------|---------|-------|
| `setup.sh` | 17-phase bootstrap | `--dry-run`, `--skip-restore` |
| `audit.sh` | Pre-migration readiness scan | — |
| `backup.sh` | Export configs/data/secrets | `--skip-secrets`, `--skip-projects` |
| `restore.sh` | Restore from backup | `<backup_dir>` argument |
| `tests/verify.sh` | Post-setup automated checks | — |

## Architecture
- All scripts use `set -euo pipefail` with colored output helpers (`ok`, `warn`, `fail`, `skip`)
- Backup creates timestamped dirs under `backups/` (gitignored)
- Secrets encrypted with `openssl enc -aes-256-cbc -salt -pbkdf2`
- Manifest uses SHA-256 checksums via Python's `hashlib`
- Restore helper scripts in `scripts/restore_{claude,editors,raycast}.sh`
- Config snapshots committed to `config/{claude,vscode,cursor}/`

## Conventions
- Bash scripts — no Python except for JSON/manifest generation
- Idempotent — every phase checks state before acting
- `SCRIPT_DIR` pattern for portable path resolution
- Color codes: green=success, yellow=skip/warn, red=fail, cyan=headers, purple=dry-run
- Brewfile comments use `# description` after the package name

## Security Rules
- NEVER commit `backups/` directory (contains secrets)
- `config/claude/installed_plugins.json` has paths sanitized to `/Users/$USER/`
- No API keys, passwords, or personal identifiers in committed files
- `.gitignore` covers: `backups/`, `audit_report_*.txt`, `*.enc`, `.DS_Store`

## GitHub Pages Site
- Single self-contained `docs/index.html` (1245 lines)
- Design matches prsa.me: cyberpunk/terminal aesthetic, Roboto Mono, neon glows
- CSS variables match prsa.me exactly (--neon-pink, --neon-blue, --neon-green, --neon-yellow)
- Only external dependency: Google Fonts (Roboto Mono)
- Responsive: sidebar on desktop, stacked on mobile

## Working With This Repo
- `gh auth status` — verify GitHub CLI auth before push
- Interactive prompts in `backup.sh` (openssl passphrase) won't work in Claude Code Bash tool — must run directly in terminal
- `brew leaves` only shows direct installs, not deps — audit comparison may show false "not installed" for dependency packages
- Git committer is auto-configured from hostname — user should set `git config --global user.name/email`
