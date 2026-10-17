# Developer Notes — Site Completion Matrix

## Purpose

The Site Completion Matrix tracks the public HTML pages generated for each enabled language. It helps maintain SEO, distribution, and search-indexing status for pages that can be monitored in Google Search Console.

## Data source and inclusion rule

The translated matrix pages are in `content/<language>/docs/the-movement-matrix/site-completion-matrix.md`. Each includes the `site-completion-matrix` shortcode implemented in `layouts/shortcodes/site-completion-matrix.html`.

The shortcode uses Hugo's `site.Pages` collection for the current language and retains pages with an HTML output format. Hugo's collection includes the home page, regular content pages, section pages (including `_index.md` pages with `bookCollapseSection: true`), and generated taxonomy/listing pages. This means menu membership, series membership, page date, and section naming do not control inclusion. Each page appears once in the current language's collection and links to its own `.RelPermalink`.

## Matrix columns and thumbnails

The dated table columns are Date, Image, Title, SEO, Distribution, and Search. The undated table omits Date and begins with Image, followed by Title and the same status columns. The title remains the page link.

The Image column uses the row page's existing `image` and `alt` Front Matter fields. A valid local image under `static/` renders at 32 × 32 CSS pixels with a square crop, subtle border, and rounded corners. If the image field is absent, empty, or points to no file under `static/`, the cell stays blank. If a valid image has no alt description, it uses empty alt text because the adjacent title labels the same row. The table remains horizontally scrollable on narrow screens. See `DEVELOPER_NOTES_thumbnails.md` for the compact variant and the shared thumbnail standard; other components retain their established sizes.

Non-HTML output formats and static files are excluded because they are not HTML pages to monitor in Search Console. Technical endpoints such as `sitemap.xml` and `robots.txt`, Hugo alias redirect files, and paginator continuation URLs are also outside `site.Pages`; these are redirect or duplicate listing variants rather than distinct content pages. The canonical section and taxonomy landing pages remain included. There are no content-category exceptions in the shortcode.

## Language behavior

The shortcode uses the current site language's page collection and permalink, so it does not combine translated URLs or require matching source filenames. Hugo is currently configured for Ukrainian (`uk`), English (`en`), and Portuguese (`pt`). Russian (`ru`) content exists, but its language definition is commented out and a separate `[languages.ru] disabled = true` setting appears in `hugo.toml`; its pages are therefore not built or listed. This note documents the repository's current configuration and does not imply that Russian should be enabled. If Russian is intentionally enabled later, the localized matrix page and shortcode can use its page collection.

## Status fields

For every listed page, the matrix reads `seo`, `distribution`, and `search` from that page's Front Matter. Green indicates a truthy `seo` or `distribution` value, and for `search` the value `indexed`; yellow indicates `search: submitted`; other or missing search values show white. The existing `completion` Front Matter remains editorial metadata and is not a displayed column. No extra status fields are required to make a page appear.

## Dates and ordering

Pages with `publication_date` appear in the dated table, sorted newest first. Pages without it appear in a separate **Undated Content** table, sorted alphabetically by title. Missing dates do not remove pages from the matrix.

## Future content and taxonomies

New regular pages, standalone works, series, collapsed sections, non-menu sections (including Archive, Research, Series & Projects, Studio, and Tools), and HTML taxonomy pages such as categories and tags are included automatically when Hugo generates them for the current language with an HTML output format. Future taxonomy configuration should be verified in the built output; no taxonomy names are hardcoded here.

## Local verification

Run a full `hugo` build, then inspect `public/<language>/docs/the-movement-matrix/site-completion-matrix/index.html` for every enabled language. Compare its table links with the canonical HTML page inventory (exclude Hugo aliases and paginator continuation URLs). Normalize the language root as `/<language>/` (not `/<language>//`) and decode HTML character references and percent-encoding in URL paths before comparing. This matters for paths such as the `3+36` tag, whose `+` can be emitted as `&#43;` in HTML. Confirm every link is language-local, section and taxonomy pages appear where generated, no URL occurs twice, and dated and undated groups retain their ordering. A new language must have its own translated matrix page to show the shortcode.
