# Progress

## Completed (2026-02-27)

### Step 1: Create audit.sh
- [x] 12-section pre-migration audit
- [x] System info, brew formulae/casks, App Store, unmanaged apps
- [x] Claude Code, editors, Raycast, project data, secrets, git repos
- [x] Summary with coverage counts
- [x] Output: colorized terminal + `audit_report_<timestamp>.txt`
- [x] Fixed: git `@{u}..HEAD` crash on repos without upstream
- [x] Fixed: Brewfile sed parsing for inline comments
- [x] Fixed: Simplified section 5 (unmanaged apps) — removed slow `brew info --cask` lookups
- [x] Ran successfully on current Mac

### Step 2: Expand Brewfile
- [x] Added 18 formulae (mas, deno, ffmpeg, lazygit, ncdu, pandoc, etc.)
- [x] Added 28 casks (spotify, vlc, stats, helium-browser, brave-browser, etc.)
- [x] Added 39 Mac App Store apps with exact IDs from `mas list`
- [x] Total: 37 formulae + 39 casks + 39 mas = 115 packages

### Step 3: Create backup.sh
- [x] Claude Code: settings, plugins metadata, 12 memory directories
- [x] VS Code: 86 extensions list, settings, snippets
- [x] Cursor: 86 extensions list, settings, keybindings, snippets
- [x] Raycast: plist preferences
- [x] Project data: LLM-BENCH tarball (5MB), git repo inventory
- [x] Secrets: AES-256 encrypted .env + SSH keys (interactive prompts)
- [x] System snapshot: brew dump, mas list, app inventory, dock/finder plists
- [x] Manifest: SHA-256 checksums for all files
- [x] Copies stable configs to `config/` for git commit
- [x] Ran successfully (5.2MB backup, 27 files)

### Step 4: Create restore.sh + helper scripts
- [x] `restore.sh` — orchestrator with manifest verification
- [x] `scripts/restore_claude.sh` — settings, plugins, memory files
- [x] `scripts/restore_editors.sh` — VS Code + Cursor extensions + settings
- [x] `scripts/restore_raycast.sh` — plist + config
- [x] All check existing files before overwriting

### Step 5: Update setup.sh
- [x] Extended from 11 → 17 phases
- [x] Added `--dry-run` flag (purple output, no changes)
- [x] Added `--skip-restore` flag
- [x] New phases: 4 (MAS verification), 12-16 (restore + manual checklist)
- [x] Verification phase expanded with additional tools

### Step 6: Create .gitignore
- [x] Excludes `backups/`, `audit_report_*.txt`, `.DS_Store`, `*.enc`

### Step 7: Create tests/verify.sh + tests/checklist.md
- [x] verify.sh: 30+ CLI tools, 10+ GUI apps, config symlinks, Claude, SSH, Ollama, editors
- [x] checklist.md: manual verification items for terminal, Ollama, editors, Claude, Raycast, Git, macOS prefs, secrets

### Step 8: Security & Publishing
- [x] Sanitized `installed_plugins.json` (username → `$USER`)
- [x] Scanned all committed files for personal info
- [x] Initialized git repo, created initial commit (27 files, 3141 insertions)
- [x] Created private GitHub repo
- [x] Renamed repo: mac-setup → dotstrap → llm-setup-kit-for-mac

### Step 9: GitHub Pages Site
- [x] Created `docs/index.html` — cyberpunk design matching prsa.me
- [x] Sections: hero, overview, tool cards, workflow, features, tech stack, CTA
- [x] Typing animation, scroll reveals, neon hover effects, scanline overlay
- [x] Responsive sidebar layout
- [x] Enabled GitHub Pages from `docs/` folder
- [x] Live at: https://parsamivehchi.github.io/llm-setup-kit-for-mac/

## Not Yet Done / Future Work

- [ ] Run `./backup.sh` with secrets (needs interactive terminal for passphrase)
- [ ] Update README.md to match new scope (currently still the original basic version)
- [ ] Add the 3 missing formulae to Brewfile (`minicodemonkey/chief/chief`, `mole`, `tcl-tk`)
- [ ] Test `./setup.sh --dry-run` end-to-end
- [ ] Full migration test on UTM VM or new Mac
- [ ] Consider extracting shared CSS if more HTML pages are added
- [ ] Git config: set proper user.name and user.email (currently auto-detected from hostname)
- [ ] Review GitHub Pages site design in browser and iterate
- [ ] Make repo public once ready
