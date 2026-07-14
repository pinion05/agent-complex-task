# YouTube Transcript Extraction — Agent Debug Session

Raw GJC agent session log of attempts to extract YouTube video transcripts at scale. Published as a case study of YouTube's anti-bot defenses in 2026.

## What Happened

Goal: Extract transcripts from 49 YouTube videos comparing AI models (Claude Fable 5 vs GLM 5.2 vs GPT 5.6).

### Methods Tried (all failed from this environment)

| Method | Result | Block Layer |
|---|---|---|
| youtube-transcript-api | IpBlocked after 10 reqs | IP rate limit |
| yt-dlp subtitle download | HTTP 429 | IP rate limit |
| Direct timedtext API (curl) | Google captcha page | Bot detection |
| Browser fetch (same-origin) | Google captcha page | Headless detection |
| youtubetranscript.com | Their server also blocked | Service-level block |
| Innertube get_transcript | 400 (protobuf params) | Protocol complexity |
| Tor SOCKS5 proxy | Bot detection / consent page | Tor exit node block |
| yt-dlp + Tor | "Sign in to confirm not bot" | Bot detection |
| yt-dlp + cookies | PO Token required | PO Token system |
| yt-dlp + Android client | 429 on download | IP rate limit |
| bgutil PO Token provider | Token generated but 429 persists | IP rate limit separate |
| PO Token + Tor | No subtitles found (consent) | Tor exit restricted |

### What Worked

- YouTube watch page: HTTP 200 (not rate-limited)
- YouTube search page: Normal
- Video metadata/descriptions via `read` tool: Full access
- PO Token generation (bgutil-ytdlp-pot-provider): Successful

### Root Cause

YouTube applies **4 independent anti-bot layers** on the timedtext/caption endpoint:
1. IP rate limiting (429)
2. Bot detection (captcha / "Sign in")
3. PO Token (Proof of Origin) requirement
4. Tor exit node blocking

No single bypass solves all 4 layers simultaneously from a datacenter IP.

### Solutions That Would Work

1. Wait 12-24h for rate limit expiry + PO Token
2. Residential proxy (WebShare ~$3/mo)
3. Hosted transcript API (TranscriptAPI ~$5/mo)
4. Different network/IP entirely

## Infrastructure Used

- GJC v0.10.1 (gajae-code)
- yt-dlp 2026.07.04 + bgutil-ytdlp-pot-provider 1.3.1
- tor 0.4.8.10 (SOCKS5 proxy)
- youtube-transcript-api
- Headless Chromium

## File

| File | Description |
|---|---|
| `session.jsonl` | 382 JSONL entries — transcript extraction attempts, tor setup, PO Token provider, proxy tests |

## PII Masking

All API keys, tokens, IP addresses, emails, and file paths have been masked with `***MASKED***`.

## License

MIT
