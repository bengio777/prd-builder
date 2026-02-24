# AI Building Block Spec: Product Requirements Development (PRD Builder)

## Execution Pattern
**Recommended Pattern:** Skill-Powered Prompt (with 10 reference files)
**Reasoning:**
- SKILL.md contains the full 6-phase workflow with explicit instructions for when to load each reference file
- Reference files are loaded on demand (not all at once), keeping context lean while providing deep expertise per phase
- The conversational back-and-forth of discovery and version coaching maps naturally to the skill pattern
- No external tool integrations required — the skill reads references and writes markdown files
- Optional deep-dive modules are additive, never blocking — the skill offers and loads them dynamically

---

## Scenario Summary
| Field | Value |
|-------|-------|
| **Workflow Name** | Product Requirements Development (PRD Builder) |
| **Description** | Generate production-ready Product Requirements Documents through structured discovery, version coaching, and iterative refinement. |
| **Process Outcome** | Production-ready PRD saved as a versioned markdown file, ready for a solo founder, dev team, or AI coding agent to build from. |
| **Trigger** | New app idea or product concept. |
| **Type** | Augmented |
| **Business Process** | Product Development |

---

## Step-by-Step Decomposition
| Step | Name | Autonomy Level | Building Block(s) | Tools / Connectors | Skill Candidate | HITL Gate |
|------|------|---------------|-------------------|-------------------|----------------|-----------|
| 1 | Discovery interview | AI + Human | Skill, Reference (deep-dive-modules.md) | Web Search (optional) | `prd-builder` | User provides vision, features, constraints |
| 2 | Version coaching | AI + Human | Skill, Reference (version-coaching.md, deep-dive-modules.md, optional modules) | — | `prd-builder` | User reviews Version Placement Map, resolves disagreements |
| 3 | Generate PRD | AI-Semi-Autonomous | Skill, Reference (prd-template.md, prd-template-examples.md, quality-systems.md, implementation-handoff.md) | File Write | `prd-builder` | — |
| 4 | Validate and output | AI + Human | Skill, Reference (quality-systems.md) | File Write | `prd-builder` | User gut-checks 3 riskiest assumptions |
| 5 | Iterate and version | Human + AI | Skill, Reference (iteration-scaling.md) | File Write | `prd-builder` | User directs iteration scope |
| 6 | Scaling checkpoints | AI + Human | Skill, Reference (iteration-scaling.md) | — | `prd-builder` | User reviews scaling assessments |

## Autonomy Spectrum Summary

```
|--Human + AI Collaborative------------|--AI-Semi-Autonomous--|--AI-Autonomous--|
       1, 2, 4, 5, 6                          3
```

| Level | Steps | Count |
|-------|-------|-------|
| **AI + Human Collaborative** | Steps 1, 2, 4, 5, 6 | 5 |
| **AI-Semi-Autonomous** | Step 3 | 1 |
| **AI-Deterministic** | — | 0 |
| **AI-Autonomous** | — | 0 |

---

## Skill Candidates
### `prd-builder`
- **Purpose:** Guide a user from "I have an idea" to a production-ready PRD through structured discovery, opinionated version coaching, and validated generation.
- **Inputs:**

| Input | Source | Required |
|-------|--------|----------|
| Product vision and problem statement | User (interview) | Yes |
| Jobs-to-be-done | User (interview) | Yes |
| Personas | User (interview) | Yes |
| Feature brain dump | User (interview) | Yes |
| Constraints (solo/team, budget, timeline, tech) | User (interview) | Yes |
| Competitive landscape | User + Web Search | No |
| Monetization model | User (interview) | No |
| Kill criteria | User (interview) | No |
| Version coaching decisions | User (confirmation/override) | Yes |
| Deep-dive module opt-ins | User | No |

- **Outputs:**

| Output | Destination | Format |
|--------|-------------|--------|
| Version Placement Map | In-session review | Markdown table with Feature IDs |
| Production-ready PRD | Working directory | `PRD-[ProductName]-v[X.X].md` |
| Riskiest assumptions | In-session review | Top 3 with gut-check prompt |
| Implementation handoff | Included in PRD header | Build chunking + dependency graph |

- **Decision Logic:**
  - Feature versioning uses 6 criteria: persona dependency, dependency chain, complexity vs. value, architectural implications, revenue unlock, learning value
  - Feature IDs (F001, F002...) assigned during coaching and persist across all versions
  - Quality checks run before output: deduplication, cross-reference integrity, narrative coherence
  - Deep-dive modules offered after discovery, never blocking: "Want to go deeper, or should I draft first?"
  - v0.1 for drafts, v1.0 for complete PRDs

- **Failure Modes:**

| Failure | Impact | Handling |
|---------|--------|----------|
| Discovery interview goes too long | User loses momentum | Adapt to quick v0.1 — capture vision and constraints, draft lean, iterate later |
| Feature brain dump is overwhelming | Scope bloat | Actively deduplicate during discovery; consolidate overlapping capabilities |
| v1 scope exceeds constraints | Unshippable PRD | Move features to v1.1 or v2; cut aggressively for solo builders |
| PRD sections contradict each other | Internal inconsistency | Cross-reference integrity check before presenting; persona-feature-job-version chains must connect |
| Feature IDs drift across versions | Broken traceability | IDs are immutable once assigned; validation catches mismatches |

---

## Step Sequence and Dependencies

```
Step 1: Discovery Interview [AI + Human]
    │
    ▼
Step 2: Version Coaching [AI + Human]
    │   (optional deep-dive modules load here)
    ▼
Step 3: Generate PRD [AI]
    │   (reads template, examples, quality systems, handoff references)
    ▼
Step 4: Validate and Output [AI + Human]
    │   (quality checks, assumption gut-check, file save)
    ▼
Step 5: Iterate and Version [Human + AI]
    │   (minor iterations or major version progressions)
    ▼
Step 6: Scaling Checkpoints [AI + Human]
    (evaluated at each major version boundary)
```

### Dependency Map

| Step | Depends On |
|------|-----------|
| Step 1 | Trigger (user has app idea or product concept) |
| Step 2 | Step 1 (discovery data collected) |
| Step 3 | Step 2 (version alignment reached) |
| Step 4 | Step 3 (PRD generated) |
| Step 5 | Step 4 (PRD delivered, user wants changes) |
| Step 6 | Step 5 (major version boundary reached) |

### Parallel Opportunities
- None — the workflow is strictly sequential. Each phase builds on the output of the previous one.

### Critical Path
Discovery (1) → Coaching (2) → Generate (3) → Validate (4)

Steps 5 and 6 are iterative and only fire on user request.

---

## Prerequisites
- Claude Code with `prd-builder` skill installed (includes 10 reference files)
- An app idea, product concept, or feature to scope
- Understanding of constraints: solo or team? Budget? Timeline? Tech preferences?

## Context Inventory

| Artifact | Type | Used By Steps | Status |
|----------|------|---------------|--------|
| SKILL.md | Skill definition | All phases | Exists |
| prd-template.md | Reference | 3 | Exists |
| prd-template-examples.md | Reference | 3 | Exists |
| quality-systems.md | Reference | 3, 4 | Exists |
| version-coaching.md | Reference | 2 | Exists |
| deep-dive-modules.md | Reference | 1, 2 | Exists |
| module-competitive-analysis.md | Reference (optional) | 2 | Exists |
| module-platform-integration.md | Reference (optional) | 2 | Exists |
| module-revenue-architecture.md | Reference (optional) | 2 | Exists |
| implementation-handoff.md | Reference | 3, 4 | Exists |
| iteration-scaling.md | Reference | 5, 6 | Exists |
| INSTALL.md | Setup guide | — | Exists |

## Tools and Connectors

| Tool / Connector | Purpose | Used By Steps | Status |
|-----------------|---------|---------------|--------|
| Web Search | Competitive landscape research (optional) | 1 | Available |
| File Write | Save generated PRD to working directory | 3, 4, 5 | Available |

## Recommended Implementation Order
1. SKILL.md with Phase 1 discovery interview logic
2. version-coaching.md and deep-dive-modules.md for Phase 2
3. prd-template.md and prd-template-examples.md for Phase 3
4. quality-systems.md for validation
5. implementation-handoff.md for build handoff sections
6. iteration-scaling.md for versioning and scaling
7. Optional deep-dive modules (competitive, platform, revenue)
8. INSTALL.md for operationalization guide

## Where to Run
**Platform:** Claude Code (skill)
**GitHub:** bengio777/prd-builder
**Entry points:** "I have an app idea", "help me write a PRD", "scope this project", "what should I build first", "help me ship this"
