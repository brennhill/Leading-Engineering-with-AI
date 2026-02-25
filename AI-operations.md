# AI Operations
## Delivery and Runtime Standards for AI Systems

AI operations is where most teams discover whether their AI strategy is real or just a prototype with good demos. The model is only one component. Production behavior comes from the full system: model, prompts, policies, tools, data, runtime controls, and people making decisions under pressure.

## Points of control
1. Inside the model itself. You probably do not control this directly; Anthropic, OpenAI, or another provider does. Leverage: low.
2. Inside the agent harness itself. You might control this directly, especially when the harness is open source (for example, Codex-style agent code). Leverage: medium to high.
3. Inside files like `agent.md` or `claude.md`. These are not truly enforceable controls, but they are still better than nothing for shaping behavior. Leverage: medium.
4. At a proxy layer using `LiteLLM` or equivalent. This is strong for monitoring and policy visibility, but often harder for fully proactive or reactive control in real time. Leverage: medium.
5. At the sandbox level. Running AI under a restricted user account with constrained permissions gives direct OS-level control over blast radius. Leverage: high.
6. At the engineering process level. Restrict AI to opening pull requests, never direct repo updates or autonomous deploys, and enforce tests/linters as hard gates. Leverage: very high.
7. At the strategic and governance level. Define what AI systems are allowed, what policies apply, and how those policies are enforced over time. Leverage: high, depending on your role.

This list should make leverage obvious: focus first on what you can control directly, and actively advocate for improving the layers you cannot directly control.

The delivery model should stay straightforward and strict. Start with a real problem and baseline metric. Design explicit capabilities, constraints, fallback behavior, and clear ownership. Build with prompts, policies, and model configuration versioned like code. Evaluate before release with representative and adversarial cases. Release gradually behind flags with a verified kill switch and a tested fallback path. Operate continuously by monitoring quality, safety, reliability, latency, and cost together, because any single one can erase the value of the others.

Reliability for AI systems is not optional and not abstract. You need circuit breakers, rollback paths, and runbooks that treat AI incidents with the same seriousness as outages in core services. Security must be practical and enforced: least privilege for tools and data access, strong redaction in logs and traces, and explicit policy for where sensitive data can go and which providers are approved for which data classes.

Economics matters early. A feature that demos well but cannot run at healthy unit economics is not a success. Cost discipline should be built into release decisions from the start, not added after scale makes the problem expensive and political.

Operational leadership means building fast feedback loops without lowering the quality bar. The goal is not to slow teams down. The goal is to move quickly with control, so learning compounds while risk stays bounded.
