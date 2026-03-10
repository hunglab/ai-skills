---
name: problem-solving-framework
description: Apply structured frameworks to decompose, diagnose, and solve ambiguous product and engineering problems. Use this skill whenever the user presents an unclear problem, a complex tradeoff, a persistent bug, a strategic dilemma, or says things like "I don't know where to start", "we keep having this issue", or "help me think through this". Always apply this skill before jumping to solutions for multi-faceted problems.
---

# Problem-Solving Framework

## Phase 1: Problem Definition

Before solving anything, define the problem precisely. Most "hard" problems are hard because they're poorly defined.

### The Problem Statement Template
```
We observe: [specific symptom or measurement]
We believe the cause is: [hypothesis]
We want to achieve: [desired state]
We'll know we succeeded when: [measurable outcome]
```

### Problem Inversion
Ask: *What would make this problem worse?* 
Invert: *Avoid doing those things.*

This often reveals non-obvious root causes and solutions.

### Is It Actually a Problem?
Before solving, challenge the premise:
- Is this a real constraint or an assumed one?
- What happens if we do nothing?
- Are we solving the symptom or the root cause?

---

## Phase 2: Root Cause Analysis

### The 5 Whys
Recursively ask "why" until you reach a root cause (usually 3–6 levels deep).

```
Problem: Users are churning after week 2
Why? → They stop logging in
Why? → They don't see value in returning
Why? → The product doesn't remember their context
Why? → We store no user state between sessions
Why? → We built it as a stateless tool, not an ongoing product
Root cause: Product architecture doesn't support persistence
```

### Fishbone Diagram (for complex multi-cause problems)
Categorize potential causes:
- **People**: Team skills, incentives, communication
- **Process**: Workflow, handoffs, feedback loops
- **Product**: Features, UX, performance
- **Technology**: Infrastructure, tooling, dependencies
- **Data**: Quality, availability, freshness
- **External**: Market, regulation, competition

---

## Phase 3: Solution Generation

### Diverge Before Converging
Generate at least 5 candidate solutions before evaluating any of them. Premature convergence kills creative solutions.

**Prompt yourself:**
- What's the most boring/obvious solution?
- What would a competitor do?
- What if we had 10x the budget?
- What if we had 10% of the budget?
- What would we do if we couldn't use technology?
- What's the opposite of our current approach?

### Solution Evaluation Matrix

| Solution | Effort | Impact | Reversibility | Risk | Score |
|----------|--------|--------|---------------|------|-------|
| Option A | Low | High | High | Low | ⭐⭐⭐⭐ |
| Option B | High | High | Low | Med | ⭐⭐⭐ |
| Option C | Low | Low | High | Low | ⭐⭐ |

Score: (Impact × Reversibility) / (Effort × Risk)

---

## Phase 4: Decision Making Under Uncertainty

### The Reversibility Test
- **Reversible + Low Stakes** → Decide fast, learn from outcome
- **Reversible + High Stakes** → Run a small experiment first
- **Irreversible + Low Stakes** → Decide carefully but don't overthink
- **Irreversible + High Stakes** → Move slowly, gather data, get second opinions

### Pre-Mortem
Before committing to a solution, imagine it's 6 months later and the solution failed. 
Ask: *What went wrong?*
This surfaces hidden risks and stress-tests assumptions.

### Confidence Levels
State your confidence explicitly:
- **High (>80%)**: Execute. Don't over-deliberate.
- **Medium (40–80%)**: Run a time-boxed experiment.
- **Low (<40%)**: Gather more data before committing.

---

## Phase 5: Execution Planning

### The Minimum Viable Test
What's the smallest action that would increase our confidence by the most?

- Not a full build — a prototype, a survey, a manual test, a spike
- Time-box it: 1–3 days max for high-uncertainty bets

### Dependency Mapping
```
Task → Depends on → Blockers → Owner
```
Find the critical path. Parallelize everything off it.

### Success Metrics
Define before executing:
- **Leading indicators**: What signals early success? (early, measurable)
- **Lagging indicators**: What confirms success? (delayed, definitive)
- **Kill criteria**: At what point do we stop and pivot?

---

## Framework Selection Guide

| Situation | Best Framework |
|-----------|---------------|
| Unknown root cause | 5 Whys |
| Complex, multi-cause problem | Fishbone |
| Choosing between options | Solution Evaluation Matrix |
| High-stakes decision | Pre-Mortem |
| Unclear problem | Problem Statement Template |
| Stuck in analysis paralysis | Reversibility Test |
| Need creative solutions | Diverge-before-converge |

---

## Anti-Patterns

- **Solutionizing**: Jumping to a solution before understanding the problem
- **Root Cause Laziness**: Stopping at the first "why" (proximate vs. root cause)
- **Analysis Paralysis**: Running more analyses when you have enough to decide
- **Scope Creep in Problem Definition**: Adding more to the problem instead of solving it
- **Hero Problem-Solving**: Solving alone when the right people aren't in the room
