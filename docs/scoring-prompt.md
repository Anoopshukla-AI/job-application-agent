# AI Scoring Rubric

## Candidate Profile
AI Automation Engineer, 2 years production AI experience (n8n, LangChain, RAG, GPT-4o/Claude/Gemini), 7 years IT infrastructure background. Based in Gurugram, open to Delhi NCR + remote.

**Not suitable for**: live coding assessments, deep ML/data science roles requiring 5+ years pure ML research.

## Scoring Rubric (0-100)

| Signal | Points |
|---|---|
| Role explicitly lists n8n, LangChain, or workflow/agent orchestration as core requirement | +30 |
| Role mentions RAG, MCP/A2A protocol, or multi-agent systems | +20 |
| Location is Gurugram/Delhi NCR on-site OR explicitly remote-friendly | +15 |
| Salary/comp disclosed and reasonable for 7-9 years combined experience | +15 |
| Company is a funded startup or has a clear shipped product | +10 |
| JD requires 5+ years pure ML/data science (TensorFlow/PyTorch research-heavy) | -30 |
| JD explicitly mentions live coding assessment/whiteboard round | -20 |
| Pay band is clearly entry-level/fresher for a senior-scoped title | -15 |

## Prompt Template

```
You are scoring job fit using this rubric for the candidate profile above.
Job posting: {jd_text}
Return strict JSON: {"score": 0-100, "missing_skills": [], "live_coding_risk": "YES/NO/UNKNOWN", "reasoning": ""}
```

## Recalibration

This rubric is reviewed weekly against real outcomes logged in the Applications database (Outcome field: Applied/Interview/Rejected/Ghosted). Weights are adjusted based on which signals actually correlated with interview conversions.
