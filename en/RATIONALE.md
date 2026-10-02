# Rationale

Companion to the [Manifesto for Trustworthy AI-Driven Testing](MANIFESTO.md) · Draft v0.1 · 2026-10-02 · [Русская версия](../ru/RATIONALE.md)

This document explains why the four values were chosen, what each principle means in practice, how a team could pilot the principles, and where the ideas came from. The examples illustrate requirements on the process. They are not a defect report on any tool or a claim that any tool conforms. No pilots have been run yet; everything below is a proposal open to challenge.

The manifesto has two layers. The core (scope, values and principles) should change rarely. This rationale holds examples and practices and may be revised more often. If a conformance specification is ever needed, it will be a separate document with its own assessment procedure.

## Key terms

| Term | Meaning in these documents |
| --- | --- |
| Evidence | A record of an observation or execution, with enough context to judge what it supports. A file existing does not by itself make it reliable. |
| Test oracle | The basis for deciding whether observed behavior matches expectations: a rule, a contract, a property, an expert judgment or another explicitly chosen criterion. |
| Testing intent | The question about the product or the risk that the work exists to answer. It can survive changes to concrete steps and locators. |
| Autonomy | The scope of decisions and actions delegated to a system within set limits. It is a property of a process, not a goal in itself. |
| Human accountability | Assigned authority and duty to decide on rules and consequences. It does not require manually approving every action. |
| Repeatability | The ability to reproduce the essential conditions and check a result again. For changing systems and probabilistic evaluations, an exact match is not always achievable. |

"AI-driven" here covers every degree of AI involvement, including a specialist occasionally asking an assistant for help. Whether "AI-assisted" would read more clearly is one of the open questions below.

## Why these four values

| Value | Decision it helps make | Cost and acceptable tradeoff |
| --- | --- | --- |
| Evidence that supports decisions over the volume of generated tests | Choose work that checks a meaningful risk, even if it produces fewer test artifacts. | Bulk generation is useful for exploring variants and widening coverage. Judge its volume together with the novelty and quality of the checks. |
| Reviewable conclusions over the speed of reaching a verdict | Keep the ability to understand why a result was accepted as convincing. | A fast preliminary signal is fine when its preliminary status is visible. How much to retain depends on how important the decision is. |
| Accountable human judgment over the extent of agent autonomy | Delegate work together with its limits, a decision owner and stop conditions. | For repetitive operations, an agreed policy is enough. Approving every step by hand often just slows feedback and trains people to click "approve". |
| Preserving testing intent over the convenience of automatic adaptation | Check that an automatic repair still verifies the original product property. | Replacing the technical way of reaching an element can be automatic. Changing expected behavior needs a separate review. |

These are priorities for discussing concrete choices. They do not set approval deadlines, an automation ratio or a mandatory amount of logging. If applying a principle costs more than its expected benefit, discuss how it is implemented and what risk remains, instead of hiding the exception.

## The principles in practice

### P1. Start from risk, not from test count

AI makes it cheap to produce many scenarios. To judge their value, tie them to questions about the product: can a user lose data, see someone else's document, or be locked out of an important flow by the interface?

Practical test: the team can say which decision would change if the problem were found. For an exploratory session, a meaningful question and recorded findings are enough; a permanent automated test is not required. For accessibility and usability, AI does not replace observing real users.

### P2. Delegate work, not accountability

Automating execution does not assign an owner to the decision about acceptable risk. Decide in advance who sets the rules, who may widen the scope of work and who receives ambiguous results. Accountability must not turn into a formal signature by someone who has no time or authority to check.

For example, re-running an approved regression suite on a disposable environment can be fully automatic. Moving to another environment, or an action with materially different consequences, requires revisiting the permission. A release decision can be made by an assigned role or by the team's process; it does not become the AI's call just because the AI wrote the report.

### P3. No record, no claim

A proposed test, an attempt to run it and the observed result are different events. If they look the same in a report, a reader can mistake a plausible scenario for a verified fact.

A report should make clear what the AI proposed, what a tool or a person actually executed, and what a conclusion rests on. A failed tool call leaves the attempt incomplete. A model's confident wording does not replace a missing record. In manual exploratory work, a specialist's notes with the conditions and limits of the observation are a valid record.

### P4. Don't let the generator grade its own work

The same generator can propose both an action and a wrong expectation, and then successfully confirm its own assumption. The source of an expectation therefore has to be explicit: an agreed rule, a verified contract, a domain property, an expert decision, or a hypothesis labeled as such.

Independence means an independent basis for the check. A second model with the same assumptions does not provide it automatically. If the expected behavior is unknown, an exploratory result without a final verdict is acceptable. For subjective properties, model-based evaluation against set criteria can work if it has been tested on representative examples, compared with independent judgment, and its limits are stated.

### P5. A green run is not a check

A passing run shows that the runner did not register an error in the code it executed. That is not enough to conclude the intended property was checked. Having an assertion does not settle it either: asserting something always true, or irrelevant text, may say nothing about the risk.

Textbook example: a test clicks "Save" and finishes without checking the saved data. Its green status does not confirm anything was saved. For important checks, confirm they react to a known violation: corrupted data, a controlled defect, a failing dependency. Mutation testing can help, but its score does not prove every business expectation is right either.

### P6. Every verdict traces back to evidence

Another specialist should have enough context to see which observation supports a given conclusion. That usually means the source of the expectation or the exploratory question, the product version, the essential conditions, the actions, the observations and the limitations.

Size the record by risk. For a simple API property, a sanitized response and the check result may be enough; a video of the whole session is not required. A hash helps detect a change relative to a trusted record, but on its own it does not establish authorship, that an event really happened, or that a conclusion is true. If one participant can freely rewrite both an artifact and its integrity record, additional trust measures proportionate to the risk are needed.

### P7. Blocked is not passed

A report must keep the difference between a found defect, a tool error, missing access, a skipped check, a partial check and an inconclusive observation. Missing credentials, for example, usually mean the check was blocked, not that the feature under test is defective.

Status names can differ between tools; what matters is their meaning and that it survives into the summary. "All executed checks passed" should show how much work lies outside that statement. A numeric confidence reported by a model is not a measured probability of being right unless its calibration has been checked separately.

### P8. Make important findings repeatable, or say why they are not

Re-running helps investigate a problem and verify a fix. That requires keeping the essential versions, configuration, data conditions, actions and criteria. Where they are available and affect interpretation, record the model and parameters used.

Exact repetition is not always possible: external systems change, data gets deleted, model services are updated. Report such limits. For exploratory work, suitable context and evidence are enough; a probabilistic evaluation may need a series of runs with a comparison method chosen in advance. The principle does not require exposing a model's hidden reasoning or storing full conversations that contain secrets.

### P9. Instructions are not controls

An instruction to an agent describes a rule; it does not guarantee the rule is followed. Important limits must be enforced by the environment, permissions, tools or checks right before an action. Guarding one path does not protect an alternative path to the same resource.

Example: the agent may only work with test records on a dedicated environment. That limit must hold for the browser, for direct HTTP calls and for any other way the agent can act. Text on a page cannot lift it. A "read-only" label or an HTTP method does not by itself prove there are no side effects; the team assesses what actions really do and how much damage they could cause.

### P10. A self-healing test must still test the same thing

Automatic adaptation is useful when the technical way of finding an element or performing a check changes. It is dangerous when it silently changes meaning: for example, a test that used to confirm a paid order now only checks that the order page exists.

Changes to locators, data and expectations should be visible and linked to the check they affect. If a change falls within the scope of an earlier approval, that approval must be revisited. Binding approval to a hash of the exact artifact is one implementation; another process might assess the semantic impact of a change. Neither removes the need to understand what exactly was approved.

### P11. Give agents access, not secrets

Sufficient evidence is compatible with data minimization. Model context, logs, network captures and screenshots are each a separate place where information can leak. Limit what is collected, who receives it, who can access it and how long it is kept, and account for personal data that ends up in observations by accident.

Prefer a setup where the tool holds the credentials and the agent refers to a named access profile. Redacting sensitive values after they were recorded is a second line of defense, not a substitute for not passing them in the first place. If redaction limits later analysis, record that limitation too.

### P12. Measure what testing catches and costs, not what it produces

The number of tests and green runs says nothing about how many important problems were found or missed. Evaluate the quality of checks and reports, the cost of triaging, maintaining and running them, and their effect on real decisions.

In a pilot, seeded defects and independent spot checks of results are useful. On a real product, the full set of missed problems is unknown, so a detection rate cannot be claimed from the count of bugs found. The model that produced a result must not be the only basis for judging its quality. Count the people cost too: preparing context, reviewing, fixing and keeping the process running.

## How to pilot the principles

### A small record for each important conclusion

A team picks one process and writes down its starting point: which risk is being tested, what is delegated to AI, who makes the decisions and what costs are expected. Then, for a few important conclusions, it keeps a compact record:

- The question or risk, and the basis for the expected behavior.
- The product version and essential execution conditions.
- The role of AI and the actions actually performed.
- Observations and links to available evidence.
- The conclusion, unfinished work and limits of confidence.
- The acceptance rule and the accountable role; significant changes and re-decisions, if any.

This is suggested content for an experiment, not a mandatory file format. Existing records in a test management system, an exploration log or CI are fine if the links can be reconstructed from them. Sensitive data does not go into the record.

### Uncomfortable scenarios

Principles are best tested where a wrong conclusion is likely. A suggested set of training scenarios:

1. A test runs green but does not check the stated outcome. Participants should notice that the conclusion is unsupported.
2. Only part of the approved scope was executed. The summary must keep the remainder visible.
3. An automatic locator repair picks a similar but different element. The change in what the test checks must be detected.
4. An expectation changes after approval. It must be visible that the old approval no longer covers the new conclusion.
5. An external dependency is down. The failure must not turn into evidence of product quality, nor be counted as a product defect automatically.
6. The application under test tries to talk the agent into exceeding its limits. The delegated permissions must stay the same.

Run these in a suitable test environment and within its rules. A pilot never needs to touch other people's systems or real user data.

### What to measure

Before a pilot, agree on the baseline process, the sample of tasks and the method of independent evaluation. When reusing a task, remember that participants may already know the answer.

| Observation | How to report it without overstating |
| --- | --- |
| Detection of seeded defects | "Found N of M seeded defects", with a description of the set. This says nothing about unknown defects in the product. |
| False confidence | How many "check passed" results independent review found unsupported, out of how many reviewed. |
| False defect reports | How many reported defects were not confirmed, and how long triage took. |
| Reviewability | Whether another participant can reconstruct the basis of a conclusion from the retained context; record the reasons when they cannot. |
| Honest incompleteness | How many blocked, skipped and partial checks stayed correctly visible in the final report. |
| Cost | People's time, execution time, service and maintenance costs; initial setup reported separately. |
| Effect on decisions | Which choices changed because of the principles: scope adjusted, an unsupported conclusion withdrawn, a check fixed, a release reconsidered. |

Set success thresholds for the context before the comparison starts. Without a known complete set of defects, do not compute a detection rate. Failures and rising costs matter as much to revising the manifesto as positive results.

## Where the ideas came from

The principles grew out of architecture decisions in [QA-AI-STLC](https://github.com/Klim-101/QA-AI-STLC), an open-source QA framework by the same author. The table maps each decision to the general principle it illustrates. It is a comparison of intent, not an implementation audit: an `Accepted` ADR records a decision and does not by itself show that all related work is complete.

Snapshot: ADRs as of commit [`9cabb2d`](https://github.com/Klim-101/QA-AI-STLC/tree/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr), 2026-10-02.

| Decision | General principle it illustrates | What remains a project-specific choice |
| --- | --- | --- |
| [ADR 0001](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0001-no-model-calls-in-the-engine.md) No model calls in the engine | P3, P8: distinct roles for reasoning and execution; the executor can be checked on its own. | Banning LLM SDKs and keeping the model only in the agent host. |
| [ADR 0002](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0002-json-is-canonical-markdown-is-rendered.md) JSON is canonical | P6, P7: source records and their presentations stay consistent. | JSON, the schemas and the rendering mechanism. |
| [ADR 0003](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0003-hash-bound-approval-gates.md) Hash-bound approval gates | P2, P10: an approval applies to specific content. | A hash per artifact and re-approval after any change. |
| [ADR 0004](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0004-the-engine-owns-the-browser.md) The engine owns the browser | P6, P9: controlled execution and a shared evidence context. | A single owner of the browser process. |
| [ADR 0005](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0005-the-agent-has-no-browser-outside-engine-tools.md) No browser outside engine tools | P3, P6, P9: claims about actions are tied to observed execution. | Exclusive access through this engine's tools. |
| [ADR 0006](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0006-generated-tests-reference-a-locator-module.md) Generated tests use a locator module | P10: technical details can change while intent is preserved. | The generated module and element ID scheme. Extracting locators does not by itself prove meaning is preserved. |
| [ADR 0007](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0007-engine-and-plugin-share-one-version.md) Engine and plugin share one version | P8, P10: known component compatibility and controlled change. | A single version number; other systems might check a compatibility matrix. |
| [ADR 0008](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0008-tiered-coverage-thresholds-by-package-trust-level.md) Tiered coverage thresholds | P1, P5, P12: verification effort matches a component's responsibility. | The percentages and package split. Code coverage does not certify oracle quality. |
| [ADR 0009](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0009-execution-sessions-may-relax-the-get-only-rule.md) Execution sessions may relax the GET-only rule | P2, P9: delegation is bounded by the context and purpose of the work. | The GET-only rule and how other requests are allowed. |
| [ADR 0010](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0010-generation-contract.md) Generation contract | P6, P8, P10: test provenance, staleness detection and preserving manual edits. | Input and output structures, manual-region markers and contract stamps. They do not prove checks are sufficient under P5. |
| [ADR 0011](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0011-layered-project-configuration.md) Layered project configuration | P6, P9: effective settings and the origin of relaxations are visible. | Two layers and their merge rules. A warning about a relaxation does not by itself forbid it. |
| [ADR 0012](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0012-api-authentication-profiles.md) API authentication profiles | P9, P11: using credentials while passing as few secrets as possible. | Profile format, environment variables and token acquisition. |
| [ADR 0013](https://github.com/Klim-101/QA-AI-STLC/blob/9cabb2ddb47fed3f05aa1161d2edce159480e295/docs/adr/0013-browser-toolset-parity-and-compact-page-views.md) Browser toolset parity and compact page views | P3, P5, P6, P9: registered actions and expectations; bounded untrusted input. | The browser tool set, session references and snapshot format. |

An architecture with direct model calls, distributed execution or a different storage format can follow the same principles. Pilots should explain which properties they achieve and their limits, not copy the design of QA-AI-STLC.

## Prior work

Selected primary sources, reviewed 2026-10-02. This list acknowledges related work; it is not an exhaustive search or a claim of novelty. Listing a source does not imply its authors endorse this initiative.

| Source | What it covers and how it relates |
| --- | --- |
| [Manifesto for Agile Software Development](https://agilemanifesto.org/) | A short form of value priorities. The form is borrowed; the content is about the reliability of AI-driven testing results. |
| [Ministry of Testing: Day 21, Develop your AI in Testing manifesto](https://club.ministryoftesting.com/t/day-21-develop-your-ai-in-testing-manifesto/75315) | A 2024 community thread where participants wrote personal manifestos on collaborating with AI, verifying output, transparency and accountability. An open discussion, not a single adopted document. |
| [AI Quality Manifesto (sysWisdom)](https://github.com/sysWisdom/AIQualityManifesto) | A broader declaration on human accountability, verifying AI output and process governance. Overlaps substantially; trust in AI is not a theme unique to this initiative. |
| [Appvance Manifesto](https://appvance.ai/manifesto) | A vendor's vision of AI in QA and changing tester roles. A company position, not independent evidence or industry consensus. |
| [ISTQB Certified Tester Testing with Generative AI](https://istqb.org/certifications/gen-ai/) | A syllabus and certification on using GenAI in testing, including evaluating output and managing risk. An educational document of a different kind. |

This initiative's intended focus is the traceable link between a testing question, the work performed, the evidence and the conclusion, combined with honest limits and change control.

## Path to community review

| Stage | What to do | What lets us move on |
| --- | --- | --- |
| 1. Open draft | Publish v0.1 in a public repository with sources, change history and a clear way to propose amendments. | The text can be discussed without installing any tool or supporting any project. |
| 2. Independent critique | Ask 5–8 practitioners from different organizations to critique the text: manual QA, automation, tool builders, QA leads, security or accessibility. | Substantive objections and the decisions on them are recorded, including reasoned disagreement. The number of reviewers is a guide, not proof of consensus. |
| 3. Diverse pilots | Start with three contexts: exploratory work, CI regression, and an agent with delegated execution. At least one should use a different tool and be run by an independent team. | Documented cases of benefit, limits and cost; dependence of the wording on one architecture checked in practice. |
| 4. Community discussion | Present the text and pilot results in testing communities. Ask for counterexamples, not just signatures. | Feedback handled openly, wording fixed, contested points visible to readers. |
| 5. Agreed version | Prepare v1.0 with change rules, a list of real contributors and limits on claims of use. | Contributors confirm this exact version; translations checked; significant objections published. |

Real impact would mean independent teams using the principles to choose tools, design processes and evaluate results. Signatures, stars and mentions show interest, not that kind of use. A formal standard would need separate work: a defined scope, testable requirements, an assessment procedure and adoption by a relevant community or body.

## How this document evolves

The author maintains the initial text and records decisions openly. As regular contributors appear, a small editorial group with people from different organizations and approaches should form. No single vendor should have exclusive say over the principles. See [CONTRIBUTING.md](../CONTRIBUTING.md) for how to propose a change.

Endorsing the principles, reporting a pilot and confirming that specific requirements are met are three different things. v0.1 has no "certified" badge and no single conformance score. Contributors and their roles are listed only with their consent.

The manifesto is licensed under [CC BY 4.0](../LICENSE). It does not change the license of QA-AI-STLC or relicense other authors' material. References to prior work and credit for real contributors are kept in later versions.

## Open questions for the first review

1. Is "AI-driven" clear to a specialist who only occasionally uses AI as an assistant, or would "AI-assisted" be better?
2. Do the four values help choose between real, useful alternatives? Which important tradeoff is missing?
3. What is the minimum evidence a small team needs, so that applying the principles does not become bureaucracy of its own?
4. When is model-based evaluation of a result acceptable, and which independent checks does it need?
5. Where does automatic adaptation preserve intent, and where must it hand the decision to a person?
6. Which principle works poorly outside QA-AI-STLC, and how should it be rewritten without tying it to that architecture?
7. Which counterexample shows that following the text to the letter still allows an unsupported conclusion?
