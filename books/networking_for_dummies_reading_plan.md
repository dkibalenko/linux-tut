# Networking For Dummies (11th ed., Doug Lowe) — Reading Plan

Maps the book's parts and chapters onto the course curriculum in `CLAUDE.md` and
the progress in `PROGRESS.md`. Page numbers come from `networking_for_dummies_11th_toc.md`.

**How to use it**
- Hands-on first: read a chapter *after* you've done the matching topic in the terminal, never as a prerequisite.
- The book is Windows-centric (Windows Server, Active Directory, Exchange, Hyper-V). Read it for the **concepts**; ignore the click-through Windows steps. The Linux commands come from this course.
- Reading order = course order. Start at Block A; it matches what you've already finished.
- This is a companion to the freeCodeCamp / PowerCert / NetworkChuck suggestions, not a replacement.

---

## Status key
- ✅ done in course, so read now to consolidate
- 🔜 next in course, so read after the hands-on lesson
- ⏳ later pillar
- ⛔ skip (Windows-specific or off-topic for support on Linux)

---

## Block A — Pillar 6 networking you've already done ✅

| Course topic (notebook) | Book section | Pages | What it adds |
|---|---|---|---|
| Key networking vocab (`3vocab…`) | Ch 1 *Let's Network!* — Defining a Network, Servers and Clients, Dedicated Servers and Peers | 8–14 | Client/server vocabulary used in every ticket |
| IP addresses, binary (`IP-Address`, `IP-Internet-Protocol`) | Ch 5 *Dealing with TCP/IP* — Understanding Binary, Introducing IP Addresses, Classifying IP Addresses | 69–76 | Second explanation of octets and classes |
| Subnetting, masks, CIDR (`IP-Subnet-Mask*`, `IP-Subnetting`) | Ch 5 — Subnetting, Private and Public Addresses | 77–80 | Short and gentle; do your open exercises *before* reading |
| WSL NAT, `10.255.255.254`, hotspot | Ch 5 — Understanding Network Address Translation | 81 | Why a private IP can reach the internet |
| `ip link`, MAC address (`4ip-link`, `MAC-Address`) | Ch 6 *Cables, Switches, and Routers* — What Is Ethernet?, Working with Switches | 96–97, 109–110 | What a link and a switch do at layer 2 |
| `ip route`, default gateway (`2ip-route`) | Ch 6 — Using a Router | 111 | What a gateway actually is |
| `dig` / `nslookup`, DNS (`8dns`) | Ch 5 — Using DNS (domains, FQDNs) | 89–91 | FQDN and domain concepts behind your `search` domain finding |
| `ping`, `traceroute`, `nc`, error triage (`5ping`, `7traceroute`, `10nc`, `9error-reference`) | Ch 17 *Solving Network Problems* — Ways to Check a Network Connection, Double-Checking Your Network Settings, Who's on First? | 266–270 | A support-desk view of the same escalation ladder |
| Ticket scenario (`11ticket-scenario1`) | Ch 17 — Documenting Your Trials and Tribulations; Ch 28 — Always Blaming the Network | 278, 415 | The documentation habit and the "not always the network" mindset |

---

## Block B — Pillar 6 networking still ahead 🔜

| Upcoming topic | Book section | Pages | Note |
|---|---|---|---|
| `/etc/hosts`, `resolv.conf`, `nsswitch.conf`, `hostname` | Ch 5 — Working with DNS clients (concept only, skip the Windows steps) | 92–93 | |
| DHCP concepts (leases, scopes, reservations); relevant to why `ip addr` shows what it does | Ch 5 — Configuring Your Network for DHCP | 82–86 | Skip the Windows Server 2016 steps (87–88) |
| `curl`, `wget`, `ss -tlnp` | Ch 4 — To Dedicate or Not to Dedicate (web/mail/database server roles) | 62–65 | Names the services you'll find listening |
| `iptables` / `ufw` | Ch 8 — Securing Your Connection with a Firewall; Ch 20 — The Many Types of Firewalls (packet filtering, SPI, circuit-level, application gateway) | 127–128, 311–317 | Explains "port blocked though the service is running" |
| SSH, `scp`, `rsync` | Ch 24 — Using a Virtual Private Network (VPN security, servers and clients) | 364–367 | Remote access ideas; SSH itself isn't in the book |
| WSL networking deep dive | Ch 10 *Virtual Networking* — Understanding Virtualization, Hypervisors, Network Virtualization, Benefits; Ch 8 — Sharing an Internet Connection | 151–158, 126 | The virtual switch/NAT idea is exactly what WSL2 does. Skip the Hyper-V steps (160–174) |
| Wireless (optional, helps your hotspot sessions) | Ch 9 *Wireless Network* — Wireless Standards, Home on the Range, Wireless Network Security | 137–139, 147–149 | Optional |

---

## Block C — Later pillars ⏳

| Pillar | Book section | Pages | What it adds |
|---|---|---|---|
| **P1–2** Filesystem, FHS | Ch 25 *Networking with Linux* — Comparing Linux with Windows, Getting to a Command Shell | 372–374, 379 | Orientation only; light |
| **P3** Permissions & ownership | Ch 13 *Managing Network Storage* — Understanding Permissions, Understanding Shares; Ch 19 — Permissions (who gets what), Group therapy | 208–210, 306–307 | Same permission thinking in a different OS |
| **P3** `sudo` / `su` | Ch 25 — Enabling the SUDO Command | 380–382 | Reinforces escalation and risk |
| **P3 / P8** Security basics | Ch 19 *Securing Your Network* — Securing User Accounts, Using passwords wisely, Secure the Administrator account, user rights | 299–305 | Least privilege, shared-admin risks |
| **P8** User management | Ch 12 *Managing Windows User Accounts* — account properties, Resetting Passwords, Disabling/Enabling, Deleting a User, Working with Groups; Ch 25 — Managing User Accounts | 191–193, 201–205, 383 | Lifecycle concepts map to `useradd`/`usermod`/`passwd`/`userdel`; skip the Windows dialogs |
| **P4 / P5** Logs, restarting services | Ch 17 — Restarting Network Services, Restarting a Network Server, Looking at Event Logs | 275–277 | The support-engineer reflex: check logs before restarting |
| **P5** Process & performance | Ch 21 *Network Performance Anxiety* — What Is a Bottleneck, The Five Most Common Bottlenecks, Monitoring Network Performance | 325–332 | Frames `top`, load, and "the system is slow" tickets |
| **P7** Disk & storage | Ch 28 — Running Out of Space on a Server; Ch 21 — Servers that do too much; Ch 13 — File servers, Storage appliances | 414, 328, 207–208 | The "disk full" ticket from the business side |
| **P7 / P5** Backups, cron | Ch 18 *Backing Up Your Data* — Comparing Types of Backups, Local vs Network, Keeping Sets | 284–290 | Why backup jobs (cron) matter; full / incremental / differential |
| **Support mindset** (any time, easy) | Ch 28 *Ten Big Network Mistakes*; Ch 27 *Ten Networking Commandments* | 405–415 | Fast reads; good interview talking points |
| **P9** Scripting | none | — | The book has nothing on this |

---

## Block D — Skip (or skim once) ⛔

| Chapter | Why |
|---|---|
| 2, 3 *Life on the Network*, *More Ways to Use Your Network* | Windows shared folders, mapped drives, printers, Office |
| 7 *Configuring Windows Clients* | Windows GUI only |
| 11 *Setting Up a Server* | Windows Server installation |
| 14 *Exchange Server 2016* | Exchange-only |
| 15 *Creating an Intranet* | IIS-only |
| 23 *Managing Mobile Devices* | iOS/Android MDM |
| 26 *Mac Networking* | macOS-only |
| 29 *Ten Things You Should Keep in Your Closet* | Hardware closet humor |
| Ch 25 Samba (386–391) | Only if a ticket involves Windows↔Linux file sharing |
| Ch 6 cabling detail (98–108) | Physical layer; read only if you move toward field/onsite support |
| Ch 22 *Life in Cloud City* (337–345) | Optional context for cloud-hosted support |

---

## Suggested reading order

1. **Now (Pillar 6 consolidation, ~1–2 hours):** Ch 1 (8–14) → Ch 5 (69–81, 89–91) → Ch 6 (96–97, 109–111) → Ch 17 (264–270, 278).
2. **After `curl` / `ss` / `wget`:** Ch 4 (62–65).
3. **After `/etc/*` consolidation:** Ch 5 (82–86, 92–93) for DHCP and DNS clients.
4. **After `iptables` / `ufw`:** Ch 8 (127–128) → Ch 20 (311–317).
5. **After SSH:** Ch 24 (364–367).
6. **After WSL networking:** Ch 10 (151–158).
7. **Pillar 7:** Ch 28 (414), Ch 21 (325–332), Ch 18 (284–290).
8. **Pillar 8:** Ch 12 (selected pages), Ch 19 (299–305), Ch 25 (380–383).
9. **Pillar 3 review (any time):** Ch 13 (208–210), Ch 19 (306–307).
10. **Last:** Ch 27, Ch 28 — the support mindset.

Skipping every ⛔ row and the optional rows leaves roughly 120–150 pages of the 400+ page book, almost entirely in Parts 2, 4 and 6.

## Caveats
- Pillars 1–5 progress in `PROGRESS.md` is inferred from notebook filenames, so Block C rows for those pillars are a best guess.
- The book is a generalist, Windows-oriented text. Where it disagrees with Linux behavior (e.g. its DHCP/DNS client steps), trust your terminal.
