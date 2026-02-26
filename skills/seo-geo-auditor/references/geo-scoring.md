# Scoring Rubrics

## 1. GEO Score (/100)

Measures how well the site's content would be cited by AI engines (ChatGPT, Perplexity, Claude).

### Breakdown

| Criteria | Points | What to Check |
|----------|--------|---------------|
| **Structured Data** | 0-20 | JSON-LD presence, variety (Organization, FAQ, SoftwareApplication, Article, HowTo, Breadcrumb) |
| **Self-Contained Answers** | 0-20 | Each page has extractable answer blocks (definition, comparison, verdict) |
| **Authority Signals** | 0-15 | Statistics with sources, expert quotes, official references, dates |
| **Content Density** | 0-15 | Unique content per page (not just template variables), data richness |
| **AI Bot Access** | 0-10 | robots.txt allows GPTBot, Claude-Web, PerplexityBot, etc. |
| **Topical Completeness** | 0-10 | Coverage of subtopics within theme (FAQ breadth, related content) |
| **Freshness Signals** | 0-10 | Updated dates, year in titles, current data |

### Grading Scale

| Score | Grade | Meaning |
|-------|-------|---------|
| 90-100 | A | Excellent — likely cited by AI engines |
| 75-89 | B | Good — some gaps in coverage or signals |
| 60-74 | C | Average — significant improvement needed |
| 40-59 | D | Poor — minimal GEO optimization |
| 0-39 | F | Not optimized for AI engines |

## 2. Fan-Out Coverage (%)

Measures what percentage of realistic search queries are covered by existing content.

### Calculation

```
Coverage = (Fully_Covered + 0.5 * Partially_Covered) / Total_Queries * 100
```

**Fully Covered**: A page exists that directly targets the query with:
- Query keyword in title or H1
- Dedicated content addressing the specific intent
- Proper metadata targeting the query

**Partially Covered**: A page exists that addresses the topic but:
- Query is only mentioned, not focused on
- Content is generic (not specific to the query)
- Metadata doesn't target this specific query

**Not Covered**: No existing page addresses the query.

### Benchmarks

| Coverage | Assessment |
|----------|------------|
| >80% | Excellent — focus on depth and quality |
| 60-80% | Good — clear gaps to fill |
| 40-60% | Average — significant content creation needed |
| 20-40% | Poor — many gaps |
| <20% | Critical — site barely covers the topic |

## 3. Next.js SEO Score (/100)

Measures technical SEO implementation quality specific to Next.js App Router.

### Breakdown

| Criteria | Points | What to Check |
|----------|--------|---------------|
| **Metadata** | 0-20 | `generateMetadata` or `metadata` export on every route, unique titles/descriptions |
| **Static Generation** | 0-15 | `generateStaticParams` for all dynamic routes, proper ISR/SSG |
| **Sitemap** | 0-10 | `sitemap.ts` present, all pages included, dynamic generation |
| **Robots** | 0-10 | `robots.ts` present, AI bots allowed, proper disallow rules |
| **Structured Data** | 0-15 | JSON-LD on relevant pages, variety of schemas |
| **Performance** | 0-10 | next/image usage, font optimization, loading.tsx, dynamic imports |
| **OpenGraph** | 0-10 | OG images, Twitter cards, proper social metadata |
| **URL Structure** | 0-5 | Clean URLs, consistent patterns, no query params for content |
| **Accessibility** | 0-5 | Alt text, heading hierarchy, semantic HTML |

### Grading Scale

| Score | Grade | Meaning |
|-------|-------|---------|
| 90-100 | A | Production-ready, well-optimized |
| 75-89 | B | Good, minor improvements needed |
| 60-74 | C | Functional but missing key optimizations |
| 40-59 | D | Significant gaps in implementation |
| 0-39 | F | Needs fundamental work |

## Presenting Scores

Always present the 3 scores together on a single line:

```
GEO: XX/100 | Fan-Out: XX% | Next.js SEO: XX/100
```

Follow with a one-line assessment per score when relevant:
- If a score is below 60, flag it as priority
- If a score is above 80, note what's working well
- Always indicate the highest-impact improvement for each score
