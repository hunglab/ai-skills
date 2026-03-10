---
name: viral-feature-design
description: Design product features that spread organically through sharing, collaboration, and word-of-mouth. Use this skill when trying to add virality to a product, designing features that attract new users through existing users, thinking about referral mechanics, or building features that make products naturally shareable. Trigger when someone says "how do I make this go viral", "add virality to my product", "how do I get users to share this", or wants to reduce CAC through organic growth features.
---

# Viral Feature Design

## What Makes Things Spread?

Virality isn't luck — it's engineered. Products spread when:
1. **Users create value for others** by using the product (sharing, inviting, collaborating)
2. **The product is visible** in the act of being used
3. **Recipients have a reason to try it** (they benefited from it, they saw it, they were invited)
4. **The barrier to try** is low enough that they actually do

---

## Viral Mechanics Taxonomy

### Type 1: Collaboration Virality
The product requires inviting others to get its core value.

**How it works**: User can't fully use the product alone → must invite teammates, clients, friends.

**Examples**:
- Figma: Can't design collaboratively without inviting collaborators
- Calendly: Scheduling link only works when shared with someone who can book
- Loom: Video recorded → must share with viewer who sees Loom branding
- DocuSign: Can't get a signature without sending to the signer

**Design pattern**:
```
Core feature value → Requires another person → Must invite → 
Invitee sees/uses product → Natural discovery
```

**How to add it**:
- Find features that create an artifact or output (document, video, report)
- Make sharing that output the primary way to deliver value
- Ensure the recipient's experience with the artifact exposes your product

### Type 2: Product-Led Sharing
Users share content/outputs that are branded with your product.

**How it works**: The artifact carries the brand. Every share is an impression.

**Examples**:
- "Made with Canva" watermark on designs shared to social
- Typeform: Survey forms carry Typeform branding for respondents
- Substack: Newsletter footer with "Get your own Substack"
- Notion: "Made in Notion" on public pages

**Design pattern**:
```
User creates artifact → Shares publicly → 
Viewer sees brand → Views product link → Converts
```

**Design guidelines**:
- Branding must not obstruct the artifact's value (users will remove it otherwise)
- Include a clear CTA with low friction ("Create your own in 30 seconds")
- Track conversion from artifact views → signups

### Type 3: Utility Virality
The product creates so much value that users tell others because they feel compelled to help.

**How it works**: Users evangelize because they genuinely love the product.

**Examples**:
- Superhuman: Users in every tech office tell their colleagues
- Linear: Dev teams switch after one person champions it
- Raycast: Power users become ambassadors

**Design pattern**:
```
Surprisingly high value → User must tell someone → 
Recipient trusts referrer → Easy to try → Converts
```

**How to trigger it**:
- Identify your product's "wow moment" — the thing that makes users tell others
- Design onboarding to reach wow moment as fast as possible
- Make sharing frictionless when users are in the emotional peak

### Type 4: Network Effects / FOMO Virality
Users feel pressure to join because others in their network are using it.

**How it works**: The product publicly shows who uses it, creating FOMO or social pressure.

**Examples**:
- GitHub activity graph: visible to colleagues and employers
- Twitter/LinkedIn: public follower counts create social proof
- Strava: seeing friends' workouts drives engagement and signup

**Design pattern**:
```
Activity is visible → Non-users see activity → 
Feel excluded / FOMO → Sign up to participate
```

### Type 5: Referral Mechanics
Explicit incentives for users to invite others.

**How it works**: Users get rewarded (credits, features, cash) for inviting users who convert.

**Examples**:
- Dropbox: +500MB for each referral (used in original viral growth phase)
- Robinhood: Free stock for referral
- Cash App: $5 for referral

**Design pattern**:
```
User → Invited friend signs up → 
Both get reward → Reward visible to friend's network → Cascade
```

**Guidelines**:
- Reward must be valuable enough to motivate sharing, but not so high it attracts fraud
- Two-sided rewards outperform one-sided
- In-product credit works better than cash for SaaS
- Set a CAC-based cap on referral reward

---

## Viral Feature Design Process

### Step 1: Map Your Natural Sharing Moments
When do users naturally want to share what they've created or discovered?
```
User creates [output] → Natural impulse to share with [recipient]
User achieves [milestone] → Natural impulse to tell [community]
User learns [insight] → Natural impulse to share with [peers]
```

### Step 2: Remove Friction from Sharing
Every click between impulse and action = lost viral event.
- One-click share to common destinations (email, Slack, Twitter, LinkedIn)
- Auto-generated share card/image
- Public URL that works without login

### Step 3: Make the Recipient Experience Excellent
The recipient's first touch with your product IS your marketing.
- Shared artifact must work beautifully without signup
- Show what they can do IF they sign up (value preview)
- One-click to try the product

### Step 4: Measure Your Viral Coefficient
```
K = (invites sent per user) × (conversion rate of invitees)
```
- K > 1 = exponential growth
- K = 0.5 = each user brings 0.5 more users (still helps)
- K < 0.1 = virality is not a meaningful growth channel

### Step 5: Optimize by Segment
Not all users are equally viral. Find the high-K segments:
- By persona (content creators share more than developers)
- By use case (team collaboration features > solo features)
- By feature (what's the most shared workflow?)

---

## Viral Feature Checklist

- [ ] Is there an artifact/output that users naturally want to share?
- [ ] Does sharing the artifact expose your brand to the recipient?
- [ ] Is the recipient's experience excellent without requiring signup?
- [ ] Does the feature require collaboration (inviting others is the point)?
- [ ] Is there a frictionless share path (1–2 clicks max)?
- [ ] Is the referral reward high enough to motivate but sustainable?
- [ ] Can you measure K factor for this feature?
- [ ] Is there a "made with [product]" attribution on shared content?
