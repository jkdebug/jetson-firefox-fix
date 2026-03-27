# CLAUDE.md

This file provides context for AI assistants working in this repository.

## Project Overview

**jetson-firefox-fix** is a documentation-only repository. It documents a tested workaround to install a functional non-Snap Firefox on NVIDIA Jetson AGX Orin systems running Ubuntu 22.04 (JetPack 6.x). No source code, build system, or CI/CD exists.

## Repository Structure

```
jetson-firefox-fix/
├── CLAUDE.md                     # This file
├── README.md                     # Project overview and quick reference
└── docs/
    └── firefox_fix_jetson.md     # Full step-by-step fix with context
```

## Problem Being Documented

Ubuntu 22.04's default `apt install firefox` pulls a Snap package that fails on Jetson platforms with:

```
cannot set capabilities: Operation not permitted
exec: "matchpathcon": executable file not found in $PATH
```

Root cause: Jetson environments lack full Snap/SELinux support.

## Documented Solution Summary

1. Remove the Snap Firefox: `sudo snap remove firefox`
2. Pin Mozilla PPA with priority 1001 in `/etc/apt/preferences.d/mozilla-firefox`
3. Add Mozilla PPA: `sudo add-apt-repository ppa:mozillateam/ppa -y && sudo apt update`
4. Install specific `.deb` build: `sudo apt install firefox=140.0.4+build1-0ubuntu0.22.04.1~mt1`

**Confirmed platform**: Jetson AGX Orin 64GB, Ubuntu 22.04, JetPack 6.0, kernel `5.15.148-tegra`, aarch64.

## Development Conventions

### Documentation Style
- Files are written in Markdown with emoji section headers (e.g., `## ✅ Confirmed Setup`)
- Shell commands are in fenced code blocks with `bash` syntax highlighting
- Keep docs concise and practical — context first, then exact commands

### File Conventions
- All documentation lives under `docs/` except the top-level `README.md`
- `README.md` serves as a brief overview and pointer to `docs/`
- Detailed technical steps belong in `docs/`

### Commit Style
- Short, descriptive messages (e.g., `"Add project README for Jetson Firefox fix"`)
- No ticket references or conventional commit prefixes observed

## What AI Assistants Should Know

- **No build steps** — nothing to compile, install, or test
- **No code to lint or format** — Markdown only
- **Changes are documentation edits** — focus on clarity, accuracy, and command correctness
- **Target audience**: embedded Linux/Jetson developers who may not be familiar with Snap packaging internals
- When adding new content, follow the existing emoji + heading style used in `docs/firefox_fix_jetson.md`
- Version pin (`firefox=140.0.4+build1-0ubuntu0.22.04.1~mt1`) is intentional — do not generalize it without testing
- The Mozilla PPA pin priority (1001) is intentional and must exceed Ubuntu's default (500) to prevent Snap re-installation on `apt upgrade`
