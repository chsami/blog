# The Bottleneck Was Never the Code

## Research Notes for Blog Post

Last updated: 2026-06-18

---

## TL;DR

Coding agents made writing code nearly free, and the moment they did, everyone discovered the code was never the slow part. The bottleneck moved — but **where** it moved is now a live fight. The dominant narrative says it moved to **human review** (Faros AI: high-AI-adoption teams merged 98% more PRs but PR review time rose **91%**). A second camp says it didn't move at all — it was **externalized into future maintenance debt** (James Shore's math: 2x code output at normal maintenance cost is net-negative within ~19 months). A third (thetypicalset) says the real bottleneck was always **human agreement about what to build** — "software is what's left over after a group of humans finishes negotiating."

**The contrarian angle for this post (author's own stance):** the consensus fix — "put humans back in control of review" — is backwards. If review is now the bottleneck, don't make humans review *more*; have **AI review most code against clear, explicit rules**, and reserve scarce human attention for **authoring and owning the critical parts of the system**. Flip which half of the work the human does.

---

## Primary Sources

### thetypicalset — "The bottleneck was never the code"
Source: [thetypicalset.com](https://www.thetypicalset.com/blog/thoughts-on-coding-agents) · [HN 586pts/414c](https://news.ycombinator.com/item?id=48006967)

Core argument: for 50 years we optimized the cost of *implementation* (typing, languages, tooling) because the residue was expensive enough to hold our attention. Agents dropped that cost far enough to expose what was underneath: **people trying to agree.**

Key quotes:
- "Software is what's left over after a group of humans finishes negotiating with each other about what the system should do."
- "Negotiating, agreeing, communicating the shared picture of what we are building has become *the* work."
- "The bottleneck moves from the people writing the code to the people deciding what code should exist. Which is to say: management."
- "Every vibe-coded product with 12 features is 11 features away from being great." (the discipline to say no gets *harder*)
- "Context is the commodity an organization runs on" — the why-we-did-it-this-way that nobody documented is now the rate-limiting input.
- Reframe: agents are "overestimated as a way to make individuals write code faster, and underestimated as a way to make organizations externalize what they know."

### James Shore — "You need AI that reduces your maintenance costs"
Source: [jamesshore.com](https://www.jamesshore.com/v2/blog/2026/you-need-ai-that-reduces-your-maintenance-costs)

Core claim: maintenance cost, not output speed, governs long-term effectiveness. "For every month you spend writing code, you'll spend some amount of time in the following year maintaining that code, and some in each year after that, forever."

The math (the killer stat): if an agent doubles output but maintenance cost per line stays the same, the productivity gain is gone within ~19 months and goes **permanently negative** after — what Shore calls "permanent indenture." "If you're producing twice as much code, you need code that costs half as much to maintain."

On review: critiques teams that "don't actually read the code before smashing the approve button" — but offers no explicit ownership policy. **This is the gap the post can fill.**

---

## Empirical Data (the spine of the argument)

### Agoda / InfoQ + Faros AI study
Source: [InfoQ](https://www.infoq.com/news/2026/03/agoda-ai-code-bottleneck/)

Faros AI, 10,000+ developers across 1,255 teams:
- High-AI-adoption teams completed **21% more tasks**
- Merged **98% more pull requests**
- **PR review time increased 91%**

Leonardo Stern: this is just Fred Brooks again — "improvements in speed to only one part of the development lifecycle produce diminishing returns." The constraint moved upstream (spec) and downstream (review/verification), not away.

**This is the single best data point for the post:** code throughput nearly doubled; the human review queue is where it all jammed.

---

## Community Insights (HN + cross-platform)

### The strongest critique — mental models, not typing
- **fao_ (HN):** the bottleneck was never code *writing* but *building the mental model* of the system. LLMs "cannot construct consistent mental models of codebases" — so maintainability, testing, and verification suffer; "there is absolutely no guarantee around accuracy of that text." → **Note: this cuts against the author's AI-as-reviewer thesis too, and must be addressed head-on, not dodged.**

### Maintenance debt as the hidden cost
- Faster output is only a win "*if speed was the bottleneck*." Otherwise the gain converts into unmaintainable code + lost organizational context. The "second system" problem: rebuilds deliver less because the original held undocumented complexity.

### Review as the new bottleneck
- Recurring theme: when AI generates volume, review becomes the binding constraint. Spawned a product wave — e.g. **Stage** ("putting humans back in control of code review", [Show HN](https://stagereview.app/)) and **Fata** (spaced repetition to fight AI skill-rot). The market is betting on *more human review*. The post's thesis bets the opposite.
- Older but on-point HN comment: "the bottleneck is QA/Code review and that is never going away."

### Collaboration nuance
- Devs aren't rejecting collaboration, just "pointless communication" / performative agile ritual. Direct stakeholder contact ≠ ceremony. "It's not hypocritical to change your opinion when the facts have changed."

### Cross-platform convergence
Same thesis showing up everywhere this cycle: [Rob Bowley](https://blog.robbowley.net/2026/01/05/coding-has-never-been-the-bottleneck/), [Lobsters](https://lobste.rs/s/wiu8md/writing_code_was_never_bottleneck), [The AI Journal](https://aijourn.com/the-bottleneck-was-never-code-and-product-teams-arent-ready-for-what-comes-next/), plus the older viral [HN thread (44429789)](https://news.ycombinator.com/item?id=44429789). Strong slow-burn trend, not a one-day spike.

---

## The Author's Thesis (the differentiator)

The whole discourse agrees review is now the jam point and then concludes *humans must review harder*. That's treating the symptom by adding more of the scarce resource (human attention) to the exact place it's scarcest.

**Invert it:**
1. **AI reviews most code, against explicit written rules.** Review is largely rule-application: style, conventions, common bug patterns, security checks, test coverage, "does this match the spec." That's mechanical and tireless — exactly what an agent with a clear rubric is good at. Make the rules a checked-in artifact, not tribal knowledge.
2. **Humans author and own the critical parts.** The 10–20% that is load-bearing — core data models, security boundaries, money-touching paths, concurrency, the architecture that's expensive to change — stays human-authored and human-owned. That's where mental models matter most (the fao_ objection) and where being wrong is unrecoverable.
3. **Net effect:** you stop spending your scarcest hours rubber-stamping boilerplate ("smashing the approve button") and spend them where judgment compounds. It directly attacks the +91% review-time stat instead of accepting it.

### Honest counterarguments to address (don't dodge)
- **fao_'s mental-model problem applies to AI reviewers too.** Rebuttal: that's *why* humans keep the critical 20% — AI review is for the mechanical 80% where a clear rubric, not a deep mental model, is what's needed. Pair AI review with strong tests/types so the guarantee comes from the harness, not the model's "understanding."
- **Who writes the rules?** The rules become the new high-leverage artifact — and writing good rules is itself the "deciding what should exist" work thetypicalset is pointing at. (Ties review-rules back to the spec-is-the-bottleneck thesis.)
- **Maintenance debt (Shore).** AI-review-with-rules only pays off if the rules actively enforce maintainability, not just correctness. Bake Shore's "half the maintenance cost" goal into the review rubric.

---

## Angle (Phase 4)

1. **What problem does this solve?** Your agents doubled your code output and your PR queue is now on fire (+91% review time). Throwing more human reviewing at it doesn't scale — you're feeding the bottleneck with the scarcest input.
2. **What actually changed?** Code got cheap; the bottleneck surfaced. Three camps on where it went (review / maintenance / agreement) — lay them out fairly.
3. **Why is this different from what exists?** The market says "put humans back in control of review" (Stage, etc.). This post argues the opposite split: AI reviews the 80%, humans author/own the critical 20%.
4. **Who has an advantage?** Teams that write down their rules and conventions as checked-in, AI-readable artifacts — they can delegate review; teams running on tribal knowledge can't.
5. **What does this mean for users?** Concrete: a review-rules file, what belongs in the human-owned critical set, how tests/types provide the guarantee AI review can't.
6. **Where is this going?** "Context is the commodity" — the durable advantage is externalizing the why, not typing faster.

### Title candidates
- "Let the AI review the code. Keep the critical parts human."
- "Your PR queue is the bottleneck now. Stop adding humans to it."
- "Code got cheap. Reviewing it didn't. Here's the swap."
- "Who owns this in six months? Rethinking review after agents."

### Style notes (house style)
- Lead with the pain: the +91% review-time jam, told from a dev drowning in agent-generated PRs.
- First-person, realistic example: a concrete review-rules snippet + a worked "this belongs to a human / this doesn't" call.
- State the position plainly, then steelman fao_/Shore — credibility comes from addressing the strongest objection, not hiding it.
- No hype. The thesis is a *workflow* claim, not an AI-can-do-everything claim — be explicit that the critical 20% staying human is the whole point.

---

## Sources
- thetypicalset (primary): https://www.thetypicalset.com/blog/thoughts-on-coding-agents
- HN 586pts/414c: https://news.ycombinator.com/item?id=48006967
- James Shore (maintenance cost): https://www.jamesshore.com/v2/blog/2026/you-need-ai-that-reduces-your-maintenance-costs
- InfoQ / Agoda / Faros AI study: https://www.infoq.com/news/2026/03/agoda-ai-code-bottleneck/
- Stage (humans-in-review product): https://stagereview.app/
- Rob Bowley: https://blog.robbowley.net/2026/01/05/coding-has-never-been-the-bottleneck/
- Lobsters: https://lobste.rs/s/wiu8md/writing_code_was_never_bottleneck
- Older viral HN thread: https://news.ycombinator.com/item?id=44429789
