# Same question, different tools

One investigative question written in each tool's language. Every query has the same shape: **filter → extract the field → count → sort.** An entry is marked tested only after I've run it myself and checked the output.

---

## Count failed SSH logins per source IP

**Linux command line** (tested: ⬜)

```bash
grep "Failed password" /var/log/auth.log | grep -oE "from [0-9.]+" | sort | uniq -c | sort -rn
```

**Splunk SPL** (tested: ⬜)

```
index=main "Failed password"
| rex "from (?<src_ip>\d+\.\d+\.\d+\.\d+)"
| stats count by src_ip
| sort -count
```

**Microsoft Sentinel KQL** (tested: ⬜)

```
Syslog
| where SyslogMessage contains "Failed password"
| extend SrcIP = extract(@"from (\d+\.\d+\.\d+\.\d+)", 1, SyslogMessage)
| summarize Attempts = count() by SrcIP
| sort by Attempts desc
```
