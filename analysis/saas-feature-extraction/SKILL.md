---
name: saas-feature-extraction
description: Systematically extract, categorize, and document features from any SaaS product. Use this skill when the user wants to catalog what a product does, map features to user jobs-to-be-done, prioritize a feature set for cloning, or build a feature comparison matrix. Trigger when someone says "what features does X have", "I want to build something like X", "help me map out this product", or is preparing to clone or compete with a SaaS product.
---

# SaaS Feature Extraction

## Extraction Framework

Features exist at three levels. Extract all three:

```
Level 1: Core Features       — What the product fundamentally does
Level 2: Supporting Features — What makes core features work well
Level 3: Growth Features     — What makes users stay, share, or expand
```

---

## Step 1: Feature Discovery

### Sources to mine:
1. **Product UI** — Walk every screen as each user role
2. **Marketing site** — Features page, pricing page (shows what they charge for)
3. **Help docs / knowledge base** — Most comprehensive feature list
4. **Changelog / release notes** — Shows feature evolution and priorities
5. **App Store reviews** — Real users describing features they love/hate
6. **G2 / Capterra reviews** — Structured feature ratings
7. **YouTube demos / tutorials** — Often shows power-user features not in docs
8. **Twitter/Reddit** — Users discussing workarounds reveal missing features

---

## Step 2: Feature Categorization

### Universal SaaS Feature Categories

**Core Product**
- [ ] Primary action (what users come to do)
- [ ] Data creation / input
- [ ] Data processing / transformation
- [ ] Data output / export
- [ ] Search and filtering

**Collaboration**
- [ ] Multi-user workspaces
- [ ] Permissions and roles
- [ ] Real-time co-editing
- [ ] Comments and annotations
- [ ] Activity feeds / audit logs
- [ ] Guest / external sharing

**Integrations**
- [ ] OAuth / SSO
- [ ] Native integrations (list them)
- [ ] Webhook support
- [ ] API access
- [ ] Zapier / Make connectors
- [ ] Embed / iframe support

**AI Features**
- [ ] Generation (create content/data)
- [ ] Classification (label/sort)
- [ ] Extraction (pull info from inputs)
- [ ] Summarization
- [ ] Recommendations
- [ ] Autopilot / automation

**Personalization**
- [ ] User preferences
- [ ] Custom templates
- [ ] Saved filters / views
- [ ] Keyboard shortcuts
- [ ] Notification settings

**Admin & Billing**
- [ ] Workspace management
- [ ] Usage analytics
- [ ] Billing portal
- [ ] Invoicing / receipts
- [ ] Team invitations

**Onboarding**
- [ ] Interactive walkthroughs
- [ ] Sample data / templates
- [ ] Checklist / progress
- [ ] Email drip sequences
- [ ] In-app tooltips

---

## Step 3: Feature Documentation Template

For each feature:

```markdown
### [Feature Name]

**Category**: [Core / Supporting / Growth]
**User role**: [who can use it]
**Job-to-be-done**: [what user need it addresses]
**Trigger**: [what action activates it]
**Inputs**: [what data/content goes in]
**Output**: [what result comes out]
**Complexity**: [Low / Medium / High to build]
**Differentiating?**: [Yes / No — is this table stakes or unique?]
**Notes**: [anything interesting about the implementation]
```

---

## Step 4: Feature Priority Matrix

Once features are catalogued, score them for build priority:

| Feature | User Value | Build Effort | Differentiating | Priority Score |
|---------|-----------|--------------|-----------------|---------------|
| Feature A | High | Low | Yes | P0 |
| Feature B | High | High | Yes | P1 |
| Feature C | High | Low | No | P1 |
| Feature D | Low | Low | No | P3 |
| Feature E | Low | High | No | Drop |

**Priority Score** = (User Value × Differentiating) / Build Effort

---

## Step 5: MVF — Minimum Viable Feature Set

For cloning or competing, identify:

**Must-Have (P0)**: Without these, the product doesn't work at all
**Should-Have (P1)**: Users expect these; absence causes immediate churn
**Nice-to-Have (P2)**: Delights users but not table stakes
**Later (P3)**: Competitive but not required at launch

### MVF Template:
```markdown
## Minimum Viable Feature Set for [Product]

### P0 — Core Loop (week 1–2)
- [ ] Feature 1
- [ ] Feature 2

### P1 — Retention (week 3–6)
- [ ] Feature 3
- [ ] Feature 4

### P2 — Delight (month 2+)
- [ ] Feature 5

### Deliberately Excluded
- Feature X — too complex, no clear user demand
- Feature Y — can use integration instead of building
```

---

## Output: Feature Comparison Matrix

| Feature | [Product A] | [Product B] | [Your Product] |
|---------|------------|------------|----------------|
| Feature 1 | ✅ Full | ✅ Full | 🎯 Target |
| Feature 2 | ✅ Full | ❌ None | 🎯 Target |
| Feature 3 | ⚠️ Partial | ✅ Full | ➖ Exclude |
| Feature 4 | ❌ None | ❌ None | ⭐ Differentiator |

Legend: ✅ Full | ⚠️ Partial | ❌ None | 🎯 Target | ⭐ Your advantage
