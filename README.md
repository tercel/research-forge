# Research Forge

The "Deep Research" skill for projects — Codebase, Architecture, and Strategic analysis, judged by lifecycle stage.

Perform comprehensive, **stage-aware** analysis on technical projects (open-source repos, commercial products, internal systems) across business, technical, and moat/strategy dimensions — then generate structured, actionable reports with pre-registered kill criteria.

## Core Idea: Stage-Aware Evaluation

Most evaluation errors come from applying the wrong stage's standards — demanding a moat from a pre-PMF prototype, or excusing a market leader's missing moat because it still grows. Research-Forge classifies every project into a lifecycle stage FIRST, then weights all scoring by that stage:

| Stage | Name | One Question | Top Death Causes |
|---|---|---|---|
| **S0** | Concept / Pre-launch | Should this exist? (real demand + why now + why you) | Pseudo-demand; mistimed market |
| **S1** | PMF Search (0→1) | Do people who try it stay? | Buying growth before retention flattens |
| **S2** | Scaling (1→10) | Is the growth engine repeatable, with improving unit economics? | Org failure; scaling losses |
| **S3** | Market Leadership (10→100) | What stops others from taking this? (moat + second curve) | Paradigm shift; failure to self-disrupt |

Each sub-dimension is Critical (×2), Standard (×1), or Context (unscored) depending on stage. A Critical sub-dimension rated ≤ 2 caps the verdict at "Hold / Wait".

## Quick Start

```bash
# Full auto-chain pipeline (scan → analyze → report)
/research-forge:run                                    # Analyze current directory
/research-forge:run https://github.com/example/project # Analyze remote project
/research-forge:run ./my-local-project                 # Analyze local directory
/research-forge:run --lang en                          # Output in English

# Individual commands
/research-forge:scan <target>              # Quick scan + stage classification
/research-forge:analyze <target>           # Stage-weighted 3-dimension analysis
/research-forge:compare <target1> <target2> # Stage-fair side-by-side comparison
/research-forge:report <target>            # Formal report generation
```

## Target Types

- **Remote URL** — `https://github.com/...`, any web address
- **Local directory** — `/path/to/project`, `./my-project`
- **Local file** — `./README.md`, `~/project/package.json`

## Analysis Framework

### Dimension 1: Business & Market (6 sub-dimensions)
Problem Validity, Why Now, PMF Evidence, Unit Economics, Market Ceiling, Growth Engine

### Dimension 2: Technical & Architecture (6 sub-dimensions)
Architecture Quality, Engineering Culture, Scalability, Security Posture, Documentation, Maintainability & Tech Debt

### Dimension 3: Moat & Strategy (4 rated + qualitative theses)
Moat Strength (five-tier hierarchy: network effects > switching costs > scale economies > brand > data/tech lead), Founder-Market Fit, Org Capability, Second Curve Readiness — plus Bull Case, Bear Case, Comparable Outcomes.

## Rating & Verdict

- Each sub-dimension scored 1-5; Overall Score is stage-weighted (Critical ×2, Standard ×1, Context excluded).
- Strategic Verdict: Strong Recommend | Watch Closely | Hold / Wait | Not Recommended.
- Investment Signal (optional): Strong Buy / Watch / Hold / Pass.
- **Kill Criteria (mandatory)**: every verdict ships with 2-4 falsifiable, time-bound signals that would flip it — verdicts without kill criteria are opinions, not analysis.

## Options

| Flag | Description |
|---|---|
| `--lang zh\|en` | Output language (default: zh) |
| `--focus business\|technical\|strategy` | Deep-dive one dimension |
| `--output path` | Custom report output path |

## Output

Reports saved to `./research-reports/[project-name]-due-diligence-[date].md` by default.
