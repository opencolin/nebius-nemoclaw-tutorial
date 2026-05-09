# Slack message — Token Factory support channel

Hi team 👋 — flagging one issue we hit while building a NemoClaw + Token Factory tutorial, plus a quick acknowledgment of one you've already triaged.

**Main flag — Nemotron models unusable through NemoClaw's OpenAI-compatible provider.** Already filed on our side: https://github.com/nebius/api/issues/211 (companion to https://github.com/NVIDIA/NemoClaw/issues/3279 on the NVIDIA side).

TL;DR: all three Nemotron models on TF return `reasoning_content` with empty `content`. NemoClaw's Option 3 reads only `content`, so onboarding's smoke check fails and tool calls 400. The cleanest fix from your side would be exposing/documenting a non-reasoning toggle for Nemotron — e.g. forwarding `extra_body={"chat_template_kwargs": {"enable_thinking": false}}` to the engine, honoring `"detailed thinking off"` system prompt for Ultra, or shipping a separate non-thinking model ID. Even just **documenting** that Nemotron on TF is reasoning-only and returns `reasoning_content` would help — the API reference doesn't currently mention reasoning fields, so users hit this with no hint.

Tutorial workaround: pinned to `meta-llama/Llama-3.3-70B-Instruct`. Also tested working: `NousResearch/Hermes-4-70B`. Skipped DeepSeek V3.2 because it's also thinking-capable and the TF default behavior isn't documented, so it's a latent footgun.

**Already on your radar — `max_completion_tokens` 400 on `nvidia/nemotron-3-super-120b-a12b`.** Saw the thread from Apr 30 — we hit this too. Tutorial workaround is to send `max_tokens` via `extra_body`. No action needed from us, just confirming it's blocking the modern-OpenAI-SDK path for users targeting that model.

Tutorial repo (with full issues tracker + workarounds in place): https://github.com/opencolin/nebius-nemoclaw-tutorial

Thanks!
