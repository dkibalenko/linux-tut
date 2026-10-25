# Linux Tutor — Progress Tracker

Last updated: 2026-10-20

This file tracks curriculum progress against the pillars defined in `CLAUDE.md`. Status for Pillar 6 is based on direct session history (verified). Status for Pillars 1-5 is inferred from notebook filenames only — I have not re-read their content in this session, so topic lists there are a best guess, not a verified audit. Flag it if you want those reviewed properly before trusting the detail.

---

## PILLAR 1 — Filesystem & Navigation — *likely substantial progress, unverified detail*

Files present: `1part-linux-filesystem.ipynb`, `2part-navig-discovery.ipynb`, `3part-stat-readlink-symlinks.ipynb`

- Inferred covered: `pwd`/`cd`/`ls` variants, absolute vs relative paths, `find`/navigation+discovery tools, `stat`, `readlink`, symlinks vs hardlinks.
- Curriculum items I can't confirm from filenames alone: `locate`, `tree`, `file`, `wc`, `sort`/`uniq`, `head`/`tail`/`tail -f`, `less`/`more`, `diff`, `touch`.
- **Remark:** worth a quick self-check — if `tree`, `file`, or `tail -f` weren't explicitly drilled, they're high-value for support work (log monitoring, identifying unknown files) and shouldn't be skipped even if "basic."

## PILLAR 2 — Filesystem Hierarchy Standard (FHS) — *appears partial*

Files present: `2part-fhs-sudo-su.ipynb` (note: numbered "2part" — no "1part" file exists, worth confirming that's intentional and not a gap)

- Inferred covered: FHS directory tour + `sudo`/`su` (note: `sudo`/`su` is technically listed under Pillar 3 in the curriculum map, so this file seems to have pulled it in early — not a problem, just noting the cross-pillar overlap).
- **Remark:** `/var/log` deep dive specifically is called out in the curriculum as the most important FHS destination for support work — confirm it got real attention, not just a mention, since it's the foundation for all of Pillar 4's log analysis work.

## PILLAR 3 — Permissions & Ownership — *appears substantial*

Files present: `1part-perm-owner.ipynb`, `2part-perm-owner-group.ipynb`

- Inferred covered: reading `ls -l`, permission triplets, numeric notation, `chmod`/`chown`/`chgrp`.
- Can't confirm from filenames: `umask`, special bits (setuid/setgid/sticky), `/etc/sudoers` concept-level.
- **Remark:** special bits (especially the sticky bit on `/tmp`) are a classic interview/ticket topic — worth confirming it was covered explicitly rather than assumed from the chmod numeric work.

## PILLAR 4 — Text Processing & Log Analysis — *appears substantial, practice-heavy*

Files present: `text-processing.ipynb`, `practice1.ipynb`, `practice2-ticket.ipynb`, `practice3-ticket.ipynb`

- Good sign: three separate ticket-style practice files, consistent with the pattern that's worked well in Pillar 6 (scenario-based drilling, not just lecture).
- **Remark:** this pillar is the one most directly tested in support interviews ("find the top 10 errors in syslog" style questions) — the practice-heavy file list here is a good sign it got the attention it needs.

## PILLAR 5 — Process & Service Management — *appears thorough*

Files present: `cron-crontab-systemctl.ipynb`, `journalctl.ipynb`, `nice-renice.ipynb`, `pgrep-find-pid.ipynb`, `ps-aux-grep.ipynb`, `ps-aux-grep2.ipynb`, `systemctl.ipynb`, plus `practice1.ipynb`, `practice2-ticket1.ipynb`, `practice3-ticket2.ipynb`

- Broad coverage across the pillar's core topics (process inspection, job/service control, cron, journald), with three practice/ticket files again.
- Can't confirm from filenames: `/proc/PID/*` inspection, `nohup`/`&`/`fg`/`bg`/job control specifically, kill signal nuance (`SIGTERM` vs `SIGKILL` vs `SIGHUP`).
- **Remark:** worth double-checking `/proc/PID/fd` and signal-type nuance got hands-on time — easy to gloss over `pkill`/`kill -9` as "just stop the process" without the signal-type reasoning that actually matters in an incident.

---

## PILLAR 6 — Networking — **IN PROGRESS, verified in detail (sessions through 2026-10-20)**

### Done

| Topic | Notebook | Notes |
|---|---|---|
| `ip addr` | `1ip-addr.ipynb` | |
| `ip route` | `2ip-route.ipynb` | |
| Key networking vocab | `3vocab-key-networking-definitions.ipynb` | |
| `ip link` | `4ip-link.ipynb` | |
| `ping` | `5ping.ipynb` | Includes real-world gateway-ICMP-silent-but-forwards example from your own WSL hotspot run |
| General practice | `6practice.ipynb` | |
| `traceroute` | `7traceroute.ipynb` | Includes live mobile-hotspot driving session with real `*` patterns (mid-path silence vs destination-edge filtering), ICMP rate-limiting, and an `mtr` preview follow-up |
| `nslookup` / `dig` | `8dns.ipynb` | Includes real `+trace` failure diagnosis (WSL resolver choking on the root priming query, fixed via `@8.8.8.8`), IPv6-route-gap explanation, and a full DNS-architecture Q&A (stub resolver vs recursive resolver vs authoritative nameserver) |
| Error-message reference | `9error-reference.ipynb` | Living cheatsheet — 3-bucket triage model (resolution failed / transport failed / reached-but-rejected); will keep growing as new commands are covered |
| Ticket scenarios (Drill + 2 Scenarios) | `9ticket-scenario1-2.ipynb` | Full step-by-step solutions written up per scenario, with corrections folded in (host-alive-vs-service-down, using ticket context as evidence, not just command output) |
| `nc` (netcat) | `10nc.ipynb` | Lesson + live TRY NOW (OpenBSD netcat; `google.com:8080` timeout vs `10.255.255.254:53` success) + drill 3/3 scored. Core skill: **refused (fast, RST, host answered) vs timeout (slow, packets dropped)**; always use `-w`; `-4` to skip WSL's missing IPv6 route; `nc -zvu` is not proof for UDP |
| Error reference update | `9error-reference.ipynb` | New `nc errors` table added (succeeded / refused / timed out / Network is unreachable / name not known / UDP false positive), each filed under its bucket; intro and bucket list updated |
| Ticket scenario 1 (full) | `11ticket-scenario1.ipynb` | P2 "Cannot connect to database": `dbo1` typo → DNS detour (NXDOMAIN, root SOA vs company zone, `dig` ignores `search` domains, `getent hosts` = what apps see) → `nc` timeout on 5432 vs 22 OK → port-specific drop → host-firewall allowlist `10.20.2.0/24` excluded `app01` (`10.20.1.0/24`) → escalate → verify (`nc`, `pg_isready`, logs, customer confirmation). Includes debrief and a **blank reusable checklist** (intake / diagnosis path / resolution) for "Cannot connect to <service>" tickets |
| Authoritative DNS queries | in `11ticket-scenario1.ipynb` | `dig NS <zone> +short`, `dig @<ns> <fqdn>`, `aa` vs `ra` flags, zone SOA vs root SOA; practiced on `google.com` |
| `/etc/hosts`, `/etc/nsswitch.conf`, `/etc/resolv.conf` (partial) | in `11ticket-scenario1.ipynb` | Lookup order `files dns`, `search` domains, WSL's generated `resolv.conf` (no `search` line). Hands-on `/etc/hosts` demo done. Not yet a standalone lesson |

### IP addressing & subnetting (theory notes, written this period)

- Notes: `IP-Address.ipynb`, `IP-Internet-Protocol.ipynb`, `IP-Subnet-Mask.ipynb`, `MAC-Address.ipynb` (your own notes), plus `IP-Subnet-Mask-CIDR.ipynb` and `IP-Subnetting.ipynb` (tutor-written lessons).
- `IP-Subnetting.ipynb` teaches the fixed method for reading any `IP/N`: interesting octet → block size → network start → broadcast → usable hosts, with worked examples (`172.30.240.133/20`, `192.168.10.77/26`, `172.16.37.9/19`), subnet-splitting, nesting ("subnet is relative"), and a Python `ipaddress` checker.
- Corrections given: `IP/N` is a *host* in a network (network address = host bits zero); each extra mask bit doubles subnets and halves size; zeros = network address, ones = broadcast.
- **Open exercises (unanswered):** `IP-Subnetting.ipynb` TRY YOURSELF (7 questions) and `IP-Subnet-Mask-CIDR.ipynb` section 6 (4 questions). Send answers in a future session for checking.
- The `Checklist` cell in `11ticket-scenario1.ipynb` is a blank template; filling it in for this ticket as a worked example is optional.

### Not yet covered (remaining curriculum items for Pillar 6)

- `curl` (headers, verbose, follow-redirect, reading status codes)
- `wget`
- `netstat` / `ss` (`ss -tlnp`, `ss -s`)
- `telnet` (legacy port test)
- `hostname`, and `/etc/hosts` / `/etc/resolv.conf` / `/etc/nsswitch.conf` as standalone topics (all three touched hands-on in the ticket scenario, so this is a short consolidation, not a first look)
- `iptables` / `ufw` (concept level)
- SSH basics (`ssh`, `~/.ssh/authorized_keys`, `known_hosts`, troubleshooting connection refused/key rejected/host key changed)
- `scp`, `rsync`
- WSL networking deep dive (virtual adapter behavior, why `localhost` differs from bare Linux)

**Recommended next topic:** `curl` (`-I`, `-v`, `-L`, reading 4xx/5xx status codes). It is the natural step after `nc`: `nc` proves the TCP port, `curl -v` proves the protocol layer above it (this is the "Step 4" in the ticket checklist). After that: `ss -tlnp` / `ss -s` (the server-side half of "refused" diagnosis, already used in the ticket), then `telnet`/`wget`, then SSH.

---

## General remarks on the process so far

- The pattern that's worked best: **lesson notebook → live TRY NOW output pasted back → verified/corrected → drill → scenario → written-up solution notebook.** Worth keeping this exact rhythm for future pillars/topics rather than changing it.
- Several genuinely useful real-world findings have come out of your *own* environment (WSL's `10.255.255.254` resolver instead of the textbook `127.0.0.53`, the `dig +trace` priming-query failure, the mobile-hotspot traceroute patterns) — these are better teaching material than anything scripted, and are now preserved in the notebooks rather than lost in chat scroll.
- The error-reference notebook (`9error-reference.ipynb`) is a good standing asset — keep feeding it one row at a time as new commands/errors come up, rather than writing it once and forgetting it.
- New this period: a reusable **ticket checklist** (intake → diagnosis path → resolution) lives at the bottom of `11ticket-scenario1.ipynb`. Plan: copy it per ticket of that type, and consider making a similar one per ticket group (e.g. "service won't start", "disk full", "permission denied") as those pillars get scenario work.
- Recurring habits to keep drilling: copy-paste names instead of retyping (the `dbo1` typo); separate ticket facts from assumptions; read the SOA before concluding on NXDOMAIN; check refused-vs-timeout by message *and* elapsed time (`time nc ...`).
- Video follow-ups already suggested (do after hands-on, not before): freeCodeCamp *TCP Flags & Handshake — 9:40:48*, *DNS Hierarchy & Queries — 11:57:10*, *IPv4 Logical Addressing — 48:09*, *Classful vs. Classless (CIDR) — 55:17*, and *Subnetting & Borrowing Bits — 2:15:55* for the subnetting depth.
