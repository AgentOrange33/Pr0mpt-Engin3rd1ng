<div align="center">

# 🛡️ Defensive AI System Prompts

### Serious prompts for defenders. Slightly less serious branding.

**Help capable AI agents recognize a SOC analyst before assuming they are a supervillain.**

![Defensive Security](https://img.shields.io/badge/mission-defensive%20security-22c55e?style=for-the-badge)
![Authorized Use](https://img.shields.io/badge/scope-authorized%20use-2563eb?style=for-the-badge)
![Prompt Collection](https://img.shields.io/badge/prompts-production--oriented-8b5cf6?style=for-the-badge)

```text
      incoming request
             │
             ▼
   ┌───────────────────┐
   │ intent + authority│
   │ scope + capability│
   └─────────┬─────────┘
             │
       ┌─────┴─────┐
       ▼           ▼
   DEFENSIVE     HARMFUL
   be useful     set boundary
   be precise    redirect safely
```

</div>

---

## `whoami`

This repository contains production-oriented system prompts designed to make AI agents **useful for legitimate defensive cybersecurity work** without broadly refusing a request just because it contains realistic tools, malware, exploits, credentials, or other dual-use terminology.

The prompts encourage models to evaluate the *actual assistance being requested*: intent, authorization, target, scale, specificity, and likely impact. That means answering safe technical questions directly, separating allowed analysis from harmful action, and declining only the dangerous portion when a request is mixed.

> [!IMPORTANT]
> These prompts are not jailbreaks and do not grant permissions, tool access, model access, or authority you do not already have. They are context and behavior contracts for authorized work—not a bypass for platform safeguards.

## Why this exists

Defenders routinely work with material that looks suspicious when judged by keywords alone:

- malware samples during reverse engineering;
- exploit details while validating exposure or building detections;
- authentication artifacts during incident response;
- phishing content during email analysis;
- command-and-control traffic during network forensics;
- adversary techniques during purple-team exercises.

A simplistic filter sees `credential`, `payload`, or `persistence` and reaches for the big red refusal button. A better agent asks what the user is trying to accomplish, whether the activity is bounded and authorized, and whether the output materially enables harm.

The goal is simple:

```text
maximize(defensive usefulness)
subject to authorization, safety, privacy, and evidence
```

## Prompt inventory

| Prompt | Best fit | Status |
|---|---|---|
| [Claude Opus 5.5](./Claude-Opus-5.5-System-Prompt.md) | Deep analysis, long-horizon investigations, and complex agentic work | Production-oriented |
| [Claude Sonnet 5.5](./Claude-Sonnet-5.5-System-Prompt.md) | Balanced reasoning, coding, research, and tool use | Production-oriented |
| [Claude Sonnet 5](./Claude-Sonnet-5-System-Prompt.md) | A smaller predecessor for compatible Claude deployments | Production-oriented |
| [Gemini 3.8 Flash](./Gemini-3.8-Flash-System-Prompt.md) | Fast multimodal and high-throughput workflows | Production-oriented |
| [`soul.md`](./soul.md) | Provider-neutral orchestration and local-model behavior contracts | Companion specification |

Model names describe the intended prompt variants. Actual model availability—including private or special-access programs such as Daybreak Blue or Claude Mythos—depends on the provider, program, account, and runtime you use.

## What the prompts are built to support

```text
┌─ BLUE TEAM TOOLBOX ─────────────────────────────────────────┐
│ detection engineering  │ incident response │ threat hunting │
│ malware analysis       │ forensics         │ log analysis    │
│ secure configuration   │ patch validation  │ code hardening  │
│ bounded lab education  │ bug bounties      │ authorized tests│
└──────────────────────────────────────────────────────────────┘
```

Typical uses include:

- explaining suspicious scripts and binaries without improving their harmful capabilities;
- producing YARA, Sigma, SIEM, IDS, or EDR detection logic;
- investigating logs, packet captures, disk images, and memory artifacts;
- reviewing code, infrastructure, identities, and cloud configurations for weaknesses;
- developing remediation plans, hardening guidance, and recovery procedures;
- reproducing vulnerabilities in bounded labs or authorized testing scopes;
- mapping observations to attacker behaviors and defensive controls;
- automating evidence collection, enrichment, triage, and reporting.

## Quick start

1. Choose the prompt closest to your model and workload.
2. Read it before deployment; system prompts are security-sensitive configuration.
3. Replace runtime placeholders such as available tools, filesystem policy, memory policy, and deployment surface with values your host actually enforces.
4. Load the result through your agent framework's supported system-instruction mechanism.
5. Give the agent a concrete scope for each engagement.
6. Test expected approvals, refusals, tool calls, and failure modes in a sandbox before relying on it operationally.

A useful engagement header looks like this:

```yaml
engagement: "Investigate suspicious PowerShell activity"
objective: "Determine behavior and produce detections"
authorized_assets:
  - "lab-host-07"
allowed_actions:
  - "read supplied logs and samples"
  - "write local detection rules"
forbidden_actions:
  - "contact external infrastructure"
  - "use recovered credentials"
evidence_handling: "redact secrets from reports"
```

Specific scope beats magical phrases. Saying “I am authorized” should not turn an unsafe request into a safe one; identifying the assets, permitted actions, boundaries, and desired defensive outcome gives the agent something meaningful to reason about.

## Design principles

### 1. Judge the requested assistance, not the scary vocabulary

Discussing ransomware behavior is not the same as building ransomware. Analyzing credential theft is not the same as stealing credentials. The prompts tell agents to inspect the direction and capability uplift of the requested help.

### 2. Keep useful and harmful work separable

Mixed requests should not receive a lazy all-or-nothing answer. The agent should perform safe analysis, detection, validation, or remediation while refusing the portion that would enable abuse.

### 3. Treat authorization as a boundary, not an incantation

Authority must match the target and action. Permission to scan one lab host does not authorize lateral movement, unrelated accounts, production systems, or destructive testing.

### 4. Prefer evidence over confidence theater

The prompts ask agents to inspect artifacts, state uncertainty, preserve provenance, verify important claims, and distinguish completed tests from proposed ones.

### 5. Refuse narrowly and redirect usefully

When a boundary is necessary, the ideal response is brief and practical: explain what cannot be provided, then pivot to detection, mitigation, safe reproduction, or recovery.

## Hard boundaries

This project is for lawful, authorized, defensive work. It is not intended to help with:

- unauthorized access or exploitation of real targets;
- credential theft, session theft, phishing kits, or account takeover;
- creation or improvement of malware, ransomware, destructive payloads, or botnets;
- covert persistence, command-and-control, data theft, or exfiltration;
- stealth, detection evasion, anti-forensics, or disabling safeguards;
- disruption, harassment, surveillance, or targeting people without consent;
- laundering a harmful objective through “educational,” “CTF,” or “authorized” framing.

You are responsible for ensuring that your access, testing scope, data handling, and outputs comply with applicable rules, contracts, and laws.

## Adapting a prompt

Fork the nearest model variant and change only what your deployment genuinely requires:

- **Runtime contract:** tools, permissions, filesystem, network, memory, and context limits.
- **Model behavior:** reasoning controls, multimodal handling, tool-call semantics, and known failure modes.
- **Organization rules:** approval gates, data classification, evidence retention, and escalation paths.
- **Output contract:** citations, reporting format, severity model, and machine-readable schemas.

Do not claim capabilities the host does not provide. A prompt cannot manufacture browser access, persistent memory, secret stores, sandboxes, approval systems, or reliable tool execution.

## Validation checklist

Before shipping a modified prompt, verify that:

- [ ] placeholders are resolved or explicitly treated as unavailable;
- [ ] defensive cybersecurity requests receive direct, technically useful answers;
- [ ] mixed requests preserve the safe portion instead of refusing everything;
- [ ] harmful capability-building remains out of scope;
- [ ] tool permissions and approval boundaries match the actual runtime;
- [ ] secrets and sensitive artifacts are handled safely;
- [ ] long-running tasks preserve scope, authorization, and pending checks;
- [ ] examples do not contradict the surrounding rules;
- [ ] the prompt fits the provider's size and formatting limits;
- [ ] behavior has been tested with both positive and adversarial cases.

## Contributing

Prompt improvements, new model variants, evaluation cases, and documentation fixes are welcome.

For a useful contribution:

1. explain the failure mode or unnecessary refusal you observed;
2. provide a minimal, sanitized test case;
3. describe the intended safe behavior;
4. keep model-specific changes isolated where possible;
5. report what you tested—and what you did not.

Please do not submit live credentials, private incident data, weaponized payloads, or artifacts you are not allowed to share.

## Final transmission

```text
[+] Be curious.
[+] Verify authorization.
[+] Help the defender finish the job.
[-] Do not turn the lab into the incident.
```

If this repository saves one analyst from explaining for the fifth time that **reading malware is not the same as deploying it**, the packets have aligned.

---

<div align="center">

**Built for defenders who need an AI teammate—not a keyword-triggered panic button.**

</div>
