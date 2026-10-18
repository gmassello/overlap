# Overlap — Qloo Agentic Hackathon

> Project brief to kick off in Claude Code. Collects everything we defined up to Oct 18, 2026.

## The hackathon

- **Event:** Qloo Agentic Hackathon — https://qloo.devpost.com/
- **Deadline:** Sat Oct 31, 2026, 00:45 ART (Oct 30, 11:45 pm ET)
- **Prizes (all cash):** US$15,000 / 6,000 / 4,000
- **Eligibility:** Argentina is eligible. Must be of legal age. Solo participation allowed.
- **Hard requirements:**
  - Use the **Qloo API**. Access is requested through the Google Form linked in the rules.
  - It must be **agentic**: any agentic tool or agent framework you like.
  - Public **open source repo**.
  - **Working demo.**
- Language and model: free choice per the rules.

## The idea

A family (or a group of friends) wants to decide what to do on Friday night. Each person has **their own agent**, with a taste profile built from the Qloo API. The agents **negotiate with each other** until they agree on a full plan for the night: a movie or outing, a place for dinner, and music.

### What sets it apart

1. **Agent-to-agent negotiation**, shown live in the demo. Nobody in the hackathon is doing multi-agent negotiation.
2. **Group memory:** each agent remembers what its person accepted and rejected on previous outings, and the group remembers which nights worked. There is one project with persistent memory (rajat552), but it is individual.
3. **Explanation for each choice:** why each part of the plan was picked.
4. **Live correction:** when someone says "not that", the plan is rebuilt.

### Scale

- No technical limit on the number of people.
- **Demo with 3 or 4 people**, so the negotiation is easy to follow, responses are fast, and the API quota doesn't blow up.
- For large groups: cluster by affinity before negotiating.

## Demo scenario: family of four, Friday night

> Fictional family profiles.

| Person | Age | Tastes |
|---|---|---|
| **Lucía** | 17 | Gym, going out with friends, nightclubs, movies. Everything Apple. Speaks English very well. Very responsible. |
| **Tomás** | 13 | Programming. Hangs out with school friends. Studies English. Football, especially European: Premier League, idol Messi. |
| **Carla** | adult | Tennis, pilates, theater, music and singing (takes lessons), family and friends. |
| **Martín** | adult | Gym, running, restaurants, theater, movies. |

**Common ground to start with:** movies (Lucía, Martín), theater (Carla, Martín), gym (Lucía, Martín).
**Useful tension for the demo:** the teenager who wants nightclubs and friends versus the family plan, and the 13-year-old with the Premier League match.

## Qloo API

- **Hackathon base URL:** `https://hackathon.api.qloo.com/v2`
- **Auth:** `X-Api-Key` header
- **Main endpoints:**
  - **Insights:** the core. You pass input tastes and it returns recommendations filtered by type: movies, places, music, books, TV shows, and more.
  - **Search:** from text ("Los Simuladores") to Qloo's internal ID.
  - **Compare:** compares two sets of tastes and shows overlaps and differences. **It's the basis of the negotiation:** each agent measures how far it is from the others before negotiating.
  - **Audiences / Trending:** audience profiles and trends.
- **Quota:** there is a call limit for the hackathon; the exact number isn't published.
- **TypeScript SDK (optional):** `@devma/qloo`. Not official, it's community-made (manasseh-zw). Points to the hackathon by default. **Check that it has Compare**; if not, Compare goes through direct HTTP.
- **Official starter kit:** on Qloo's GitHub account (github.com/qloo). I don't know the exact repo name, only the description: "starter kit for building taste-powered…". Review it before starting.

## Qloo access from the agents

- Agents query through **qloo-mcp** — https://github.com/NoBanks/qloo-mcp (MIT).
- **Watch out:** qloo-mcp uses the same API and the same quota, so **it doesn't work as a fallback**.
- **Real fallback:** Supabase cache + the legacy **TasteDive** API (owned by Qloo but independent, ~300 queries/hour).

## Memory

- **Supabase** (Postgres + pgvector), free tier.
- `person_memory` table: what each person accepted or rejected, with date.
- `group_nights` table: each group night, what was chosen and how it went.
- More recent entries weigh more than older ones (in case someone's taste changed).
- Option: reuse **Recall** as the memory layer.

## Cache

- **One table in Supabase.** Key = hash of function + normalized parameters. Stores the response and the date.
- **Expiration by data type:**
  - Search (IDs): ~30 days
  - Insights: ~1 day
  - Trending: a few hours
- **Preload the demo:** run the scenario once before recording, so no call depends on the live API.
- **To decide:** if the API fails, serve stale cache? (proposal: yes, flagged as stale).

## Competition on GitHub (same hackathon)

| Project | What it does | Relation to Overlap |
|---|---|---|
| Common Ground | Finds shared tastes; not tested with a real key | Closest in concept |
| Home2Here | First week in a new city; has "I don't like this" and explanations | Already does explain + correct |
| Taste Trail | Weekend plan | Individual plan |
| Quorum | Simulated focus group for businesses | Different use case |
| TasteRoute | Profile with tastes, budget, and time → next place | Individual |
| TasteTwin | Recommends food (React + FastAPI), with made-up data | Individual |
| rajat552 (unnamed) | Persistent memory | Individual memory, not group |

**Conclusion:** explaining and correcting are already done. What's open is **multi-agent negotiation + group memory**. That's the focus.

There are no public projects using Qloo on GitLab.

## Still to design

1. **Negotiation:** how many rounds, what happens if there's no agreement, who breaks ties (a moderator agent?), how concessions are spread across nights (whoever gave in last time gets priority).
2. **Demo script:** the family of four, the "not that" moment, how the live discussion looks.
3. **Stack:** language, agent framework, model, and where the app is deployed.
4. **Submission:** review the exact Devpost submission requirements (video, description, repo).

## Next steps

- [ ] Register for the hackathon on Devpost (as of Oct 13 it still showed "Join hackathon").
- [ ] Request the API key through the Google Form in the rules (may take a while).
- [ ] Review Qloo's official starter kit and qloo-mcp.
- [ ] Test Insights, Search, and Compare with the key.
- [ ] Design the negotiation protocol.
- [ ] Set up Supabase: `person_memory`, `group_nights`, and the cache table.
