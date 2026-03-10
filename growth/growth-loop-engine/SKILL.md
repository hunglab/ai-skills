---
name: growth-loop-engine
description: Design and optimize compounding growth loops for SaaS products. Use this skill when building a growth strategy, designing acquisition and retention mechanics, modeling unit economics, or trying to find self-sustaining growth engines. Trigger when someone says "how do I grow this product", "what's my growth strategy", "design a growth loop for X", "my growth is linear and I want it to be compounding", or is trying to move beyond paid acquisition. Always apply before making significant growth investment decisions.
---

# Growth Loop Engine

## Funnels vs. Loops

Most teams think in funnels — linear flows from acquisition to conversion. But the fastest-growing products think in **loops** — systems where each cycle produces inputs for the next cycle.

```
FUNNEL:                    LOOP:
Awareness                  [Acquisition]
    ↓                           ↓
Consideration          [Activation / Value]
    ↓                           ↓
Conversion            [Retention / Usage]
    ↓                           ↓
Revenue               [Output (users/data/content)]
                                ↓
                     ←── feeds back into Acquisition
```

**Key difference**: A loop's output powers its own input. A funnel's output is revenue. Loops compound; funnels don't.

---

## Loop Archetypes

### 1. Viral / Product-Led Loop
```
User gets value → Creates/shares output → New user sees output → 
New user signs up → Gets value → Creates/shares → [repeat]
```

**Fuel**: Users who naturally share or collaborate
**Amplifier**: Quality of the shared artifact; friction of signup
**Examples**: Figma (design links), Loom (shared videos), Notion (public pages), Calendly (scheduling links)

**Metrics**: K-factor, viral coefficient, time-to-share after signup

### 2. Content / SEO Loop
```
Build product → Users solve problems → Capture learnings as content → 
Content ranks on search → New users discover → 
Some become customers → Solve problems → [repeat]
```

**Fuel**: User activity generating case studies, templates, community content
**Amplifier**: Content quality + SEO; community engagement
**Examples**: Canva (template library), Notion (template gallery), HubSpot (knowledge base)

**Metrics**: Organic search traffic, content-to-signup conversion, user-generated content volume

### 3. Sales-Assisted Loop
```
Marketing generates leads → Sales converts to customers → 
Customers generate revenue → Invest in more marketing → 
More leads → [repeat]
```

**Fuel**: Margin between CAC and LTV
**Amplifier**: Sales efficiency; ICP clarity; product quality (reduces churn)
**Examples**: Enterprise SaaS with SDR/AE model

**Metrics**: CAC payback period, LTV:CAC ratio, sales velocity

### 4. User-Generated Content Loop
```
Platform attracts early creators → Creators publish content → 
Content attracts viewers → Some viewers become creators → 
More content → Attracts more viewers → [repeat]
```

**Fuel**: Creator incentives; viewer volume
**Amplifier**: Creator success stories; revenue sharing; audience tools
**Examples**: YouTube, Substack, Product Hunt, GitHub

**Metrics**: Creator-to-consumer ratio, content volume growth, consumption rates

### 5. Data / AI Loop
```
Users use product → Usage generates training data → 
Model improves → Better outputs → More users → 
More data → [repeat]
```

**Fuel**: User activity volume
**Amplifier**: Data quality; model improvement cycle speed; personalization
**Examples**: Spotify, Grammarly, Google Search

**Metrics**: Model quality over time, personalization engagement lift

### 6. Community / Network Loop
```
Early power users join → Community provides value → 
More users join for community → Community grows → 
More value → [repeat]
```

**Fuel**: Community activation; peer value delivery
**Amplifier**: Community quality; moderation; events
**Examples**: Figma Community, Linear's developer community, dbt Slack

**Metrics**: Community DAU, member-generated value events, community-to-product conversion

---

## Designing Your Loop

### Step 1: Identify Your Natural Loop
What does your product do that could create a loop? Ask:
- Do users create shareable outputs?
- Does usage generate data that improves the product?
- Do users have problems that content could address?
- Is there a community angle?

### Step 2: Map the Full Cycle
Draw the loop explicitly:
```
[Input] → [Action] → [Output] → [Distribution] → [New Input]
```

Identify:
- What FUELS the loop (what users need to provide for it to run)
- What AMPLIFIES the loop (what makes each cycle produce more output)
- Where the loop LEAKS (where users drop off before completing the cycle)

### Step 3: Measure Loop Efficiency
```
Loop efficiency = (outputs in cycle N+1) / (inputs in cycle N)
```
- > 1.0 = loop accelerates over time
- = 1.0 = loop sustains
- < 1.0 = loop decays

### Step 4: Fix the Biggest Leak
Every loop has a weakest link. Find it:
- Where do users drop out before creating the next cycle's input?
- What friction prevents the output from reaching new users?
- Where is the activation moment delayed or unclear?

---

## Unit Economics for Growth

### CAC Payback Period
```
CAC payback = CAC / (monthly gross margin per customer)
```
- SaaS target: < 12 months for SMB, < 18 months for mid-market
- If payback > 24 months, your loop must be viral-heavy to compensate

### LTV:CAC Ratio
```
LTV = ARPU × Gross Margin % × (1 / Churn Rate)
LTV:CAC target: > 3x (ideally > 5x)
```

### Payback-Funded Growth
For product-led growth, the loop can be self-funding when:
```
Revenue from cohort month 1–12 > CAC spent to acquire that cohort
```
This enables reinvestment without external funding.

---

## Growth Experiment Framework

### Hypothesis Template
```
We believe [user segment] will [desired behavior] 
if we [product/marketing change].
We'll measure this with [metric].
We'll run this for [time period].
Success = [specific threshold].
```

### Experiment Priority Matrix
| Experiment | Expected Impact | Build Effort | Confidence | Priority |
|-----------|----------------|--------------|-----------|---------|
| Experiment A | High | Low | Medium | P0 |
| Experiment B | High | High | High | P1 |
| Experiment C | Low | Low | High | P2 |

Prioritize: High impact + Low effort + High confidence

### Minimum Experiment Duration
- User behavior changes: 2 weeks minimum (weekly seasonality)
- Conversion rate changes: 1 week minimum (enough volume)
- Retention/churn: 90 days minimum (early cohort behavior misleads)

---

## Growth Loop Audit Checklist

**Acquisition:**
- [ ] Is there a scalable, low-CAC acquisition channel?
- [ ] Does product usage drive organic acquisition (virality, SEO, word of mouth)?
- [ ] Is CAC payback < 12 months?

**Activation:**
- [ ] Do users reach the "wow moment" within their first session?
- [ ] Is there a clear next action after signup?
- [ ] What % of signups activate within 7 days? (target: > 40%)

**Retention:**
- [ ] What's the D1, D7, D30 retention? (target varies by product type)
- [ ] Are there habit-forming use cases (daily/weekly)?
- [ ] Is there a notification/re-engagement mechanism that's value-add, not spam?

**Revenue:**
- [ ] Does the free tier deliver enough value to activate but enough friction to upgrade?
- [ ] Is the upgrade trigger clear and well-timed?
- [ ] Does expansion revenue (upsell/seats) compound over time?

**Loop:**
- [ ] Can you draw your primary growth loop on a whiteboard?
- [ ] Does each customer cycle produce inputs for the next cycle?
- [ ] Is the loop efficiency > 1.0?
