# 01 — Learners, Functions and Use Cases

**Status:** PROPOSED — 2026-10-14  
**Role:** Specify who the course serves and what a learner should be able to do, independently of the delivery software.

## Target users

1. **Curious beginner:** likes fictional settings but has no structured project. Needs a simple entry point and permission to start small.
2. **Idea-rich beginner:** has disconnected notes, maps or characters. Needs boundaries, relationships and a reusable method.
3. **Story-first creator:** has a story or character and wants a world that supports believable choices and consequences.
4. **Hobby or portfolio learner:** wants a personal project that can grow, without publishing or monetization pressure.
5. **Optional later track:** a beginner with academic or research curiosity may use causal models, but the course does not complete their academic work.

## User needs / proposed functions

| ID | Learner need | Course function | Evidence artifact |
| --- | --- | --- | --- |
| F-01 | I do not know where to begin | Scope a meaningful creative seed | World premise |
| F-02 | My ideas contradict each other | Specify rules and exceptions | World foundations sheet |
| F-03 | The setting feels empty or artificial | Connect rules to agents' everyday life | Lived-experience note |
| F-04 | I have disconnected lore categories | Relate systems and dependencies | System interaction map |
| F-05 | I do not know what happens next | Trace actions and world-state changes | Consequence map |
| F-06 | I cannot explain my world to others | Select an appropriate expressive format | Reader-facing artifact |
| F-07 | Revisions erase prior context | Keep a simple source of truth | Canon/decision register |
| F-08 | I run out of ideas after each finished piece | Use output as structured input | Second-cycle log |
| F-09 | I fear losing creative freedom | Separate provisional drafts from published facts | Version/status labels |
| F-10 | I know a creative technique but cannot tell where else it helps | Extract the reasoning pattern, adapt it to a small real-world problem and identify invalid assumptions | Bounded transfer note |
| F-11 | I follow examples but struggle with unfamiliar situations | Reframe a fresh scenario, compare alternatives, explain uncertainty and revise with feedback | Independent problem-solving trace |

## Use-case specifications

### UC-01 — Begin with one thought

- **Actor:** creator with a fragmentary idea.
- **Trigger:** wants a world but lacks a starting structure.
- **Flow:** observe interest → ask a what-if question → choose a small scope → articulate a premise → list possible consequences.
- **Done when:** learner can describe the world premise and say what is deliberately not yet designed.

### UC-02 — Diagnose conflicting rules

- **Actor:** creator whose notes disagree.
- **Flow:** identify both claims → determine scope (global/local/exception) → locate missing assumptions → revise or document an exception.
- **Done when:** apparent contradiction is either resolved or explicitly tracked as unresolved.

### UC-03 — Make the world feel inhabited

- **Actor:** creator with abstract environmental or magical rules.
- **Flow:** select one location → choose at least one agent → describe routine and an actual choice → connect routine to world rules.
- **Done when:** daily life is causally related to the setting, rather than generic decoration.

### UC-04 — Connect two systems

- **Actor:** creator with separate cultural, resource or governance facts.
- **Flow:** identify inputs → identify incentives/constraints → describe interactions → show a downstream effect.
- **Done when:** changing one system would produce a traceable effect in the other.

### UC-05 — Simulate a meaningful change

- **Actor:** creator unsure what happens next.
- **Flow:** capture initial state → introduce a decision/event → derive first and second-order effects → define changed state → ask a new question.
- **Done when:** the next idea depends demonstrably on the previous event.

### UC-06 — Share without exposition overload

- **Actor:** creator presenting to a peer.
- **Flow:** define audience question → choose scene/backstory/reference → reveal only necessary facts → obtain feedback.
- **Done when:** another reader can summarize one relevant causal relationship without memorizing an encyclopedia.

### UC-07 — Resume creative work after a break

- **Actor:** creator revisiting older notes.
- **Flow:** read source-of-truth summary → check canon statuses → inspect last changed state → choose one open loop.
- **Done when:** learner independently chooses a defensible next step.

### UC-08 — Grow beyond the first world

- **Actor:** graduate applying the method again.
- **Flow:** abstract method from first project → begin new seed or expand existing one → rerun a smaller cycle.
- **Done when:** method transfers without reproducing Asthortera or the tutorial example.

## Context-first discovery and first useful action

The learner personas are **hypotheses**, not verified needs of specific people. When necessary ask only: “Where does your world idea stop developing?”

| Situation | Human question | Smallest evidence |
| --- | --- | --- |
| Disconnected ideas | What changes when two ideas meet? | One explained consequence |
| Contradictory rules | Which rule actually applies? | One valid boundary/exception |
| Empty-feeling world | Who lives with this condition? | One everyday choice |
| No next step | What remained different after the last event? | S0 → event → S1 → new question |
| Communication difficulty | What does the audience need to know now? | One small scene or record |

**UC-09: independent first try.** Select a seed, one limit, interacting elements, consequence, changed state and next question, then keep a short note. This is a **proposed use case**, not a claim of a live interface. No account, AI, paid mentor, long novel or public sharing is needed for the conceptual practice. Polite interest is not proof of adoption, payment intent or testimonial consent.

## UC-10 — Apply a mental model outside fictional worldbuilding (proposed)

- **Actor:** learner seeking practical relevance beyond fiction, not presumed to hold specialist credentials.
- **Trigger:** a safe everyday problem such as a study schedule that fails when a dependency changes, conflicting responsibilities in a group activity, or communicating a plan to a peer.
- **Flow:** (1) describe the actual context, (2) select a mental model practiced in worldbuilding, (3) identify what maps and what does not, (4) collect or request needed real evidence, (5) propose two bounded options, (6) choose a reversible low-risk test or a justified decision to defer, (7) reflect on observed results.
- **Done when:** the learner gives a usable reasoning trace including **one invalid analogy or unknown**, not merely renames fictional variables.
- **Not assumed:** business success, clinical/financial/legal expertise, adoption of a particular ideology or guaranteed skill transfer.

## UC-11 — Diagnose a problem rather than decorate its description (proposed)

A learner distinguishes symptom from mechanism, actors from assumptions, and immediate effects from downstream effects. They produce a concrete problem statement, a causal hypothesis with stated uncertainty, and an action that could test or falsify it. A small fictional setting provides initial practice; a second, unfamiliar low-risk scenario checks whether the mental model can be **adapted**, not memorized.

**Audience protection:** these use cases are optional beginner extensions until piloted, and should never replace worldbuilding with a generic productivity or professional certification course.

## Service and learner-agency boundaries

Paper, diagrams, plain-text/Markdown and accessible tools are valid. No account, instructor call, camera, AI subscription or purchased software is a conceptual prerequisite. Mentorship and commercial offerings, if any, are separate decisions requiring evidence and authorization. Independent learner agency is the target; dependence is not an upsell strategy.

## Negative use cases

- Learner should **not** be required to build a planet-sized universe to pass.
- Learner should **not** be told an invented world rule is scientifically proven.
- Learner should **not** have their own lore promoted as Asthortera canon.
- Course should **not** promise publication, popularity, sales, mental-health treatment or guaranteed anti-burnout results.
