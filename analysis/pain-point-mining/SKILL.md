---
name: pain-point-mining
description: Systematically uncover real user pain points from online signals, reviews, communities, and behavioral data. Use this skill when the user wants to validate a problem, find what users actually struggle with, identify product opportunities from real frustration, or build user empathy before designing a solution. Trigger when someone says "what do users really want", "is this a real problem", "find me pain points in X industry", or is doing discovery research before building. Always apply before designing any new product or feature.
---

# Pain Point Mining

## The Pain Point Hierarchy

Not all pain is equal. Prioritize:

```
Level 1: CRITICAL   — Causes revenue loss, legal risk, or major workflow failure
Level 2: CHRONIC    — Happens repeatedly, accepted as "just how it is"
Level 3: LATENT     — User doesn't realize it's a problem until shown an alternative
Level 4: MINOR      — Annoying but doesn't change behavior
```

Build products for Level 1–2. Level 3 is innovation territory. Level 4 is noise.

---

## Mining Sources

### Tier 1: Highest Signal (Real frustration, in the moment)

**Reddit**
- Subreddits for the industry/niche
- Search: `[topic] problem`, `[topic] alternative`, `[tool] sucks`, `[task] frustrating`
- Look for upvoted posts + comments; votes = how many share the pain
- Threads starting with "Why is it so hard to..." or "Am I the only one who..."

**App Store / Chrome Web Store reviews**
- Filter by 1–3 stars
- "Cons" sections in structured reviews
- Look for specific complaints, not vague ratings

**G2 / Capterra / Trustpilot**
- Sort by "Most Recent" + filter by lowest rating
- "What problems are you solving?" field reveals the job-to-be-done

**Twitter / X**
- `"[tool name]" -filter:replies` — see what people say unprompted
- `[industry task] "I wish"`, `[tool] "can't believe"`, `[process] "why is it so hard"`

### Tier 2: High Signal (Structured feedback)

**Interviews & surveys** (if you have access)
- Jobs-to-be-done interviews: "Walk me through the last time you did X"
- Pain ranking: "What's the most frustrating part of your workflow?"

**Product teardown forums**
- Hacker News "Ask HN: How do you handle X?"
- Indie Hackers discussions
- Quora "What are the biggest problems with X?"

### Tier 3: Useful Context

**LinkedIn / industry blogs** — professional frustrations, industry vocabulary
**Job postings** — companies hiring for X = they have a problem with X
**Conference talk titles** — topics = common problems people pay to solve
**VC investment theses** — funds investing in a space understand the pain

---

## Mining Protocol

### Step 1: Define the domain
Specify: Who is the user? What is the workflow? What tools do they currently use?

### Step 2: Collect raw signals
For each source, collect 20–50 raw quotes/complaints. Don't filter yet — just collect.

Format each as:
```
Source: [Reddit / G2 / etc]
Quote: "[exact text]"
Context: [what they were trying to do]
Apparent pain: [1-sentence summary]
```

### Step 3: Cluster by theme
Group raw signals into pain themes. Name each cluster.

```
Pain Cluster: "Slow manual data entry"
- Quotes: [3-5 examples]
- Frequency: mentioned in X of Y sources
- Severity: Level [1-4]
- Current workarounds: [how they cope today]
```

### Step 4: Score each pain cluster

| Pain Cluster | Frequency | Severity | Willingness to Pay | Opportunity Score |
|-------------|-----------|----------|-------------------|-------------------|
| Data entry  | High      | Critical | High              | ⭐⭐⭐⭐⭐ |
| UI confusion | High     | Minor    | Low               | ⭐⭐ |
| Missing feature X | Low | Chronic | Medium           | ⭐⭐⭐ |

**Opportunity Score** = Frequency × Severity × Willingness to Pay

### Step 5: Validate the top pains
Before building, verify:
- Is this pain specific and consistent (not one person's edge case)?
- Is there a clear job-to-be-done behind the pain?
- Are people already paying workarounds (VA, custom tools, manual processes)?
- Would a solution make someone's day meaningfully better?

---

## Interview Technique: The Pain Funnel

When talking to potential users, use this question sequence:

1. **Set the context**: "Tell me about how you currently [workflow]."
2. **Find friction**: "What's the most tedious part of that process?"
3. **Quantify**: "How often does that happen? How long does it take?"
4. **Probe the workaround**: "What do you do when that happens?"
5. **Get the cost**: "What does that cost you — in time, money, or quality?"
6. **Test urgency**: "If you had a magic button that fixed that, how much would you pay for it?"

Red flags:
- "It's annoying but I've learned to live with it" → Level 4 pain, don't build
- "We actually built our own tool for this" → Level 1 pain, strong signal
- Pause before answering "how much would you pay" → not a real problem

---

## Output: Pain Point Report

```markdown
# Pain Point Report: [Domain / Persona]

## Research Sources
- Reddit: [subreddits searched]
- Reviews: [G2/Capterra categories]
- Other: [...]
- Total signals collected: [N]

## Top Pain Clusters

### Pain 1: [Name]
- **Severity**: Level [1-4]
- **Frequency**: [how often mentioned]
- **Representative quotes**:
  > "[quote 1]"
  > "[quote 2]"
- **Current workaround**: [how they cope]
- **Opportunity**: [what a product could do]
- **Willingness to pay signal**: [evidence]

### Pain 2: ...

## Prioritized Opportunity Matrix
[Table with scores]

## Recommended Focus
[Top 1-2 pain points to build for, with rationale]
```
