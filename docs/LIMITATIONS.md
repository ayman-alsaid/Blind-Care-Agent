# Limitations and Evidence Boundaries

## Real perception providers are not the current evidence base

Vision, STT, TTS and LLM interfaces exist, and deterministic mocks support repeatable testing. The current evidence should not be read as proof that a production vision model reliably detects hazards in uncontrolled environments.

**Status:** real provider wiring / validation — NEXT.

## Navigation is not implemented evidence

Continuous indoor/outdoor guidance is a materially harder safety problem than on-demand scene description.

It requires temporal scene understanding, localization, latency guarantees, route reasoning, obstacle dynamics and extensive real-world validation.

**Status:** PLANNED.

## Smart glasses are not implemented evidence

The product vision includes camera + bone-conduction wearable hardware with phone/edge processing and a server-side brain.

**Status:** PLANNED.

## Current persistence is MVP-scale

The supplied implementation uses SQLite with 12 tables. PostgreSQL + pgvector migration is a documented scale-out plan.

**Status:** scale-out PLANNED.

## Automated tests are not user-outcome evidence

125 passing tests demonstrate software behavior within their tested scope. They do not prove:

- fewer accidents;
- improved independent mobility;
- reduced isolation;
- improved educational attainment;
- improved employment;
- improved mental health;
- quality-of-life change.

These remain **NOT YET VALIDATED**.

## Accessibility needs participatory evaluation

ARIA semantics, keyboard behavior and RTL support are important, but technical conformance is not the same as lived usability.

The project still needs structured evaluation with blind and visually impaired users across different ages, blindness histories, technology familiarity, hearing profiles and daily environments.

## Danger detection has asymmetric risk

Smart Silence assumes a meaningful priority classification exists. With real perception providers, a false negative can be more serious than an unwanted false-positive interruption.

The current deterministic danger fixture validates the software path after danger is known; it does not quantify perception error.

## Guardian support can become surveillance if poorly governed

Safety relationships require consent, role boundaries, minimum necessary access and clear visibility into what guardians can see.

Current application isolation is part of the solution, not the complete social/privacy policy.

## Synthetic demo data is not field evidence

The evaluation environment uses fictional profiles, memory facts, conversations, safety events, learning resources and emergency scenarios.

Synthetic data is appropriate for safe portfolio review, but it cannot demonstrate real-user effectiveness.

## Cross-domain analogies are research, not deployments

Smart Silence has researched structural parallels in critical-care alarm fatigue and industrial safety, plus an adjacent accessible-learning mechanism.

Blind Care Agent has not been deployed or validated in those domains.

## The project is not a replacement for established mobility aids

No current evidence supports presenting Blind Care Agent as a replacement for orientation and mobility training, canes, guide dogs, trained human support, emergency services or other established assistive practices.

## Humanitarian scale is an ambition, not a measured result

The system is motivated by the possibility of improving access and independence for very large populations. Current evidence supports an implemented/tested software architecture, not a claim of population-scale impact.

Future impact claims should be earned through real deployment, accessibility research and longitudinal evidence.