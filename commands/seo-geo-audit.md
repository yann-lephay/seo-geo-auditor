---
description: SEO/GEO audit with fan-out query methodology for Next.js sites
argument-hint: [--express|--deep] [URL or topic]
allowed-tools: Read, Grep, Glob, Bash
---

Perform an SEO/GEO audit using the seo-geo-auditor skill.

**Input**: $ARGUMENTS

**Mode detection**:
- If arguments contain `--express`: Express mode (scores + top 5 quick wins + 3 pages)
- If arguments contain `--deep`: Deep mode (exhaustive analysis with 50-80 queries)
- Otherwise: Standard mode (balanced audit with 25-50 queries)

**Instructions**:

1. Load the seo-geo-auditor skill and read its reference files as needed
2. Detect the site's thematic, type, stack, and architecture by reading the codebase
3. Generate fan-out queries grouped by semantic cluster
4. Score the 3 metrics (GEO /100, Fan-Out Coverage %, Next.js SEO /100)
5. Identify gaps and quick wins with specific file paths
6. Output in the exact structure specified by the skill (strict order)

**Critical rules**:
- Code-first: always read source files before attempting to crawl or fetch
- Deltas only: never output complete files, only the changes
- Every gap must point to a specific file path or missing route
- All 3 scores must be present in every audit
