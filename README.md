# Leading Engineering in the Time of AI

## Preamble
This repo started as a practical leadership playbook for software teams. AI changes the details, but not the need for clear standards.

The core update is this:
engineering leaders now need to manage probabilistic systems, autonomous behaviors, and faster change cycles while keeping human accountability.

## Repo map
- `eng-principles.md`: baseline engineering and leadership standards.
- `SolutionDesign/README.md`: design template for system planning.
- `DataScienceManagement.md`: audit guide for probabilistic/ML system health.

## The core shift in AI product design
Designing for AI is not mainly about what your product does.
It is about what your product enables the AI to do safely and reliably.

For every feature, define:
- What the AI can observe.
- What the AI can decide.
- What the AI can do (actions/tools).
- What the AI is explicitly not allowed to do.
- How humans review, override, and recover.

If these are not defined, you do not have an AI feature yet. You have a demo.

## Guardrails are not optional
Treat guardrails as a layered system, not a single control point.

| Layer | Example controls | Why it matters |
| --- | --- | --- |
| Agent spec (`agent.md`) | Goal boundaries, allowed tools, refusal rules, output format contracts | Prevents unsafe intent at the instruction layer |
| Agent container/runtime | Tool allowlists, schema validation, retries with bounds, idempotency keys, hard timeouts | Prevents unsafe or repeated execution |
| Connection layer (for example `LiteLLM`) | Authentication, rate limits, centralized audit logs, request/response policy checks, redaction | Gives observability and centralized policy enforcement |
| Local process layer | Run as permission-constrained user, restricted filesystem/network access, short-lived credentials | Limits blast radius from compromise or model mistakes |
| Development process layer | AI cannot push to `main`, AI can open PRs only, required human review, CI gates | Keeps accountability and quality in the merge path |
| Organizational policy layer | Approved model/vendor list, data classification rules, retention rules, legal/privacy controls | Aligns day-to-day engineering with business risk |

Assume each layer can fail. Build defense in depth.

## Human role: judgment, not autopilot
AI is an excellent teacher, pair partner, and research accelerator.
Use it to level up people in the loop, not to replace critical thinking.

Good uses:
- Rapid literature and standards research.
- Drafting design alternatives with tradeoffs.
- Explaining unfamiliar code and generating test ideas.
- Producing first-pass runbooks and incident timelines.

Bad uses:
- Blindly accepting architectural decisions.
- Delegating production approval decisions to the model.
- Letting generated code bypass review standards.

Team rule:
AI can propose. Humans decide and own outcomes.

## The infrastructure is early
Current AI tooling is early-stage infrastructure.
The closest analogy is software development before mature Git workflows and container standards.

Expect rough edges:
- Inconsistent tooling behavior.
- Fast-moving APIs and model changes.
- New failure modes across orchestration and context handling.
- Vendor churn and pricing changes.

Leadership implication:
design for portability, observability, and change from day one.

## What else should be included
In addition to the four key points above, a strong AI leadership README should include:

### 1) Decision rights and accountability
- Define who is responsible for model choice, prompt/policy changes, deployment approval, and incident sign-off.
- Use clear ownership so "the AI did it" is never accepted as root cause.

### 2) Evaluation strategy
- Require offline evals before release and online monitoring after release.
- Track quality, safety, latency, cost, and fallback rate.
- Version prompts, policies, and model configs like code.

### 3) Reliability and incident response
- Add circuit breakers, kill switches, and safe fallback behavior.
- Define AI-specific incident severity, paging rules, and rollback paths.
- Record and review near-misses, not only outages.

### 4) Security and data governance
- Map data classes to allowed models and providers.
- Default to least privilege for tools and secrets.
- Audit for leakage in logs, traces, prompts, and model outputs.

### 5) Economics and ROI
- Tie AI features to measurable value, not novelty.
- Track cost-to-serve by feature and customer segment.
- Set stop conditions for experiments that do not deliver value.

### 6) Team capability growth
- Train engineers and PMs to evaluate AI output critically.
- Reward evidence-backed judgment, not prompt tricks.
- Build shared playbooks so capability compounds across teams.

## AI addendum to Definition of Done
For AI-enabled features, done means all of the following are true:
- Guardrails are implemented at all six layers above.
- Human approval checkpoints are explicit.
- Eval suite passes agreed thresholds.
- Logs and audits are reviewable and privacy-safe.
- Fallback behavior is tested.
- Rollback and kill switch are verified.
- Ownership for ongoing monitoring is assigned.

## Practical operating principle
Move fast with AI, but only inside explicit boundaries.
Speed without guardrails creates hidden risk.
Guardrails without speed creates irrelevance.
Leadership is building both at the same time.
