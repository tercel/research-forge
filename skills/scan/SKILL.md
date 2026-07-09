---
name: scan
description: >
  Quick scan of a project — gather metadata, key metrics, lifecycle stage
  classification, and first impressions. Supports remote URLs, local
  directories, and local files.
---

# Research-Forge — Scan

Quick reconnaissance scan of a project to gather key signals and classify its lifecycle stage before a full analysis.

## Command: `/research-forge:scan`

### Usage:
`/research-forge:scan <target> [--lang zh|en]`

Target can be a URL, local directory path, or local file path.

### Scan Logic:

#### 1. Detect Target Type & Fetch Project Metadata

**Remote URL:**
- Use WebFetch to retrieve the project's README, GitHub API data, or landing page.
- Extract: name, description, language, license, creation date, last commit date.

**Local Directory:**
- Read README (README.md, README.rst, README.txt — whichever exists).
- Read package manifest (package.json, Cargo.toml, go.mod, pyproject.toml, pom.xml, build.gradle, etc.).
- Glob project structure to understand scope: source files, test files, config files, docs.
- Check git history: `git log --oneline -20`, `git remote -v`, `git shortlog -sn`.
- Extract: name (from manifest or directory name), description, language, license, creation date (first commit), last commit date.

**Local File:**
- Read the file. If it's a README or spec doc, extract project info directly.
- If it's source code, identify the parent project directory and treat as Local Directory.

#### 2. Quantitative Signals

**Remote projects:**
- Popularity: Stars, forks, watchers count and growth trajectory.
- Activity: Commit frequency (last 30/90/365 days), open vs. closed issues ratio, PR merge velocity.
- Community: Number of contributors, contributor concentration (bus factor), Discord/Slack links.
- Dependencies: Key dependencies, number of dependents (who uses this?).

**Local projects:**
- Structure: Total file count, source file count, test file count, lines of code estimate.
- Activity: Commit frequency from git log, number of contributors, branch count.
- Dependencies: Key dependencies from manifest, dependency count, outdated signals.
- Quality signals: Presence of CI config, linter config, test framework, documentation.

#### 3. Stage Classification (MANDATORY)

Classify the project into a lifecycle stage per the Stage Model in the research-forge framework — this determines how the entire downstream analysis is weighted:

- **S0 — Concept / Pre-launch**: No working product or prototype only; no real users; no releases or v0.0.x.
- **S1 — PMF Search (0→1)**: Working product, early adopters, rapid iteration, little/no revenue.
- **S2 — Scaling (1→10)**: Retention evidence, monetization live or forming, sustained growth, team beyond founders.
- **S3 — Market Leadership (10→100)**: Category leader/top-3; third parties build on it; de-facto default choice.

State the classification with:
- 2-3 pieces of converging evidence (age, releases, adoption trajectory, revenue signals, ecosystem signals)
- A confidence level (High / Medium / Low)
- When torn between two stages, pick the earlier one — under-claiming maturity is the safer error.

#### 4. Qualitative First Impressions
- README quality: Is it clear, professional, well-structured?
- Documentation: Does it exist? Is it maintained?
- Positioning: How does the project describe itself? What problem does it claim to solve?
- Code organization: Is the structure clean and conventional for the language/framework?

#### 5. Output Format
Produce a concise snapshot card:

```
Project Snapshot: [Name]
Target: [URL or Path]
Scan Date: [Date]

Quick Stats:
  [Remote] Stars: X | Forks: X | Contributors: X
  [Local]  Files: X | Source: X | Tests: X
  Last Commit: [Date] | Open Issues: X
  Language: [Lang] | License: [License]

Lifecycle Stage: [S0/S1/S2/S3 — Name] (Confidence: High/Medium/Low)
  Evidence: [2-3 converging signals]
  One Question for this stage: [the stage's core question]

First Impressions:
  [2-3 sentence summary]

Key Signals:
  [Bullet list of notable positive/negative signals]

Recommended Next Step:
  [ ] Full analysis warranted → /research-forge:analyze <target>
  [ ] Compare with competitors → /research-forge:compare <target> <competitor>
  [ ] Not worth pursuing → [reason]
```
