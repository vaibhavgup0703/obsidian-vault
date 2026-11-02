---
type: project
status: active
date:
---

## What Vaani is

A multi-tenant outbound Hindi/Hinglish AI voice sales agent (India-first). First tenant: Gupta Wire (wire and cable manufacturer calling dealers). The business is data (`tenants/<id>/config.json`), not code.


## Stack and environment

Windows, PowerShell, venv at `.venv`, Python 3.14, Pipecat 1.10.0. STT: Sarvam saaras:v4. LLM: OpenAI gpt-4o-mini (optional `LLM_BASE_URL` / `LLM_API_KEY` for other OpenAI-compatible providers). TTS: Sarvam bulbul:v3, voice "rahul". VAD: Silero, `VAD_STOP_SECS=0.8`.

Pipeline (`vaani/bot.py`): `transport.input -> stt -> user_agg -> llm -> tts -> transport.output -> assistant_agg`

Entry points:

- `run_webrtc.py`: browser demo, WORKS end to end. Run: `python -m uvicorn run_webrtc:app --host 0.0.0.0 --port 7860`, open http://localhost:7860.
- `run_local.py`: mic and speakers. BLOCKED (pyaudio won't build on Python 3.14).
- `server.py` and `vaani/telephony/plivo.py`: real phone calls, not started (Plivo signup blocked).


## Roadmap (priority order)

- Tier 0 (this week): latency baseline per stage, interruption handling, fix worst failures, git hygiene.
- Tier 1 (weeks 2-3): in-call memory trimming, per-lead memory across calls (database), RAG as a tool with a real knowledge base, better prompt and examples, an evaluation harness (scripted caller scenarios).
- Tier 2 (weeks 3-4): Postgres, tenant onboarding, call dashboard, error handling and retries.
- Tier 3 (weeks 3-4): Docker, AWS deploy with public demo, monitoring and cost tracking, security basics, README with architecture diagram and demo video.
- Tier 4 (later, "sellable"): real telephony, India outbound-call compliance (get legal advice), voicemail detection, WhatsApp, billing.

## Decisions made

- RAG is for capability (knowledge that doesn't fit in the prompt), not for cost savings. Build it as an LLM tool to protect latency and prompt caching.
- Recordings are not "fed to the model": transcribe, mine for better prompts and few-shot examples, and use consent-cleared recordings only.
- Browser demo is the public face. Phone calls are a documented future item.
![[Pasted image 20261101123026.png]]
    
![[Pasted image 20261031185309.png]]
# Architecture
dynamic-outbound-voice-agent/
├── run_local.py        ← front door 1: your mic and speakers
├── run_webrtc.py       ← front door 2: a browser link
├── server.py           ← front door 3: real phone calls (Plivo)
│
├── vaani/              ← the kitchen (all the real logic)
│   ├── bot.py          ← head chef: builds and runs one call
│   ├── services.py     ← supplier list: picks STT / TTS / LLM / VAD
│   ├── prompt.py       ← turns business info into the agent's instructions
│   ├── tools.py        ← actions the agent can take (end call, mark DNC)
│   ├── compliance.py   ← the bouncer: may we call this number at all?
│   ├── postcall.py     ← after the call: transcript → structured summary
│   ├── store.py        ← saves each call to a file
│   ├── tenant.py       ← data shapes: Tenant, Lead, CallState
│   ├── settings.py     ← reads your .env (keys, model names)
│   └── telephony/plivo.py   ← phone-specific plumbing
│
├── tenants/gupta_wire/config.json   ← recipe card: one business as data
├── db/schema.sql       ← planned database tables (not used yet)
├── tests/test_core.py  ← 11 automatic checks
├── data/calls/         ← output: one JSON per call
├── .env                ← your secret keys (never commit this)
├── requirements.txt    ← list of libraries to install
└── bot.py (old root)   ← your first experiment, now unused
## Next actions
- [ ] 

## Log
TTS, STT Cartesia
Pipekit framework,



