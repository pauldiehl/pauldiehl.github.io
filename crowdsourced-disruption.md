# CrowdSourced Disruption

**Status:** Thought experiment / working doc
**Author:** Paul Diehl
**Last updated:** 2026-03-19

---

## The Concept

A live, autonomous build system powered by crowdsourced intent. One DIAB node. One Forkless instance. A coordinating agent. Subagents. A live stream. The crowd provides the *what*, the node provides the *how*, governance provides the *guardrails*.

Set it off and walk away. Come back to something that didn't exist before.

---

## The Setup

A child AWS account (isolated, budget-capped) running a DIAB node with a VERY OPEN Forkless configuration. The node is pointed at a general objective — disrupt a specific industry, build a specific class of system, solve a specific problem. The stream goes live. The audience contributes.

**Three agents minimum:**

1. **The Coordinator** — triages incoming prompts from the crowd. Validates against governance protocols. Ranks by merit. Dispatches to the build queue. This is the brain.

2. **The Builder(s)** — subagents dispatched by the Coordinator. Each picks up a queued task, builds it, tests it, deploys it. Could be many running in parallel. This is the workforce.

3. **The Narrator** — constantly demoing what's been built. Walks through completed artifacts. Shows what's on deck. Explains why certain prompts were accepted or rejected. Generates the live stream content. This is the voice.

---

## Core Standards

### Meritocracy

Ideas rise on quality, not on who submitted them. The Coordinator evaluates each prompt against:

- **Alignment:** Does this serve the stated objective?
- **Feasibility:** Can a subagent build this with available tools?
- **Non-conflict:** Does this contradict something already built or in-queue?
- **Novelty:** Is this adding something new vs. restating what exists?
- **Specificity:** Is this actionable or is it vague hand-waving?

Scoring is transparent. The audience sees why things get accepted or rejected.

### Radical Transparency

- All code generated is visible in real-time
- All agent decisions are logged and explainable
- The Driftboard shows every work item's status
- Rejected prompts get a reason, not silence
- Architecture decisions are narrated as they happen

### Decision-Making Algorithms

The Coordinator doesn't just accept/reject — it *sequences*. Some good ideas need to wait because a dependency hasn't been built yet. Some ideas are good individually but conflict in aggregate. The decision tree:

```
Incoming prompt
  → Governance check (hard pass/fail against protocols)
  → Alignment scoring (0-1 against objective)
  → Conflict detection (against in-progress and completed work)
  → Dependency analysis (what needs to exist first?)
  → Merit ranking (composite score)
  → Queue position assignment
  → Dispatch when ready
```

### Governance Controls (The "CRAZY Good" Part)

This is the sealed-tight layer. Non-negotiable constraints:

- **Budget ceiling** — child AWS account has hard spend limits. Period.
- **No secrets in code** — nothing generated can contain API keys, credentials, PII
- **No destructive operations** — agents can create and modify, never delete infrastructure
- **Scope boundary** — the objective defines a domain. Nothing outside it gets built.
- **Rate limiting on prompt intake** — prevents flooding/spam
- **Human circuit breaker** — Paul (or designee) can pause the entire system at any time
- **Artifact sandboxing** — live artifacts are read-only for the audience. No write access.
- **Agent permission boundaries** — subagents can write code, deploy to the child account. They cannot modify governance, the coordinator, or the stream infrastructure.

---

## The Stream — Three Layers Live

**Platform:** Twitch (or YouTube Live, or both)

**What the audience sees is the three-layer stack composited in real-time:**

```
┌─────────────────────────────────────────────┐
│  FORKLESS (Agent Layer)                      │  Chat bubble + Narrator
│  ┌─────────────────────────────────────────┐ │  commentary on top
│  │ DRIFTBOARD (Planning Layer)             │ │  Transparent card overlay
│  │ ┌─────────────────────────────────────┐ │ │  showing pipeline state
│  │ │ PRODUCT (Transaction Layer)         │ │ │  The actual app being
│  │ │ The thing being built, live         │ │ │  built underneath
│  │ └─────────────────────────────────────┘ │ │
│  └─────────────────────────────────────────┘ │
└─────────────────────────────────────────────┘
```

The Narrator agent controls what's visible. In overview mode: all Driftboard cards visible over the product. In demo mode: single focused card expanded, product visible beneath, Narrator explaining what the subagent built. Cards appear, get discussed, get dismissed. The stream IS a Driftboard walkthrough.

### Participation Levels — The Trust Gradient

Not everyone participates at the same depth. Each level requires giving more, and gets more:

| Level | Friction | What They Give Up | What They Get |
|-------|----------|-------------------|---------------|
| **Twitch Viewer** | Zero | Nothing | Watch the stream. See the board. Learn. |
| **Twitch Chatter** | Minimal | Twitch account | `!idea` to submit to INTAKE. `!comment` on cards. Low trust weight. |
| **Registered User** | Medium | Email or SMS (OTP) | Access the actual product. Test artifacts. Comments have MORE WEIGHT. Can pick up validation tasks and human blockers. |
| **Trusted User** | Earned | Track record of quality contributions | Unblock items. Handle sensitive tasks. Validation counts as 1x. Grooming notes carry real weight. |
| **Founder** | N/A | Owns the algorithm | Priority bumps. Circuit breaker. Algorithm tuning. Not an "override" — a priority signal. |

The leap from Twitch viewer → registered user is the key moment. They leave the passive safety of the stream and enter the product. They give up an email or phone. In return: hands-on access, testing power, real influence. This is the no-gatekeeping principle — anyone CAN participate, but deeper access requires deeper commitment. The unspoken trust agreement flows both ways.

**What makes it compelling:**
- It's not a person coding. It's a system building itself from crowd input.
- The audience can USE the artifacts being built — they're live, accessible
- Registered users have real power — their testing and feedback shapes outcomes
- The feedback loop is minutes, not months
- It's 24/7 — the system doesn't sleep, doesn't eat, doesn't get tired
- People watching are simultaneously users, contributors, and evangelists

---

## The Driftboard View (Planning Layer)

Driftboard is the **Planning Layer** in the three-layer stack — a transparent overlay between the Forkless agent (top) and the product being built (bottom). In Crowd-Dis context, it's the primary stream visual.

Six fixed columns. Cards flow left to right as the Coordinator moves them:

```
INTAKE → QUALIFIED → GROOMING → BUILDING → VALIDATE → DONE
```

Display modes for the stream:

- **Full Board:** All columns, all cards. Overview of the entire pipeline. Default stream view.
- **Focused Card:** Single card expanded. Product visible beneath. Narrator demoing a specific feature.
- **Highlights Only:** Only VALIDATE items (calling for human testers) or only BUILDING items (showing active work).

The board canvas is transparent. Cards float over the actual product. The stream captures all three layers composited — Forkless chat on top, Driftboard cards in the middle, live product on the bottom.

See: `driftboard/DRIFTBOARD-V2-HANDOFF.md` for the full spec. Driftboard is its own project — broader than Crowd-Dis. It's the universal Planning Layer for any Forkless product.

---

## Why This Matters

This isn't a hackathon in the traditional sense. Nobody is staying up all night writing code. The system writes the code. The humans provide direction, taste, and judgment. The governance ensures nothing goes off the rails.

If it works — even partially — it proves the Milliprime thesis in the most dramatic way possible: one founder's architecture, powered by crowd intelligence, building something that none of them could build alone, running autonomously for hours or days.

If it fails, it fails transparently, on stream, and the failure itself is instructive.

---

## Open Questions

- [ ] What industry / problem to target for the first run?
- [ ] How long should the first run be? (Hours? Days? A full week?)
- [ ] Invite-only vs. open participation?
- [ ] How to handle prompt volume at scale? (What if 1000 people are submitting?)
- [ ] Should completed artifacts persist after the stream ends?
- [ ] Revenue model? (Tips? Subscriptions? Free as a proof of concept?)
- [ ] Legal: who owns the output? (Open source by default?)
- [ ] How to prevent the Coordinator from being gamed? (Adversarial prompt injection)
- [ ] Should there be "rounds" with themed objectives, or one continuous build?

---

## Ideas Parking Lot

*Add raw ideas here as they come. No filtering. That's the Coordinator's job.*

- The Narrator agent could have personality — make it entertaining, not just informative
- "Contributor of the hour" — highlight the person whose prompt had the most impact
- Spawn child journeys from accepted prompts (DIAB journey nesting pattern)
- The FAQ crystallization pattern could apply here — common prompt patterns get auto-accepted
- Could the audience VOTE on queued items? Democratic prioritization layer?
- What if the Driftboard itself is the first thing the system builds? Bootstrap paradox.
- Integration with Discord for deeper async discussion alongside the Twitch stream
- "Replay mode" — after the run, anyone can scrub through the full build timeline

---

## Technical Stack (Draft)

```
Infrastructure:
  - Child AWS account (isolated, budget-capped)
  - DIAB node (EC2 or ECS)
  - Forkless (VERY OPEN config — low gatekeeping threshold)

Agents:
  - Coordinator: Claude + governance protocols + merit scoring
  - Builders: Claude subagents with code execution (sandboxed)
  - Narrator: Claude + screen capture + TTS for stream narration

Stream:
  - OBS or similar → Twitch/YouTube
  - Driftboard as primary visual (web app, embedded in stream)
  - Chat integration (Twitch IRC → prompt intake pipeline)

Artifacts:
  - S3 static hosting for generated apps/sites
  - API Gateway for generated APIs
  - DynamoDB for state

Governance:
  - Protocol files (DIAB Layer 1)
  - Budget enforcement (DIAB operational pattern)
  - Human circuit breaker (admin endpoint)
```

---

*This doc is alive. Add to it freely. When it's time to build, this becomes the spec.*
