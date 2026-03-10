---
name: competitor-analysis
description: Conduct deep competitive analysis of SaaS products and markets. Use this skill when the user wants to understand the competitive landscape, find gaps in the market, evaluate how a product stacks up against rivals, or identify opportunities to differentiate. Trigger when someone mentions "competitors", "competitive landscape", "how does X compare to Y", "what's already out there", or is validating a startup idea. Always apply this skill before defining a product's differentiation strategy.
---

# Competitor Analysis

## Framework Overview

```
1. Landscape Mapping     → Who are all the players?
2. Segmentation          → Which tier are they in?
3. Deep Dives            → How does each competitor really work?
4. Positioning Matrix    → Where is the whitespace?
5. Weakness Mining       → Where do they fail users?
6. Strategic Implications → What should YOU do?
```

---

## Step 1: Landscape Mapping

### Discovery channels:
- **G2 / Capterra / Product Hunt** — Category pages list all players
- **"Alternatives to X"** searches — find comparison sites
- **VC portfolio pages** — show funded players in a space
- **App stores** — search category keywords
- **LinkedIn company search** — find startups in a niche
- **Google "X software", "X tool", "best X"** — SEO-ranked players

### Competitor tiers:
```
Direct competitors    → Same customer, same problem, same solution
Indirect competitors  → Same customer, same problem, different solution
Substitute solutions  → Same customer, different approach (e.g. spreadsheets vs software)
Adjacent players      → Different customer, overlapping features
```

---

## Step 2: Competitor Profiling Template

For each major competitor:

```markdown
## [Competitor Name]

**Founded**: 
**Funding**: 
**Team size**: 
**Pricing**: 
**Primary market**: [SMB / Mid-market / Enterprise]
**Primary persona**: [who is their main user]

### Core Value Proposition
[One sentence: what they promise, to whom]

### What They Do Well
- 
- 

### Notable Weaknesses
- 
- 

### Pricing Model
| Plan | Price | Key Limits |
|------|-------|-----------|
| Free | $0 | [limits] |
| Pro | $X/mo | [limits] |
| Business | $Y/mo | [limits] |

### Review Summary (G2/Capterra/App Store)
- ⭐ Average rating: X.X
- Most praised: 
- Most complained about: 

### Tech signals:
- Stack: 
- AI features: 
- Integrations: 
```

---

## Step 3: Positioning Matrix

Plot competitors on 2x2 axes that matter for your market. Choose axes based on the key tradeoffs in your space.

### Common axis pairs:
- **Simplicity vs. Power** (ease of use vs. feature depth)
- **Price vs. Quality** (cost vs. output quality)
- **Speed vs. Accuracy** (throughput vs. precision)
- **Generalist vs. Specialist** (broad vs. niche)
- **Self-serve vs. High-touch** (PLG vs. sales-led)

### Example:
```
                    POWERFUL
                        │
    [Competitor C]      │      [Competitor A]
                        │
SIMPLE ─────────────────┼───────────────────── COMPLEX
                        │
    [Competitor D]      │      [Competitor B]
                        │
                    LIMITED

        ← Whitespace in Simple + Powerful quadrant? →
```

---

## Step 4: Weakness Mining

The richest source of competitive intelligence is **negative reviews**. Mine these systematically.

### Where to look:
- G2 reviews → filter by 1–3 stars
- Capterra reviews → "Cons" section
- Reddit: `r/[industry]` + competitor name + "problem"
- Twitter/X: "@CompetitorName" + frustration keywords
- App Store: 1–2 star reviews
- Hacker News: "Ask HN" about the product or space

### What to look for:
| Category | Example complaints |
|----------|------------------|
| Performance | "Too slow", "crashes", "unreliable" |
| Pricing | "Too expensive", "hidden fees", "limits hit too fast" |
| Missing features | "Wish it could...", "lacks X" |
| UX friction | "Hard to use", "confusing", "too many clicks" |
| Support | "Slow to respond", "bugs not fixed" |
| AI quality | "Hallucinations", "outputs are generic", "wrong results" |
| Integration gaps | "Doesn't connect to X" |

### Synthesize into opportunity clusters:
```
Pain cluster 1: [Theme] — mentioned in N reviews
  → Users want: [specific need]
  → Implication: [opportunity for you]

Pain cluster 2: ...
```

---

## Step 5: Strategic Implications

After mapping the landscape, answer:

### The 4 Strategic Questions

1. **Where is the whitespace?**
   - What customer segment is underserved?
   - What feature set is missing?
   - What price point has no good option?

2. **What's the "and" opportunity?**
   - Can you combine two things competitors treat as separate?
   - Example: "Good UX AND enterprise features" (most tools have one, not both)

3. **What moat can you build that they can't easily copy?**
   - Data network effects?
   - Workflow lock-in?
   - Brand/community?
   - Integration depth?

4. **What do users hate about the category leader?**
   - Positioning against a known incumbent frustration is a proven GTM strategy

### Strategic Options Matrix:
| Option | Differentiation | Risk | Defensibility |
|--------|----------------|------|---------------|
| Undercut on price | Low | High (race to bottom) | Low |
| Outperform on quality | Medium | Medium | Medium |
| Serve underserved niche | High | Low | High |
| New paradigm (10x better) | High | High | Very High |

---

## Output: Competitive Landscape Report

```markdown
# Competitive Landscape: [Space]

## Market Overview
[2-3 sentence summary of the market]

## Players
| Company | Tier | Funding | Strength | Weakness |
|---------|------|---------|----------|---------|
| ...     |      |         |          |         |

## Positioning Map
[Describe or embed matrix]

## Key Pain Points in the Market
1. [Pain] — seen in X/Y competitor reviews
2. ...

## Whitespace Opportunities
1. [Opportunity]: [who it serves, why it exists, why it's valuable]
2. ...

## Recommended Positioning
[Your differentiation recommendation based on analysis]
```
