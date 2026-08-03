# Legal Agent Skills Guide

A practical, independent guide to discovering, evaluating, and safely using open legal Agent Skills.

> This repository is a **curated guide and recommendation layer**. It does not copy, certify, or redistribute the projects listed below.

[Português](README.pt-BR.md) · [Project catalog](catalog/projects.yml) · [Contributing](CONTRIBUTING.md) · [Security](SECURITY.md)

## Why this repository exists

Legal Agent Skills are growing quickly, but the available projects serve different purposes:

- some are official reference implementations;
- some are discovery catalogs;
- some are practitioner-built collections;
- some focus on one legal workflow;
- some prioritize scale across many jurisdictions.

A large library is not automatically safer, more accurate, or more useful. This guide helps legal professionals and technical teams choose the right starting point, understand installation models, and evaluate risks before using a skill with real legal work.

## What is an Agent Skill?

An Agent Skill is a portable package of instructions, metadata, and optional resources that teaches an AI agent how to perform a specific workflow.

The open Agent Skills specification defines a skill as a directory containing at least a `SKILL.md` file. A skill may also include:

```text
skill-name/
├── SKILL.md       # Required: metadata and instructions
├── scripts/       # Optional: executable code
├── references/    # Optional: supporting material
└── assets/        # Optional: templates and resources
```

A legal skill can encode workflows such as:

- reviewing an NDA against a playbook;
- building a sourced case chronology;
- checking whether cited authorities support a proposition;
- extracting obligations and deadlines;
- generating a due-diligence matrix;
- reviewing a DPA against a regulatory framework.

A skill is **not the model itself**. It is a reusable operating procedure that guides the model, may call tools, and can include executable code or reference materials.

Specification: [agentskills.io/specification](https://agentskills.io/specification)

## Recommended projects

The table below reflects upstream documentation reviewed on **2026-08-03**. Repository activity, scope, licensing, and compatibility can change.

| Project | Best for | Main strength | Main trade-off | Recommendation |
|---|---|---|---|---|
| [anthropics/claude-for-legal](https://github.com/anthropics/claude-for-legal) | Teams using Claude for legal workflows | Official, broad reference suite covering commercial, corporate, privacy, employment, litigation, regulatory, AI governance, IP, clinics, and legal education | Primarily designed around the Claude plugin and managed-agent ecosystem; not specialized for Brazilian law | **Best overall reference implementation** |
| [lawvable/awesome-legal-skills](https://github.com/lawvable/awesome-legal-skills) | Discovering third-party legal skills | Broad curated directory organized for legal workflow discovery | Listed projects have separate authors, licenses, maintenance levels, and security profiles | **Best discovery catalog** |
| [LegalQuants/lq-skills](https://github.com/LegalQuants/lq-skills) | Practitioner-built and jurisdiction-aware workflows | Transparent skills created by a community of lawyer-builders across multiple jurisdictions; designed to be harness-agnostic | Smaller library than mass-scale collections; jurisdiction coverage varies by skill | **Best high-signal practitioner collection** |
| [evolsb/claude-legal-skill](https://github.com/evolsb/claude-legal-skill) | First-pass contract review | Focused, position-aware contract review with risk flags, benchmarks, and suggested redlines | Primarily US-oriented and focused on contracts; not a general legal library | **Best focused contract-review starting point** |
| [ThomasMoreAI/legal-skills-open](https://github.com/ThomasMoreAI/legal-skills-open) | Exploring broad jurisdiction and practice-area coverage | Large open library using the `SKILL.md` format, organized by jurisdiction and practice area | Scale makes independent validation, freshness review, and depth assessment essential before production use | **Best breadth and taxonomy reference** |

## Which project should I start with?

### I use Claude and want a complete legal workflow reference

Start with [`anthropics/claude-for-legal`](https://github.com/anthropics/claude-for-legal).

Use it to understand:

- plugin structure;
- practice profiles;
- legal workflow design;
- citation gates;
- MCP connectors;
- scheduled legal agents;
- security and trust checks.

### I want to discover many legal skills

Start with [`lawvable/awesome-legal-skills`](https://github.com/lawvable/awesome-legal-skills).

Treat it as a directory, not as an approval list. Review the original repository, license, scripts, permissions, and maintenance history of every skill before installation.

### I want skills written by legal practitioners

Start with [`LegalQuants/lq-skills`](https://github.com/LegalQuants/lq-skills).

It is particularly useful for studying:

- jurisdiction metadata;
- citation verification;
- proposition checking;
- chronology building;
- contract QA;
- redlining workflows;
- legal quality control.

### I need one practical contract-review skill

Start with [`evolsb/claude-legal-skill`](https://github.com/evolsb/claude-legal-skill).

Use it for first-pass issue spotting and structured review. Confirm governing law, commercial position, source assumptions, and proposed redlines before relying on the output.

### I need maximum jurisdiction and practice-area coverage

Explore [`ThomasMoreAI/legal-skills-open`](https://github.com/ThomasMoreAI/legal-skills-open).

Use its taxonomy to discover candidate workflows. Validate each selected skill independently rather than assuming that library-level scale implies skill-level quality.

## How to use a skill

Installation differs by agent and repository. Always follow the upstream project's current instructions.

### Generic local workflow

```bash
# 1. Inspect the repository before installation
git clone https://github.com/OWNER/REPOSITORY.git
cd REPOSITORY

# 2. Review the skill files
find . -name "SKILL.md" -o -name "*.py" -o -name "*.sh" -o -name "*.js"

# 3. Check the license and recent changes
git log -10 --oneline

# 4. Copy or link only the skill you reviewed
# The destination depends on the agent being used.
```

### Claude Code plugin example

The Anthropic legal suite documents plugin installation through its marketplace:

```text
/plugin marketplace add https://github.com/anthropics/claude-for-legal
/plugin install commercial-legal@claude-for-legal
```

Run the plugin's setup or cold-start interview before using workflow skills. Generic results often come from skipping practice-profile configuration.

### Direct skill installation example

Some standalone projects document cloning into an agent-specific skills directory:

```bash
# Claude Code example
git clone https://github.com/evolsb/claude-legal-skill \
  ~/.claude/skills/contract-review

# Codex example documented by the same project
git clone https://github.com/evolsb/claude-legal-skill \
  ~/.codex/skills/contract-review
```

Directory conventions and support can change. Confirm them in the selected agent's current documentation.

## Safety checklist for legal skills

Do not install or use a legal skill with client or matter data until these checks are complete.

### 1. Jurisdiction

Verify:

- country and state;
- court or regulator;
- applicable date;
- procedural posture;
- governing law;
- whether the skill defaults to another jurisdiction.

A US contract-review skill should not be treated as a Brazilian contract-review skill merely because the language appears transferable.

### 2. Source authority and freshness

Check whether the skill:

- identifies primary and secondary sources;
- requires citations;
- distinguishes model memory from verified sources;
- records the date of legal materials;
- flags uncertainty and unsettled law;
- has a process for updating references.

### 3. Confidentiality and privilege

Before supplying real documents, determine:

- where files are processed;
- whether prompts or files are retained;
- whether data is used for training;
- which subprocessors receive data;
- whether connectors can read entire drives, matters, or mailboxes;
- whether organizational policy permits the tool;
- whether privilege and secrecy obligations are preserved.

Use synthetic or redacted documents during initial evaluation.

### 4. Executable code

A skill may contain Python, shell, JavaScript, binaries, or installation hooks.

Review:

- filesystem access;
- network calls;
- package installation;
- subprocess execution;
- environment-variable access;
- credential handling;
- document upload behavior;
- hidden or encoded instructions.

Run unknown skills in an isolated environment with minimum permissions.

### 5. Prompt injection and untrusted documents

Legal documents, emails, web pages, and data rooms may contain text that attempts to alter agent behavior.

A production workflow should:

- treat document content as untrusted data;
- separate instructions from evidence;
- restrict tools and write permissions;
- require confirmation before external actions;
- log tool calls;
- prevent documents from changing system or policy instructions.

### 6. Human review

Legal skills are best used for:

- first-pass review;
- issue spotting;
- extraction;
- organization;
- comparison;
- drafting assistance;
- quality-control support.

Material legal conclusions, filings, advice, deadlines, and external communications require accountable professional review.

### 7. Licensing

Check the license of:

- the repository;
- each imported skill;
- bundled datasets;
- templates;
- scripts;
- reference material.

A curated list does not grant permission to copy, modify, embed, or commercially distribute the listed projects.

### 8. Version pinning and change control

For production use:

- pin a commit or release;
- record the reviewed hash;
- review updates before deployment;
- keep an installation inventory;
- re-run security and legal-quality tests after updates;
- retain rollback capability.

## Evaluation framework

Use this scorecard before recommending a legal skill internally.

| Dimension | Questions |
|---|---|
| Workflow clarity | Does it define when to use the skill, required inputs, steps, and output contract? |
| Jurisdiction | Is the applicable jurisdiction explicit and correctly scoped? |
| Authority | Are sources identifiable, current, and ranked by authority? |
| Traceability | Can every material conclusion be traced to document text or external authority? |
| Security | Are scripts, tools, connectors, and permissions understandable and constrained? |
| Confidentiality | Is data handling compatible with client, firm, and regulatory requirements? |
| Testing | Are there examples, evaluation cases, expected outputs, or regression tests? |
| Maintenance | Is the project active, versioned, and clear about changes? |
| License | Is the intended use allowed? |
| Human control | Are review and approval gates explicit? |

Suggested decision:

```text
Adopt       → reviewed, tested, scoped, and approved for a defined workflow
Pilot       → useful candidate; synthetic or redacted data only
Reference   → valuable design pattern, not approved for matter work
Reject      → unclear provenance, unsafe permissions, stale law, or unsuitable license
```

## Important distinctions

### Skill vs prompt

A prompt is usually a single instruction. A skill is a reusable, versioned workflow package that may contain metadata, multi-step procedures, references, tools, scripts, and output requirements.

### Skill vs MCP server

A skill describes how work should be performed. An MCP server exposes tools or data sources. A skill may use MCP tools, but the two are not interchangeable.

### Skill vs agent

A skill is a capability. An agent combines goals, policies, tools, memory, orchestration, and one or more skills to execute a broader workflow.

### Catalog vs certification

This repository recommends starting points. It does not certify legal accuracy, security, privacy, or fitness for a specific matter.

## Brazil-specific gap

The current ecosystem has broad global and US coverage, with some Brazilian entries in large multi-jurisdiction libraries. The main open opportunity remains a deeply reviewed Brazilian collection with:

- official Brazilian sources;
- federal and state jurisdiction metadata;
- court-system awareness;
- Portuguese legal terminology;
- citation verification;
- legal-review provenance;
- source-freshness dates;
- evaluation cases;
- confidentiality and LGPD controls;
- workflows for litigation, contracts, compliance, insolvency, and legal operations.

This guide may later maintain a separate section for **reviewed Brazilian legal skills**, but inclusion should require explicit evidence and a transparent methodology.

## Inclusion policy

A project may be added when it has:

- a public repository;
- a clear legal workflow purpose;
- identifiable ownership or maintainers;
- installation or usage instructions;
- visible licensing information;
- enough documentation for independent evaluation.

Inclusion does not imply endorsement. See [CONTRIBUTING.md](CONTRIBUTING.md).

## Disclaimer

This repository provides technical and research information about third-party software. It is not affiliated with the listed projects unless explicitly stated. Project names and trademarks belong to their respective owners. Legal and security suitability must be evaluated for each organization, jurisdiction, workflow, and matter.

## License

The original content of this guide is released under the [MIT License](LICENSE). Third-party projects retain their own licenses.
