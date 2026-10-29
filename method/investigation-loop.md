# The investigation loop

Every case in this repo is worked through the same seven stages. Each step in a case report says which stage it belongs to.

| # | Stage | The question it answers |
|---|---|---|
| 1 | **Know normal (baseline)** | What does healthy activity look like here? You can't spot odd without knowing normal. |
| 2 | **Collect & scope** | What data do I have, what time window does it cover, and what question am I answering? |
| 3 | **Filter & focus** | What can I cut away? Narrow to the host, user, IP, port or time range that matters. |
| 4 | **Spot the anomaly** | What doesn't fit? Failed logins, a rare port, a large upload, a regular beacon, an odd user agent. |
| 5 | **Follow the thread** | Where does this indicator lead? Pivot from one clue to the next and put events in order. |
| 6 | **Conclude** | What happened, how confident am I, and what is the evidence? |
| 7 | **Write it up** | A short, plain timeline someone else could act on. |

## Fact vs inference

Every finding is written in two parts:

- **The data shows:** what is literally in the log line or packet.
- **I infer:** my interpretation, with the reasoning behind it.

Example (illustrative):

- *The data shows:* 412 failed SSH logins from 203.0.113.45 between 07:41 and 07:44, against 37 different usernames.
- *I infer:* an automated password-guessing (brute-force) attempt, because a person doesn't try 37 usernames in three minutes.

## False positives

Not every anomaly is an attack. Before calling something malicious, I write down the benign explanations I considered and why the evidence rules them in or out.

## Skill stages

| Stage | How sessions run |
|---|---|
| 1 | Mentor gives every command with a full explanation; I run it and we read the output together |
| 2 | Mentor gives the command; I predict the output before running it |
| 3 | Mentor names the goal; I recall the command myself |
| 4 | I drive the investigation; mentor reviews and sharpens |
