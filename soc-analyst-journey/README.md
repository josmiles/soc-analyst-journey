# SOC Analyst Journey: Log & Packet Analysis

A hands-on record of learning defensive security analysis: reading logs and network captures to work out what happened on a system, and writing it up the way a SOC team would.

Every case in this repo was worked on data I am authorised to examine: my own lab, training platforms, or published sample files.

- **Analyst:** Joseph <!-- add LinkedIn / contact link -->
- **Started:** 29 October 2026
- **Learning setup:** guided sessions with an AI mentor. I run every command, read every output and write every report myself.

## What this repo demonstrates

- Investigating Linux, Windows and web server logs from the command line
- SIEM searching: Splunk (SPL), Microsoft Sentinel (KQL), Wazuh
- Packet analysis in Wireshark and tshark
- Separating fact from inference, and writing timelines a SOC team could act on

## How every case is worked

**Baseline → Collect & scope → Filter & focus → Spot the anomaly → Follow the thread → Conclude → Write it up**

Full method: [method/investigation-loop.md](method/investigation-loop.md)

## Case index

| # | Date | Case | Data source | Tools | Key finding |
|---|------|------|-------------|-------|-------------|
| — | — | First case coming next session | — | — | — |

## Skill map

**Current stage:** 1 of 4, guided (mentor gives each command; I run it and interpret the output)

| Track | Topic | Status |
|---|---|---|
| Logs | Reading a single log line | ✅ Done |
| Logs | Linux auth.log / syslog | 🟡 In progress |
| Logs | Web server logs (Apache / Nginx) | ⬜ |
| Logs | Windows Event Logs | ⬜ |
| Logs | Correlating multiple sources | ⬜ |
| SIEM | Splunk (SPL) | ⬜ |
| SIEM | Microsoft Sentinel (KQL) | ⬜ |
| SIEM | Wazuh | ⬜ |
| Network | Wireshark interface & display filters | ⬜ |
| Network | TCP/UDP on the wire, following streams | ⬜ |
| Network | HTTP / DNS / TLS analysis | ⬜ |
| Network | Scans, brute force, exfiltration, C2 beaconing | ⬜ |
| Network | Extracting files from a capture | ⬜ |
| Combined | Matching log events to packets in one timeline | ⬜ |

## Repo layout

```
.
├── README.md        ← overview, case index, skill map
├── method/          ← how I investigate: the loop, fact vs inference
├── cases/           ← one folder per investigation, each with a report
│   └── _template/   ← copy this to start a new case
├── journal/         ← dated session notes: what I covered and learned
├── notes/           ← concept notes (log formats, tool landscape)
├── toolkit/         ← every command, query and filter I use, explained
└── labs/            ← practice data (synthetic or published samples only)
```

## Data handling rules

1. **Authorised data only.** My own systems, training platforms, published samples.
2. **Sanitise before committing.** Real public IPs, hostnames and usernames from my own systems are replaced with placeholders or the documentation ranges (192.0.2.0/24, 198.51.100.0/24, 203.0.113.0/24).
3. **No secrets.** No passwords, keys or tokens, ever.
4. **No malware.** Packet captures and anything extracted from malware-traffic exercises stay out of the repo (see `.gitignore`). Reports link to the original exercise instead.
