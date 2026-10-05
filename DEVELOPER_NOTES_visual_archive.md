# DEVELOPER NOTES --- Timeline / Visual Archive

## Purpose

`Timeline — Visual Archive` is the visual chronological archive of
Pivtorak.Studio.

It collects dated, illustrated articles from the `/docs/` content tree
and displays them as a vertical visual timeline.

The archive is not maintained manually as a list of articles.\
Its contents are generated automatically from Front Matter and page
location.

------------------------------------------------------------------------

## 1. Page locations

The Timeline page exists in all four site languages:

``` text
content/en/docs/timeline/_index.md
content/pt/docs/timeline/_index.md
content/ru/docs/timeline/_index.md
content/uk/docs/timeline/_index.md
```

Each page contains the language-specific title and introductory text,
followed by:


{{< visual-archive >}}


The same shortcode generates the actual archive content for every
language.

The public route remains:

``` text
/en/docs/timeline/
/pt/docs/timeline/
/ru/docs/timeline/
/uk/docs/timeline/
```

------------------------------------------------------------------------

## 2. Files involved

### Primary files

  ------------------------------------------------------------------------------
  File                                       Function
  ------------------------------------------ -----------------------------------
  `content/{lang}/docs/timeline/_index.md`   Timeline page itself and its
                                             introductory text

  `layouts/shortcodes/visual-archive.html`   Collects, filters, sorts, and
                                             renders archive entries

  `assets/_custom.scss`                      Visual Archive layout and
                                             responsive styling
  ------------------------------------------------------------------------------

### Navigation / surrounding structure

  ---------------------------------------------------------------------------
  File                                    Function
  --------------------------------------- -----------------------------------
  `content/{lang}/archive/_index.md`      Archive landing page; links to
                                          Timeline and The Movement Matrix

  `layouts/partials/menu-filetree.html`   Places Timeline and The Movement
                                          Matrix under Archive in the sidebar
  ---------------------------------------------------------------------------

The navigation files do **not** determine which articles appear in the
Timeline.\
Article inclusion is controlled by
`layouts/shortcodes/visual-archive.html`.

------------------------------------------------------------------------

# 3. How the Timeline is built

The shortcode first creates an empty collection:

``` text
$pages := slice
```

It then opens the site's `/docs/` section:

``` text
site.GetPage "/docs"
```

and recursively examines its regular pages:

``` text
.RegularPagesRecursive
```

Therefore the Timeline searches through the `/docs/` content tree
recursively.

For each page, the shortcode checks three conditions:

``` text
.Params.date
.Params.image
not $isStructural
```

Only pages satisfying all three conditions are added to the Timeline.

After collection, pages are sorted by their Hugo `Date` value in
descending order:

``` text
sort $pages "Date" "desc"
```

Therefore:

**newest item → oldest item**

------------------------------------------------------------------------

# 4. Mandatory conditions for an article to appear

An article must satisfy **all** of the following conditions.

## 4.1 It must be a regular page under `/docs/`

The page must belong to the `/docs/` section and be included by:

``` text
.RegularPagesRecursive
```

Section pages, `_index.md` pages, and other non-regular pages are not
collected as archive entries.

------------------------------------------------------------------------

## 4.2 Front Matter must contain `date`

The article must have a non-empty:

``` yaml
date:
```

Without `date`, the article is excluded.

### Required project format

For consistency, Timeline dates must be written as a full ISO-style
datetime with seconds:

``` yaml
date: 2026-09-07T21:00:00
```

Use:

``` text
YYYY-MM-DDTHH:MM:SS
```

Examples:

``` yaml
date: 2026-10-01T15:30:00
date: 2026-09-22T10:00:00
date: 2024-10-18T15:00:00
```

### Important

The shortcode checks whether `.Params.date` exists; it does not itself
validate the number of datetime components.

The `YYYY-MM-DDTHH:MM:SS` format is therefore a **project documentation
requirement and content standard**, not a validation rule implemented by
the shortcode.

Use the full format consistently so that all articles have an
unambiguous chronological timestamp.

------------------------------------------------------------------------

## 4.3 Front Matter must contain `image`

The article must have a non-empty:

``` yaml
image:
```

Example:

``` yaml
image: /images/core-recalibration-000-2024-high-standards.webp
```

Without `image`, the article is excluded from the Timeline.

The image value should point to an existing site image.

The shortcode does not independently test whether the referenced file
exists. A missing or incorrect image path can therefore produce a broken
image even though the article satisfies the `image` condition.

------------------------------------------------------------------------

# 5. Structural exclusions

Some pages may contain both `date` and `image` but are intentionally
excluded.

The shortcode defines them as structural pages.

Current exclusions are:

``` text
site-completion-matrix.md
atlas.md
docs/calculators/
docs/converters/
```

Specifically:

-   `site-completion-matrix.md`
-   `atlas.md`
-   anything inside `docs/calculators/`
-   anything inside `docs/converters/`

These pages are excluded because they are structural / utility content
rather than Timeline works or documented developments.

If a new structural area should never appear in the Timeline, its
exclusion rule must be added to:

``` text
layouts/shortcodes/visual-archive.html
```

------------------------------------------------------------------------

# 6. What information is displayed

For every selected article, the shortcode renders:

### Image

The value from:

``` yaml
image:
```

### Image alternative text

If Front Matter contains:

``` yaml
alt:
```

that value is used.

Otherwise the article title is used as the image `alt` text.

### Title

The page title:

``` text
.Title
```

is displayed and linked to the article.

### Date

The Hugo page date is displayed as:

``` text
YYYY-MM-DD
```

Although the Front Matter stores the full datetime, the visual archive
intentionally displays only the calendar date.

### Series

If present:

``` yaml
series:
```

the series name is displayed.

Both a single value and a YAML slice are supported.

### Project

If present:

``` yaml
project:
```

the project name is displayed.

`series` and `project` are optional.\
They do **not** affect whether the article enters the Timeline.

------------------------------------------------------------------------

# 7. Front Matter: required vs optional

## Required for Timeline inclusion

``` yaml
date: 2026-09-07T21:00:00
image: /images/example.webp
```

These are the two conditions explicitly required by the shortcode.

## Normally expected for a normal article

``` yaml
title: "Article Title"
```

A regular content page should have a title, and the Timeline displays
`.Title`.

## Optional Timeline metadata

``` yaml
alt: "Descriptive alternative text"
series: "Series Name"
project: "Project Name"
```

These fields improve the displayed entry but are not required for
inclusion.

------------------------------------------------------------------------

# 8. Complete example

A normal Timeline-compatible article may therefore contain:

``` yaml
---
title: "001 The Path in My Hands"
date: 2026-10-01T15:00:00
image: /images/the-path-in-my-hands.webp
alt: "The Path in My Hands"
series: LivingTopography
project: agi rE CLDS 5G
---
```

The minimum required Timeline data is:

``` yaml
date: 2026-10-01T15:00:00
image: /images/the-path-in-my-hands.webp
```

------------------------------------------------------------------------

# 9. Why an article may be missing from the Timeline

Check the following in order:

1.  Is the article under `content/{lang}/docs/`?
2.  Is it a regular page rather than a section page?
3.  Does Front Matter contain `date:`?
4.  Is `date:` non-empty and written in the project-standard format?
5.  Does Front Matter contain `image:`?
6.  Is `image:` non-empty?
7.  Is the page one of the intentionally excluded structural pages?
8.  Is it inside `docs/calculators/` or `docs/converters/`?
9.  Does the image path point to an actual file?

The most important rule is:

> **No `date` or no `image` = no Timeline entry.**

------------------------------------------------------------------------

# 10. Chronological order

The archive is sorted automatically:

``` text
sort $pages "Date" "desc"
```

Therefore the most recent article appears first.

The visible date is formatted as:

``` text
2006-01-02
```

which produces:

``` text
2026-10-01
```

The full datetime in Front Matter is still used by Hugo as the page
date.

If two articles have the same date, their relative order should not be
treated as a separately defined Timeline rule. If precise ordering
between same-day entries matters, use distinct timestamps.

------------------------------------------------------------------------

# 11. Visual structure

The Visual Archive is rendered as a vertical timeline.

The CSS is maintained in:

``` text
assets/_custom.scss
```

The main classes are:

``` text
.visual-archive
.visual-archive-card
.visual-archive-card__image
.visual-archive-card__image img
.visual-archive-card__body
.visual-archive-card__title
.visual-archive-card__date
.visual-archive-card__meta
```

The timeline uses:

-   a vertical axis;
-   a circular point for each entry;
-   a square image area;
-   article information beside the image on desktop;
-   a single-column layout on mobile.

The image itself carries its visual border and rounded corners. The
image container provides the square geometry.

------------------------------------------------------------------------

# 12. Important maintenance rule

Do not manually add individual articles to the Timeline.

To make a normal article appear in the archive, maintain its Front
Matter correctly:

``` yaml
date: YYYY-MM-DDTHH:MM:SS
image: /images/filename.webp
```

The Timeline will collect it automatically.

Do not create a manual list of Timeline entries in:

``` text
content/{lang}/docs/timeline/_index.md
```

The `_index.md` file is the page shell and introduction only.

The collection logic belongs exclusively to:

``` text
layouts/shortcodes/visual-archive.html
```

------------------------------------------------------------------------

# 13. If the Timeline logic is changed

If the selection rules, excluded paths, displayed metadata, sorting, or
HTML structure are changed, update this developer note at the same time.

The following two files should normally be reviewed together:

``` text
layouts/shortcodes/visual-archive.html
DEVELOPER_NOTES_visual_archive.md
```

This keeps the technical documentation synchronized with the actual
archive logic.
