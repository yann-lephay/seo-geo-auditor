# Next.js App Router SEO Checklist

Complete checklist for Next.js 14+ App Router sites.

## Metadata (Critical)

### Per-Route Metadata

- [ ] Every `page.tsx` exports `metadata` or `generateMetadata`
- [ ] Unique `title` per page (50-60 chars, keyword near start)
- [ ] Unique `description` per page (150-160 chars, includes keyword)
- [ ] `title.template` set in root `layout.tsx` (e.g., `"%s | SiteName"`)
- [ ] `title.default` set in root `layout.tsx`
- [ ] No duplicate titles across pages
- [ ] No duplicate descriptions across pages

### Dynamic Metadata

For dynamic routes (`[slug]`, `[id]`):
- [ ] `generateMetadata` reads params and returns unique metadata
- [ ] Fallback metadata for missing data
- [ ] Proper error handling in `generateMetadata`

### OpenGraph

- [ ] `openGraph.title` and `openGraph.description` set
- [ ] `openGraph.images` with proper dimensions (1200x630)
- [ ] `openGraph.type` set (website, article, etc.)
- [ ] `openGraph.url` set
- [ ] `openGraph.siteName` set
- [ ] Twitter card metadata (`twitter.card`, `twitter.title`, `twitter.description`)

## Static Generation (High Impact)

### generateStaticParams

- [ ] All dynamic routes implement `generateStaticParams`
- [ ] Returns all valid params (not just a subset)
- [ ] Data source matches actual content
- [ ] `dynamicParams` set appropriately (false for strict, true for fallback)

### Static vs Dynamic

- [ ] Content pages are statically generated (SSG)
- [ ] Only auth/user-specific pages are dynamic
- [ ] ISR configured where fresh data is needed (`revalidate`)
- [ ] `force-static` or `force-dynamic` used intentionally

## Sitemap

- [ ] `sitemap.ts` exists in `app/` directory
- [ ] All public pages included
- [ ] Dynamic pages generated from data source
- [ ] `lastModified` dates are accurate
- [ ] `changeFrequency` and `priority` set appropriately
- [ ] No auth-required or noindex pages in sitemap
- [ ] Sitemap accessible at `/sitemap.xml`

## Robots

- [ ] `robots.ts` exists in `app/` directory
- [ ] `sitemap` URL referenced
- [ ] AI bots allowed (GPTBot, ChatGPT-User, Claude-Web, PerplexityBot, Applebot-Extended)
- [ ] Appropriate `Disallow` rules (admin, api, auth routes)
- [ ] No accidental blocking of important pages

## Structured Data (JSON-LD)

### Essential Schemas

- [ ] `Organization` on homepage (name, url, logo, description)
- [ ] `WebSite` with `SearchAction` if applicable
- [ ] `BreadcrumbList` on inner pages
- [ ] `FAQPage` on pages with FAQ sections

### By Page Type

**Comparator/Directory:**
- [ ] `SoftwareApplication` per solution (name, applicationCategory, offers, aggregateRating)
- [ ] `ItemList` on listing pages
- [ ] `WebPage` with `speakable` for key content

**Blog/Article:**
- [ ] `Article` or `BlogPosting` (headline, datePublished, dateModified, author, image)
- [ ] `HowTo` on tutorial/guide pages
- [ ] `FAQPage` on FAQ sections

**SaaS/Product:**
- [ ] `SoftwareApplication` (name, offers, operatingSystem, applicationCategory)
- [ ] `Product` with `offers` for pricing pages
- [ ] `Review` or `AggregateRating` if applicable

### Implementation

- [ ] JSON-LD in `<script type="application/ld+json">`
- [ ] Valid according to Google Rich Results Test
- [ ] No errors in Search Console structured data report

## Performance (SEO Impact)

### Images

- [ ] All images use `next/image` component
- [ ] `alt` text on every image
- [ ] Proper `width` and `height` set (or `fill` with `sizes`)
- [ ] AVIF/WebP formats enabled (default in Next.js)
- [ ] `priority` set on above-the-fold images (LCP)
- [ ] Lazy loading on below-the-fold images (default)

### Fonts

- [ ] Using `next/font` (Google or local)
- [ ] `display: "swap"` configured
- [ ] Font subsetting where possible
- [ ] Preloaded critical fonts

### Loading States

- [ ] `loading.tsx` in key route groups
- [ ] Skeleton loaders for dynamic content
- [ ] No layout shift during loading (CLS)

### Bundle Size

- [ ] `dynamic(() => import())` for heavy components
- [ ] `ssr: false` for client-only components
- [ ] `optimizePackageImports` in `next.config` for barrel imports
- [ ] No unnecessary client-side JavaScript on static pages

### Caching

- [ ] Cache-Control headers on static assets
- [ ] `immutable` on fonts, images with hashed filenames
- [ ] Proper `revalidate` values for ISR pages

## URL Structure

- [ ] Clean, readable URLs (no query params for content)
- [ ] Consistent pattern (all lowercase, hyphens)
- [ ] Keywords in URLs where natural
- [ ] No unnecessary nesting (keep under 3 levels)
- [ ] Trailing slash consistency

## Internal Linking

- [ ] All pages reachable within 3 clicks from homepage
- [ ] Breadcrumbs with structured data
- [ ] Related content links on each page
- [ ] No broken internal links
- [ ] Hub pages link to all child pages
- [ ] Cross-links between related content

## Accessibility (SEO Overlap)

- [ ] One `<h1>` per page
- [ ] Heading hierarchy (h1 > h2 > h3, no skips)
- [ ] Alt text on all images
- [ ] Semantic HTML (main, nav, article, section, aside)
- [ ] Language attribute on `<html>`
- [ ] Skip navigation link

## Internationalization (if applicable)

- [ ] `hreflang` tags for multi-language
- [ ] Canonical URLs per language
- [ ] Language in URL path (`/fr/`, `/en/`)
- [ ] Proper locale in metadata

## Security Headers (SEO Trust)

- [ ] HTTPS everywhere
- [ ] HSTS header
- [ ] `security.txt` in `.well-known/`
- [ ] CSP configured
- [ ] X-Frame-Options set

## Monitoring

- [ ] Google Search Console connected
- [ ] Bing Webmaster Tools connected
- [ ] Vercel Analytics or equivalent
- [ ] Core Web Vitals monitoring
- [ ] Sitemap submitted to search engines
