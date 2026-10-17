# Developer Notes — Site Completion Matrix

## Purpose

The Site Completion Matrix tracks the public HTML pages generated for each enabled language. It helps maintain SEO, distribution, and search-indexing status for pages that can be monitored in Google Search Console.

## Data source and inclusion rule

The translated matrix pages are in `content/<language>/docs/the-movement-matrix/site-completion-matrix.md`. Each includes the `site-completion-matrix` shortcode implemented in `layouts/shortcodes/site-completion-matrix.html`.

The shortcode uses Hugo's `site.Pages` collection for the current language and retains pages with an HTML output format. Hugo's collection includes the home page, regular content pages, section pages (including `_index.md` pages with `bookCollapseSection: true`), and generated taxonomy/listing pages. This means menu membership, series membership, page date, and section naming do not control inclusion. The shared collection partial deduplicates by each page's canonical `.RelPermalink` before partitioning it into dated and undated sets; the tables link to that same permalink. Repeated visible titles are not sufficient evidence of a duplicate: category and tag pages for the same term, or a content page and a taxonomy term, are distinct pages when their canonical permalinks differ and must remain included.

## Matrix columns and thumbnails

The dated table columns are Date, Image, Title, SEO, Distribution, and Search. The undated table omits Date and begins with Image, followed by Title and the same status columns. The title remains the page link.

The page title remains independent of the table counts. The **Dated Content** heading immediately above the first table (localized for English, Ukrainian, and Portuguese) displays the dated-row count; **Undated Content** above the second table displays the undated-row count. The shortcode computes each count as the length of its corresponding dated or undated page slice and renders rows from that same slice. Counts therefore match the data rows, exclude table headers, include pages with missing images or status fields, use localized thousands separators, and update automatically when pages enter, leave, or move between subsets. Their sum equals the number of matrix data rows for that language. Counting is implemented in the main shortcode; there is no separate dated-count shortcode or partial.

Each title link is followed by a compact localized page-type label derived from Hugo's Page Model. `Kind == "term"` plus `Data.Plural == "categories"` or `"tags"` identifies Category or Tag; `Kind == "taxonomy"` with those plural names identifies Categories or Tags indexes. `Kind == "page"`, `"section"`, and `"home"` identify Page, Section, and Home. Unrecognized taxonomy names receive a generic Term or Taxonomy label; unrecognized kinds omit the label. The label is outside the title link. Type labels are visual metadata only and do not change page inclusion or ordering.

The Image column uses the row page's existing `image` and `alt` Front Matter fields. A valid local image under `static/` renders at 40 × 40 CSS pixels with a square `object-fit: cover` crop, subtle 1px gray border, and 3px corner radius. Its fixed 40px frame does not shrink, and the Image column is fixed at 64px including cell padding in both tables; extra left padding separates it from Title. The matrix-scoped rule targets the actual image element with higher specificity than the theme's `.book-page article img` rule and uses important width and height resets, preventing the theme's 260px article-image sizing or full-width narrow-screen rule from enlarging it. If the image field is absent, empty, or points to no file under `static/`, the cell stays blank. If a valid image has no alt description, it uses empty alt text because the adjacent title labels the same row. If the page title is empty, the visible link label falls back to a humanized label derived from its canonical URL path; the page remains included and its existing sort position is unchanged. The dated table's Date column has a 104px minimum width and keeps the existing `YYYY-MM-DD` format on one line; the undated table has no Date column. Both tables remain horizontally scrollable on narrow screens. See `DEVELOPER_NOTES_thumbnails.md` for the compact variant and the shared thumbnail standard; other components retain their established sizes.

Non-HTML output formats and static files are excluded because they are not HTML pages to monitor in Search Console. Technical endpoints such as `sitemap.xml` and `robots.txt`, Hugo alias redirect files, and paginator continuation URLs are also outside `site.Pages`; these are redirect or duplicate listing variants rather than distinct content pages. The canonical section and taxonomy landing pages remain included. There are no content-category exceptions in the shortcode.

## Language behavior

The shortcode uses the current site language's page collection and permalink, so it does not combine translated URLs or require matching source filenames. Hugo is currently configured for Ukrainian (`uk`), English (`en`), and Portuguese (`pt`). Russian (`ru`) content exists, but its language definition is commented out and a separate `[languages.ru] disabled = true` setting appears in `hugo.toml`; its pages are therefore not built or listed. This note documents the repository's current configuration and does not imply that Russian should be enabled. If Russian is intentionally enabled later, the localized matrix page and shortcode can use its page collection.

## Status fields

For every listed page, the matrix reads `seo`, `distribution`, and `search` from that page's Front Matter. Green indicates a truthy `seo` or `distribution` value, and for `search` the value `indexed`; yellow indicates `search: submitted`; other or missing search values show white. The existing `completion` Front Matter remains editorial metadata and is not a displayed column. No extra status fields are required to make a page appear. Localized type labels are visual metadata rendered immediately after (and outside) the title link; they do not change membership, row order, or status interpretation.

## Dates and ordering

Pages with `publication_date` appear in the dated table, sorted newest first. Pages without it appear in a separate **Undated Content** table, sorted alphabetically by title. Missing dates do not remove pages from the matrix.

## Future content and taxonomies

New regular pages, standalone works, series, collapsed sections, non-menu sections (including Archive, Research, Series & Projects, Studio, and Tools), and HTML taxonomy pages such as categories and tags are included automatically when Hugo generates them for the current language with an HTML output format. Future taxonomy configuration should be verified in the built output; no taxonomy names are hardcoded here.

## Local verification

Run a full `hugo` build, then inspect `public/<language>/docs/the-movement-matrix/site-completion-matrix/index.html` for every enabled language. Count the data rows in each table (excluding its header) and compare them with the corresponding displayed heading counts; their sum must match the total rows. Compare the actual row links from both tables with the canonical HTML page inventory (exclude Hugo aliases and paginator continuation URLs). Normalize the language root as `/<language>/` (not `/<language>//`) and decode HTML character references and percent-encoding in URL paths before comparing. This matters for paths such as the `3+36` tag, whose `+` can be emitted as `&#43;` in HTML. Confirm every canonical permalink occurs once across both tables, dated and undated sets do not overlap, and totals match the unique eligible page inventory. Repeated titles may be legitimate when the links point to distinct category, tag, or content pages; compare URLs and Page Model labels rather than deduplicating by title. Confirm labels for category/tag terms, taxonomy indexes, pages, sections, and the home page where present; verify labels are outside title links, links remain language-local, section and taxonomy pages appear where generated, image paths resolve as expected, and dated and undated groups retain their ordering. Check that status indicators and thumbnail cells remain present. Run `git diff --check`. A new language must have its own translated matrix page and translated type labels to show the shortcode.
