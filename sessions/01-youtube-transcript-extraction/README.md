# YouTube Transcript Extraction at Scale

Attempts to extract transcripts from 49 YouTube videos. Tests youtube-transcript-api, yt-dlp, browser fetch, tor proxy, PO Token provider (bgutil). All blocked by YouTube 4-layer anti-bot system.

| Field | Value |
|---|---|
| Duration | ~3 hours |
| Models | GLM-5.2, Xiaomi MiMo-V2.5-Pro |
| Tools | bash, browser, read, write, web_search |
| Outcome | Failed — IP rate limited. PO Token installed but 429 persists. |

## Files

| File | Description |
|---|---|
| `session.jsonl` | Raw JSONL session log (PII masked) |
