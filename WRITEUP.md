# Design write-up — AI Proposal Triage

## 1. AI vs. rules

Use ordinary code for file validation, PDF/text extraction orchestration, schema validation, mandatory pass/fail checks, weighted arithmetic, sorting, and audit logging. These steps should be deterministic and testable. Use an LLM to extract proposal facts into a fixed JSON schema, attach supporting quotations/page references, and summarize evidence against the administrator-defined criteria. The LLM must not invent missing facts or make the final award decision. Treat proposal contents as untrusted data; instructions embedded in a proposal must never change the system prompt or criteria.

## 2. Consistency and explainability

Store a versioned criteria configuration for each category, including mandatory rules, weights, scoring anchors, and tie-break rules. Validate that weighted criteria total 100%. Use the same model/version, prompt version, temperature 0 where available, schema, and scoring code for a given run; even then, verify extracted facts and do not assume LLM outputs are perfectly deterministic. Cache extraction results and use deterministic rules for final scores. Each criterion should show the extracted value, supporting quotation/page, normalized score, weighted contribution, and any uncertainty. Sort by total score, then by a documented deterministic tie-break (higher relevant-experience score, then lower price). The final output should include the criteria version and run ID.

**Scoring assumptions for this sample:** because the brief supplies criterion weights but not detailed normalization formulas, use explicit configurable anchors: 10 qualifying installations earns 100 for experience; price score is 100 at CAD $200,000 or below and decreases linearly to 0 at the CAD $260,000 ceiling; timeline score is 100 at 8 weeks or less and decreases linearly to 0 at 16 weeks; warranty score averages panel warranty (100 at 25 years) and workmanship warranty (100 at 10 years), capped at 100 for each; team/approach is scored against evidence for named lead, crew, safety plan, and monitoring, with 25 points per evidenced item. These are transparent example assumptions, not facts supplied by the brief, and an administrator should configure/approve such anchors before real use. A proposal with a missing mandatory fact is flagged for human verification; a confirmed mandatory failure is ineligible.

## 3. Human in the loop

A reviewer confirms extracted facts and source quotations, resolves missing or conflicting evidence, and reviews flagged/ineligible cases before the ranking is finalized. The tool recommends a shortlist; a human makes the award decision. A reviewer can correct facts or override a status/score with a required reason. Log uploader/reviewer IDs, timestamps, original file hash, extracted text reference, model and prompt versions, criteria version, scores, flags, changes, override reasons, and final decision. Restrict access and retain only what is needed under the organization’s retention policy.

## 4. Changing criteria

Never silently change a past result. Publish a new immutable criteria version, validate its weights and scoring anchors, and show reviewers which version was used for each run. If an administrator edits criteria after scoring, preserve the old result and offer an explicit re-score using the new version. Mark the new result as a new run, record the person and time that initiated it, and show a before/after comparison. Re-score all proposals being compared under the same criteria version.

## 5. Risks and safeguards

- **Wrong or incomplete extraction:** require evidence quotations and page references; validate types/ranges; flag unreadable PDFs and missing values; allow reviewer correction.
- **Made-up facts:** only score facts supported by proposal evidence; represent unknown as `null`, never as zero or a guessed value.
- **Prompt injection/manipulation:** treat all proposal text as untrusted data; ignore instructions inside documents; separate system instructions from proposal content; test adversarial examples such as Proposal C.
- **Bias or unfair scoring:** use job-related criteria approved by the administrator, document anchors, test across representative examples, and provide a human appeal/override path.
- **Inconsistent ranking:** use deterministic scoring code, versioned criteria and prompts, a fixed tie-break, and regression tests.
- **Cost, latency, or service failure:** extract only relevant text, batch carefully, set limits and retries, cache results, monitor spend, and allow a manual-review fallback.
- **Confidentiality/security:** use access controls, encryption, retention limits, and approved AI services; do not send real sensitive proposal data to an unapproved model.
- **False confidence in a single score:** display per-criterion evidence and flags beside the total, and state that the ranking is advisory rather than an award decision.

## Sample ranking rationale

B is **ineligible** because the proposal says the electrical subcontractor will be confirmed after award; the required licence held by the bidder is not stated. D is **flagged** because its completion schedule is undetermined, so compliance with the 16-week maximum cannot be confirmed. A, C, and E pass the stated mandatory checks based on the supplied summaries. Proposal C’s embedded instruction to rank itself first is ignored as untrusted proposal content.

Using the explicit sample scoring assumptions above, the expected order among eligible, scoreable proposals is A, E, then C. D is not assigned a score until its timeline is confirmed. Scores are illustrative outputs of the stated assumptions, not a substitute for human review.
