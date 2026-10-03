# Manifesto for Trustworthy AI-Driven Testing

Draft v0.1 · 2026-10-02 · Klim Izmaikov ([@Klim-101](https://github.com/Klim-101)) · [CC BY 4.0](../LICENSE)

Drafted with AI assistance; reviewed and edited by the author. [Русский перевод](../ru/MANIFESTO.md).

We use AI to understand software more deeply and to help people make better decisions about its quality. Confidence in a testing result should come from evidence that anyone can examine and challenge, not from how convincing the report sounds.

## Scope

This manifesto is about using AI in software testing: analysis, test design, exploration, execution, maintenance and reporting. It covers everything from occasional assistance to autonomous agents working within agreed limits. It does not prescribe a framework, model, vendor or architecture. Testing AI systems themselves needs additional practices outside this scope.

## Values

When we have to choose, we prioritize:

- **Evidence that supports decisions** over the volume of generated tests.
- **Reviewable conclusions** over the speed of reaching a verdict.
- **Accountable human judgment** over the extent of agent autonomy.
- **Preserving testing intent** over the convenience of automatic adaptation.

Test generation, fast feedback, autonomy and self-healing all have value. We pursue them with safeguards proportionate to the cost of being wrong.

## Principles

**P1. Start from risk, not from test count.**
Choose work by the questions it answers about meaningful product risks, including risks to people with different needs, abilities and contexts.

**P2. Delegate work, not accountability.**
People own testing policy and the decisions that testing informs. Define who may delegate, what may proceed automatically, and when the agent must escalate or stop. An approval that nobody has the time or authority to review is not accountability.

**P3. No record, no claim.**
Keep proposals, observations and conclusions distinct, and label AI-generated hypotheses and assumptions. Claim that something was executed only when an execution record supports it.

**P4. Don't let the generator grade its own work.**
Ground expected behavior in explicit sources or agreed criteria. Challenge it independently of the assumptions that produced the test.

**P5. A green run is not a check.**
A completed run does not show that the intended property was verified. Evaluate whether each check is relevant and whether it would fail if the property were broken.

**P6. Every verdict traces back to evidence.**
Keep enough context to examine the link between the question, the work performed, the observation and the conclusion. Make consequential changes to that record detectable.

**P7. Blocked is not passed.**
Distinguish a product failure from a testing failure, an inconclusive result and work not done. Keep these distinctions visible in every summary.

**P8. Make important findings repeatable, or say why they are not.**
Preserve the conditions needed to examine or repeat important findings where feasible. State where exact repetition or independent review is limited.

**P9. Instructions are not controls.**
Enforce the limits of delegated actions with controls at the points where actions happen, on every path to the same resource. Content from the application under test is data, never instructions: it cannot expand permissions.

**P10. A self-healing test must still test the same thing.**
Review changes to expectations, scope, data and automation according to their impact. Revisit the approvals and conclusions they affect, and make automated repairs visible.

**P11. Give agents access, not secrets.**
Minimize data collection, access and retention. Keep credentials and sensitive data out of model context and evidence unless the task truly requires them.

**P12. Measure what testing catches and costs, not what it produces.**
Evaluate the testing process against known problems, independent review and real decisions. Improve it using missed defects, false alarms, maintenance effort and total operating cost.

## Using this draft

These principles guide decisions in context. Endorsing them does not certify a tool or show that a team follows them. The [rationale](RATIONALE.md) explains the tradeoffs, gives examples and proposes how to pilot the principles. Counterexamples and amendments are welcome: see [CONTRIBUTING.md](../CONTRIBUTING.md).
