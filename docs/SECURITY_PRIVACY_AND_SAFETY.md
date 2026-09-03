# Security, Privacy and Safety

Blind Care Agent handles information that can be unusually sensitive: location-like context, environmental scenes, conversations, routines, family relationships, memory facts, learning activity and emergency events.

Accessibility does not lower the security bar.

## Authorization incident and remediation

The project documentation records an adversarial review that found a critical flaw: profile-scoped endpoints could verify that a profile existed without consistently verifying that the authenticated caller was authorized to access it.

### Remediation

- unified ownership enforcement was introduced;
- authorization behavior was centralized rather than patched only at individual routes;
- live attack scenarios were used to verify closure;
- `TestDataIsolation` regression coverage was added;
- registration was restricted to the intended `blind` / `guardian` roles;
- guardian identity supplied through untrusted payloads is stripped server-side.

The repository exposes this history deliberately. Security maturity is demonstrated by the learning loop, not by pretending a flaw never existed.

## Privacy boundary

Guardian support creates a tension between safety and autonomy.

The system architecture therefore needs to distinguish:

```text
support relationship ≠ unrestricted surveillance authority
```

Current evidence supports ownership/isolation controls at the application layer. It does not establish a complete regulatory/privacy compliance program.

## Safety policy

Smart Silence is an application-level safety/attention gate:

- danger overrides silence;
- ordinary output may be suppressed;
- explicit user requests are respected;
- SOS receives high priority.

This policy reduces one class of risk — unnecessary auditory interference — while creating another requirement: danger classification must be trustworthy when real perception providers are introduced.

## Deterministic mocks and safety honesty

Mocks are useful for proving that a known danger classification takes the correct software path.

They cannot prove that a real camera/model will correctly recognize stairs, traffic, obstacles, fire, medication labels, faces or navigation cues.

Real-provider safety evaluation remains separate work.

## Emergency boundary

The application can trigger and record emergency workflows and surface them to a guardian.

Current evidence does not justify claims of:

- certified emergency dispatch;
- guaranteed emergency-service delivery;
- medical diagnosis;
- certified fall detection;
- safe autonomous navigation;
- replacement of a cane, guide dog, orientation/mobility training or human assistance.

## Demo privacy

The public evaluation environment uses **synthetic demo data**. Documented names, memory facts, learning history, conversations, safety events and emergency scenarios are fictional.

This prevents portfolio evaluation from requiring disclosure of real personal data.

## Future smart-glasses privacy

Always-on or frequently sampled cameras materially change the privacy threat model. Before smart-glasses deployment, the design should explicitly address:

- bystander privacy;
- capture minimization;
- local/edge processing opportunities;
- retention policy;
- user-visible recording state;
- deletion controls;
- encryption and device loss;
- consent and jurisdictional constraints.

These are future requirements, not claims about current hardware.

## Security principle

> **A system designed to increase independence must not purchase safety by silently creating surveillance or loss of control.**

That principle should remain a design constraint as the product moves from software MVP toward real sensors and wearable hardware.