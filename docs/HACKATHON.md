# Qloo Agentic Hackathon

Sources, read 2026-10-21: https://qloo.devpost.com/ · https://qloo.devpost.com/rules · https://qloo.devpost.com/details/dates

## 1. Event

- **Name:** Qloo Agentic Hackathon — "Agents, but with taste."
- **URL:** https://qloo.devpost.com/
- **Organizer:** Qloo (Sponsor and Administrator), 100 Crosby Street, New York, NY 10012. Hosted on Devpost.
- **Sponsors:** Qloo. Bonus investment from Jason Calacanis.
- **Format:** online, public. 2104 participants as of 2026-10-21.
- **Judges listed:** Jason Calacanis, Mike Diolosa (CTO, Qloo), Nicole Seligman, Todd Boehly, Cedric the Entertainer, Michael Abrams (Live Nation). The rules say judges may change and may not all be listed.

## 2. Timeline

| Stage | Event time (ET) | Local time (ART) |
|---|---|---|
| Submission deadline | 2026-10-30 23:45 -04:00 | 2026-10-31 00:45 -03:00 |
| Period opens | 2026-09-30 09:00 -04:00 | 2026-09-30 10:00 -03:00 |
| Judging starts | 2026-11-02 12:00 -05:00 | 2026-11-02 14:00 -03:00 |
| Judging ends | 2026-11-05 23:45 -05:00 | 2026-11-06 01:45 -03:00 |
| Winners announced (on or around) | 2026-11-05 15:00 -05:00 | 2026-11-05 17:00 -03:00 |

- `/rules` gives the opening as 9:00 am ET; `/details/dates` gives 9:30 am EDT. `/rules` prevails and is used above.
- `/rules` gives the end of judging as 2026-11-05 11:45 pm ET; `/details/dates` gives November 05 at 9:00 am EST. `/rules` prevails.
- Updated 2026-10-21: judging used to end 2026-11-16 and winners were due 2026-11-23.
- After the deadline the submission can no longer be changed (rules § 5).

## 3. Prizes and tracks

| Prize | Amount | Eligible |
|---|---|---|
| 1st Place | US$15,000 cash | All eligible submissions |
| 2nd Place | US$6,000 cash | All eligible submissions |
| 3rd Place | US$4,000 cash | All eligible submissions |
| Bonus | Jason Calacanis "will personally invest an additional $25,000 into his favorite entry" | Terms not published |

- There is a single track. Each project can win at most one prize.
- The bonus appears on the home page only; it is not in the Official Rules.
- **Live finals (home page only, added by 2026-10-21):** "On November 5th, the Top 3 Finalists will appear on air with Jason Calacanis, Cedric the Entertainer, and Alex Elias, who will pick the winner!" Finalists present, answer questions, and learn the results live. They are notified soon after the close and "must be able to appear, and must be available for preparation prior to the appearance."

## 4. Judging criteria

Stage One is pass/fail: the project must "reasonably fit the theme and reasonably apply the required APIs/SDKs featured in the Hackathon."

Stage Two uses "the following equally weighted criteria":

| Criterion | Weight | Rule text |
|---|---|---|
| Technological Implementation | 25% (equal weight) | "How thoroughly and skillfully does the project use Qloo? Does the code reflect genuine effort and a working, non-trivial implementation?" |
| Design | 25% (equal weight) | "Does the project deliver a complete, coherent product experience, not just a technical proof of concept?" |
| Potential Impact | 25% (equal weight) | "Does the project make a credible, specific case for solving a real problem for a real audience and does the solution actually address that problem based on what's demonstrated?" |
| Quality of the Idea | 25% (equal weight) | "Is this a creative, non-obvious use of Qloo and does the team demonstrate genuine understanding of the problem space they're working in?" |

- **Tie-break:** the higher score on the first criterion listed wins, then the next criterion, and so on.
- The rules allow judging by "expert panels, peer review, automated AI-driven analysis, or any combination thereof."
- From the home page: "If your submission would work the same without Qloo, you're building the wrong thing."

## 5. Required tech

- **Qloo API.** API access is requested through the Google Form at https://docs.qloo.com/reference/qloo-llm-hackathon-developer-guide#getting-your-api-key
- **Agentic.** The project must do one of the following: (a) function as an agentic tool, (b) be built with an agent framework, or (c) integrate the Qloo API into an existing agent.
- **How use is proven:** not published as a specific artifact. Judges assess "how thoroughly and skillfully" Qloo is used from the code, the description, and the demo.
- **API quota:** a call limit exists; the number is not published.

## 6. Submission requirements

| Item | Requirement | Limit |
|---|---|---|
| Functional demo link | A live, working app judges can try end-to-end. Must be hosted and fully published externally; local-only or private-access demos do not qualify | — |
| Code repository URL | Public, on GitHub, GitLab, or Bitbucket. Must contain all source code, assets, and instructions to run | — |
| Open-source license | A license file detectable and visible in the repository's About section | — |
| Text description | Features and functionality: what the agent does and what makes it "Qloo-powered" | Character limit: not accessible (the form requires a login) |
| Testing access | Free, unrestricted access until judging ends. A private site must include login credentials in the testing instructions | — |
| Language | English, or an English translation of all materials | — |
| Demo video | Not required by the rules ("Demo videos are not required") | Length and format: not published |
| Other form fields | Not accessible without a session | not accessible |

- Judges are not required to test the project. They "may choose to judge based solely on the text description, images, and video provided in the Submission."

**Project decision:** we ship a demo video and a landing page anyway, as extra material for judges who don't open the live demo.

## 7. Disqualifiers

- A demo that is not externally hosted, or a repository that is private or has no open-source license.
- A project that existed before 2026-09-30 and was not significantly updated during the submission period. The update must be explained.
- A project developed with financial or preferential support from Qloo or Devpost.
- Entrants who reside in Brazil, Quebec, Russia, Crimea, Cuba, Iran, North Korea, or any OFAC-sanctioned territory. Argentina is not excluded.
- Entrants below the age of majority. Sponsor or Devpost staff, judges, and their immediate family or household.
- Work that is not original, not solely owned, or infringing third-party IP or privacy rights.
- Multiple submissions from one entrant that are not "substantially different."
- Unauthorized use of third-party SDKs, APIs, or data.

## 8. Blockers

- **Qloo API key:** requested through the Google Form; it may take time to arrive.
- **Devpost registration:** click "Join hackathon" on qloo.devpost.com before submitting.
- **API quota:** the limit is not published. The demo must survive it through caching.
- **Live finals availability:** if selected as a finalist, appear live on 2026-11-05 and prepare beforehand.
