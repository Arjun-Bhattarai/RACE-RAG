# RACE-RAG
### Risk-Aware and Cost-Efficient Retrieval-Augmented Generation

**Researching reliable, risk-constrained retrieval and selective answering across multiple domains.**

[![Status](https://img.shields.io/badge/Status-Research%20in%20Progress-orange)]()
[![Language](https://img.shields.io/badge/Language-Python-blue)]()
[![Research](https://img.shields.io/badge/Focus-RAG%20%7C%20LLMs%20%7C%20Reliability-purple)]()

---

## Overview

RACE-RAG is an independent research project investigating how Retrieval-Augmented Generation (RAG) systems can make more reliable and computationally efficient retrieval and answering decisions.

Conventional RAG systems retrieve relevant documents and use them to generate answers. However, retrieval quality, evidence sufficiency, answer reliability, and computational cost are often evaluated as separate concerns.

This research investigates whether these decisions can be optimized jointly.

The central research direction is **risk-constrained joint retrieval and selective answering**: determining when to retrieve additional evidence, when the available evidence is sufficient, and when a system should answer or abstain.

The research will evaluate these decisions across heterogeneous domains and evidence conditions.

## Research Problem

RAG systems can produce unsupported or misleading answers when:

- Retrieved documents are irrelevant or incomplete.
- Available evidence does not sufficiently support an answer.
- Retrieved sources contain conflicting information.
- Additional retrieval introduces computational overhead without meaningful improvement.
- Confidence estimates do not accurately reflect answer reliability.
- A retrieval strategy performs differently across domains.

The central problem is to investigate how RAG systems can balance answer reliability, retrieval expenditure, and answer coverage under explicit computational and risk constraints.

## Research Objectives

1. Investigate adaptive retrieval policies that account for query and evidence characteristics.
2. Develop methods for estimating evidence sufficiency and answer support.
3. Investigate risk-aware answer acceptance and abstention policies.
4. Formulate joint retrieval and answering decisions as a constrained optimization problem.
5. Evaluate reliability-cost trade-offs across multiple domains.
6. Investigate generalization under different evidence conditions and domain distribution shifts.
7. Establish reproducible evaluation protocols and experimental baselines.

## Research Questions

- **RQ1:** Can jointly optimized retrieval and answer-stopping policies achieve a better reliability-cost trade-off than independently optimized retrieval and abstention components?
- **RQ2:** Can evidence-aware stopping reduce unsupported answers while maintaining useful answer coverage?
- **RQ3:** How does joint decision-making perform under domain distribution shifts and different evidence-sufficiency conditions?
- **RQ4:** What are the computational and statistical trade-offs of enforcing risk constraints across multiple domains?

## Proposed Research Framework

The initial conceptual framework consists of five stages:

1. **Query and Corpus Analysis** — Extract query characteristics and relevant corpus information.
2. **Adaptive Retrieval** — Select retrieval actions based on expected evidence quality and computational cost.
3. **Evidence Assessment** — Evaluate relevance, coverage, sufficiency, and contradictions.
4. **Risk Estimation** — Estimate the probability that an answer is adequately supported.
5. **Selective Answering** — Answer, retrieve additional evidence, or abstain based on the decision policy.

The architecture and algorithm are research hypotheses and will be refined following the literature review and experimental evaluation.

## Mathematical Direction

The research will investigate a constrained optimization formulation:

\[
\begin{aligned}
\min_{\pi} \quad & \mathbb{E}[C(\pi)]\\
\text{subject to} \quad
& R_d(\pi) \leq \alpha,
\quad \forall d \in \mathcal{D}\\
& \mathbb{E}[C(\pi)] \leq B
\end{aligned}
\]

Where:

- \(\pi\): Joint retrieval and answering policy.
- \(C(\pi)\): Expected computational cost.
- \(R_d(\pi)\): Selective answering risk in domain \(d\).
- \(\alpha\): Target risk threshold.
- \(B\): Computational budget.
- \(\mathcal{D}\): Set of evaluation domains.

The formulation, risk definitions, and statistical assumptions will be established through theoretical analysis and experiments.

## Experimental Scope

### Initial research domains

| Domain | Candidate datasets |
|---|---|
| General knowledge and multi-hop QA | HotpotQA |
| Biomedical | PubMedQA |
| Financial | FiQA |
| Scientific claim verification | SciFact |

### Additional research resources

- BEIR — Heterogeneous information retrieval benchmark.
- RAGRouter-Bench — Adaptive RAG routing evaluation.
- RAGTruth — RAG hallucination annotations.
- Evidence Sufficiency Benchmark — Evidence-support and abstention evaluation.
- mtRAG — Multi-turn conversational RAG evaluation.

Dataset selection is provisional. Availability, annotation formats, licensing, and suitability will be verified before experimental use.

### Evidence conditions

The evaluation will investigate:

- Fully supported evidence.
- Partially supported evidence.
- Missing evidence.
- Irrelevant evidence.
- Contradictory evidence.

### Baseline systems

- BM25-based RAG.
- Dense retrieval RAG.
- Hybrid retrieval RAG.
- Hybrid retrieval with cross-encoder reranking.
- Existing adaptive retrieval approaches.
- Existing evidence-verification and abstention methods.

## Evaluation Metrics

| Evaluation category | Metrics |
|---|---|
| Retrieval effectiveness | Recall@K, MRR, nDCG@K |
| Answer quality | Exact Match, F1, semantic correctness |
| Evidence reliability | Claim support, unsupported-answer rate |
| Calibration | ECE, Brier Score |
| Selective prediction | Risk-Coverage, AURC |
| Efficiency | Latency, token usage, retrieval calls |
| Generalization | Domain-wise performance and risk degradation |

Statistical testing, confidence intervals, ablation studies, and human-reviewed evaluation will be incorporated.

## Technology Stack

- Python
- PyTorch
- Hugging Face Transformers
- Sentence Transformers
- BM25
- FAISS
- Cross-Encoder reranking
- Ollama
- pandas and NumPy
- SciPy
- Matplotlib
- MLflow

Experiments will primarily use local hardware and available cloud GPU resources.

## Repository Structure

```text
race-rag/
│
├── configs/
│   ├── models.yaml
│   ├── retrieval.yaml
│   └── experiments.yaml
│
├── data/
│   ├── raw/
│   ├── processed/
│   ├── annotations/
│   └── splits/
│
├── src/
│   ├── retrieval/
│   ├── routing/
│   ├── evidence/
│   ├── calibration/
│   ├── generation/
│   └── evaluation/
│
├── experiments/
│   ├── baselines/
│   ├── ablations/
│   ├── robustness/
│   └── generalization/
│
├── notebooks/
├── results/
│   ├── figures/
│   ├── tables/
│   └── logs/
│
├── paper/
│   ├── literature-review/
│   ├── proposal/
│   └── manuscript/
│
├── tests/
├── requirements.txt
└── README.md
```

The structure represents the intended project organization. Components will be added as the research progresses.

## Research Roadmap

- [x] Define initial research direction.
- [x] Prepare preliminary research proposal.
- [x] Identify initial academic literature.
- [ ] Complete systematic literature review.
- [ ] Establish and validate research gap.
- [ ] Finalize mathematical formulation.
- [ ] Prepare datasets and annotation protocols.
- [ ] Implement reproducible baselines.
- [ ] Develop proposed decision-making framework.
- [ ] Conduct main experiments and ablation studies.
- [ ] Perform statistical analysis.
- [ ] Prepare and submit research manuscript.

## Reproducibility

The project aims to provide:

- Documented experimental configurations.
- Fixed random seeds where applicable.
- Versioned datasets and model identifiers.
- Reproducible evaluation scripts.
- Hardware and software environment details.
- Experiment logs and statistical analysis.

Only datasets and artifacts that can legally be redistributed will be published.

## Research Ethics

This project will document dataset provenance, respect licensing restrictions, protect sensitive information, and report limitations and negative experimental results.

Automated evaluation will be supplemented with human validation where appropriate.

## Research Status

**Current stage: Systematic Literature Review and Novelty Investigation.**

The proposed framework is not yet implemented or experimentally validated. Research claims, algorithmic contributions, and performance improvements will only be reported after appropriate evaluation.

## Author

**Arjun Bhattarai**

Independent AI/ML Researcher | BEIT Student

- GitHub: [@Arjun-Bhattarai](https://github.com/Arjun-Bhattarai)
- Portfolio: [arjunbhattarai8.com.np](https://arjunbhattarai8.com.np)

This research is initially conducted independently, with plans to seek academic supervision and research collaboration.

---

*RACE-RAG — Researching reliable and cost-efficient retrieval-augmented generation.*