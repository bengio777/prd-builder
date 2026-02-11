# PRD Builder — Installation & Operationalization Guide

## Skill File Structure

```
prd-builder/
├── SKILL.md                                    ← Main skill (Claude reads this first)
└── references/
    ├── prd-template.md                         ← PRD section structure (lean)
    ├── prd-template-examples.md                ← Worked examples for each section
    ├── quality-systems.md                      ← Dedup, cross-ref, validation, coherence
    ├── version-coaching.md                     ← Coaching criteria, placement map format
    ├── deep-dive-modules.md                    ← Module index and offer script
    ├── module-competitive-analysis.md          ← Optional: competitive deep dive
    ├── module-platform-integration.md          ← Optional: platform/integration deep dive
    ├── module-revenue-architecture.md          ← Optional: revenue modeling deep dive
    ├── implementation-handoff.md               ← Build chunking, dependency graphs, handoff
    └── iteration-scaling.md                    ← Version progression, retros, scaling
```

## Step-by-Step Installation

### Step 1: Locate Your Skills Directory

Claude skills live in `/mnt/skills/user/` within your Claude environment.
This is the directory where your existing skills (like `suggest-next-topic`)
already reside.

### Step 2: Create the Skill Folder

Create the `prd-builder` folder inside your user skills directory:

```
/mnt/skills/user/prd-builder/
```

### Step 3: Copy Files

Copy the entire `prd-builder/` folder from your downloads into the skills
directory. The final structure should be:

```
/mnt/skills/user/
├── suggest-next-topic/
│   └── SKILL.md
└── prd-builder/
    ├── SKILL.md
    └── references/
        ├── prd-template.md
        ├── prd-template-examples.md
        ├── quality-systems.md
        ├── version-coaching.md
        ├── deep-dive-modules.md
        ├── module-competitive-analysis.md
        ├── module-platform-integration.md
        ├── module-revenue-architecture.md
        ├── implementation-handoff.md
        └── iteration-scaling.md
```

### Step 4: Verify Installation

Start a new Claude conversation and say one of these trigger phrases:
- "I have an app idea"
- "Help me write a PRD"
- "I want to plan a product"

Claude should recognize the skill and begin the Discovery Interview (Phase 1).

## How the Skill Operates

### File Loading Behavior

1. **Always loaded:** `SKILL.md` metadata (name + description) is always in
   Claude's context. This is how Claude knows when to trigger the skill.

2. **Loaded on trigger:** When the skill activates, Claude reads the full
   `SKILL.md` body — the workflow, quality checklist, and reference file index.

3. **Loaded on demand:** Reference files are read only when needed. Claude
   reads `prd-template.md` during generation, `version-coaching.md` during
   coaching, etc. This keeps context lean.

### Workflow Sequence

```
User says "I have an app idea"
  ↓
Claude reads SKILL.md → starts Phase 1: Discovery Interview
  ↓
Discovery complete → Claude reads deep-dive-modules.md → offers modules
  ↓
User opts in/out of modules → Claude reads relevant module files if opted in
  ↓
Claude reads version-coaching.md → Phase 2: Version Coaching
  ↓
Alignment reached → Claude reads prd-template.md + prd-template-examples.md
                     + quality-systems.md → Phase 3: Generate PRD
  ↓
Claude reads implementation-handoff.md → adds handoff sections
  ↓
Runs quality checklist + narrative coherence check + validation prompts
  ↓
Phase 4: Output → saves PRD-[ProductName]-v[X.X].md to outputs
  ↓
User iterates → Claude reads iteration-scaling.md for version progression
```

### Trigger Phrases

The skill activates on any of these (or similar):
- "I have an app idea"
- "Help me plan this product"
- "Write a PRD"
- "Scope this project"
- "What should I build first"
- "Help me ship this"
- "Update my PRD"
- "Let's iterate on the PRD"
- "Version 2 planning"

### Output Location

All generated PRDs are saved to `/mnt/user-data/outputs/` with the naming
convention `PRD-[ProductName]-v[X.X].md`.

## Updating the Skill

To modify the skill's behavior:

- **Change the interview questions:** Edit `SKILL.md` Phase 1
- **Change PRD structure:** Edit `references/prd-template.md`
- **Change examples:** Edit `references/prd-template-examples.md`
- **Change quality rules:** Edit `references/quality-systems.md`
- **Add a new deep-dive module:** Create a new file in `references/` with
  the naming pattern `module-[name].md`, add a parent skill reference at the
  top, and add it to `references/deep-dive-modules.md`

Changes take effect on the next conversation (skills are read fresh each time).

## Quick Reference: Which File Does What

| I want to change... | Edit this file |
|---------------------|---------------|
| When the skill triggers | `SKILL.md` → description field |
| Discovery interview questions | `SKILL.md` → Phase 1 |
| How features get assigned to versions | `references/version-coaching.md` |
| PRD document structure | `references/prd-template.md` |
| Worked examples in the PRD | `references/prd-template-examples.md` |
| Quality checks and validation | `references/quality-systems.md` |
| Build order and dependency graph format | `references/implementation-handoff.md` |
| Version progression and retrospectives | `references/iteration-scaling.md` |
| Available deep-dive modules | `references/deep-dive-modules.md` |
| Competitive analysis process | `references/module-competitive-analysis.md` |
| Integration/platform strategy | `references/module-platform-integration.md` |
| Revenue modeling process | `references/module-revenue-architecture.md` |
