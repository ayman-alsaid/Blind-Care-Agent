# Engineering Decisions

## 1. Optimize for interruption quality, not response volume

**Problem:** Conventional assistants reward responsiveness. For a blind user, unnecessary speech can mask environmental and social audio.

**Decision:** Introduce Smart Silence as an explicit gate.

**Rejected alternative:** Prompt the LLM to “be concise and only speak when useful.”

**Why rejected:** A safety/attention boundary should not depend only on probabilistic instruction following.

**Trade-off:** Useful information can be suppressed in quieter modes. The user therefore controls the policy and explicit requests remain meaningful.

**Evidence:** IMPLEMENTED / TESTED.

---

## 2. Danger overrides every silence setting

**Problem:** A user-selected quiet mode must not suppress a detected high-priority hazard.

**Decision:** Define danger as a policy invariant that pierces all speech levels.

**Trade-off:** False-positive danger classification can cause unwanted interruption, so future real-provider deployment requires perception-quality evaluation beyond current deterministic tests.

**Evidence:** IMPLEMENTED / TESTED under current provider-test architecture.

---

## 3. Explicit user request is a first-class signal

**Problem:** An early behavior incorrectly allowed `on_demand` semantics to conflict with the user's explicit Describe action.

**Decision:** Treat the action itself as permission to respond.

**Engineering consequence:** A regression test now locks the intended behavior.

**Lesson:** Accessibility policy must represent user intent, not merely global configuration.

---

## 4. Education is equal to safety in product priority

**Problem:** Assistive products can unintentionally reduce disabled users to risk-management subjects.

**Decision:** Make learning a first-class module with readable chunks, deterministic comprehension checks and progress tracking.

**Rejected framing:** “Safety assistant with some learning features.”

**Reason:** The product thesis is independence and participation, not only protection.

**Evidence:** Current learning module IMPLEMENTED / TESTED; expanded ingestion and audiobook workflows NEXT.

---

## 5. Keep consequential policy deterministic

**Problem:** LLMs are useful for interpretation and composition but are not an ideal location for hard safety priorities.

**Decision:** Keep intent priority, SOS escalation and speech gating in explicit application logic.

**Pattern:**

```text
AI capability → deterministic policy boundary → user-facing action
```

This mirrors a wider AgentCraft philosophy: design boundaries around AI, not only capabilities for AI.

---

## 6. Provider abstraction before production-provider dependence

**Problem:** Real Vision/STT/TTS/LLM services introduce cost, nondeterminism, availability and credential dependencies.

**Decision:** Define provider interfaces with deterministic mock implementations.

**Benefit:** Repeatable offline tests can verify the application's control plane.

**Trade-off:** Mock success is not evidence of real perception accuracy.

**Evidence:** IMPLEMENTED / TESTED; real production provider wiring NEXT.

---

## 7. Build the blind-user interface differently from the guardian interface

**Problem:** A dashboard optimized for sighted administration is not automatically an accessible primary interface.

**Decision:** Reduce the blind-user home surface to three dominant actions while allowing richer guardian panels elsewhere.

**Evidence:** IMPLEMENTED.

---

## 8. Use ownership enforcement as a shared dependency

**Problem:** Adversarial review found endpoints that checked profile existence but not consistent caller ownership.

**Decision:** Centralize ownership enforcement rather than patching individual routes ad hoc.

**Trade-off:** Centralized authorization dependencies require disciplined route adoption, but make the policy auditable and regression-testable.

**Evidence:** FIX IMPLEMENTED / TESTED.

---

## 9. Do not treat smart glasses as proof of current capability

**Problem:** Wearable hardware makes the product vision compelling but can blur roadmap and implementation.

**Decision:** Present smart glasses, continuous navigation and edge/server distribution only as PLANNED architecture.

**Reason:** Mobility guidance changes the safety case substantially and requires hardware, latency and real-world evaluation.

---

## 10. Test generalization claims by trying to falsify them

**Problem:** “This architecture applies everywhere” is easy to say and usually weak evidence.

**Decision:** Compare Smart Silence with external domains and explicitly document a domain that did **not** fit the pattern.

Research found structural parallels in alarm-fatigue management and industrial hazard prioritization, but deaf/hard-of-hearing assistive alerting often solves the inverse problem: insufficient signal reaching the user.

**Lesson:** Reusable architecture does not mean interchangeable populations or safety policies.

**Evidence:** RESEARCHED ARCHITECTURAL ANALOGY; NOT DEPLOYED / NOT VALIDATED in those domains.