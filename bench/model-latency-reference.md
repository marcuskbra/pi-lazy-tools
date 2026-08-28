# Model Latency Reference

Source: user-supplied AI Proxy performance snapshot.

Use this reference to select candidates for local lazy-tools categorization
benchmarks. It covers 14 days of successful, streamed, cache-free, non-batch
final requests with 100 to 1,000 output tokens. Every `provider_family =
'centml'` row is excluded. Rankings use p90 time to first token.

## Fastest Non-CentML Models

| Rank | Model | Unparsed Upstream Model ID | Provider | Requests | p90 TTFT | p90 TTLT | p50 tok/s |
|---:|---|---|---|---:|---:|---:|---:|
| 1 | gpt-oss-20b | openai/gpt-oss-20b | Groq | 352,486 | 172 ms | 888 ms | 738 |
| 2 | gpt-oss-safeguard-20b | openai/gpt-oss-safeguard-20b | Groq | 3,669 | 195 ms | 509 ms | 1,813 |
| 3 | gpt-5-nano-2025-08-07 | gpt-5-nano-2025-08-07 | OpenAI | 2,794,508 | 419 ms | 3,784 ms | 147 |
| 4 | gpt-oss-120b | openai/gpt-oss-120b | Groq | 807 | 426 ms | 2,774 ms | 215 |
| 5 | gpt-5.1-2025-11-13 | gpt-5.1-2025-11-13 | OpenAI | 407,429 | 462 ms | 8,727 ms | 78 |
| 6 | gpt-5.2-2025-12-11 | gpt-5.2-2025-12-11 | OpenAI | 9,015,565 | 487 ms | 4,243 ms | 55 |
| 7 | gpt-5.4-mini | gpt-5.4-mini | OpenAI | 1,887,326 | 490 ms | 3,403 ms | 140 |
| 8 | gpt-5.4-mini-2026-03-17 | gpt-5.4-mini-2026-03-17 | OpenAI | 18,526 | 508 ms | 3,966 ms | 118 |
| 9 | gpt-5-mini-2025-08-07 | gpt-5-mini-2025-08-07 | OpenAI | 506,220 | 532 ms | 6,512 ms | 114 |
| 10 | gpt-4.1-mini-2025-04-14 | gpt-4.1-mini | OpenAI | 325,818 | 565 ms | 3,372 ms | 76 |
| 11 | gpt-5.4-nano | gpt-5.4-nano | OpenAI | 9,082 | 594 ms | 3,020 ms | 91 |
| 12 | gemini-2.5-flash-lite | google/gemini-2.5-flash-lite | Google Vertex | 10,694 | 648 ms | 1,484 ms | 284 |
| 13 | gpt-5.4-2026-03-05 | gpt-5.4-2026-03-05 | OpenAI | 367,037 | 674 ms | 5,374 ms | 134 |
| 14 | grok-4.3 | grok-4.3 | xAI | 1,099 | 680 ms | 5,407 ms | 122 |
| 15 | gpt-4.1-mini-2025-04-14 | gpt-4.1-mini-2025-04-14 | OpenAI | 385,130 | 722 ms | 3,362 ms | 119 |
| 16 | claude-haiku-4-5-20251001 | claude-haiku-4-5@20251001 | Google Vertex | 1,224,228 | 741 ms | 3,229 ms | 117 |
| 17 | gpt-4.1-nano-2025-04-14 | gpt-4.1-nano-2025-04-14 | Azure | 312 | 767 ms | 2,919 ms | 105 |
| 18 | gpt-4.1 | gpt-4.1 | OpenAI | 256 | 778 ms | 7,118 ms | 120 |
| 19 | gpt-5.1-2025-11-13 | gpt-5.1-2025-11-13 | Azure | 234,982 | 804 ms | 9,504 ms | 81 |
| 20 | gpt-5.4-nano-2026-03-17 | gpt-5.4-nano-2026-03-17 | Azure | 3,489 | 813 ms | 5,198 ms | 51 |

## Fastest High-Volume Non-CentML Models

This ranking retains models with at least 500,000 requests.

| Rank | Model | Unparsed Upstream Model ID | Provider | Requests | p90 TTFT | p90 TTLT | p50 tok/s |
|---:|---|---|---|---:|---:|---:|---:|
| 1 | gpt-5-nano-2025-08-07 | gpt-5-nano-2025-08-07 | OpenAI | 2,794,508 | 418 ms | 3,783 ms | 147 |
| 2 | gpt-5.2-2025-12-11 | gpt-5.2-2025-12-11 | OpenAI | 9,015,565 | 487 ms | 4,239 ms | 55 |
| 3 | gpt-5.4-mini | gpt-5.4-mini | OpenAI | 1,887,326 | 489 ms | 3,404 ms | 140 |
| 4 | gpt-5-mini-2025-08-07 | gpt-5-mini-2025-08-07 | OpenAI | 506,220 | 531 ms | 6,516 ms | 114 |
| 5 | claude-haiku-4-5-20251001 | claude-haiku-4-5@20251001 | Google Vertex | 1,224,228 | 741 ms | 3,228 ms | 117 |
| 6 | gpt-5.6-luna | gpt-5.6-luna | OpenAI | 19,512,816 | 1,000 ms | 5,340 ms | 151 |
| 7 | gpt-5.5-cyber-preview | gpt-5.5-cyber-preview | OpenAI | 2,221,752 | 1,180 ms | 7,951 ms | 84 |
| 8 | gpt-5.5 | gpt-5.5 | OpenAI | 1,907,530 | 1,647 ms | 9,994 ms | 70 |
| 9 | gpt-5.6-terra | gpt-5.6-terra | OpenAI | 744,508 | 1,971 ms | 9,453 ms | 84 |
| 10 | claude-sonnet-4-6 | claude-sonnet-4-6 | Anthropic | 22,388,970 | 2,176 ms | 9,902 ms | 56 |
| 11 | gemini-3.6-flash | gemini-3.6-flash | Google Vertex | 2,267,533 | 2,177 ms | 3,699 ms | 619 |
| 12 | gpt-5.6-sol | gpt-5.6-sol | OpenAI | 12,167,045 | 2,395 ms | 13,039 ms | 57 |
| 13 | claude-sonnet-5 | claude-sonnet-5 | Anthropic | 1,216,217 | 2,634 ms | 10,126 ms | 94 |
| 14 | claude-sonnet-4-6 | claude-sonnet-4-6 | Google Vertex | 9,030,033 | 2,849 ms | 10,316 ms | 57 |
| 15 | claude-opus-5 | claude-opus-5 | Google Vertex | 3,112,846 | 3,042 ms | 11,891 ms | 92 |
| 16 | claude-opus-4-8 | us.anthropic.claude-opus-4-8 | Bedrock | 559,718 | 3,384 ms | 11,931 ms | 93 |
| 17 | deepseek-v4-flash-0731 | accounts/fireworks/models/deepseek-v4-flash-0731 | Fireworks | 677,566 | 3,405 ms | 8,933 ms | 116 |
| 18 | claude-opus-5 | claude-opus-5 | Anthropic | 5,499,333 | 3,417 ms | 12,127 ms | 93 |
| 19 | claude-opus-4-8 | claude-opus-4-8 | Anthropic | 2,012,343 | 3,453 ms | 12,608 ms | 87 |
| 20 | claude-opus-4-6 | claude-opus-4-6 | Anthropic | 719,420 | 6,850 ms | 11,391 ms | 107 |
