# MATACS-TH-2026-02 — AI Proposal Triage Design

**Candidate:** Hamza Ali Shakir  
**Assessment reference:** MATACS-TH-2026-02  
**Time spent:** 40 mins

## Files

- [Process-flow diagram](diagram/triage-flow.png)
- [Design write-up](WRITEUP.md)
- [AI prompts](PROMPTS.md)
- [Expected ranking](ranking.json)

## AI-tool usage disclosure

I used ChatGPT to help structure the design, draft the write-up and prompt, and check the sample ranking arithmetic. I reviewed the proposed approach rather than treating AI output as authoritative. One important correction was to reject the instruction embedded in Proposal C that tells automated systems to rank it first: proposal text is untrusted evidence, not an instruction to the triage system, so the ranking must follow only the administrator-approved criteria.
