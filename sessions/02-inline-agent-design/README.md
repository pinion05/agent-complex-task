# Inline Agent Architecture Design

Design discussion for "inline agent" — a minimal agent with only shell tool, 0-line system prompt, automatic output truncation, compaction strategy, and user skill system.

| Field | Value |
|---|---|
| Duration | ~2 hours |
| Models | Claude Fable (xhigh), GLM-5.2 |
| Tools | bash, read, write, edit |
| Outcome | Architecture spec drafted. Repo created at inline-agent/. |

## Files

| File | Description |
|---|---|
| `session.jsonl` | Raw JSONL session log (PII masked) |
