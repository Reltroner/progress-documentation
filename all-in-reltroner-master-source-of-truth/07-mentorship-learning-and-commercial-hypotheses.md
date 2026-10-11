# 07 — LMS Learning Experience, 1:1 Mentorship & Monetization Hypotheses

> Commercial status: **CANDIDATE / NOT ACTIVATED**. The one-year mentorship idea is a founder intention and business hypothesis, not revenue, launched subscription, or finished LMS capability.

## What the learner pays for
The primary intellectual product is an **individualized creative mental model and a creator-owned generative framework**, not Zoom minutes, paywalled commodity lessons or a generic software platform.

Potential learner tracks:
- **Hobby**: enjoyment, personal expression, connected ideas, sustainable scope.
- **Production / public publishing**: intentional constraints, project decomposition, causal continuity, release planning, self-directed workflow. No guarantee of publisher acceptance or earnings.
- **Academic**: support independent thinking and work; never ghostwrite or silently complete school/university assignments.

Free learning remains genuinely usable by guest visitors. An account may add persistence, progress, learner projects, personalized work and authorized support, but a free reader should not be required to accept optional analytics tracking simply to read a lesson.

## Candidate offer ladder (not an approved price list)

| Potential offer | Purpose | Delivery artifact | Validation need |
|---|---|---|---|
| Free public LMS | establish common concepts/mental model | lessons, exercises, case studies | comprehension and independent application |
| Single diagnostic session | locate one real creative bottleneck | problem map + proposed experiment | buyer need, price fit, session usefulness |
| Creative Compound Sprint | build a personalized method over bounded sessions | evolving creative-system map | observable learner independence |
| Recurring 1:1 mentorship | continuous review and feedback with defined boundaries | session history + experiments + feedback | sustainable workload, retention and payment |

Do not build all tiers because a value-ladder marketing graphic has five steps. Subscription entitlements must be explicit; “paid” must not mean unlimited anytime DM and calls.

## Desired learner journey (product concept)
~~~text
free discovery
→ study framework / complete exercise
→ optional account + project context
→ optional goal mapping (hobby, production, academic)
→ future eligible paid offer, if separately activated
→ available slots
→ session confirmation
→ live mentorship
→ mentor-reviewed session artifact
→ learner independently applies method
→ review / feedback / next cycle
~~~

## Mentorship as a human capability
Mentor function: listen, ask Socratic questions, diagnose disconnects, map causality, challenge assumptions, choose suitable frameworks and review learner-generated outcomes. Zoom/Meet is the synchronous transport; **learner change and retained mental model** are the value. Follow-up artifacts: diagnosis, mental model, exercise, blockers, owner decisions, next actions.

### Operational automation, only after approved scope
- Learner selects meeting/timezone/notification preference (WhatsApp, Discord or email); keep verified fallback.
- Mentorship Service owns booking and entitlement; calendar/meeting provider and communication automations are *external side effects*.
- n8n can orchestrate calendar/Meet/Zoom reminders and approved notifications; it **does not own booking truth**.
- Rescheduling must respect policy, version/locking, authorization, consent, idempotency, provider failure, retry and record reconciliation.
- Human approves AI-generated meeting summaries before saving/sending; meeting transcripts and personal data require appropriate opt-in/privacy safeguards.
- Google Meet may be a simpler default; Zoom can remain preference where support and costs justify. Vendor preference is not a frozen LMS requirement.

## Learner profile vs identity
Keycloak owns OIDC identity, credentials, password/MFA and primary profile authority. Learning preferences, goals, project state and mentorship data belong to the relevant LMS domain service. Link by stable canonical principal/issuer context; do **not** mirror credentials into LMS or invent a second identity source.

A uniform Reltroner-branded UX is a valid product goal. It does not justify bypassing Keycloak security. Reconcile any custom theme/account experience with frozen OIDC client/realm architecture.

## Commercial validation gates
1. Technical delivery and operational safety demonstrated for the promised scope.
2. Creator problem detected through interactions, not guessed from follower count.
3. Small understandable offer and boundaries (sessions, async response, privacy, rescheduling, refunds/cancellation).
4. Capacity and resource budget defined.
5. Actual voluntary paid transaction if claiming revenue.
6. Outcomes, retention and user satisfaction evaluated independently; **no assumed burnout cure, publication success or fan-growth guarantee**.

**Sequence policy:** The Phase 1 → Phase 2 contract is binding. This document does not activate new paid sales before founder approval.

## Source
[Studio Master §§46, 52–55](https://github.com/Reltroner/reltroner-studio/blob/main/content/principles/reltroner-studio-master-source-of-truth.md) · [LMS logical service contract](../lms/logical-service-boundary-api-contract.md).
