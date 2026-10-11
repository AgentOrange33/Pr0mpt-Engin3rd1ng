# Build Your Own System Prompt

This repository will receive more system prompts from the author over time. If you cannot wait for a prompt tailored to your model or use case, you can create one yourself with the workflow below. You can also copy the closest prompt from the [existing prompt inventory](./README.md#prompt-inventory) and ask an AI agent of your choice to adapt it to your needs.

## 1. Use a separate meta-prompting agent

Use one AI agent to design the system prompt that another AI model will follow. Keeping these roles separate helps the drafting agent evaluate the prompt as an engineered artifact instead of merely following it.

Ask the meta-prompting agent to:

- write clinically precise, objective, and testable instructions;
- remove ambiguity, unnecessary persuasion, and conflicting rules;
- preserve the useful structure of the source prompt;
- account for the target model's architectural preferences, supported instruction format, context window, reasoning controls, tool-calling behavior, multimodal capabilities, and known failure modes;
- avoid claiming tools, permissions, memory, or runtime capabilities that the deployment does not actually provide;
- define expected behavior for normal requests, edge cases, malformed inputs, failures, and adversarial instructions;
- produce a validation checklist for the finished prompt.

Here is a reusable request for the meta-prompting agent:

```text
Act as a system-prompt engineer. Create or adapt a production system prompt for
[TARGET MODEL AND VERSION] running in [RUNTIME OR AGENT FRAMEWORK].

The prompt must achieve [GOALS] while respecting [SAFETY, AUTHORIZATION, AND
ORGANIZATION RULES]. The runtime provides [TOOLS AND CAPABILITIES] and does not
provide [UNAVAILABLE CAPABILITIES]. The required output behavior is [OUTPUT
CONTRACT].

Use clinically precise, objective, and testable language. Account for the
target model's documented architectural preferences, instruction hierarchy,
context limits, reasoning controls, tool-call format, multimodal support, and
known failure modes. Do not invent capabilities. Identify unresolved
assumptions, remove contradictions, and include a validation checklist.

If I provide an existing prompt, preserve its proven structure and change only
what the target model or deployment genuinely requires.
```

Replace every bracketed field with real deployment information. Treat model documentation and the actual runtime configuration as authoritative; a model name alone does not establish available capabilities.

## 2. Switch to self-refinement when needed

If the first draft is incomplete, inconsistent, too vague, or poorly matched to the target model, switch to a self-refinement loop:

1. **Draft:** Produce the prompt and list its intended behaviors.
2. **Critique:** Check it against the requirements, model documentation, runtime limits, safety boundaries, and likely failure cases.
3. **Revise:** Correct specific weaknesses without redesigning sections that already work.
4. **Test:** Exercise normal, edge, adversarial, tool-use, and failure scenarios.
5. **Repeat:** Continue only while the next revision fixes an identified defect or meaningfully improves a measured result.

You can trigger this process with:

```text
Self-refine this system prompt. First create a requirement-by-requirement
coverage table. Then identify contradictions, ambiguity, unsupported runtime
claims, missing failure behavior, model-specific mismatches, and untestable
instructions. Revise only the defects you find, preserve working sections, and
finish with concrete tests and any remaining limitations.
```

Do not accept a revision merely because it sounds more polished. Compare it with the previous version using the same checklist and test cases.

## Start from an existing prompt if that is faster

You do not have to begin with a blank page. Choose the closest option from the [prompt inventory](./README.md#prompt-inventory), copy it, and tell an AI agent of your choice:

- which model and exact version you use;
- where the prompt will run;
- which tools and permissions are actually available;
- what behavior you want to preserve, add, or remove;
- which output format and size limits apply;
- which safety, privacy, and authorization boundaries must remain intact.

Ask the agent to preserve the source prompt's proven framework and make targeted changes for your model and requirements. Review the result yourself before deployment.

## Final checklist

Before using the prompt, confirm that:

- every placeholder has been replaced or explicitly marked unavailable;
- the instructions are precise, objective, internally consistent, and testable;
- model-specific claims match current authoritative documentation;
- tool, permission, memory, network, and filesystem claims match the real runtime;
- instruction priority and prompt-injection handling are clear;
- normal requests, edge cases, downstream failures, and mixed safe/unsafe requests have defined behavior;
- examples agree with the rules they demonstrate;
- the prompt fits the provider's formatting and size limits;
- representative positive and adversarial tests produce the intended behavior.

More ready-made system prompts are planned from the author. Until then, meta-prompting, self-refinement, and careful adaptation of an existing prompt provide a practical way to create a prompt suited to your own model and deployment.
