# Research Forge

The "Deep Research" skill for projects — Codebase, Architecture, and Strategic analysis.

Perform comprehensive analysis on technical projects (open-source repos, commercial products, internal systems) across business, technical, and strategic dimensions — then generate structured, actionable reports.

## Quick Start

```bash
# Full auto-chain pipeline (scan → analyze → report)
/research-forge:run                                    # Analyze current directory
/research-forge:run https://github.com/example/project # Analyze remote project
/research-forge:run ./my-local-project                 # Analyze local directory
/research-forge:run --lang en                          # Output in English

# Individual commands
/research-forge:scan <target>              # Quick scan
/research-forge:analyze <target>           # Deep 3-dimension analysis
/research-forge:compare <target1> <target2> # Side-by-side comparison
/research-forge:report <target>            # Formal report generation
```

## Target Types

- **Remote URL** — `https://github.com/...`, any web address
- **Local directory** — `/path/to/project`, `./my-project`
- **Local file** — `./README.md`, `~/project/package.json`

## Analysis Framework

### Dimension 1: Business & Market (6 sub-dimensions)
Problem Acuteness, Solution Fit, Business Model Clarity, Market Timing, Competitive Position, Adoption Momentum

### Dimension 2: Technical & Architecture (6 sub-dimensions)
Architecture Quality, Technical Moat, Engineering Culture, Scalability, Security Posture, Documentation

### Dimension 3: Strategic Verdict & Investment Thesis
Bull Case, Bear Case, Team Assessment, Comparable Outcomes, Strategic Verdict, Investment Signal, Final Evaluation

## Rating System

Each sub-dimension scored 1-5. Strategic Verdict: Strong Recommend / Watch Closely / Hold / Not Recommended. Investment Signal (optional): Strong Buy / Watch / Hold / Pass.

## Options

| Flag | Description |
|---|---|
| `--lang zh\|en` | Output language (default: zh) |
| `--focus business\|technical\|investment` | Deep-dive one dimension |
| `--output path` | Custom report output path |

## Output

Reports saved to `./research-reports/[project-name]-due-diligence-[date].md` by default.
