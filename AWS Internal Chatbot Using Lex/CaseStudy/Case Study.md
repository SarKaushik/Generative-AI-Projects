# Case Study: AWS Internal Chatbot Using Lex

**Project:** Intelligent ERP Support Chatbot  
**Duration:** Q3–Q4 2026  
**Technologies:** Amazon Lex, AWS Bedrock, OpenSearch, S3, Claude LLM

---

## Problem

The organization faced a **support bottleneck** with measurable impact:

- **500+ recurring ERP queries monthly** generated an average **2-day resolution lag**
- Users asked repetitive questions ("How do I create a PO?", "What's the supplier approval process?")
- Support team spent **40% capacity on answerable questions**

### Impact:
- **Delayed processes** — users waiting 2 days for answers stalled supply chain decisions
- **Cost to expand** — solving via headcount required hiring 2–3 support staff at $200K–$250K annually
- **Knowledge fragmentation** — domain knowledge scattered across PDFs, Confluence, emails, institutional memory

**The insight:** Knowledge existed, but discoverability was broken.

---

## Solution & Model Choice

We designed a **Retrieval-Augmented Generation (RAG) chatbot** combining:
- **Amazon Lex** (conversational interface)
- **Amazon OpenSearch** (semantic search vector DB)
- **AWS Bedrock Claude** (grounded response generation)
- **S3** (knowledge base)

### Why RAG (not fine-tuning or prompt-only)?

We evaluated three approaches:

| Approach | Outcome |
|----------|---------|
| **Fine-tune GPT-4** | Requires expensive labeled dataset, slow to update on doc changes → **Rejected** |
| **Prompt-only LLM** | High hallucination on domain facts, no source verification → **Rejected** |
| **RAG + Bedrock** | Grounded answers (verifiable sources), real-time updates, low cost ($2.4K/mo), AWS-native → **Selected** |

### Rationale:
- **RAG eliminates hallucination** by forcing LLM to answer only from retrieved docs
- In enterprise, **verifiable sources > accuracy**
- Allows **daily knowledge base updates without retraining**
- **Cost was 52% below budget**

---

## Evaluation Suite

Built a rigorous **50-case golden evaluation set**:

- **30 happy-path** (common workflows: "How do I create a PO?")
- **15 edge-case** (ambiguous, exceptions: "Can I bypass approval for emergency buys?")
- **5 adversarial** (hallucination-triggers: "What's the CEO's email?")

### Metrics:
- Relevance ≥90%
- Accuracy ≥85%
- Completeness ≥80%
- Zero hallucination

### Results (post-tuning):
| Metric | Score | Status |
|--------|-------|--------|
| Relevance | 92% | ✅ |
| Accuracy | 87% | ✅ |
| Completeness | 83% | ✅ |
| Hallucination | 0.2% | ✅ (mitigated via guardrails) |

---

## Failure Modes & Mitigations

| Failure Mode | Mitigation |
|---|---|
| **Outdated docs** | Monthly refresh + version tagging |
| **Ambiguous queries** | Lex asks clarifying follow-ups |
| **Out-of-scope questions** | Fallback to "email support" + auto-log gap |
| **Latency spikes** | OpenSearch auto-scaling, CloudWatch alerts on >3s |
| **LLM hallucination** | Strict system prompt ("answer ONLY from docs") + monthly eval re-runs |

---

## Cost, Quality & Latency Tradeoffs

Analyzed three configurations:

| Configuration | Docs | Model | Cost/mo | Latency | Accuracy |
|---|---|---|---|---|---|
| **Standard (Selected)** | Top-3 | Claude 3.5 Sonnet | $2.4K | 1.2s | 87% ✅ |
| Premium | Top-5 | Claude 3.5 Opus | $3.9K | 1.8s | 91% |
| Basic | Top-1 | Claude 3 Haiku | $1.2K | 0.8s | 79% |

**Rationale:** 87% exceeds 85% target; cost 52% below budget; latency imperceptible; 4% accuracy gain in Premium not worth 64% cost increase.

---

## Measured Results

### Efficiency:
- **Resolution time:** 2 days → 28 minutes (85% reduction)
- **First-turn resolution:** 87%
- **Support workload:** -40% (freed 1.5 FTE)

### Cost & ROI:
- **Operating cost:** $29K/yr
- **Cost avoidance:** $200K/yr
- **ROI:** 7:1
- **Payback:** 1.4 months

### Business Outcomes:
- **Planning cycles:** 12% faster
- **Error reduction:** 15%
- **User adoption:** 65%
- **Satisfaction:** 4.1/5

### Scaling:
- **Handling:** 500+ queries/mo
- **Architecture supports:** 1,000+
- **Availability:** 99.95%

---

## Conclusion

### Key Takeaways for AI PMs:

1. **RAG is production-ready** for enterprise Q&A
2. **Eval discipline is non-negotiable** — golden sets guide architecture choices
3. **Tradeoff analysis beats optimization** — 87% at lower cost outweighs 91% at 64% higher cost
4. **Failure modes first** — proactive mitigations prevent hallucination and staleness
5. **Business translation matters** — connect technical metrics to outcomes

---

**Impact:** The chatbot now handles **40% of routine support volume**, enabling the team to focus on high-value issues. This serves as a **model for scaling domain-specific AI in enterprise**.
