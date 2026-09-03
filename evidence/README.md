# Engineering Evidence Index

This directory indexes evidence claims without publishing proprietary production source or real personal data.

## Evidence summary

| Claim | Classification | Evidence / scope |
|---|---|---|
| Smart Silence has four explicit modes | IMPLEMENTED | Application policy: silent / on_demand / balanced / chatty. |
| Danger pierces all silence modes | TESTED | Policy/regression coverage documented by project source. |
| Explicit Describe request works under on-demand semantics | TESTED | Regression test created after an early behavior error. |
| Backend automated suite | TESTED | 125 tests passed in supplied project evidence. |
| TypeScript strict validation | TESTED | `npx tsc --noEmit` recorded with 0 errors. |
| Deterministic danger fixture | VERIFIED IN A CONTROLLED TEST PATH | `DANG` image fixture → danger classification → silence override → warning path. |
| Tenant/profile isolation remediation | TESTED | Unified ownership enforcement + `TestDataIsolation` regression suite. |
| Voice-first PWA | IMPLEMENTED | VoiceHome with Describe / Repeat / SOS. |
| EN/AR + RTL | IMPLEMENTED | Bilingual locale/UI behavior documented. |
| Learning library and deterministic quizzes | IMPLEMENTED / TESTED | Chunked reading, quiz submission and progress workflows. |
| Demo scenarios | SYNTHETIC | Fictional profile, memory, learning, safety, conversation and emergency data. |
| Real production Vision/STT/TTS | NEXT | Provider abstraction exists; real provider evidence not claimed. |
| Smart glasses | PLANNED | Roadmap only. |
| Continuous navigation | PLANNED | Roadmap only. |
| PostgreSQL + pgvector migration | PLANNED | Current MVP uses SQLite. |
| Real-world humanitarian impact | NOT YET VALIDATED | Requires real-user deployment and longitudinal evaluation. |

## Review documents

- [Case Study](../docs/CASE_STUDY.md)
- [Architecture](../docs/ARCHITECTURE.md)
- [Engineering Decisions](../docs/ENGINEERING_DECISIONS.md)
- [Accessibility](../docs/ACCESSIBILITY.md)
- [Testing and Verification](../docs/TESTING_AND_VERIFICATION.md)
- [Security, Privacy and Safety](../docs/SECURITY_PRIVACY_AND_SAFETY.md)
- [Design Generalization](../docs/DESIGN_GENERALIZATION.md)
- [Limitations](../docs/LIMITATIONS.md)

## Evidence rule

A compelling humanitarian goal does not weaken the evidence standard.

**Implemented software, controlled tests, planned hardware and hoped-for human outcomes are four different things.** This repository keeps them separate.