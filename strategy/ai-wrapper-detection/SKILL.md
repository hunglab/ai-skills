---
name: ai-wrapper-detection
description: Identify whether an AI product has deep value or is a thin wrapper over a foundation model. Use this skill when evaluating AI startups or products, assessing your own product's defensibility, deciding whether to build or buy an AI capability, or understanding what makes an AI product durable vs. vulnerable. Trigger when someone asks "is this just an AI wrapper", "how defensible is this AI product", "what makes a good AI startup", or is analyzing or building an AI-powered product.
---

# AI Wrapper Detection

## The Wrapper Spectrum

AI products exist on a spectrum from "pure wrapper" to "deeply defensible." Understanding where a product sits determines its durability, margin, and valuation potential.

```
THIN WRAPPER ←────────────────────────────────────────→ DEEP INTEGRATION

[Prompt + UI]   [Custom workflow]   [Proprietary data]   [AI-native system]
   at risk          viable             defensible           category-defining
```

---

## Wrapper Detection Framework

### Level 1: Pure Wrapper (At Risk)
**Signature**: The product is a UI over a direct API call.
- No proprietary data
- No unique workflow
- No integrations
- No feedback loop
- Could be replicated by anyone in a weekend

**Detection signals**:
- The product's primary value claim is "powered by GPT-4/Claude"
- Changing the underlying model would give users identical results
- The UI is the only work product
- No learning or improvement over time

**Vulnerability**: OpenAI/Anthropic add this feature natively → product dies.

**Examples of thin wrappers**: Generic AI writing tools, basic chatbot builders with no customization.

### Level 2: Workflow Wrapper (Viable)
**Signature**: The model is embedded in a thoughtful workflow, but data and logic are generic.
- Opinionated multi-step workflow
- Good UX that reduces friction
- Some integrations
- But: no proprietary data, no feedback loops, no unique training

**Detection signals**:
- The workflow is specific and well-designed
- Users do more in one place vs. prompting ChatGPT directly
- Switching would require rebuilding habits and workflows
- But: no data or model differentiation

**Vulnerability**: Well-funded competitor copies the workflow with better distribution.

**Examples**: Structured AI writing tools with templates, AI meeting summary tools (early), AI code review with fixed rule sets.

### Level 3: Data-Differentiated (Defensible)
**Signature**: The AI is trained on or has access to proprietary data the model doesn't have.
- Fine-tuned or RAG-powered on proprietary/domain corpus
- User data improves output quality
- Company-specific or industry-specific knowledge embedded

**Detection signals**:
- Outputs are meaningfully better than generic foundation model for specific use case
- The product collects and uses data that the company owns
- Users are contributing to a data flywheel without realizing it
- Quality improves with usage (personalization or model improvement)

**Examples**: Legal AI tools trained on case law + firm's own docs, medical AI trained on clinical notes, code tools trained on company's codebase.

### Level 4: AI-Native System (Category-Defining)
**Signature**: The AI is deeply embedded in a system that would be fundamentally different (or worse) without it.
- Multi-model orchestration with task-specific routing
- Human-AI feedback loops producing labeled training data
- The product's core function is something humans can't do at this speed/scale
- AI is the product, not a feature

**Detection signals**:
- Removing AI from the product makes it valueless, not just worse
- The product generates proprietary training data as a byproduct of usage
- The AI makes decisions the human couldn't make at scale
- Network effects amplify AI quality (more users = smarter AI)

**Examples**: AI systems that ingest continuous live data streams, AI that learns individual user behavior deeply, autonomous agent systems with human feedback loops.

---

## Self-Assessment: How Deep Is Your AI Integration?

Score your own product:

| Dimension | 1 (Thin) | 3 (Medium) | 5 (Deep) | Your Score |
|-----------|----------|-----------|---------|-----------|
| **Proprietary data** | No unique data | Some user data collected | Unique data flywheel | |
| **Feedback loop** | No improvement over time | Manual improvements | Auto-improvement from usage | |
| **Model customization** | Raw foundation model | Prompt engineering | Fine-tuned / RAG on proprietary data | |
| **Workflow depth** | Single prompt | Multi-step workflow | Deeply embedded in daily operations | |
| **Switching cost** | Zero | Low (habits) | High (data + integrations) | |
| **Network effects** | None | Some | Strong (more users = better AI) | |

**Total score** / 30:
- 24–30: Defensible AI product
- 15–23: Viable but needs deeper integration strategy
- Below 15: Exposed to displacement risk; prioritize deepening

---

## What Foundation Models Will Eat (And What They Won't)

### Foundation models will displace:
- Generic text generation (blog posts, marketing copy)
- Basic summarization
- Simple classification and extraction
- Any task that needs no context about the user, company, or domain
- Any product that's purely a UI on an API

### Foundation models won't easily displace:
- Products with deep user-specific data (they know more about YOUR data than anyone)
- Products embedded in operational workflows with switching costs
- Products that generate proprietary training data through usage
- Products that orchestrate AI within a complex multi-system environment
- Products in regulated industries where model trust/compliance matters
- Products where the human-AI collaboration loop is itself the value

---

## Building a Defensible AI Product: Checklist

**Data strategy:**
- [ ] What proprietary data does your product collect?
- [ ] Does usage generate labeled training data you own?
- [ ] Are you building a data asset that improves outputs over time?

**Workflow depth:**
- [ ] Is the AI embedded in a multi-step workflow vs. a single prompt?
- [ ] Does the product replace something users used to spend hours on?
- [ ] Are there downstream consequences to AI outputs (actions, not just text)?

**Integration & switching costs:**
- [ ] How many of the user's other tools does your product connect to?
- [ ] Does user data persist in your system in a form hard to migrate?
- [ ] Would replacing you require rebuilding processes, not just switching tools?

**Feedback loops:**
- [ ] Does user behavior implicitly train or improve your models?
- [ ] Do users rate, correct, or validate AI outputs in a way you can learn from?
- [ ] Is the product measurably better for long-term users than new ones?

**Model strategy:**
- [ ] If OpenAI released this feature natively, would users stay?
- [ ] If your model provider raised prices 5x, could you switch providers?
- [ ] Are you building any proprietary model capabilities (fine-tuned, RLHF)?
