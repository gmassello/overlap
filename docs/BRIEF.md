# Overlap — Brief

## Summary
Every member of a family has their own agent that knows their taste through Qloo. On Friday night the agents trade parts of the plan with each other (the movie or outing, dinner, and music) until they agree on a full night out. A shared ledger of concessions makes the plan fair over the weeks.

## Problem frame
In families with teenagers, ages and tastes under one roof are far apart. A 17-year-old wants nightclubs and friends, a 13-year-old wants the Premier League match, and the parents want theater or a dinner out (`docs/IDEA.md:47`). Friday night ends in "I don't know, what do you want?", and the same person usually gives in. Today's group tools let people vote on a single movie. They don't build the whole night, and they don't remember who gave in last time (D1). No one has measured how much this costs a family (D4), so the need is argued from the demo scenario, not from data.

## Discovery
- D1. Several apps already solve "pick a movie as a group" by swiping until there is a match: Squadflick, WatchLitz, Swyf Together, and pickaru, which adds one veto and hidden votes. All of them cover one domain and decide by voting. None negotiates or remembers past nights. — https://news.fiu.edu/2019/computer-science-grad-creates-app-for-movie-nights · https://hunted.space/product/pickaru
- D2. MAGReS is an academic group recommender with one agent per user. The agents negotiate the item with the Monotonic Concession Protocol, and a 2025 extension weights members by trust. The mechanism has a precedent, but not as a consumer product. — https://mdpi.com/2504-2289/9/1/1
- D3. LLM agents asked to reach consensus mostly converge by averaging unless given explicit rules. A naive negotiation would flatten into "something everyone tolerates" and look like a chatbot. — https://arxiv.org/abs/2310.20151
- D4. I found no figures on how long groups take to decide or how often they give up. The closest result is a questionnaire that asks exactly that. — https://tally.so/r/0QKglA
- D5. Among the same hackathon's projects, explanations and "I don't like this" corrections already exist (Home2Here), and persistent memory exists only per individual (rajat552). Multi-agent negotiation with group memory is open (`docs/IDEA.md:98`).

## Impact
- **Persona**: a parent of two teenagers (13 and 17) planning Friday night for the family; `sin contactar`.
- **Pierde hoy**: Friday ends in "I don't know, what do you want?" and the same person gives in again.
- **La cifra**: `sin medir: no family has used it yet; the app records minutes from "start night" to an accepted plan and vetoes per night, readable from the health endpoint`.
- **Despues del evento**: four Fridays with three real families with teenagers.

## Safety
- **Accion irreversible**: `sin accion irreversible: the plan names places and times but never books or pays, and every memory entry can be removed`.

## Demo surface
- **Que ejecuta el jurado**: picks who is in from the preloaded family, starts Friday night, then taps "not that" on one part of the plan.
- **Que resultado nuevo sale**: a full plan negotiated live from current Qloo data and the concession ledger, and after the veto a replacement part with its own reason.
- **Que apuesta demuestra**: agents trade parts of the night instead of averaging, and fairness spans weeks: the tie goes to whoever gave in most before, not to the majority.
- **Donde**: the hosted demo URL in `PENDING.md` (Site row), pending deploy.

## Actors
- A1. Family member — talks to their agent once, then says yes or "not that" on Friday night.
- A2. Member's agent — holds the member's taste profile and memory, and argues for the member in the negotiation.
- A3. The group — the shared memory: which nights worked and the concession ledger.
- A4. Host — the family member who runs the shared screen and starts the night.

## Requirements
- R1. Each person has their own agent with a taste profile grounded in Qloo (`docs/IDEA.md:20`). [criterion: Technological Implementation]
- R2. The agents negotiate with each other, visibly and live, until they agree on a three-part plan: a movie or outing, dinner, and music (`docs/IDEA.md:20`, `docs/IDEA.md:24`). [criterion: Quality of the Idea]
- R3. Before negotiating, each agent measures through Qloo how close its person's taste is to the others' (`docs/IDEA.md:56`). [criterion: Technological Implementation]
- R4. Each part of the plan says why it was chosen, and for whom (`docs/IDEA.md:26`). [criterion: Design]
- R5. When any member says "not that", the plan is rebuilt (`docs/IDEA.md:27`). [criterion: Design]
- R6. Each agent remembers what its person accepted and rejected, and recent choices weigh more than old ones (`docs/IDEA.md:25`, `docs/IDEA.md:73`). [criterion: Quality of the Idea]
- R7. The group remembers which nights worked and how they went (`docs/IDEA.md:25`, `docs/IDEA.md:72`). [criterion: Potential Impact]
- R8. The demo keeps working when the Qloo API is down or out of quota (`docs/IDEA.md:66`, `docs/IDEA.md:83`). [criterion: Technological Implementation]
- R9. A member can join from their own phone with a link, follow the negotiation, and say "not that" from there. [criterion: Design]
- R10. A new member builds their profile by chatting with their agent, which anchors each stated taste to a Qloo entity. [criterion: Design]
- R11. A nightly process reviews the latest nights and consolidates each person's and the group's memory, so recommendations improve week after week. [criterion: Quality of the Idea]
- R12. If the agents don't agree within the round limit, the proposal of the member who has conceded most wins, and the app says so. [criterion: Quality of the Idea]
- R13. Agents negotiate by trading parts of the plan ("you pick the movie if I pick dinner"), not by averaging, and each concession is written to the group's ledger. [criterion: Quality of the Idea]
- R14. The demo makes the problem and the audience visible: a family with teenagers whose Friday night usually ends with the same person giving in. [criterion: Potential Impact]

## Key flows
- F1. **Onboarding** — a new member opens their profile → their agent asks a few questions about what they love → each answer is matched to a Qloo entity and confirmed → the profile is saved. (A1, A2; R1, R10)
- F2. **Friday night** — the host picks who is in → the agents measure their distance to each other → they trade parts of the plan in rounds, live on the shared screen → if there's no deal by the round limit, the ledger breaks the tie → the plan shows movie or outing, dinner, and music, each with its reason. (A4, A2, A3; R2, R3, R4, R12, R13, R14)
- F3. **"Not that"** — a member vetoes one part, on the shared screen or from their phone → only that part is renegotiated → the plan updates with a new reason, and the rejection goes to that member's memory. (A1, A2; R5, R6, R9)
- F4. **Nightly consolidation** — after a night, the process reviews what was chosen, rejected, and conceded → it updates each person's preferences, with recent choices weighing more, and the group's record of nights → the next Friday starts from that memory. (A3; R6, R7, R11)

## Acceptance examples
- AE1. **Covers R1, R10.** Given a new member who says "I love Messi and the Premier League", when the chat ends, then the profile lists the matching Qloo entities and the member can remove any of them.
- AE2. **Covers R2, R13.** Given four members with clashing tastes, when the night starts, then the screen shows at least one trade between two agents (one concedes a part of the plan to win another) before the final plan appears.
- AE3. **Covers R12.** Given a ledger where Lucía has conceded three times and nobody else more than twice, when the agents hit the round limit without a deal, then Lucía's proposal wins and the plan states that reason.
- AE4. **Covers R4.** Given a final plan, when the host looks at any of its three parts, then it shows which members it was chosen for and which of their tastes it matches.
- AE5. **Covers R5, R9, R6.** Given a final plan, when Tomás taps "not that" on dinner from his phone, then only dinner changes, the other two parts stay, and the rejected restaurant doesn't come back next week.
- AE6. **Covers R11, R7.** Given a past night where Carla rejected theater, when the nightly process runs, then the next night's proposals for Carla rank theater lower than before.
- AE7. **Covers R8.** Given the preloaded demo scenario and no network access to Qloo, when the night starts, then the full plan is produced from cached data and marked as such.
- AE8. **Covers R3.** Given Tomás (13, Premier League) and Carla (theater), when the night starts, then before the first round the screen lists how close each pair's tastes are according to Qloo, and the most distant pair is the first to trade.

## Key decisions
- Negotiation by trading parts of the plan — chosen over round-table discussion and red-lines-first because it avoids the averaging failure mode (D3) and makes the agents' trade-offs visible on screen. settled: user-approved
- Deadlock is broken by the concession ledger (whoever has given in most wins) — chosen over a moderator agent and over handing the choice back to the family because it is fair across nights and it is the one place group memory decides something. settled: user-approved
- Profiles are built by chatting with the agent — chosen over typing 3-5 favorites and over preloaded profiles only, because the agent learns how the person talks about their taste, and memory keeps improving it weekly. settled: user-directed
- A nightly process consolidates memory — the system improves week after week instead of only appending raw history. settled: user-directed
- Shared screen first, joining from a phone second — chosen over phone-only so a judge can try the whole product alone. settled: user-approved
- Audience: families with teenagers — chosen over groups of friends and over "any group" because the age gap creates a visible, specific tension. settled: user-approved
- A demo video and a landing page ship even though the rules don't require them (`docs/HACKATHON.md`, § 6). settled: user-directed

## Scope boundaries
### Deferred
- Large groups that are clustered by affinity before negotiating (`docs/IDEA.md:33`). The demo uses 3 or 4 people (`docs/IDEA.md:32`).
- Booking tickets or tables. The plan names places and times but doesn't reserve them.
### Outside this product
- A recommender for one person alone (`docs/IDEA.md:98`) — with one person there is nobody to trade with, so the negotiation has no reason to exist.
- Voting or swiping on a single movie (D1) — a vote picks one item and forgets; this product builds the whole night and remembers who gave in.

## Assumptions
- Families with teenagers feel this pain often enough to open an app on Friday night. No data backs it (D4). If false, the pitch leans on fairness over time rather than on frequency.
- The demo family comes preloaded with a history of past nights, so the ledger already has concessions and a judge sees the tie-break without setting anything up. If false, AE3 can't be shown in the first session.
- The nightly process can also be triggered by hand ("run tonight's review now"). Otherwise a judge can't see the system learn within one session.
- A "not that" reopens only the vetoed part, not the whole plan. If the family expects a full reshuffle, F3 changes.
- Qloo's taste data is rich enough to tell a 13-year-old's and a parent's taste apart. If not, R3 measures a distance that doesn't drive the negotiation.

## Outstanding questions
- How many rounds before the ledger breaks the tie? — blocks: R12 | resolve before planning: no
- Is a "not that" from a phone instant, or confirmed by the host? — blocks: R9 | resolve before planning: no
