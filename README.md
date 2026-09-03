# Blind Care Agent

![Human-Centered AI](https://img.shields.io/badge/Human--Centered_AI-7A6F86?style=flat-square)
![Assistive Technology](https://img.shields.io/badge/Assistive_Technology-5F7A72?style=flat-square)
![Voice First](https://img.shields.io/badge/Voice--First-526D82?style=flat-square)
![Smart Silence](https://img.shields.io/badge/Smart_Silence-5B6F8A?style=flat-square)
![Accessibility](https://img.shields.io/badge/Accessibility-596B73?style=flat-square)
![125 Tests](https://img.shields.io/badge/Tests-125_passing-4F6B7A?style=flat-square)
![EN + AR](https://img.shields.io/badge/Languages-EN_%2B_AR-6B6F86?style=flat-square)

> **Eyes through sound — and a university in your ear.**

**Voice-first assistive AI for blind and visually impaired people — designed around independence, access to knowledge, safety, and the discipline to remain silent when speech would become interference.**

[Live Evaluation](https://blind-care.agentcraft.info) · [AgentCraft](https://agentcraft.info) · [Engineering Case Study](docs/CASE_STUDY.md)

---

## Engineering thesis

Most AI assistants are optimized to answer more often.

Blind Care Agent begins with a different question:

> **When hearing is one of a person's most important channels to the world, how do you build an AI that knows when not to occupy it?**

That question produced **Smart Silence**: an explicit policy gate between intelligence and speech.

```text
Perceive → Understand → Assess Priority → Smart Silence Gate → Speak / Stay Silent
                                      ↑
                               danger overrides
```

The model's ability to generate a response is deliberately separated from the system's authority to interrupt the user.

**AI can speak. Smart Silence decides whether it should.**

This is the central engineering boundary of the project.

---

## The human premise

Blind Care Agent is not built around the assumption that a blind person needs simplified thinking. It is built around the opposite assumption: **the person may be fully capable of learning, working, parenting, creating, and participating — while information that sighted people receive effortlessly remains unnecessarily difficult to access.**

The product therefore treats two capabilities as peers:

1. **Safety and environmental access** — describe scenes, prioritize hazards, support SOS and guardian workflows.
2. **Education and knowledge access** — turn readable material into navigable audio learning, comprehension checks, and progress.

The person is not reduced to a safety problem. **They are a learner, family member, professional, citizen, and independent decision-maker.**

---

## Current evidence status

| Capability / evidence | Status | Boundary |
|---|---|---|
| Voice-first interaction model | **IMPLEMENTED** | PWA interaction is centered on three large actions and screen-reader semantics. |
| Smart Silence policy | **IMPLEMENTED · TESTED** | `silent`, `on_demand`, `balanced`, `chatty`; danger pierces every level. |
| Scene/safety pipeline | **IMPLEMENTED · TESTED WITH DETERMINISTIC PROVIDERS** | Real production vision provider integration is next-stage work. |
| Emergency / guardian workflows | **IMPLEMENTED · TESTED** | Software workflow evidence; not a substitute for emergency services. |
| Learning library, chunked reading, deterministic quizzes, progress | **IMPLEMENTED · TESTED** | Expanded document sync/audiobook pipeline is next-stage work. |
| Long-term memory facts | **IMPLEMENTED · TESTED** | Current implementation uses the MVP data architecture. |
| English + Arabic / RTL | **IMPLEMENTED · TESTED** | Language choice is exposed in the accessible experience. |
| Automated backend suite | **TESTED** | **125 tests passed** in the supplied project evidence. |
| TypeScript strict check | **TESTED** | **0 errors** in the supplied project evidence. |
| Tenant-isolation fix and regression coverage | **TESTED** | Adversarial review exposed an ownership flaw; unified authorization was added and regression-tested. |
| Synthetic evaluation dataset | **DEPLOYED FOR DEMO** | Demo identities, conversations, safety events and scenarios are fictional. |
| Real Vision / STT / TTS / LLM providers | **NEXT** | Provider interfaces exist; production provider wiring is not presented as complete. |
| Smart-glasses client | **PLANNED** | Not implemented evidence. |
| Navigation mode | **PLANNED** | Not implemented evidence. |
| PostgreSQL + pgvector scale-out | **PLANNED** | Current MVP evidence uses SQLite. |

---

## Smart Silence: accessibility as a control system

A blind user's hearing is not an empty output channel waiting for an assistant. It carries traffic, voices, footsteps, orientation cues, social interaction, alarms, vehicles, and everything else the user needs to interpret the environment.

Constant AI narration can therefore become an accessibility failure.

Blind Care Agent makes interruption an explicit policy decision:

| Mode | Speech policy |
|---|---|
| `silent` | Speak only for danger. |
| `on_demand` | Speak when the user explicitly requests it. |
| `balanced` | Danger + warnings + requested responses. |
| `chatty` | Broad narration; intentionally not the default. |

### Safety invariant

> **Danger pierces every silence level.**

The inverse is equally important: an explicit **Describe** action counts as a user request, so `on_demand` must answer it. The project documentation records a regression test created after an earlier implementation got that boundary wrong.

This is an example of a broader AgentCraft principle:

> **A deliberate non-feature can be stronger engineering evidence than another feature.**

---

## Deterministic interaction pipeline

```text
voice / text / image
        │
        ▼
┌─────────────────────────────┐
│ Intent                      │  rule-based EN/AR matching
│ SOS > read > describe > …   │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ Context                     │  memory facts + recent conversation
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ Scene analysis              │  when visual input exists
│ → persisted safety events   │
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ Response composition        │  provider abstraction
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ Priority                    │  SOS ⇒ danger; else scene level
└──────────────┬──────────────┘
               ▼
┌─────────────────────────────┐
│ SMART SILENCE GATE          │  explicit, testable policy
│ danger always passes        │
└─────────┬───────────┬───────┘
          │           │
        speak       silence
          │
          ▼
      TTS + log
```

The architecture intentionally keeps consequential safety policy outside unconstrained model behavior.

---

## VoiceHome: the interface is part of the architecture

The blind user's primary experience is deliberately small:

| Action | Purpose | Shortcut |
|---|---|---|
| **Describe the scene** | Capture/select an image and request a spoken description. | `D` |
| **Repeat last** | Replay the last spoken response without regenerating it. | `R` |
| **Emergency SOS** | Trigger the emergency/guardian workflow. | `E` |

Accessibility evidence in the supplied implementation includes ARIA labels, `aria-live` announcements, logical focus order, high-contrast presentation, English/Arabic switching, RTL support, and spoken language confirmation.

**The design target is not a beautiful dashboard a blind user must learn to navigate. It is a low-friction auditory control surface.**

---

## Education is not an add-on

The founding product thesis treats access to knowledge as a first-class independence problem.

The implemented learning module includes:

```text
Learning Resource
      ↓
chunked audio-readable content
      ↓
user-controlled progression
      ↓
deterministic comprehension quiz
      ↓
score + progress history
```

The important product decision is conceptual: **the blind user is a student, not a patient.**

The roadmap extends this direction toward document synchronization, PDF-to-audiobook workflows, summaries, language learning, and spoken search. Those extensions remain **NEXT**, not shipped claims.

---

## Safety, emergency and guardianship

The MVP separates ordinary assistance from safety-critical events.

Implemented surfaces include scene safety reporting, persisted danger/warning events, SOS triggering, emergency state, guardian-facing visibility, and resolution workflows.

These features are assistive software. They are **not** presented as a certified emergency-response system, navigation device, medical device, or replacement for emergency services or trained human assistance.

---

## Security lesson: accessibility data still requires hard isolation

An adversarial review identified a critical authorization flaw: some agent endpoints verified that a profile existed but did not consistently verify that the authenticated caller owned that profile.

The response was architectural rather than cosmetic:

```text
adversarial review
      ↓
profile-ownership failure discovered
      ↓
unified authorization dependency
      ↓
server-side ownership enforcement
      ↓
live attack scenarios
      ↓
TestDataIsolation regression suite
```

Registration is restricted to blind/guardian roles, and guardian identity injection from request payloads is stripped server-side according to the project evidence.

This history is documented because **a discovered and permanently regression-tested failure is more informative than an unsupported claim that a system was secure from the beginning.**

---

## Provider abstraction and offline evaluation

Vision, STT, TTS and LLM capabilities are behind provider interfaces. Deterministic mock providers allow the system and safety policy to be exercised without API keys or network access.

A controlled example documented by the project uses an image fixture whose initial bytes encode `DANG`; the deterministic vision path returns a danger scene, which must pass through Smart Silence even in `silent` mode and produce the warning path.

This supports repeatable testing of **control logic**. It does not validate the accuracy of a future real-world vision model.

---

## Architecture

```text
Blind User
   │ voice / image / explicit action
   ▼
React + TypeScript PWA
   │
   ▼
FastAPI API
   ├── Auth / profile ownership
   ├── Agent pipeline
   │    ├── intent
   │    ├── context / memory
   │    ├── scene analysis
   │    ├── priority
   │    └── Smart Silence
   ├── Safety / emergency
   ├── Learning
   ├── Memory
   └── Settings
        │
        ├── Vision provider interface
        ├── STT provider interface
        ├── TTS provider interface
        └── LLM provider interface
        │
        ▼
   SQLite MVP · 12 tables
```

See [Architecture](docs/ARCHITECTURE.md) for responsibilities, trust boundaries and roadmap separation.

---

## Cross-domain research: the pattern may travel; the safety policy does not

Airtable research explored whether **"silence unless it matters"** has structural analogues outside blindness. Three areas showed meaningful architectural similarity:

- alarm-fatigue management in critical care;
- hazard-alert prioritization in industrial/construction safety;
- audio-first learning support where print decoding is the access barrier.

The research also deliberately rejected an apparently obvious analogy: deaf/hard-of-hearing assistive systems often face **signal scarcity**, not the signal-overload problem Smart Silence is designed to solve.

This distinction matters.

**Blind Care Agent has not been deployed or validated in ICUs, industrial safety, or reading-disability programs.** The reusable idea is the gate-with-an-override pattern. Every domain requires its own danger taxonomy, escalation policy, validation, users and experts.

See [Design Generalization](docs/DESIGN_GENERALIZATION.md).

---

## Technology

- **Frontend:** React 18, TypeScript strict, Vite, Tailwind, PWA, i18next, EN/AR + RTL
- **Backend:** FastAPI, SQLModel, Pydantic v2
- **MVP persistence:** SQLite, 12 tables
- **AI boundary:** Vision / STT / TTS / LLM provider interfaces with deterministic mocks
- **Quality evidence:** pytest — 125 passed; TypeScript — 0 errors
- **API surface:** 34 routes under `/api` in the supplied project documentation

---

## Evidence map

| Question a reviewer may ask | Evidence |
|---|---|
| Why should an assistive AI sometimes refuse to speak? | [Engineering Decisions](docs/ENGINEERING_DECISIONS.md) |
| Is Smart Silence testable or just product language? | [Testing & Verification](docs/TESTING_AND_VERIFICATION.md) |
| What does the architecture actually control? | [Architecture](docs/ARCHITECTURE.md) |
| How is accessibility represented technically? | [Accessibility](docs/ACCESSIBILITY.md) |
| What happened in the security audit? | [Security, Privacy & Safety](docs/SECURITY_PRIVACY_AND_SAFETY.md) |
| What is real versus roadmap? | [Limitations](docs/LIMITATIONS.md) |
| Does Smart Silence generalize? | [Design Generalization](docs/DESIGN_GENERALIZATION.md) |
| What evidence can be inspected? | [Evidence Index](evidence/README.md) |

---

## Roadmap boundary

| Phase | Evidence status |
|---|---|
| MVP: Smart Silence, voice-first UI, safety/SOS, learning, memory, guardian dashboard | **IMPLEMENTED / TESTED** |
| Real vision/STT/TTS providers + expanded education workflows | **NEXT** |
| Smart-glasses client | **PLANNED** |
| Continuous navigation mode | **PLANNED** |
| PostgreSQL + pgvector scale-out | **PLANNED** |

A roadmap is not implementation evidence.

---

## Demo-data disclosure

The public evaluation environment is populated with **synthetic demo data**. The documented preview profile includes fictional memory facts, learning resources, safety events, conversations and a resolved emergency scenario.

No demo scenario should be interpreted as evidence of real-user outcomes.

---

## What success would actually mean

The project's ambition is large, but this repository does not turn ambition into a metric.

Success would require evidence that blind and visually impaired people can gain meaningful independence, safer access to environments, easier access to education, and greater participation **without creating new distraction, surveillance, dependence or false confidence**.

That requires real users, accessibility experts, safety evaluation, provider validation, longitudinal study, and hardware/navigation validation where those future features are introduced.

Those outcomes are **NOT YET VALIDATED** by the current engineering evidence.

---

## Review scope

The production source code is maintained privately. This public repository is an **Engineering Evidence / Technical Case Study** documenting architecture, implemented capabilities, engineering decisions, testing methodology, security lessons, accessibility boundaries, roadmap status and live evaluation while protecting proprietary implementation details and credentials.

**Use the strongest claim the evidence supports — never the strongest claim the story would benefit from.**

---

## Repository map

| Path | Purpose |
|---|---|
| [`README.md`](README.md) | Executive engineering narrative, evidence status, architecture, and roadmap boundaries. |
| [`PORTFOLIO_NOTICE.md`](PORTFOLIO_NOTICE.md) | Public-repository scope, proprietary-source boundary, and evidence-use notice. |
| [`docs/CASE_STUDY.md`](docs/CASE_STUDY.md) | Long-form technical case study and product reasoning. |
| [`docs/ARCHITECTURE.md`](docs/ARCHITECTURE.md) | System boundaries, component responsibilities, data flow, and trust boundaries. |
| [`docs/ENGINEERING_DECISIONS.md`](docs/ENGINEERING_DECISIONS.md) | Key decisions, alternatives considered, trade-offs, and why Smart Silence is explicit policy. |
| [`docs/ACCESSIBILITY.md`](docs/ACCESSIBILITY.md) | Accessibility architecture, voice-first interaction model, EN/AR RTL, and interface evidence. |
| [`docs/TESTING_AND_VERIFICATION.md`](docs/TESTING_AND_VERIFICATION.md) | Test strategy, deterministic provider fixtures, Smart Silence regression behavior, and verification limits. |
| [`docs/SECURITY_PRIVACY_AND_SAFETY.md`](docs/SECURITY_PRIVACY_AND_SAFETY.md) | Authorization, privacy, ownership isolation, adversarial findings, and safety boundaries. |
| [`docs/DESIGN_GENERALIZATION.md`](docs/DESIGN_GENERALIZATION.md) | Cross-domain architectural research, valid parallels, and the rejected deaf/hard-of-hearing analogy. |
| [`docs/LIMITATIONS.md`](docs/LIMITATIONS.md) | Current limitations, NEXT/PLANNED work, and claims that are not yet validated. |
| [`evidence/README.md`](evidence/README.md) | Inspectable evidence index and guidance for future screenshots, runs, and measurements. |

---

Built by **Ayman Alsaid** · [AgentCraft](https://agentcraft.info) · [GitHub](https://github.com/ayman-alsaid) · [LinkedIn](https://www.linkedin.com/in/ayman-al-said-000a90159/) · contact@agentcraft.info