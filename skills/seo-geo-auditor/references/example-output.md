# Example Output — SIRH Comparator Site

Real audit output from a French SIRH (HR software) comparator with 118 pages, 15 solutions, and 8 content dimensions.

---

## Scores
GEO: 74/100 | Fan-Out: 62% | Next.js SEO: 87/100

**GEO 74/100**: Good structured data (Organization, SoftwareApplication, FAQ, Breadcrumb, ItemList) but missing Review schema, no freshness signals (no year in titles, no "updated" dates), no self-contained answer blocks for LLM extraction.

**Fan-Out 62%**: Strong coverage on solution/comparison/module queries. Zero coverage on informational cluster ("what is SIRH", "how to choose") and pricing cluster ("free SIRH", "open source"). These represent the biggest gaps.

**Next.js SEO 87/100**: Excellent SSG implementation (all 118 pages pre-built), proper metadata on every route, dynamic sitemap, robots.ts allows AI bots. Minor gaps: no loading.tsx, alt text missing on logos.

---

## Fan-Out Queries (42 queries, 7 clusters)

**Cluster 1 — Solutions (reviews/pricing)** [HIGH VOLUME]
- "lucca avis" [HIGH] → Covered (`/solution/lucca`)
- "payfit sirh avis" [HIGH] → Covered (`/solution/payfit`)
- "factorial prix" [MEDIUM] → Covered (`/solution/factorial`)
- "personio avis" [MEDIUM] → Covered (`/solution/personio`)
- "eurecia tarif" [MEDIUM] → Covered (`/solution/eurecia`)
- "combo hrm avis" [NICHE] → Covered (`/solution/combo`)

**Cluster 2 — Comparisons (vs)** [HIGH VOLUME]
- "lucca vs payfit" [HIGH] → Covered (`/comparer/lucca-vs-payfit`)
- "factorial vs personio" [MEDIUM] → Covered (`/comparer/factorial-vs-personio`)
- "eurecia vs lucca" [MEDIUM] → Covered (`/comparer/eurecia-vs-lucca`)
- "bamboohr vs personio" [NICHE] → Covered (`/comparer/bamboohr-vs-personio`)
- "payfit vs silae" [MEDIUM] → NOT COVERED
- "sage vs cegid sirh" [NICHE] → NOT COVERED

**Cluster 3 — By company size** [HIGH VOLUME]
- "sirh pme" [HIGH] → Covered (`/taille/pme`)
- "logiciel rh tpe" [HIGH] → Covered (`/taille/tpe`)
- "sirh grande entreprise" [MEDIUM] → Covered (`/taille/grande-entreprise`)
- "sirh startup" [MEDIUM] → NOT COVERED
- "sirh 50 salaries" [MEDIUM] → Partial (`/taille/pme` mentions but doesn't focus)
- "sirh 500 salaries" [NICHE] → Partial (`/taille/eti`)

**Cluster 4 — By module/feature** [MEDIUM VOLUME]
- "logiciel gestion conges" [HIGH] → Covered (`/module/conges-absences`)
- "sirh paie integree" [HIGH] → Partial (no `/module/paie` page)
- "logiciel recrutement rh" [MEDIUM] → Covered (`/module/recrutement`)
- "outil entretien annuel" [MEDIUM] → Covered (`/module/entretiens`)
- "logiciel onboarding salarie" [NICHE] → Covered (`/module/onboarding`)
- "sirh avec planning" [NICHE] → Covered (`/module/planning`)
- "logiciel gpec" [NICHE] → Covered (`/module/gpec`)
- "logiciel note de frais" [MEDIUM] → Covered (`/module/notes-de-frais`)

**Cluster 5 — By sector** [MEDIUM VOLUME]
- "sirh restauration" [MEDIUM] → Covered (`/secteur/restauration-hotellerie`)
- "sirh btp" [MEDIUM] → Covered (`/secteur/btp`)
- "sirh sante" [MEDIUM] → Covered (`/secteur/sante`)
- "sirh association" [MEDIUM] → NOT COVERED
- "sirh cabinet comptable" [NICHE] → NOT COVERED
- "sirh collectivite territoriale" [NICHE] → NOT COVERED
- "sirh industrie" [NICHE] → Covered (`/secteur/industrie`)

**Cluster 6 — Informational** [HIGH VOLUME]
- "qu'est ce qu'un sirh" [HIGH] → NOT COVERED
- "sirh definition" [HIGH] → NOT COVERED
- "avantages sirh" [MEDIUM] → NOT COVERED
- "comment choisir un sirh" [HIGH] → NOT COVERED
- "cahier des charges sirh" [MEDIUM] → NOT COVERED
- "roi sirh" [NICHE] → NOT COVERED

**Cluster 7 — Pricing/free** [MEDIUM VOLUME]
- "sirh gratuit" [HIGH] → NOT COVERED
- "sirh open source" [MEDIUM] → NOT COVERED
- "prix sirh par salarie" [MEDIUM] → Partial (in `/taille/` but not dedicated)
- "comparatif prix sirh" [MEDIUM] → NOT COVERED

---

## Gaps

### Critical: Informational cluster (0% coverage)

Entire cluster 6 is uncovered. This is top-of-funnel traffic that feeds into solution/comparison pages.

| Gap | Volume | Suggested route |
|-----|--------|-----------------|
| "Qu'est-ce qu'un SIRH" | HIGH | `/guide/definition-sirh` |
| "Comment choisir un SIRH" | HIGH | `/guide/comment-choisir-sirh` |
| "Avantages SIRH" | MEDIUM | `/guide/avantages-sirh` |
| "Cahier des charges SIRH" | MEDIUM | `/guide/cahier-des-charges-sirh` |

### High: Pricing cluster (0% coverage)

| Gap | Volume | Suggested route |
|-----|--------|-----------------|
| "SIRH gratuit" | HIGH | `/gratuit` |
| "SIRH open source" | MEDIUM | `/open-source` |
| "Comparatif prix SIRH" | MEDIUM | `/prix` |

### Medium: Missing sectors

| Gap | Suggested route |
|-----|-----------------|
| "SIRH association" | `/secteur/association` |
| "SIRH cabinet comptable" | `/secteur/expertise-comptable` |
| "SIRH collectivite" | `/secteur/collectivite-territoriale` |

### Medium: Missing comparisons

| Gap | Suggested route |
|-----|-----------------|
| "PayFit vs Silae" | `/comparer/payfit-vs-silae` |
| "Sage vs Cegid SIRH" | `/comparer/sage-vs-cegid-talentsoft` |

---

## Quick Wins (<48h)

### 1. Add year to metaTitle on all solutions

`src/lib/data/solutions.ts` — every solution's metaTitle:
```diff
- metaTitle: "Lucca : Avis, Prix et Fonctionnalités SIRH"
+ metaTitle: "Lucca : Avis, Prix et Fonctionnalités SIRH (2026)"
```

### 2. Add AggregateRating schema on solution pages

`src/lib/structured-data.ts` — in the function generating solution schemas:
```diff
+ if (solution.rating) {
+   schemas.push({
+     "@context": "https://schema.org",
+     "@type": "AggregateRating",
+     "itemReviewed": {
+       "@type": "SoftwareApplication",
+       "name": solution.name
+     },
+     "ratingValue": solution.rating.score,
+     "bestRating": 5,
+     "ratingCount": solution.rating.reviewCount
+   });
+ }
```

### 3. Add alt text on solution logos

`src/components/SolutionCard.tsx`:
```diff
- <Image src={solution.logo} width={40} height={40} />
+ <Image src={solution.logo} width={40} height={40} alt={`Logo ${solution.name}`} />
```

### 4. Fix sitemap lastModified

`src/app/sitemap.ts`:
```diff
- lastModified: new Date(),
+ lastModified: new Date('2026-02-26'),
```

### 5. Add self-contained verdict block on solution pages

`src/app/solution/[slug]/page.tsx` — after the description section:
```tsx
<p className="text-lg font-medium">
  <strong>{solution.name} en bref :</strong> {solution.tagline}.
  A partir de {solution.pricing.startingPrice} EUR/mois.
  Note : {solution.rating.score}/5 ({solution.rating.reviewCount} avis).
</p>
```

---

## Routes to Create

| Route | Title | H1 | Target queries |
|-------|-------|-----|----------------|
| `/guide/definition-sirh` | Qu'est-ce qu'un SIRH ? Definition et Guide 2026 | Qu'est-ce qu'un SIRH ? | "sirh definition", "qu'est ce qu'un sirh" |
| `/guide/comment-choisir-sirh` | Comment choisir un SIRH en 2026 ? Guide complet | Comment choisir son SIRH | "comment choisir un sirh", "cahier des charges sirh" |
| `/guide/avantages-sirh` | Les 10 avantages d'un SIRH pour votre entreprise | Pourquoi adopter un SIRH ? | "avantages sirh", "roi sirh" |
| `/gratuit` | SIRH Gratuit : Les meilleures solutions en 2026 | SIRH gratuit : comparatif 2026 | "sirh gratuit", "sirh open source" |
| `/prix` | Comparatif Prix SIRH 2026 : Quel budget prevoir ? | Prix des SIRH en 2026 | "prix sirh", "comparatif prix sirh" |

---

## Roadmap

**J1-J7:**
- Quick wins 1-5 (metaTitle, Review schema, alt text, sitemap, verdict blocks)
- Create `/guide/definition-sirh`
- Add 2 missing comparisons to `comparisons.ts`
- Deploy

**J8-J30:**
- Create `/guide/comment-choisir-sirh` + `/guide/avantages-sirh`
- Create `/gratuit` and `/prix`
- Add 3 missing sectors to `sectors.ts`
- Submit sitemap to Google Search Console + Bing
- Monitor indexation (target: 100% of 130+ URLs indexed in 30 days)

---

## Bonus — Prompts to generate missing content

**Prompt 1 — SIRH definition page:**
> Write a 2000-word article for "What is an SIRH?" in French. Structure: 2-sentence definition (LLM-extractable), 3-line history, 8 main modules (leave management, recruiting, training, reviews, expenses, planning, onboarding, GPEC), benefits by company size (TPE, PME, ETI, GE), how to choose (5 criteria), FAQ with 5 questions. Tone: expert but accessible. Concrete data (number of FR companies, legal obligations). Sources: service-public.fr, legifrance.gouv.fr.

**Prompt 2 — Free SIRH page:**
> Write a comparison of free and open source SIRH solutions in France (2026) in French. Include: solutions with free tiers (Factorial, Combo, etc.), open source SIRH (OrangeHRM, Odoo HR), comparison table (free vs paid features), free tier limitations (employee count, modules), verdict: "free is sufficient for <10 employees, paid recommended beyond". FAQ with 3 questions.
