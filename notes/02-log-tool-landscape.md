# The log analysis tool landscape

**Core idea:** every log tool answers the same kind of question: *show me events matching X, pull out field Y, count them.* Tools differ in scale (one file vs. millions of events from thousands of machines), not in the thinking. The reading skill transfers; only the syntax changes.

## Layer 1: On the machine itself

Already installed, no licence. Used on a single machine, when there's no SIEM, or to check the raw source.

| Tool | Purpose |
|---|---|
| `grep` | Find lines matching a pattern |
| `awk` / `cut` | Pull a specific field out of each line |
| `sort \| uniq -c` | Count how often each value appears |
| `less` / `tail -f` | Scroll through a file / watch it live |
| `journalctl` | Read the systemd journal |
| `jq` | Slice JSON logs (cloud services, modern apps) |
| Event Viewer, `Get-WinEvent` | Windows event logs (GUI / PowerShell) |
| Sysmon | Free Microsoft tool that records detailed process and network activity on Windows |

## Layer 2: SIEMs

A **SIEM** (Security Information and Event Management) collects logs from many machines into one place, parses each line into named fields, lets you search everything at once, and fires alerts when rules match.

```
SOURCES               COLLECT             SIEM                      ANALYST
Linux servers  ──┐
Windows PCs    ──┼──► agents /     ──►  parse into fields  ──►  search, dashboards,
Firewalls      ──┤    forwarders        index & store           alerts, investigation
Cloud (Azure)  ──┘
```

| Tool | Query language | Notes |
|---|---|---|
| Splunk (Cisco) | SPL | Most common in SOC job adverts. Free licence: 500 MB/day, doesn't expire, single standalone install. |
| Microsoft Sentinel | KQL (Kusto Query Language) | Microsoft's cloud SIEM. Moving to the Microsoft Defender portal; the Azure portal experience is supported until 31 March 2027. |
| Elastic Security (Elasticsearch, Logstash, Kibana) | KQL (Kibana Query Language), ES\|QL | Widely self-hosted, free tier. |
| Wazuh | Its own dashboard | Free, open-source SIEM + XDR. Good for a home lab. |

Also seen in job adverts: IBM QRadar, Google SecOps (formerly Chronicle), Graylog.

**Name trap:** "KQL" means *Kusto* Query Language in Microsoft Sentinel and *Kibana* Query Language in Elastic. Two different languages.

*Facts on licensing and portal dates checked October 2026:*
- *[About Splunk Free](https://help.splunk.com/en/splunk-enterprise/administer/admin-manual/10.4/configure-splunk-licenses/about-splunk-free)*
- *[What's new in Microsoft unified security operations](https://learn.microsoft.com/unified-secops/whats-new)*

## Layer 3: Network side (later)

Wireshark / tshark read packets. Zeek turns traffic into logs. Suricata is an IDS that writes alerts. Security Onion is a free Linux distribution bundling these.

## My learning order

1. Command line on raw logs
2. Splunk (Splunk Free, TryHackMe Splunk rooms, Boss of the SOC datasets)
3. Microsoft Sentinel / KQL
4. Wazuh in a home lab

Reason for this order: a SIEM shows thousands of events at once. Without being able to read one raw line confidently, that volume only confuses faster.
