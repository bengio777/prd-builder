# Product Requirements Development (PRD Builder) — Project Spec

**Project:** PRD Builder

---

## Capabilities Demonstrated

### 1. 6-phase structured workflow from idea to production-ready PRD
**Met.** The skill guides users through Discovery Interview, Version Coaching, PRD Generation, Validation & Output, Iteration & Versioning, and Scaling Checkpoints. Each phase has explicit instructions, and reference files are loaded on demand to keep context lean.
**Evidence:** `SKILL.md` (Phases 1-6), `INSTALL.md` (Workflow Sequence diagram)

### 2. 10 reference files loaded on demand per phase
**Met.** The skill indexes 10 reference files and specifies exactly when each should be read. Core references (template, examples, quality systems) load during generation. Coaching references load during Phase 2. Deep-dive modules load only when the user opts in. This architecture keeps context lean while providing deep expertise.
**Evidence:** `SKILL.md` (Reference Files table), `references/` directory (10 files), `INSTALL.md` (File Loading Behavior section)

### 3. Version coaching with 6 evaluation criteria
**Met.** Every feature from the brain dump is evaluated against persona dependency, dependency chain, complexity vs. value, architectural implications, revenue unlock, and learning value. Features are placed into a Version Placement Map (v1 through v4+) with persistent Feature IDs.
**Evidence:** `SKILL.md` (Phase 2), `references/version-coaching.md`

### 4. Quality validation system with cross-reference integrity
**Met.** Before presenting any PRD, the skill runs a 21-point quality checklist covering deduplication, cross-reference consistency (persona-feature-job-version chains), narrative coherence, and assumption risk ranking. The 3 riskiest assumptions are surfaced for user gut-check.
**Evidence:** `SKILL.md` (Quality Checklist), `references/quality-systems.md`

### 5. Optional deep-dive modules (competitive, platform, revenue)
**Met.** Three optional modules extend the coaching phase without blocking the core workflow. The skill offers them naturally after discovery: "Want to go deeper on competitive analysis, integrations, or revenue -- or should I draft first and layer those in later?" Each module has its own reference file.
**Evidence:** `references/deep-dive-modules.md`, `references/module-competitive-analysis.md`, `references/module-platform-integration.md`, `references/module-revenue-architecture.md`

### 6. Implementation handoff with build chunking
**Met.** The generated PRD includes a "How to Use This PRD" header at the top with build-order chunking, dependency graphs, and handoff instructions. Designed so a solo founder, dev team, or AI coding agent can pick it up and start shipping.
**Evidence:** `references/implementation-handoff.md`, `SKILL.md` (Phase 4)

### 7. Iteration and scaling support across major versions
**Met.** The skill handles both minor iterations (refine features, adjust scope) and major version progressions (retrospective from prior version informs scope). Feature IDs persist across all versions for traceability. Scaling checkpoints evaluate technical, product, and operational readiness at each major boundary.
**Evidence:** `references/iteration-scaling.md`, `SKILL.md` (Phases 5-6)

---

## Deliverables

| # | Deliverable | File | Status |
|---|-------------|------|--------|
| 1 | Core skill definition | `SKILL.md` | Complete |
| 2 | PRD template | `references/prd-template.md` | Complete |
| 3 | PRD template examples | `references/prd-template-examples.md` | Complete |
| 4 | Quality systems | `references/quality-systems.md` | Complete |
| 5 | Version coaching criteria | `references/version-coaching.md` | Complete |
| 6 | Deep-dive module index | `references/deep-dive-modules.md` | Complete |
| 7 | Competitive analysis module | `references/module-competitive-analysis.md` | Complete |
| 8 | Platform integration module | `references/module-platform-integration.md` | Complete |
| 9 | Revenue architecture module | `references/module-revenue-architecture.md` | Complete |
| 10 | Implementation handoff | `references/implementation-handoff.md` | Complete |
| 11 | Iteration and scaling | `references/iteration-scaling.md` | Complete |
| 12 | Installation guide | `INSTALL.md` | Complete |
| 13 | Building block spec | `BUILDING-BLOCK-SPEC.md` | Complete |
| 14 | Project spec | `SPEC.md` | Complete |
| 15 | README | `README.md` | Complete |

---

## Review Criteria

| Criterion | Status | Evidence |
|-----------|--------|----------|
| Skill triggers on product/PRD-related phrases | Pass | `SKILL.md` description field with 10+ trigger phrases |
| Discovery interview covers all 9 categories | Pass | Vision, JTBD, Personas, Features, Constraints, Competitive, Monetization, Kill Criteria, Glossary |
| Version coaching uses all 6 criteria | Pass | `SKILL.md` Phase 2, `references/version-coaching.md` |
| Feature IDs assigned during coaching and persist | Pass | F001, F002... format specified in Phase 2 |
| PRD template structure is precise and opinionated | Pass | `references/prd-template.md` defines exact sections |
| Quality checklist runs before output | Pass | 21-point checklist in `SKILL.md` |
| 3 riskiest assumptions surfaced for gut-check | Pass | Phase 4 validation step |
| Deep-dive modules are offered but never block | Pass | "Want to go deeper, or should I draft first?" in Phase 2 |
| Output saves as versioned markdown file | Pass | `PRD-[ProductName]-v[X.X].md` naming convention |
| Reference files load on demand, not all at once | Pass | `INSTALL.md` File Loading Behavior section |

---

## File Inventory

| File | Location | Purpose |
|------|----------|---------|
| `SKILL.md` | `SKILL.md` | Core skill -- 6-phase workflow, quality checklist, reference file index |
| `prd-template.md` | `references/prd-template.md` | PRD section structure (lean) |
| `prd-template-examples.md` | `references/prd-template-examples.md` | Worked examples for each PRD section |
| `quality-systems.md` | `references/quality-systems.md` | Deduplication, cross-reference, validation, coherence rules |
| `version-coaching.md` | `references/version-coaching.md` | Coaching criteria, Version Placement Map format |
| `deep-dive-modules.md` | `references/deep-dive-modules.md` | Module index and offer script |
| `module-competitive-analysis.md` | `references/module-competitive-analysis.md` | Optional competitive deep-dive process |
| `module-platform-integration.md` | `references/module-platform-integration.md` | Optional platform/integration deep-dive |
| `module-revenue-architecture.md` | `references/module-revenue-architecture.md` | Optional revenue modeling deep-dive |
| `implementation-handoff.md` | `references/implementation-handoff.md` | Build chunking, dependency graphs, handoff |
| `iteration-scaling.md` | `references/iteration-scaling.md` | Version progression, retrospectives, scaling |
| `INSTALL.md` | `INSTALL.md` | Installation and operationalization guide |
| `BUILDING-BLOCK-SPEC.md` | `BUILDING-BLOCK-SPEC.md` | AI building block specification |
| `SPEC.md` | `SPEC.md` | Project spec (this file) |
| `README.md` | `README.md` | Project overview |
