---
type: project
status: active
date:
---
## Goal
An outbound AI Voice calling agent. Which can actually talk to leads.

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



