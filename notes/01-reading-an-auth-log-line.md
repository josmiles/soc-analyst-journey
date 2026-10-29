# Reading a Linux auth.log line

## What auth.log is

Linux writes every authentication event to this log: SSH logins (successful and failed), `sudo` use, `su`, and sessions opening and closing.

| Distribution | Location |
|---|---|
| Ubuntu / Debian | `/var/log/auth.log` |
| RHEL / Fedora / Rocky | `/var/log/secure` |
| Minimal installs without rsyslog (e.g. a fresh Debian 12) | No file; events are only in the systemd journal, read with `journalctl` |

## Anatomy of one line

```
Oct 29 07:41:03 web01 sshd[2143]: Failed password for invalid user admin from 203.0.113.45 port 51122 ssh2
```

| Part | Meaning |
|---|---|
| `Oct 29 07:41:03` | **When.** Classic syslog format: no year, no timezone (server local time). Recent Ubuntu releases write `2026-10-29T07:41:03.512345+03:00` instead, with year, microseconds and UTC offset. |
| `web01` | **Host** that wrote the line. Matters when correlating logs from many machines. |
| `sshd` | **Program**: the SSH server daemon. On OpenSSH 9.8+ this may appear as `sshd-session`, the separate program that now handles each connection. |
| `[2143]` | **Process ID.** One process per connection, so lines sharing a PID usually belong to the same connection attempt. Used to stitch a session together. |
| `Failed password` | **Outcome.** |
| `invalid user admin` | The username **doesn't exist** on this machine. For an existing account the line reads `Failed password for admin` with no "invalid". |
| `from 203.0.113.45` | **Source IP**: where the attempt came from. Usually the first pivot. |
| `port 51122` | **Client's source port**, a random high number picked by the connecting machine's OS. Not the port being attacked (SSH listens on 22). |
| `ssh2` | SSH protocol version 2. |

## Fact vs inference on this line

- **The log shows:** at 07:41:03 a client at 203.0.113.45 tried to log in to web01 over SSH as `admin`, which isn't an account on the machine, and failed.
- **I infer (weakly):** possibly automated password guessing, since bots try generic names like `admin`. One line isn't proof; a mistyped username produces the same failure. Volume and pattern are what confirm it.

*Note: 203.0.113.0/24 is an IP range reserved for documentation, so it's safe to use in examples.*
