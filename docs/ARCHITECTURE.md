# Architecture

## System boundary

Blind Care Agent is a voice-first assistive software platform with separate blind-user and guardian concerns.

```text
                         ┌──────────────────────┐
                         │ Guardian surfaces    │
                         │ safety / emergency   │
                         │ learning / memory    │
                         └──────────┬───────────┘
                                    │ authorized API
                                    │
┌───────────────┐        ┌──────────▼───────────┐
│ Blind user    │───────▶│ React / TS PWA      │
│ voice/image   │        │ VoiceHome           │
│ explicit act. │        └──────────┬───────────┘
└───────────────┘                   │
                                    ▼
                         ┌──────────────────────┐
                         │ FastAPI              │
                         ├──────────────────────┤
                         │ Auth + ownership     │
                         │ Agent pipeline       │
                         │ Safety / emergency   │
                         │ Learning             │
                         │ Memory               │
                         │ Settings             │
                         └──────┬────────┬──────┘
                                │        │
                  ┌─────────────▼─┐   ┌──▼────────────────┐
                  │ SQLite MVP   │   │ Provider interfaces│
                  │ 12 tables    │   │ Vision/STT/TTS/LLM │
                  └──────────────┘   └────────────────────┘
```

## Agent control flow

```text
INPUT
  │
  ├─ voice → STT abstraction
  ├─ text
  └─ image
  │
  ▼
INTENT
  │  rule-based, EN/AR, word-boundary aware
  │  safety-relevant intents prioritized
  ▼
CONTEXT
  │  recent conversation + selected memory facts
  ▼
VISION / SCENE ANALYSIS
  │  only when image context exists
  │  may persist SafetyEvent
  ▼
RESPONSE COMPOSITION
  │
  ▼
PRIORITY
  │  SOS ⇒ danger; otherwise scene-derived level
  ▼
SMART SILENCE
  │
  ├─ danger ───────────────▶ speak
  ├─ explicit request + permitted mode ▶ speak
  └─ policy suppresses ────▶ deliberate silence
  │
  ▼
TTS + conversation / scene logging
```

## Why Smart Silence sits after understanding

The system may need to understand an event in order to decide that it should not speak about it. Therefore silence is not implemented as “do not run AI.” It is a **policy gate after enough interpretation exists to assign priority**.

This makes the non-action auditable: the system can distinguish “nothing was detected” from “something was understood but correctly suppressed.”

## Trust boundaries

### User identity boundary
Profile access must be constrained to authorized ownership/guardian relationships. This became a formal architecture concern after adversarial testing exposed inconsistent ownership enforcement.

### Model boundary
Model/provider output is not itself the speech policy. Priority and Smart Silence remain explicit application logic.

### Emergency boundary
SOS receives a deterministic high-priority path. The software can create and surface emergency state, but external emergency-response guarantees are outside the current evidence scope.

### Guardian boundary
Guardian access is useful for safety but must not become arbitrary access to another user's private data. Authorization is therefore a safety/privacy requirement, not merely an API concern.

## Persistence

The documented MVP uses **SQLite with 12 SQLModel tables**. The roadmap identifies PostgreSQL + pgvector as a later scale-out phase.

The scale-out target is not represented here as currently implemented.

## Provider architecture

The codebase defines interfaces for:

- Vision;
- speech-to-text;
- text-to-speech;
- LLM response composition.

Deterministic mock implementations are the default evidence path. Real provider integration is an explicit next-stage boundary.

This allows control logic and policy to be exercised without conflating provider accuracy with application correctness.

## Frontend architecture

The blind-user surface is deliberately minimal. Guardian/admin surfaces can be richer because their interaction constraints differ.

The primary blind-user controls are:

- Describe;
- Repeat Last;
- Emergency SOS.

Accessibility semantics include screen-reader labels, live-region announcements, logical focus behavior, keyboard shortcuts, high contrast and EN/AR RTL behavior according to the project evidence.

## Future architecture — not current state

```text
Smart glasses camera + bone conduction    PLANNED
                 │
                 ▼
phone / edge processing                   PLANNED
                 │
                 ▼
Blind Care server brain
                 │
                 ├─ continuous scene flow PLANNED
                 └─ navigation mode       PLANNED

PostgreSQL + pgvector scale-out           PLANNED
```

These components belong to the target architecture only after separate implementation and validation.