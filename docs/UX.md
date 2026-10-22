# Overlap — UX

Design mode: there is no UI yet. User, job and criteria come from `docs/BRIEF.md`; the demo flow details F2 and F3.

## User & job

- **Who**: the host of a family with teenagers (A4), running the shared screen, and each family member (A1), who says yes or "not that".
- **Job**: when Friday night comes and nobody agrees, I want our agents to work it out fairly, so the same person doesn't always give in.
- **Criteria it attacks**: Quality of the Idea (R2, R12, R13), Technological Implementation (R1, R3, R8), Design (R4, R5, R9) and Potential Impact (R7, R14).

## Demo flow

Details F2 (Friday night) and F3 ("Not that"). There is no login, no setup, and the family is preloaded with four past Fridays. The judge clicks twice.

1. **Tonight** opens on the preloaded family: Lucía (17), Tomás (13), Carla and Martín, all checked. A single line from the concession ledger sets the tension: "Lucía gave in 3 of the last 4 Fridays." There is one primary CTA, `Plan Friday night`. *(R14)*
2. **Click 1.** The agents measure through Qloo how close each pair's tastes are. They appear as one bar per pair, sorted from most distant to closest, before the first round. *(R3, AE8)*
3. **Live rounds.** Each trade appears as a chat bubble between two agents ("You take the movie, I pick dinner"). A progress line reads "Round 2 of 5". If no deal is reached by the round limit, the ledger breaks the tie and the screen states why. *(R2, R13, R12, AE2, AE3)*
4. **Peak: the plan.** Three cards, Movie or outing · Dinner · Music. Each one names who it was chosen for and which of their tastes it matches. *(R4, AE4)*
5. **Click 2: the judge taps `Not that` on one card.** This is `Que ejecuta el jurado` in the brief's Demo surface. *(R5)*
6. **End.** Only that part is renegotiated, and the other two cards stay put. The new card arrives with its own reason, and the ledger records the veto: "Tomás said not that to dinner — noted for next Friday." This is the result the judge produced, which did not exist before the click. *(R5, R6, AE5)*

## Information architecture

Navigation is by task, with three tabs. **Tonight** comes first and is the landing screen.

| Screen | Seen first | Behind a control (progressive disclosure) | Covers |
|---|---|---|---|
| **Tonight** | the family with who's in, the ledger line, `Plan Friday night`; then affinities → rounds → plan | the full transcript of each round (`See all rounds`) | F2, F3 |
| **Family** | one card per member with their Qloo entities | `Add a member` (chat with the agent, F1); `Join from phone` (link + QR, R9) | F1, R1, R10, R9 |
| **Memory** | past nights, with what was chosen and who gave in; the concession ledger | `Run tonight's review now` (F4, manual trigger) and what changed in each profile | F4, R6, R7, R11 |

- A top bar holds the three toggles: language (EN/ES), theme (light/dark) and register (plain/technical). Register starts in plain.
- When a plan came from cached data instead of the live Qloo API, a `cached data` badge appears next to it (R8, AE7).

## States

| Screen | Loading (> 400 ms) | Empty | Error | Success |
|---|---|---|---|---|
| Tonight | visible steps: "Measuring tastes with Qloo…", "Round 2 of 5…", streamed bubble by bubble | fewer than two members checked: CTA disabled, hint "Pick at least two people for tonight." | the agents fail mid-negotiation: "The negotiation stopped. Start again — your picks are kept." The checked members are kept | the three-card plan; after a veto, the replaced card is highlighted once |
| Tonight (Qloo down) | same steps | — | no error screen: the plan is built from the cache and carries `cached data` | plan with the badge |
| Family | "Matching your answer to Qloo…" while the onboarding chat runs | no members: "No one here yet. Add the first member to start." + `Add a member` | no Qloo match for an answer: "I couldn't find that one. Try another way to say it, or skip it." | profile saved with its entities, each removable (AE1) |
| Family (phone) | "Joining tonight…" | — | link expired: "This link is from another night. Ask the host for a new one." | the phone follows the rounds and offers `Not that` |
| Memory | "Reviewing the last nights…" while the review runs | no nights yet: "No Fridays yet. Plan the first one in Tonight." | review failed: "The review didn't finish. Your memory is unchanged — try again." | per member, what moved up or down (e.g. theater ranked lower for Carla, AE6) |

## Copy

Keys of the copy table, English base. A `_tech`/`_plain` suffix appears only where the register changes; plain is the default and the video narration.

| Key | English |
|---|---|
| `tab_tonight` / `tab_family` / `tab_memory` | Tonight / Family / Memory |
| `tonight_cta` | Plan Friday night |
| `tonight_need_two` | Pick at least two people for tonight. |
| `ledger_line` | {name} gave in {n} of the last {m} Fridays. |
| `affinity_title_plain` | How close are your tastes? |
| `affinity_title_tech` | Pairwise taste affinity (Qloo) |
| `affinity_step` | Measuring tastes with Qloo… |
| `round_label` | Round {i} of {n} |
| `trade_bubble` | You take the {part}, I pick {part} |
| `tiebreak_plain` | No deal after {n} rounds. {name} has given in most, so {name}'s pick wins. |
| `tiebreak_tech` | Round limit reached; ledger tie-break: {name} ({k} concessions) |
| `plan_part_movie` / `plan_part_dinner` / `plan_part_music` | Movie or outing / Dinner / Music |
| `plan_reason_plain` | For {names}: they love {taste}. |
| `plan_reason_tech` | Matches {entity} in {names}'s profile (affinity {score}) |
| `veto_cta` | Not that |
| `veto_note` | {name} said not that to {part} — noted for next Friday. |
| `cached_badge` | cached data |
| `rounds_more` | See all rounds |
| `negotiation_error` | The negotiation stopped. Start again — your picks are kept. |
| `member_add` | Add a member |
| `member_empty` | No one here yet. Add the first member to start. |
| `onboarding_question` | What do you love? A movie, a team, a band, a food. |
| `onboarding_matching` | Matching your answer to Qloo… |
| `onboarding_no_match` | I couldn't find that one. Try another way to say it, or skip it. |
| `phone_join` | Join from phone |
| `phone_expired` | This link is from another night. Ask the host for a new one. |
| `review_cta` | Run tonight's review now |
| `review_running` | Reviewing the last nights… |
| `review_error` | The review didn't finish. Your memory is unchanged — try again. |
| `memory_empty` | No Fridays yet. Plan the first one in Tonight. |

The concept names stay the same everywhere: "Not that" (never "veto" in the UI), "concession ledger" only in `_tech` keys (plain says "gave in"), and the three plan parts.

## Heuristics check

| # | Heuristic | Where it is met | Gap |
|---|---|---|---|
| 1 | Visibility of system status | Tonight steps 2–3: "Measuring tastes with Qloo…", "Round i of n", streamed bubbles; `cached data` badge | — |
| 2 | Match between system and real world | plain register by default: "gave in", "Not that", "How close are your tastes?" | entity IDs and scores only in `_tech` |
| 3 | User control and freedom | step 5: `Not that` reopens one part; each Family entity is removable (AE1) | no cancel during the rounds; add `Stop` if a run takes over 20 s |
| 4 | Consistency and standards | one name per concept (Copy, last paragraph) | — |
| 5 | Error prevention | `Plan Friday night` disabled with fewer than two members; preloaded family | — |
| 6 | Recognition rather than recall | the ledger line and each card's "for whom" are on screen; no IDs to remember | — |
| 7 | Flexibility and efficiency of use | N/A: a two-click demo has no repeat users to serve shortcuts to | — |
| 8 | Aesthetic and minimalist design | Tonight shows one CTA; the round transcript is behind `See all rounds` | — |
| 9 | Recognize, diagnose, recover from errors | every error in States follows `<what happened>. <what to do>.` and keeps the picks | — |
| 10 | Help and documentation | in-context: empty states and `onboarding_question` give the example | no help page, on purpose |

## Out of scope

- Login and accounts: the demo family is open to everyone.
- Booking or paying for tickets or tables (brief, Deferred).
- Groups larger than four.
- Editing the concession ledger by hand: it only changes through nights.
- Push notifications.
- An onboarding tour or modal before the first click.
