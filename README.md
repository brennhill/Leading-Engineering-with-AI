# Leading Engineering in the Time of AI
## A Practical Leadership Playbook

## Preamble
This started as a practical leadership guide before AI became central to day-to-day engineering. The job is still leadership, and the core challenge is still the same: do the simple things well, repeatedly, under pressure. As Rich Hickey argues in *Simple Made Easy*, simple and easy are not the same. Easy is quick to start. Simple is low-coupling, understandable, and maintainable under change. AI tools often feel easy on day one and become complex in production. If you are leading a team, optimize for simple.

LLMs and AI are not magic. They are probabilistic systems that generate likely outputs from context, and that fact alone explains most of their strengths and most of their failure modes. If you understand how they work, you can reason about where they will be useful and where they will be dangerous. They can be fast, creative, and surprisingly capable, but they can also fail invisibly, confidently, and incorrectly. They can tell you everything is fine right up until it is not. There are public examples of this kind of failure, including a GitHub report where a user lost files with Gemini CLI and a separate incident where an autonomous agent deleted production data ([Gemini CLI issue](https://github.com/google-gemini/gemini-cli/issues/4586), [Replit incident post](https://twitter.com/amasad/status/1946986468586721478?ref_src=twsrc%5Etfw)).

The right posture is neither hype nor fear. Hype makes teams reckless. Fear makes teams slow and defensive. Both are bad leadership. At the same time, dismissing this shift is also a mistake. Software engineering is changing in real time: how we write code, how we design systems, how we test, and how we organize teams. The leaders who do well here will be the ones who adopt quickly with clear boundaries and explicit accountability.

## Brenn's Rule
> **"When humans get too lazy, the AI goes crazy."**  
> **Don't get (too) lazy.**  
> *- Brenn Hill*

## Core operating principles
The first principle is that AI design is not mostly about what your product does; it is about what your product enables AI to do safely. For each AI feature, you should be able to explain what the model can observe, what it can decide, what it can act on, what it is forbidden to do, and where a human can review, override, or stop execution. If you cannot explain that plainly, the feature is not ready.

The second principle is layered guardrails. Guardrails are not one prompt instruction or one policy document. They must exist at the agent specification level, at the agent runtime/container level where tool calls are actually executed, at the connection layer where you route and audit model traffic, at the local process layer where permissions and isolation constrain blast radius, at the development workflow layer where AI cannot merge directly to protected branches, and at the organization policy layer where legal, security, vendor, and data-handling standards are defined. Assume any single layer can fail and build so the others catch it.

The third principle is that AI can propose, but humans decide and own outcomes. Use AI to improve human capability, not to replace human judgment. These tools are excellent for accelerating research, exploring alternatives, understanding unfamiliar code, drafting tests, and helping people learn faster. They are not acceptable as final authority for production risk decisions.

## What Engineering Leadership Looks Like Now
Leadership in AI is not about collecting model demos. It is about creating an environment where experimentation is fast, safety is engineered, and accountability is obvious. It is about helping people level up, because teams that can reason clearly about AI systems will outperform teams that only know how to prompt them. It is about building systems that can evolve, because the infrastructure is still early and change is guaranteed.

This playbook works with the rest of the repo:
- [eng-principles.md](eng-principles.md): baseline engineering standards.
- [solution-design/README.md](solution-design/README.md): system design structure.
- [AI-operations.md](AI-operations.md): delivery and runtime operations.
- [data-science-management.md](data-science-management.md): probabilistic system audit guidance.
- [llm-code-quality.md](llm-code-quality.md): how to get high-quality production code from LLM-assisted workflows.
- [llms-for-data-engineers.md](llms-for-data-engineers.md): pragmatic do/don't guidance and checklists for data engineering with LLMs.
- [docs/README.md](docs/README.md): LLM-friendly docs structure and templates for feature-level context.

## Bottom line
Move fast with AI, but only inside explicit boundaries. Speed without guardrails creates hidden risk. Guardrails without speed creates irrelevance.
