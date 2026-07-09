---
name: compare
description: >
  Side-by-side comparison of 2+ competing projects with stage-fair scoring.
  Supports mixing remote URLs and local paths. Produces a comparison matrix
  with ranked recommendation.
---

# Research-Forge — Compare

Compare competing projects head-to-head across all analysis dimensions, judged stage-fairly.

## Command: `/research-forge:compare`

### Usage:
`/research-forge:compare <target1> <target2> [target3...] [--lang zh|en]`

Targets can be any mix of URLs, local directory paths, or local file paths.

### Comparison Workflow:

#### 1. Parallel Scan
- Run a scan (equivalent to `/research-forge:scan`) on each target in parallel using sub-agents.
- Collect metadata, metrics, stage classification, and first impressions for all projects.
- Adapt data collection strategy per target type (remote vs. local).

#### 2. Comparison Matrix
Build a side-by-side table covering:

| Dimension | Project A | Project B | Project C |
|---|---|---|---|
| **Target Type** | Remote/Local | Remote/Local | Remote/Local |
| **Lifecycle Stage** | S0-S3 | S0-S3 | S0-S3 |
| **Stars / Files** | | | |
| **Contributors** | | | |
| **Last Commit** | | | |
| **License** | | | |
| **Language** | | | |
| *Business & Market* | | | |
| **Problem Validity** (1-5) | | | |
| **Why Now** (1-5) | | | |
| **PMF Evidence** (1-5) | | | |
| **Unit Economics** (1-5) | | | |
| **Market Ceiling** (1-5) | | | |
| **Growth Engine** (1-5) | | | |
| *Technical & Architecture* | | | |
| **Architecture Quality** (1-5) | | | |
| **Engineering Culture** (1-5) | | | |
| **Scalability** (1-5) | | | |
| **Security Posture** (1-5) | | | |
| **Documentation** (1-5) | | | |
| **Maintainability & Tech Debt** (1-5) | | | |
| *Moat & Strategy* | | | |
| **Moat Strength** (1-5) | | | |
| **Founder-Market Fit** (1-5) | | | |
| **Org Capability** (1-5) | | | |
| **Second Curve Readiness** (1-5) | | | |
| **Overall Score (stage-weighted)** | | | |

Mark any sub-dimension that is Context (×0) for a project's stage as `ctx` — it is shown for information but excluded from that project's Overall Score.

#### 3. Stage-Fairness Rule
- **Same stage** → Overall Scores are directly comparable; rank by score.
- **Different stages** → raw Overall Scores are NOT directly comparable (each is weighted against different criteria). Compare each project against its own stage's One Question, then frame the recommendation as a maturity-vs-potential trade-off: "A is the safer, proven choice; B has the higher ceiling but is pre-PMF" — never as a naive score ranking.

#### 4. Key Differentiators
For each project, identify:
- **Unique Strength**: What does this project do better than all others?
- **Critical Weakness**: What is the biggest gap vs. competitors?
- **Best For**: What use case or user profile is this project ideal for?

#### 5. Verdict
- Rank projects from most to least recommended (respecting the stage-fairness rule).
- Provide context-dependent recommendation: "If you need X, choose A. If you need Y, choose B."
- Note each project's top Kill Criterion — the signal most likely to change its ranking.
