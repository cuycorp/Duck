# Product Definition

**Project:** Focus Companion  
**Status:** Pre-build  
**Version:** 0.1

---

## 1. Problem

People performing deep-focus work can experience thoughts unrelated to their current task. These thoughts may be:

- ideas;
- reminders;
- questions;
- concerns;
- future tasks;
- things they want to investigate;
- memories;
- reflections;
- unrelated distractions.

Trying to hold onto these thoughts in working memory can compete with attention devoted to the current task. Acting on them immediately can also interrupt the current workflow.

Ignoring them presents another problem: useful ideas, reminders, or observations may be forgotten.

The product provides a low-friction way to **temporarily externalize these thoughts without leaving the current task**, allowing the user to return to their work and review the captured thoughts later.

There is a second, longer-term problem:

> After a focus session, people may have little visibility into what thoughts appeared during their work, what repeatedly interrupted their attention, or which ideas emerged during the session.

The product therefore has two distinct moments of value:

```text
DURING FOCUS

"Get this thought out of my head
without leaving what I'm doing."


AFTER FOCUS

"What thoughts appeared during
this session, and what can I learn
from them?"
```

### Product perspective

The product does **not** treat distraction as inherently bad.

A thought that interrupts a task may be:

- irrelevant noise;
- an important reminder;
- a useful idea;
- a question worth investigating;
- a concern;
- a future task;
- or something personally meaningful.

The product therefore aims to **separate thoughts from the current task**, rather than eliminate or suppress them.

---

## 2. Target User

### Primary user

Students and knowledge workers who regularly perform cognitively demanding work and intentionally use uninterrupted or deep-focus sessions.

Examples include:

- software developers;
- researchers;
- students;
- engineers;
- writers;
- designers;
- people studying for exams;
- other professionals performing sustained cognitive work.

### User characteristics

The target user:

- intentionally creates periods of focused work;
- experiences thoughts unrelated to their immediate task;
- does not necessarily want to act on those thoughts immediately;
- wants to preserve useful ideas and reminders;
- values returning to their current task quickly;
- may be interested in understanding their own patterns of distraction.

### Important product assumption

Distraction is **not necessarily a problem to eliminate**.

The product treats thoughts as information that can be temporarily separated from the current task and reviewed later.

---

## 3. Core Hypothesis

### Primary hypothesis

> **If people can capture an emerging thought quickly, without significantly interrupting their current activity, they can return to their task more easily than if they have to keep the thought in working memory or act on it immediately.**

### Secondary hypotheses

**H2 — Thought preservation**

> Capturing thoughts helps users recover ideas, reminders, questions, and other information that might otherwise be forgotten.

**H3 — Pattern discovery**

> Reviewing captured thoughts allows users to identify recurring patterns in what interrupts their focus.

**H4 — Continued value**

> Users perceive enough value from capturing and reviewing thoughts that they voluntarily use the product again during subsequent focus sessions.

These are hypotheses to be tested, not claims that the product has already demonstrated.

---

## 4. Product Principles

### 4.1 Return to focus, don't create another distraction

The application should require as little attention as possible.

Consequences:

- global keyboard shortcut;
- keyboard-first interaction;
- minimal overlay;
- no navigation during capture;
- no mandatory categorization;
- immediate dismissal after submission.

The application should help the user **return to their task**, not become another productivity application demanding attention.

---

### 4.2 Capture before interpretation

Capturing a thought should be easier than understanding or organizing it.

The initial interaction should not require the user to decide:

```text
What category is this?
What project does it belong to?
What is its priority?
Should this become a task?
When should I do it?
```

Instead:

```text
Thought
  ↓
Captured
  ↓
Return to work
```

Organization and interpretation can happen later.

---

### 4.3 Thoughts are information, not noise

The product should not assume that every distraction is undesirable.

A thought may be:

```text
idea
reminder
question
concern
task
reflection
memory
unrelated distraction
```

The application should preserve the user's ability to determine what the thought means.

---

### 4.4 User remains in control

The user decides:

- what to capture;
- what to retain;
- what to review;
- what to categorize;
- what to delete;
- whether additional analysis is performed.

The product should not automatically make psychological or productivity-related interpretations about the user.

---

### 4.5 Private by default

Thoughts can be personal and sensitive.

The default architecture should therefore keep captured information on the user's machine.

The product should not require:

- an account;
- cloud synchronization;
- external APIs;
- telemetry;
- remote storage.

---

### 4.6 Evidence before complexity

New functionality should be introduced when experiments, user feedback, or observed problems demonstrate that it provides value.

Examples:

Do not add AI classification simply because AI is technically interesting.

Instead:

```text
Users struggle to organize captured thoughts
        ↓
Investigate the problem
        ↓
Design an experiment
        ↓
Determine whether automatic classification
actually reduces friction
        ↓
Only then consider implementation
```

The product should prefer a small, validated feature over a technically impressive feature that solves no demonstrated problem.

---

## 5. Core Interaction

The core interaction is the smallest loop through which the product delivers its primary value.

### During a focus session

```text
Start focus session
        ↓
User works
        ↓
A thought appears
        ↓
User presses global shortcut
        ↓
Minimal overlay appears
        ↓
User captures the thought
        ↓
Thought is saved locally
        ↓
Overlay disappears
        ↓
User returns to the task
```

### Example

```text
User is writing code.

A thought appears:

"I need to investigate that database
error later."

User presses the configured shortcut.

┌──────────────────────────────────┐
│                                  │
│  What's on your mind?            │
│                                  │
│  investigate database error...   │
│                                  │
│                         Enter ↵  │
└──────────────────────────────────┘

User presses Enter.

The thought is saved.

The overlay disappears.

The user continues coding.
```

### Interaction requirements

The capture interaction should be:

- **Fast** — ideally completed within a few seconds.
- **Keyboard-first** — the user should not need to reach for the mouse.
- **Interruptible** — Escape should cancel the interaction.
- **Non-blocking** — the user should not be moved away from their current application.
- **Low cognitive load** — no decisions should be required during capture.
- **Temporary** — the overlay should disappear immediately after capture.
- **Private** — no network request should be required.

---

## 6. Secondary Interaction: Session Review

After a focus session, the user can review the thoughts captured during that session.

```text
Focus session
      ↓
Session ends
      ↓
Session summary
      ↓
Captured thoughts
      ↓
Review / categorize / delete
```

A future session review might look like:

```text
Focus session — 09:30 → 10:45

Captured thoughts: 7

09:43  💡 Idea
       "Could simplify the parser by..."

10:02  📌 Reminder
       "Reply to Alex"

10:17  ❓ Question
       "Why does this implementation..."

10:31  🧠 Reflection
       "I may be overcomplicating..."
```

This functionality is secondary to the MVP capture interaction.

---

## 7. MVP

The MVP validates the fundamental interaction:

```text
Start focus session
        ↓
Press global shortcut
        ↓
Overlay appears
        ↓
Type thought
        ↓
Press Enter
        ↓
Thought saved locally
        ↓
Overlay disappears
        ↓
Continue working
```

### MVP data model

The minimum conceptual model is:

```text
FocusSession
├── id
├── started_at
└── ended_at

Thought
├── id
├── session_id
├── created_at
└── content
```

A future `category` field may be introduced, but categorization should not be required during capture.

### MVP capabilities

The first usable version should provide:

- start a focus session;
- end a focus session;
- configure a global keyboard shortcut;
- display a floating overlay;
- enter a thought;
- save the thought locally;
- dismiss the overlay after capture;
- associate the thought with the active focus session;
- review captured thoughts for the current session;
- delete a captured thought.

### MVP success condition

A user should be able to install and launch the application, start a focus session, capture several thoughts while working in another application, return to the task after each capture, and review the captured thoughts at the end.

---

## 8. Non-Goals

The following are deliberately outside the MVP.

### Infrastructure

- Cloud synchronization.
- User accounts.
- Remote database.
- Backend API.
- External API dependencies.
- Multi-device synchronization.

### Media

- Screen recording.
- Audio recording.
- Webcam recording.
- Automatic transcription.

### Productivity features

- Productivity scores.
- Productivity rankings.
- Gamification.
- Streaks.
- Achievement systems.
- Notifications designed to bring the user back to the application.
- Calendar integration.
- Automatic task management.

### AI

- Automatic thought classification.
- AI-generated psychological analysis.
- AI-generated productivity scores.
- AI coaching.
- Automatic recommendations.

AI may become a future experiment, but it is not required to validate the core product.

### Health

The application will not make:

- medical claims;
- therapeutic claims;
- diagnoses;
- claims about treating attention disorders;
- claims about improving mental health.

The project investigates a productivity/focus interaction, not a medical intervention.

### Behavioral control

The application will not attempt to:

- block distracting websites;
- prevent users from using other applications;
- monitor user behavior continuously;
- judge whether a thought is "good" or "bad";
- force the user to return to work.

The user remains in control.

---

## 9. Success Metrics

The initial metrics should help determine whether the product's core hypothesis is worth pursuing rather than assume that it is already correct.

### 9.1 Primary metric — Capture-to-return time

Measure the duration of the capture interaction:

```text
Overlay opens
      ↓
Thought submitted
      ↓
Overlay closes
```

This measures how much interruption the product itself introduces.

The desired direction is to minimize unnecessary interaction time.

---

### 9.2 Session metrics

Record descriptive session information such as:

- session duration;
- number of thoughts captured;
- thoughts per hour;
- time between captures;
- number of completed sessions;
- number of cancelled captures.

These metrics should not automatically be interpreted as positive or negative.

For example:

> More captured thoughts does not necessarily mean a better product.

---

### 9.3 User-reported return-to-focus

After a session, ask:

> **How easy was it to return to your task after capturing a thought?**

Example scale:

```text
1 — Very difficult
2 — Difficult
3 — Neutral
4 — Easy
5 — Very easy
```

---

### 9.4 User-reported usefulness

Ask:

> **Did capturing the thought help you stop thinking about it while working?**

Again, use a simple 1–5 scale.

---

### 9.5 Retention / repeated use

Measure:

> **How often does a user voluntarily start another focus session?**

This helps determine whether the interaction provides enough perceived value to become part of a user's workflow.

---

### 9.6 Future experiments

Potential experiments include:

#### Experiment A — Complete thought vs. categorical capture

Compare:

```text
"Type the thought..."
```

against:

```text
What type of thought?

[Idea] [Reminder] [Question] [Other]
```

Question:

> Can users obtain enough value from categorical capture without spending time writing the complete thought?

---

#### Experiment B — Overlay interaction

Compare different overlay designs and measure:

- capture time;
- cancellation rate;
- perceived interruption;
- perceived usability.

---

#### Experiment C — Capture vs. no capture

Compare a focus session in which users ignore emerging thoughts with a session where they capture them.

Potential measurements:

- perceived disruption;
- perceived ability to return to the task;
- recall of the thought afterward;
- perceived usefulness.

The experiment should be treated as exploratory rather than evidence of a medical or psychological effect.

---

## 10. Privacy Principles

### 10.1 Local-first

Captured thoughts are stored locally on the user's computer.

The MVP does not require cloud infrastructure.

---

### 10.2 No telemetry

The application does not send usage analytics to a remote service by default.

---

### 10.3 No account

The user can use the application without creating an account.

---

### 10.4 No external API

The MVP does not depend on an external API.

---

### 10.5 No thought leaves the computer

Captured thought content remains local.

If a future feature requires external processing, that feature must explicitly communicate what information is being transmitted and require appropriate user consent.

---

### 10.6 Minimal data collection

Only information required to provide the product should be stored.

For the MVP this primarily means:

```text
focus session
thought
timestamp
```

---

### 10.7 User-controlled deletion

Users should be able to delete captured thoughts and sessions.

---

### 10.8 No content analysis during capture

The initial interaction should avoid requiring the application to understand the user's thought.

The product should first validate whether **fast externalization itself** provides value.

Automatic classification or semantic analysis can be evaluated later.

---

## 11. Technology Constraints

### Platform

The initial implementation targets:

> **Linux + X11**

This minimizes platform-specific complexity during the first implementation.

Wayland compatibility is intentionally deferred until the core interaction has been validated.

---

### Primary language

**Python**

Python is the primary language for:

- application logic;
- domain logic;
- storage;
- testing;
- desktop integration.

---

### Desktop UI

**PySide6 / Qt for Python**

Used for:

- desktop windows;
- floating overlay;
- keyboard interaction;
- animations;
- system tray;
- window management.

---

### Persistence

**SQLite**

SQLite is the initial persistence layer because it:

- requires no server;
- is local-first;
- has no infrastructure overhead;
- is well supported by Python;
- is sufficient for the expected MVP data volume.

---

### Development tooling

Recommended:

```text
Python
PySide6
SQLite
pytest
Ruff
uv
PyInstaller
Git
GitHub Actions
```

All technologies should be free/open-source or available under free/open-source usage terms appropriate for the project.

---

### Architecture principles

The application should:

- remain local-first;
- avoid unnecessary infrastructure;
- keep domain logic independent from UI code;
- isolate Linux-specific functionality;
- keep the application testable without requiring the graphical interface wherever possible;
- avoid introducing dependencies without a clear product or engineering reason.

A conceptual structure:

```text
focus-companion/
│
├── app/
│   ├── ui/
│   │   ├── overlay.py
│   │   ├── session_view.py
│   │   └── settings_view.py
│   │
│   ├── domain/
│   │   ├── thought.py
│   │   └── focus_session.py
│   │
│   ├── services/
│   │   ├── focus_session.py
│   │   └── thought_capture.py
│   │
│   ├── storage/
│   │   ├── database.py
│   │   └── repositories.py
│   │
│   └── system/
│       ├── hotkeys.py
│       └── window_manager.py
│
├── tests/
│
├── docs/
│   ├── PRD.md
│   ├── ONBOARDING.md
│   ├── ARCHITECTURE.md
│   ├── PRIVACY.md
│   ├── ADR/
│   └── experiments/
│
├── pyproject.toml
├── README.md
└── uv.lock
```

---

## 12. Product Boundary

The product can be summarized as:

> **A local-first focus companion that lets users quickly externalize distracting thoughts, return to their current task, and review those thoughts after a focus session.**

The product does not attempt to eliminate distraction.

It helps the user **separate distraction from action**.

### Core product loop

```text
THOUGHT
   ↓
CAPTURE
   ↓
RETURN
   ↓
CONTINUE
   ↓
REVIEW
   ↓
UNDERSTAND
```

The MVP validates the first four stages.

The later stages are developed only when there is evidence that they provide additional value.