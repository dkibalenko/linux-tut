# linux-tut

Hands-on Linux notes, drills, for Developers and ticket scenarios for Technical Support
Engineering, written as Jupyter notebooks.

## What this repo is
- Every command is taught through a support lens: what ticket brings you to it, what to look for in the output, and the common gotchas
- Lessons are built around live commands run in a dedicated Ubuntu 22.04 WSL2 distro, with real output pasted in (WSL quirks flagged where they differ from bare Linux)
- Each topic follows the same loop: lesson → live "try now" → drill → ticket scenario → written-up solution
- Living references, such as an error-message cheatsheet that triages failures into *resolution failed / transport failed / reached-but-rejected*

## What's inside
| Area | Folder | Examples |
|------|--------|----------|
| Filesystem & navigation | `pillar1/` | Linux filesystem, `find`, `stat`, `readlink`, symlinks |
| FHS | `pillar2/` | Directory hierarchy tour, `sudo` / `su` |
| Permissions & ownership | `pillar3/` | `ls -l`, numeric modes, `chmod`, `chown`, groups |
| Text processing & log analysis | `pillar4/` | grep / awk / sed pipelines, three ticket-style practice sets |
| Process & service management | `pillar5/` | `ps`, `pgrep`, `nice`, `systemctl`, `journalctl`, cron, ticket practice |
| Networking | `pillar6/` | `ip`, `ping`, `traceroute`, `dig`, `nc`, subnetting, error reference, ticket scenario |
| Single-command notes | `commands/` | `ls`, `find`, `grep`, `awk`, `cut`, `sort`, `wc`, `stat`, `crontab`, `umask`, and more |

`PROGRESS.md` tracks status against the curriculum in detail.

## Progress
- [x] Pillar 1: Filesystem & navigation
- [x] Pillar 2: Filesystem Hierarchy Standard (partial)
- [x] Pillar 3: Permissions & ownership
- [x] Pillar 4: Text processing & log analysis
- [x] Pillar 5: Process & service management
- [ ] Pillar 6: Networking (`ip`, `ping`, `traceroute`, `dig`, `nc` done; `curl`, `ss`, SSH, firewalls next)
- [ ] Pillar 7: Disk & storage
- [ ] Pillar 8: User management
- [ ] Pillar 9: Shell & scripting basics

## Running locally
The notebooks need a Jupyter kernel (`ipykernel`, already included in `requirements.txt`); the shell commands in them are meant to be run in a Linux (or WSL) terminal.

    python3 -m venv .venv
    source .venv/bin/activate
    pip install -r requirements.txt
    jupyter notebook

## Why it exists
Development, Networking & Support work rewards knowing what's happening under the hood: why a service
won't start, why a port is refused rather than timing out, what a permission
denial is actually telling you. This repo is where I build that diagnostic
intuition, one tested-on-a-real-terminal topic at a time. It grows in bursts
as I work through each pillar, so a quiet stretch means I'm practicing, not
abandoning it.
