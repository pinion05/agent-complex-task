# Agent Complex Task Archive

A collection of raw GJC (gajae-code) agent session logs performing complex, multi-step tasks. Published for research, reproducibility, and analysis of agent behavior patterns.

## Sessions

| # | Session | Task | Outcome |
|---|---|---|---|
| 01 | [YouTube Transcript Extraction](sessions/01-youtube-transcript-extraction/) | Extract 49 video transcripts at scale | Failed — YouTube 4-layer anti-bot block |
| 02 | [Inline Agent Design](sessions/02-inline-agent-design/) | Design minimal shell-only agent | Architecture spec + repo created |
| 03 | [Raddit Dashboard PR](sessions/03-raddit-dashboard-pr/) | Feature dev + subagent review loop | PRs merged, features shipped |
| 04 | [Awesome Agent IDE](sessions/04-awesome-agent-ide/) | Research + multi-language README | Published with GitHub Pages |

## Format

Each session is stored as raw JSONL — the native GJC session format. Every line is a JSON object containing:
- `message` — user/assistant turns (text, thinking, tool calls, tool results)
- `model_change` — model switching events
- `custom` — workflow routing, intent detection
- `custom_message` — system context, workspace state

## PII Masking

All sessions have been masked:
- API keys, tokens, OAuth credentials → `***MASKED***`
- IP addresses → `***.***.***.***`
- Email addresses → `***@***.***`
- File paths with usernames → `/home/user/`

## Environment

- **Agent**: GJC v0.10.1 (gajae-code)
- **Models**: Claude Fable (xhigh thinking), GLM-5.2, Xiaomi MiMo-V2.5-Pro
- **Infrastructure**: yt-dlp, tor, bgutil-ytdlp-pot-provider, headless Chromium

## License

MIT
