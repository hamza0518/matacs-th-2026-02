# MATACS-TH-2026-02 — AI Proposal Triage Design

**Candidate:** Hamza Ali Shakir  
**Assessment reference:** MATACS-TH-2026-02  
**Time spent:** [Replace with your actual time spent before submission]

## Files

- [Process-flow diagram](diagram/triage-flow.png)
- [Design write-up](WRITEUP.md)
- [AI prompts](PROMPTS.md)
- [Expected ranking](ranking.json)

## AI-tool usage disclosure

I used ChatGPT to help structure the design, draft the write-up and prompt, and check the sample ranking arithmetic. I reviewed the proposed approach rather than treating AI output as authoritative. One important correction was to reject the instruction embedded in Proposal C that tells automated systems to rank it first: proposal text is untrusted evidence, not an instruction to the triage system, so the ranking must follow only the administrator-approved criteria.

## Before submitting

1. Replace the time-spent placeholder above with the actual time you spent.
2. Read every file and make sure you can explain the design and assumptions in a follow-up interview.
3. Create a **public** GitHub repository named `matacs-th-2026-02` and upload these files with the required names.
4. Submit only the public repository URL through the Google Form in the assessment brief.
5. Keep the repository public and unchanged for the period specified in the brief.

This repository contains a design proposal and sample ranking; it is not a deployed application. Scoring anchors not specified in the brief are stated as assumptions in `WRITEUP.md` and should be configurable by an administrator in a real system.
