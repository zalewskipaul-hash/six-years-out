# College prep site — project plan

A site that explains how college admissions actually works to students who are still years away from it.

Built by Kenzie (12, turning 13, going into 8th grade). Paul helps along the way, but this is hers.

**Six Years Out** — sixyearsout.com, registered and hosted on Cloudflare.

---

## What this is

Most college content is written for parents of juniors. This is written to students who are years out — roughly 12 to 16, middle school through early high school — and it explains the parts nobody explains: what a college application actually contains, when tests happen, what different schools expect, and what any of it has to do with you right now.

**The information asymmetry is the reason to build it.** Most people never look at a college application until they sit down to fill one out, and then find out too late what was going to be on it. Kids with private counselors know this stuff at 13. Kids without them find out junior year, when some of it is already too late.

**Not commercial to start.** No ads, no affiliate revenue, no lead gen. That's a feature — it means no ranking pressure and no hedging. Commercializing somehow, later, isn't ruled out. It's just not what this is built for.

### What success looks like

Kenzie's criteria, in her words:

- **Real families use it.** Including friends she shares it with directly.
- **It brings scattered information into one place.** This information already exists — it's just spread across a dozen sites, and none of them are talking to her.
- **It helps her think about college**, since she's starting to think about it anyway.
- **It's fun to build.** This is her first website.
- **It's still alive in a year.**

One more, down the road: the site itself is a real passion project, built over years, and that is exactly the kind of thing worth having on a college application. Her idea, and a good one.

---

## Decisions locked

| Decision | Call |
|---|---|
| Business model | None for now. Passion project. Revisit later if it's worth revisiting. |
| Primary reader | The student, roughly 12 to 16. Adults are how it gets found, and can read it too. |
| Voice | Kenzie's. Paul edits and builds. |
| Ranking | Rank tools. Don't rank schools. |
| Stance | Tell the truth, including the strategic parts, and name the tradeoffs out loud. |
| Accounts | None. Nothing stored. Quiz results encode into the URL. |
| Stack | Astro + Markdown, GitHub, Cloudflare. Static output, no server, no adapter. |

### The stance, concretely

Resume-stuffing is real. Picking up a third instrument you don't enjoy because you think Stanford wants it is a real thing people really do. The site says so plainly — and then says why it's usually a bad trade: you're less happy, and if a school only wants you for the tuba, it probably isn't your school anyway. Kenzie's article on uniqueness versus resume-stuffing sets the tone for the site.

Plenty of sites avoid saying that part out loud. This one says it.

### Why rank tools but not schools

There genuinely is a better SAT prep app, and refusing to say so is unhelpful. There is no better *school* — fit is personal, and a ranked list teaches a 13-year-old that her job is to climb toward number one. Best-school pages show an unranked spread chosen to illustrate range: one nobody's heard of, one that's easy to get into, one that's cheap, one enormous, one tiny.

### Why no accounts

The reader is a kid. Any account system means storing children's data, a privacy policy that has to be true, and a breach you'd have to disclose — for a feature nobody needs. URL-encoded results give a real saved artifact you can bookmark, text, or print, with no database.

---

## Content pillars

1. **What's actually on a college application** — the artifact itself, demystified
2. **The grade-by-grade timeline** — the spine of the site
3. **Study resources, ranked** — SAT and ACT tools, with an actual opinion
4. **College landscape literacy** — D1 vs D3, state vs private, big vs small, plus the best-for-X pages
5. **What different schools expect** — and what that means you might start doing now

---

## The timeline page (prototype complete)

The homepage and the hub everything links to.

**Structure.** Vertical centered spine running unbroken from the bottom to a graduation cap at the top. Grades alternate left and right. Reads bottom to top — earliest grade at the bottom, college at the top.

**Every grade uses the same four sections**, in this order:

- What to do now
- What most people get wrong
- What counts
- Tests and deadlines

**Section labels are larger than the lines beneath them** and colored in that grade's blue.

**"What most people get wrong"** is deliberately not "what most people do" — listing common behavior neutrally reads as an endorsement. Each line names the consequence. The earliest grades say plainly that there's nothing to get wrong, so the page isn't scolding kids for being kids.

**Colors.** One blue ramp, darkening as college gets closer:

| Grade | Hex |
|---|---|
| 6 | `#E6F1FB` (palest — needs a hairline border to read as a circle) |
| 7 | `#B5D4F4` |
| 8 | `#85B7EB` |
| 9 | `#378ADD` |
| 10 | `#185FA5` |
| 11 | `#0C447C` |
| 12 and college | `#042C53` |

Background `#FAF4EA`. Body text `#12283D`, secondary `#4A5C70`. Not white — white reads as a site nobody put effort into.

**Type.** Fraunces for headings, Inter for body. Placeholders, open to change.

**Floating key.** A bar showing which stretch you're in — explore, build, apply. Sticks to the screen and updates as sections pass. Decide later whether it earns its space, especially on mobile.

**Scroll direction.** The page reads upward, which fights habit. Don't auto-jump on load — it feels broken and breaks deep links. Instead: a short intro at the top explaining the page reads from the bottom, with one button that jumps down to the start.

### 6th grade — decided, add it

6th grade is genuinely different from 7th, for one reason: in many districts the accelerated math decision point sits between 6th and 7th grade, decided on 5th and 6th grade test scores. That placement determines whether Algebra I in 8th grade is available, which determines whether calculus by senior year is reachable.

Almost nobody realizes that's a college-relevant decision at the time. That's the site's thesis in miniature, so 6th grade gets a spot on the line — with essentially one item on it.

---

## Grade pages

One per grade, 6 through 12. Reached from the timeline via "How to: 8th grade."

**The overview answers what. The grade page answers how.** Same four section labels, so the connection to the timeline is visible. 11th grade's page covers how to actually choose between the SAT and the ACT, how to ask a teacher for a letter without it being weird, and links into the ranked study tools.

---

## Quizzes

Two to start, both URL-encoded, no storage. More later as ideas come.

1. **SAT or ACT** — linked from the 10th *and* 11th grade pages, not just 11th. You can take either test in 10th grade, and knowing which one suits you earlier means you can start studying for the right one instead of feeling behind.
2. **What kind of school fits you** — outputs a *shape* (size, cost, selectivity, setting, how central your thing is on campus), not a list of schools. Same vocabulary the best-for-X pages use.

---

## Data layer (later)

How the site gets the numbers that power the best-for-X pages. Both sources are free federal data — no scraping, no paid APIs.

**College Scorecard API** — `api.data.gov/ed/collegescorecard/v1`, free key from api.data.gov. Roughly 6,000 schools, 1,900+ data points, drawn from IPEDS, NSLDS, and Treasury. Includes field-of-study data by CIP code, which is what makes "schools where math is a real program" a query rather than a guess. Last updated June 2026.

**EADA** — `ope.ed.gov/athletics`. Every Title IV school with an athletic program discloses participants per varsity sport, athletic aid, and spending. This answers the question a 13-year-old swimmer actually has: does this school have a team, how big is it, and is there aid.

Pull both at build time into local JSON. No runtime API calls, no keys in the browser.

---

## Order of work

**Phase 1 — ship the timeline.** Astro project, GitHub repo, Cloudflare deploy, timeline page live at a real URL. Nothing else. A live one-page site beats a planned five-page one.

**Phase 2 — grade pages.** Seven of them, starting with 8th, since that's hers.

**Phase 3 — quizzes.** SAT vs ACT first; it's smaller and it has an obvious home.

**Phase 4 — data pages.** Build script, then best-for-X pages.

Realistic pace is about a page a week. Scope to that.

---

## Before anything publishes

- **Verify every test fact.** The SAT is now digital and adaptive, the ACT has changed format recently, and financial aid form timing has shifted in the last few cycles. Everything currently in the prototype is structurally right and needs checking against current sources. "What changed recently and what it means for you" may deserve its own page.
- **Byline: first name only.** "Kenzie" — possibly "Kenzie, 8th grade, Colorado." No last name, no school name, no photos. Settled up front rather than after the fact.

---

## The name

**Six Years Out.** A 7th grader has six years of school left before college — that's the reader the site is built for. It's approximate at the edges (a 6th grader is seven years out) and that's fine; names aren't specs.

Chosen over more descriptive options because the site's angle isn't "college," it's "college, years earlier than anyone tells you to think about it." The number is what makes an adult stop and go *wait, what?*

---

## Open questions

- **Tagline** — the name needs one that resolves which direction it counts. "Six years out" can be misread as six years *since* college, so the first line on the page has to make clear it means six years *until*. Current idea: open with "You're six years out. Or seven. Or four." — turning the ambiguity into an invitation to find yourself on the line.
- **Distribution** — deferred. Near-term goal is a resource Kenzie uses herself and shares with friends. Getting in front of parents, counselors, and coaches is a later problem.
- **Floating key** — whether it earns its space, especially on mobile.
