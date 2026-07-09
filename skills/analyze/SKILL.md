---
name: analyze
description: >
  Stage-aware due diligence analysis of a project across business, technical,
  and moat/strategy dimensions, weighted by lifecycle stage. Supports remote
  URLs, local directories, and local files.
---

# Research-Forge — Analyze

Deep due diligence analysis across the three dimensions defined in the Research-Forge framework, with scoring weights determined by the project's lifecycle stage.

## Command: `/research-forge:analyze`

### Usage:
`/research-forge:analyze <target> [--lang zh|en] [--focus business|technical|strategy]`

- Target can be a URL, local directory path, or local file path.
- `--focus`: Optionally deep-dive into one specific dimension while keeping others at summary level.
- Default output language: Chinese (Simplified). Override with `--lang en`.

### Analysis Workflow:

#### Phase 0: Stage Detection

If a scan has already classified the stage (auto-chain pipeline), reuse it. Otherwise classify the project into S0/S1/S2/S3 per the Stage Model, with evidence and confidence level. Then load the stage's weight profile from the framework — it decides which sub-dimensions are Critical (×2), Standard (×1), or Context (×0, reported but unscored).

State up front:
- **Stage**: [S0-S3] with evidence
- **One Question this analysis must answer**: [the stage's core question]
- **Death cause to hunt for**: [the stage's characteristic failure mode]

#### Phase 1: Data Collection

**Remote targets:**
1. **WebFetch** the project's README, docs site, and landing page.
2. **WebSearch** for:
   - Recent news, blog posts, or announcements about the project.
   - Funding rounds, acquisitions, or partnership announcements.
   - Community discussions (HN, Reddit, X.com) for sentiment.
   - Competitor landscape — search for "[project] vs" and "[project] alternatives".
3. If a GitHub URL, extract repo metrics via the GitHub web interface.

**Local targets:**
1. **Read** README, manifest files, key config files.
2. **Glob** to map project structure: source, tests, docs, CI config.
3. **Read** representative source files (entry points, core modules, tests) to assess code quality.
4. **Grep** for patterns: TODO/FIXME density, error handling, logging, security patterns.
5. Check git history for activity patterns, contributor stats, branch hygiene.
6. If git remote exists, **WebSearch** for external context about the project.
7. **WebSearch** for competitor landscape regardless of target type.

Prioritize collection toward the stage's Critical sub-dimensions — e.g., for S1 dig for retention proxies (repeat contributors, dependents growth, organic mentions); for S2 dig for pricing, margin structure, and hiring signals; for S3 dig for ecosystem breadth and emerging paradigm threats.

#### Phase 2: Business & Market Analysis
Rate each sub-dimension (1-5), applying the stage weight profile:
- **Problem Validity** (1-5): Is the pain real and acute? Key evidence: users already paying a cost today — money, time, or duct-taped workarounds. No current coping behavior → pseudo-demand.
- **Why Now** (1-5): Name the specific inflection — technology, cost, behavior, or regulation — that makes this viable now. No inflection = too early or too late.
- **PMF Evidence** (1-5): Retention over acquisition. Commercial: cohort retention flattening, organic growth share, Sean Ellis ≥ 40%. OSS proxies: repeat-contributor ratio, dependents growth, issue-reporter recurrence, production testimonials vs. promoted star spikes.
- **Unit Economics** (1-5): LTV/CAC (≥3 paper bar), gross margin direction with scale, NDR (>100% healthy, >120% excellent). OSS: credible open-core boundary and conversion path. Scale that worsens economics = wholesaling losses.
- **Market Ceiling** (1-5): Terminal market, not current TAM — total spend this could absorb at its limit.
- **Growth Engine** (1-5): Identifiable, repeatable engine (product-led / content / sales / paid-with-payback) vs. founder charisma and one-off wins.

#### Phase 3: Technical & Architecture Analysis
Rate each sub-dimension (1-5), applying the stage weight profile:
- **Architecture Quality** (1-5): Modularity, design patterns, API quality.
- **Engineering Culture** (1-5): Code quality, testing, CI/CD, PR review.
- **Scalability** (1-5): Can it handle 10x/100x growth without fundamental redesign?
- **Security Posture** (1-5): Dependency hygiene, vulnerability handling.
- **Documentation** (1-5): Quality, completeness, maintenance.
- **Maintainability & Tech Debt** (1-5): TODO density, deprecated APIs, stale branches, long-lived PRs.

For local targets, the Technical dimension benefits from direct code reading — provide specific evidence from the codebase (file paths, code patterns, architecture observations).

#### Phase 4: Moat & Strategy Analysis
Rate each sub-dimension (1-5), applying the stage weight profile:
- **Moat Strength** (1-5): Rate against the moat hierarchy — 5 network effects, 4 switching costs, 3 scale economies/brand-equals-category, 2 data/tech lead only (AI-era note: pure model lead lasts ~6-18 months; a data flywheel beats the model itself), 1 no moat.
- **Founder-Market Fit** (1-5): Unfair advantage — unique insight, resources, or technology. Include key-person risk.
- **Org Capability** (1-5): Can the org scale past the founders — delegation, senior hires, mid-level strength?
- **Second Curve Readiness** (1-5): Paradigm-shift exposure; willingness to self-disrupt; product → platform/ecosystem trajectory.

Then construct the qualitative theses:
- **Bull Case** (3-5 strongest arguments for success).
- **Bear Case** (3-5 most significant risks — MUST include an explicit check of the current stage's death cause, even if only to rule it out).
- **Comparable Outcomes**: similar projects and their trajectories.

#### Phase 5: Verdict & Kill Criteria
- Compute **Overall Score**: weighted average of non-Context sub-dimensions (Critical ×2, Standard ×1). List Context sub-dimensions separately as `ctx` — unscored.
- Produce **Strategic Verdict**: Strong Recommend | Watch Closely | Hold / Wait | Not Recommended.
  - Any Critical sub-dimension ≤ 2 caps the verdict at Hold / Wait.
  - Strong Recommend requires all Critical sub-dimensions ≥ 3.
- Produce **Investment Signal** (when applicable): Strong Buy / Watch / Hold / Pass.
- Write **Kill Criteria** (mandatory): 2-4 pre-registered, falsifiable, time-bound signals that would flip the verdict.
- Write a **Final Evaluation** paragraph: state the stage, answer the stage's One Question directly, then synthesize.

#### Phase 6: Output
Generate a structured report with:
1. Executive Summary (3-5 sentences, opening with stage + One Question answer)
2. Scorecard table (all sub-dimensions with ratings, weight class per stage, and confidence flags)
3. Detailed analysis per dimension
4. Bull Case / Bear Case (with stage death-cause check)
5. Verdict with confidence level (High/Medium/Low) + Kill Criteria
6. Recommended actions / next steps
