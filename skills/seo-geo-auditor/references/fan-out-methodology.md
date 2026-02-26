# Fan-Out Query Methodology

## Principle

Fan-out queries simulate how real users search for information related to a topic.
Instead of targeting a single keyword, map the entire **semantic space** around the topic.

## Query Generation Process

### Step 1: Identify the Core Topic

Extract the primary topic from:
- Site title and description
- H1 tags across pages
- Data files (product lists, categories)
- Navigation structure

### Step 2: Define Cluster Axes

For each site type, use these cluster axes:

**Comparator sites:**
1. **By solution** — "[solution] avis", "[solution] prix", "[solution] alternative"
2. **By comparison** — "[A] vs [B]", "comparatif [A] [B]"
3. **By use-case** — "meilleur [type] pour [besoin]"
4. **By company size** — "[type] pour TPE", "[type] pour PME", "[type] pour grande entreprise"
5. **By feature** — "[type] avec [fonctionnalite]"
6. **By pricing** — "[type] gratuit", "[type] pas cher", "prix [type]"
7. **By sector/industry** — "[type] pour [secteur]"
8. **By integration** — "[type] compatible [outil]"

**SaaS sites:**
1. **Feature queries** — "[product] [feature]", "comment [faire X] avec [product]"
2. **Alternative queries** — "alternative a [competitor]", "[product] vs [competitor]"
3. **Integration queries** — "[product] [integration] integration"
4. **Use-case queries** — "[product] pour [use-case]"
5. **How-to queries** — "comment [action] avec [product]"
6. **Pricing queries** — "[product] prix", "[product] gratuit"

**Blog/editorial sites:**
1. **Informational** — "qu'est-ce que [concept]", "[concept] definition"
2. **How-to** — "comment [action]", "guide [topic]"
3. **Best-of** — "meilleur [type] [year]", "top [N] [category]"
4. **Trends** — "[topic] tendances [year]", "evolution [topic]"
5. **Tools** — "outil [function]", "logiciel [function]"

### Step 3: Generate Queries per Cluster

For each cluster axis, generate 5-10 specific queries using:
- Real product/solution names from the site's data
- Common French search patterns
- Long-tail variations

### Step 4: Estimate Volume

Use relative indicators (not exact numbers):

| Indicator | Meaning | Criteria |
|-----------|---------|----------|
| High | >1000 searches/month | Generic terms, common problems, popular solutions |
| Medium | 100-1000/month | Specific comparisons, feature queries, medium-tail |
| Niche | <100/month | Very specific combinations, long-tail, high intent |

**Heuristics for French market:**
- "meilleur [X]" = typically high volume
- "[A] vs [B]" = medium volume (depends on solution popularity)
- "[X] pour [specific-need]" = niche but high conversion
- "[X] prix" = medium to high
- "[X] avis" = medium to high

### Step 5: Map Queries to Existing Pages

For each query, determine:
1. **Covered**: An existing page directly targets this query
2. **Partially covered**: A page exists but doesn't optimize for this specific query
3. **Not covered**: No existing page addresses this query

## Coverage Calculation

```
Fan-Out Coverage = (Covered + 0.5 * Partially Covered) / Total Queries * 100
```

## Gap Prioritization

Prioritize gap pages by:
1. **Volume x Intent score**: Higher volume + higher purchase intent = higher priority
2. **Effort to create**: Pages that can be generated from existing data = lower effort
3. **Cluster completeness**: Filling gaps in partially-covered clusters first

## Cross-Linking Strategy

After generating fan-out queries, identify natural internal links:
- Solution pages → Comparison pages (bidirectional)
- Use-case pages → Solution pages (relevant solutions)
- Feature pages → Solution pages (solutions with that feature)
- Comparison pages → Both solution pages
- Hub pages → All child pages in cluster

## Example: SIRH Comparator

**Core topic**: Logiciel SIRH

**Clusters generated:**
1. By solution: "Lucca avis", "PayFit SIRH", "Factorial prix"...
2. By comparison: "Lucca vs PayFit", "Personio vs Factorial"...
3. By company size: "SIRH TPE", "SIRH PME 50 salaries", "SIRH grande entreprise"...
4. By feature: "SIRH avec paie integree", "SIRH conges absences", "SIRH recrutement"...
5. By sector: "SIRH restaurant", "SIRH BTP", "SIRH startup"...
6. By pricing: "SIRH gratuit", "SIRH open source", "prix SIRH par salarie"...

Total: ~40 queries across 6 clusters.
