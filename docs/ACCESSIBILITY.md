# Accessibility Engineering

Accessibility is not a compatibility layer in Blind Care Agent. It is the reason the interaction architecture looks the way it does.

## Primary-channel assumption

For the target user, hearing may carry information that sighted interfaces normally place on screen. Therefore audio output has a cost: it competes with the environment.

This produces two simultaneous requirements:

1. make important software state perceivable through audio/screen-reader semantics;
2. avoid unnecessary audio that masks the user's real environment.

Smart Silence exists because satisfying requirement 1 without requirement 2 would still produce a poor assistive system.

## VoiceHome

The primary blind-user interface is organized around three actions:

- **Describe the scene** — explicit request for environmental description;
- **Repeat last** — replay without requiring regeneration;
- **Emergency SOS** — direct safety action.

Keyboard shortcuts documented by the project are `D`, `R`, and `E` respectively.

## Screen-reader and keyboard evidence

The supplied implementation documentation identifies:

- ARIA labels;
- `aria-live` announcements for results;
- logical focus order;
- keyboard-accessible core actions;
- high-contrast presentation;
- installable PWA behavior.

These are implementation claims from the project evidence. This public repository does not claim a completed independent WCAG conformance audit.

## Arabic and RTL

The current implementation supports English and Arabic with RTL behavior. Language selection is intended to be perceivable through speech rather than only a visual selector.

The source describes adding another language as a documented locale/register/selector process. That demonstrates localization structure; it does not prove quality for languages not yet implemented.

## User agency

Accessibility includes control over interruption.

```text
silent      → danger only
on_demand   → explicit requests
balanced    → danger + warnings + requests
chatty      → broad narration
```

The user can select how much unsolicited speech is acceptable. Danger is the explicit override.

## Why Repeat Last matters

A generated response should not have to be regenerated merely because the user did not hear it clearly the first time. `Repeat last` reduces model/provider dependence and gives the user deterministic control over previously spoken information.

## Accessibility claims not made

Current evidence does not establish:

- independent WCAG certification;
- usability across the full diversity of blindness and low-vision experiences;
- performance with screen readers across every browser/device combination;
- successful real-world mobility navigation;
- accessibility of future smart-glasses hardware;
- validated cognitive-load reduction in real users.

These require dedicated participatory evaluation.

## Evaluation principle

The strongest future accessibility evidence should come from blind and visually impaired users themselves.

Engineering tests can prove that a button has an ARIA label or that danger pierces silence. They cannot, by themselves, prove that the system feels empowering, unobtrusive, trustworthy or genuinely useful in daily life.