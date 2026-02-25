# Writing High-Quality Code with LLMs

## Why this exists
LLMs can write a lot of code quickly. That is not the hard part. The hard part is getting production-quality outcomes repeatedly, in real systems, without piling up silent risk.

The practical mindset is the same one described in Esco Obong's February 13, 2026 essay: use the model as a power tool, not a magic wand. High-quality code still starts with clear problem framing, tradeoff analysis, and explicit design. The model helps you execute faster, but it does not remove the need for engineering judgment.

## The core workflow
Quality improves when code generation is the final step, not the first step. Start with a short design conversation and force the model to propose approaches and tradeoffs before it writes any code. Convert the agreed approach into a mini-spec. Break that spec into small tasks with clear "done" criteria. Then implement one task at a time.

This is the single most important shift: stop prompting for code first. Prompt for understanding, options, constraints, and plan first.

When debugging, avoid doom loops by splitting diagnosis from implementation. Have the model investigate and explain likely root causes before any code edits are allowed. Once you agree on cause and fix strategy, then permit edits.

## Make your codebase legible to the model
If you want high-quality output, your repository has to be easy to navigate for both humans and agents. That means clear module boundaries, stable conventions, and documentation that explains architecture and intent, not just APIs.

A practical pattern is to maintain concise project context files and architecture notes in-repo, then keep them tightly scoped and frequently pruned. Recent evidence matters here: a February 2026 arXiv study found that repository context files like `AGENTS.md` reduced average success by 20.6% and increased cost by 22.6% when overloaded with extra requirements. The implication is not "never use context files." The implication is "use minimal, high-signal context files."

This is also why tools like Claude may ask to "Clear context and execute plan?": context hygiene is a quality control mechanism, not a UX quirk.

In other words, write context that helps the model decide correctly, not context that micromanages every action.
Use `/docs/README.md` and the files in `/docs/templates/` to standardize this across features.

## Where LLM coding context comes from (and the order that works)
When an LLM is helping with code, context comes from multiple layers. In practice, quality is highest when the model consumes context in this order: hard constraints first, task intent second, local evidence third, and broad repository background last.

The effective hierarchy is straightforward. First, the model should anchor on non-negotiable instructions and safety boundaries, because those define what actions are allowed at all. Second, it should lock onto the current user task and acceptance criteria so it optimizes for the right outcome. Third, it should read the smallest set of files and runtime evidence that directly explain the issue, including failing tests, stack traces, compiler output, and nearby code. Fourth, it should expand to architecture docs and wider repository patterns only when needed to keep changes consistent with the system. Fifth, it should consult external documentation only for unstable facts or API details.

This order matters because context has cost. More tokens can mean more confusion, more stale assumptions, and slower execution. Good agents prune aggressively, refresh context as they learn, and periodically reset working memory around an explicit plan. That is exactly why some tools ask to clear context before execution.

## What recent research says (last 3 months)
The strongest signal from recent research is that quality is constrained less by raw generation speed and more by evaluation quality, context quality, and control boundaries.

First, evaluation quality is now a bottleneck. OpenAI's February 23, 2026 analysis argues SWE-bench Verified is increasingly contaminated and has enough test-quality defects that score gains no longer cleanly track real-world capability gains. In their spot audit, many sampled tasks had flawed tests or weakly actionable issue statements. For engineering teams, this means you should not trust a single public benchmark score as evidence of production readiness. Use private evals aligned to your own repos and failure modes.

Second, long-horizon repository reasoning remains hard. January and December 2025/2026 benchmark work (RepoReason and SWE-Bench++) shows that even frontier models still struggle when tasks require broad integration across files and systems. This matches day-to-day reality: models perform much better on decomposed tasks than on broad, underspecified "build the whole feature" requests.

Third, context is a quality lever and a failure mode at the same time. HE-SNR (January 2026) highlights the long-context tax and weak correlation between generic language metrics and downstream software-engineering performance. In practice, bigger context windows do not guarantee better outcomes unless context is curated and structured.

Fourth, security controls are now inseparable from code quality. Recent system cards for GPT-5.2-Codex and GPT-5.3-Codex emphasize sandboxed execution, restricted network access, and protections against destructive actions. This is operationally important: unsafe autonomy can turn a "quality" coding session into a reliability or security incident.

Fifth, supply-chain risk in agent extensions is real. Snyk's February 2026 ToxicSkills research reports high rates of critical flaws and prompt-injection patterns in public agent skills ecosystems. If your coding workflow imports third-party skills/prompts/tools, quality assurance must include supply-chain assurance.

## Distilled operating rules
Use LLMs to accelerate design, decomposition, and implementation, but keep humans accountable for acceptance. Keep repository context minimal, current, and architecture-focused. Prefer smaller scoped tasks over monolithic prompts. Enforce hard gates with tests, linters, type checks, and security scans. Run agents in sandboxes with least privilege and restricted network defaults. Treat benchmark scores as hints, not proof. Measure quality on your own codebase, with your own regressions, before trusting autonomy.

## Addendum: How CODEX Pulls Context During a Task
This addendum comes directly from CODEX.

When executing a coding task, CODEX typically reads context in this order: behavior constraints first (session instructions and repository control docs like `AGENTS.md`, `agent.md`, or `claude.md`), then the task definition and acceptance criteria, then task-local code (target file, callers/callees, adjacent module files), then tests (failing tests first), then local docs near the code (folder README or design notes), then broader repo docs, then git history when behavior is unclear, and finally external documentation when version-sensitive API behavior is uncertain.

CODEX decides which docs to read using a relevance-first filter. Explicitly named docs are read first. Docs referenced by imports, tests, configs, or nearby files are prioritized next. Very long generic docs are deferred unless needed to unblock execution. Reading stops once there is enough context to make a safe, testable change.

## References
- Esco Obong, "Writing High Quality Production Code with LLMs is a Solved Problem" (Feb 13, 2026): https://escobyte.substack.com/p/writing-high-quality-production-code
- OpenAI, "Why SWE-bench Verified no longer measures frontier coding capabilities" (Feb 23, 2026): https://openai.com/index/why-we-no-longer-evaluate-swe-bench-verified/
- OpenAI, "GPT-5.3-Codex System Card" (Feb 5, 2026): https://openai.com/index/gpt-5-3-codex-system-card/
- OpenAI, "Addendum to GPT-5.2 System Card: GPT-5.2-Codex" (Dec 18, 2025): https://openai.com/index/gpt-5-2-codex-system-card/
- Gloaguen et al., "Evaluating AGENTS.md: Are Repository-Level Context Files Helpful for Coding Agents?" (arXiv:2602.11988, Feb 12, 2026): https://arxiv.org/abs/2602.11988
- Li et al., "From Laboratory to Real-World Applications: Benchmarking Agentic Code Reasoning at the Repository Level" (arXiv:2601.03731, Jan 7, 2026): https://arxiv.org/abs/2601.03731
- Wang et al., "SWE-Bench++" (arXiv:2512.17419, Dec 19, 2025): https://arxiv.org/abs/2512.17419
- Wang et al., "HE-SNR" (arXiv:2601.20255, Jan 28, 2026): https://arxiv.org/abs/2601.20255
- Snyk, "ToxicSkills" research post (Feb 5, 2026): https://snyk.io/blog/toxicskills-malicious-ai-agent-skills-clawhub/
