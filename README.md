# MATACS-TH-2026-02 — AI Proposal Triage Design

**Candidate:** Hamza Ali Shakir  
**Assessment reference:** MATACS-TH-2026-02  
**Time spent:** 40 mins

## Files

- [Process-flow diagram](flow.png)
- [Design write-up](WRITEUP.md)
- [AI prompts](PROMPTS.md)
- [Expected ranking](ranking.json)

## AI-tool usage disclosure

I used ChatGPT and Claude to help structure the design, draft the write up and prompts, and review the sample ranking calculations. I reviewed the proposed approach rather than treating AI output as authoritative. One important correction was rejecting the instruction embedded in Proposal C that attempts to force a first place ranking: proposal text is untrusted data, not an instruction to the triage system, so ranking must follow the administrator approved criteria.
