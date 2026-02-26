# seo-geo-auditor

Claude Code plugin that audits SEO + GEO (Generative Engine Optimization) for Next.js sites.

Uses a **fan-out query methodology**: generates 25-80 realistic search queries, maps them to existing pages, scores semantic coverage, and produces actionable fixes with code deltas.

## What it does

Every audit produces:

| Output | Description |
|--------|-------------|
| **GEO Score /100** | How well AI engines (ChatGPT, Perplexity, Claude) can extract and cite the site's content |
| **Fan-Out Coverage %** | Percentage of realistic search queries covered by existing pages |
| **Next.js SEO Score /100** | Technical SEO implementation (metadata, SSG, sitemap, structured data, performance) |
| **Gap analysis** | Missing pages and content holes, each pointing to a specific file or route |
| **Quick wins** | <48h fixes with copy-paste code deltas |
| **Routes to create** | New pages with title, H1, and target queries |
| **Roadmap** | Prioritized J1-7 and J8-30 action plan |

## Install

```bash
claude plugin add /path/to/seo-geo-auditor
```

Or from GitHub:

```bash
claude plugin add yanMusic/seo-geo-auditor
```

## Usage

### As a slash command

```
/seo-geo-audit                     # Standard audit (25-50 queries)
/seo-geo-audit --express           # Quick: scores + top 5 wins + 3 pages
/seo-geo-audit --deep              # Exhaustive: 50-80 queries, competitor analysis
```

### As a skill (auto-triggered)

The skill activates automatically when you mention:
- "audit SEO", "audit GEO", "find content gaps"
- "semantic coverage", "missing pages", "fan-out queries"
- "check schema.org", "Next.js SEO"

## 3 modes

| Mode | Queries | Best for |
|------|---------|----------|
| **Standard** | 25-50 | Regular audits, balanced depth |
| **Express** | 15-25 | Quick check, CI integration |
| **Deep** | 50-80 | Pre-launch, quarterly reviews |

## How it works

1. **Reads your codebase** — scans `app/`, `lib/`, `components/` to understand routes, data, and metadata (no crawling needed)
2. **Generates fan-out queries** — realistic search queries grouped by semantic cluster, adapted to your site type (comparator, SaaS, blog, e-commerce)
3. **Maps coverage** — checks which queries are covered, partially covered, or missing
4. **Scores 3 metrics** — GEO readiness, fan-out coverage, Next.js technical SEO
5. **Produces fixes** — code deltas, new routes, templates, and a prioritized roadmap

## Example output (excerpt)

```
## Scores
GEO: 74/100 | Fan-Out: 62% | Next.js SEO: 87/100

## Fan-Out Queries (42 queries, 7 clusters)

**Cluster 1 — Solutions**
- "lucca avis" [HIGH] → Covered (/solution/lucca)
- "payfit sirh" [HIGH] → Covered (/solution/payfit)

**Cluster 6 — Informational**
- "qu'est ce qu'un sirh" [HIGH] → NOT COVERED
- "comment choisir un sirh" [HIGH] → NOT COVERED

## Quick Wins (<48h)

1. Add year to metaTitle:
   src/lib/data/solutions.ts
   - metaTitle: "Lucca : Avis, Prix et Fonctionnalités SIRH"
   + metaTitle: "Lucca : Avis, Prix et Fonctionnalités SIRH (2026)"

2. Add Review schema on solution pages:
   src/lib/structured-data.ts — in generateSolutionStructuredData():
   + schemas.push({ "@type": "AggregateRating", ... })
```

See [full example output](skills/seo-geo-auditor/references/example-output.md) from a real audit on a comparator site with 118 pages.

## Site types supported

| Type | Auto-detected by | Cluster strategy |
|------|-----------------|-----------------|
| **Comparator / pSEO** | Data files with solutions/products | vs comparisons, by size, by sector, pricing |
| **SaaS** | Pricing page, features, auth | Features, alternatives, integrations |
| **Blog** | MDX/content directory | Topical clusters, how-to, definitions |
| **E-commerce** | Product schema, cart | Products, categories, buyer intent |

## What's checked (Next.js)

- `generateMetadata` / `metadata` on every route
- `generateStaticParams` for dynamic routes
- `sitemap.ts` completeness
- `robots.ts` with AI bot permissions (GPTBot, Claude-Web, PerplexityBot)
- JSON-LD structured data (Organization, FAQ, SoftwareApplication, Article, Breadcrumb)
- OpenGraph images and Twitter cards
- next/image, next/font optimization
- `loading.tsx` and dynamic imports
- Internal linking depth and orphan pages
- URL structure consistency

## License

MIT
