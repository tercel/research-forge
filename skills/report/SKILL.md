---
name: report
description: >
  Generate a polished, professional stage-aware due diligence report. Supports
  remote URLs, local directories, and local files as analysis targets.
---

# Research-Forge — Report

Generate a formal, polished due diligence report ready for sharing.

## Command: `/research-forge:report`

### Usage:
`/research-forge:report <target> [--lang zh|en] [--output path/to/output.md]`

- Target can be a URL, local directory path, or local file path.
- Default output: `./research-reports/[project-name]-due-diligence-[date].md`
- Default output language: Chinese (Simplified).

### Report Generation Workflow:

#### 1. Full Analysis
- Execute the complete `/research-forge:analyze` workflow internally (including Phase 0 stage detection).
- Adapt data collection to target type (remote vs. local).
- Gather all data, ratings, weight classes, and assessments.

#### 2. Report Structure

Generate a formal document with the following sections:

```markdown
# [Project Name] — Due Diligence Report
> Analysis Date: [Date] | Analyst: Research-Forge | Verdict: [Verdict]
> Target: [URL or Local Path]
> Lifecycle Stage: [S0-S3 — Name] (Confidence: High/Medium/Low)

## Executive Summary
[3-5 sentences: open with the detected stage and a direct answer to the
stage's One Question, then the key finding and recommendation]

## 1. Project Overview
- Name, URL/path, founding date, team size
- One-paragraph description
- Key metrics snapshot table

## 2. Stage Assessment
- Detected stage with converging evidence
- The One Question for this stage — and this report's answer to it
- The stage's characteristic death cause — found, or explicitly ruled out
- What "graduating to the next stage" would require

## 3. Business & Market Analysis
### 3.1 Problem Validity & Why Now
### 3.2 PMF Evidence
### 3.3 Unit Economics & Business Model
### 3.4 Market Ceiling & Competitive Landscape
### 3.5 Growth Engine & Adoption Traction
**Business Score: X.X / 5.0** (stage-weighted)

## 4. Technical & Architecture Analysis
### 4.1 Tech Stack & Architecture
### 4.2 Code & Engineering Quality
### 4.3 Scalability & Performance
### 4.4 Security & Reliability
### 4.5 Maintainability & Tech Debt
**Technical Score: X.X / 5.0** (stage-weighted)

## 5. Moat & Strategy
### 5.1 Moat Assessment (against the moat hierarchy)
### 5.2 Founder-Market Fit & Team
### 5.3 Org Capability
### 5.4 Second Curve & Paradigm Risk
### 5.5 Bull Case
### 5.6 Bear Case / Key Risks
### 5.7 Comparable Outcomes

## 6. Scorecard

| Dimension | Rating | Weight ([Stage]) | Notes |
|---|---|---|---|
| Problem Validity | X/5 | Critical/Standard/ctx | ... |
| Why Now | X/5 | ... | ... |
| PMF Evidence | X/5 | ... | ... |
| Unit Economics | X/5 | ... | ... |
| Market Ceiling | X/5 | ... | ... |
| Growth Engine | X/5 | ... | ... |
| Architecture Quality | X/5 | ... | ... |
| Engineering Culture | X/5 | ... | ... |
| Scalability | X/5 | ... | ... |
| Security Posture | X/5 | ... | ... |
| Documentation | X/5 | ... | ... |
| Maintainability & Tech Debt | X/5 | ... | ... |
| Moat Strength | X/5 | ... | ... |
| Founder-Market Fit | X/5 | ... | ... |
| Org Capability | X/5 | ... | ... |
| Second Curve Readiness | X/5 | ... | ... |
| **Overall (stage-weighted)** | **X.X / 5.0** | Critical ×2, Standard ×1, ctx excluded | |

## 7. Verdict & Kill Criteria
- Strategic Verdict with confidence level (High/Medium/Low)
- Investment Signal (when applicable)
- **Kill Criteria**: 2-4 pre-registered, falsifiable, time-bound signals that
  would flip this verdict — each with the signal, the deadline, and the
  resulting verdict change
- Recommended next steps

## Appendix
- Data sources and references
- Methodology notes (stage model, weight profile applied)
- Disclaimer
```

**Scoring note**: Per-dimension scores (Business / Technical / Moat & Strategy) use the same stage weight profile as the Overall Score — Critical ×2, Standard ×1, Context excluded. At some stages a dimension may have only one or two scored sub-dimensions; state this explicitly next to the score rather than padding with unscored items.

#### 3. Save Report
- Write the report to the specified output path (or default location).
- Inform the user of the file location.
