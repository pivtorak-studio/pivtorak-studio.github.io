# DEVELOPER NOTES Thumbnails

## 1. Purpose

Pivtorak.Studio uses a unified thumbnail standard across the site.

The thumbnail format and visual styling remain consistent, while the layout depends on the component in which the thumbnail appears.

## 2. Thumbnail Standard

All list thumbnails must follow these rules:

- **Format:** square, 1:1 aspect ratio.
    
- **File format:** WebP for published image assets.
    
- **Desktop size:** 8rem.
    
- **Narrow-screen size:** 5rem, where the component uses the responsive thumbnail layout.
    
- **Border:** subtle 1px gray border.
    
- **Corner radius:** 8px.
    
- **Alignment:** preserve the component's intended image alignment and prevent distortion.
    
- **Accessibility:** use descriptive `alt` text from the page's Front Matter.
    

Use the existing image assets whenever possible. Do not generate duplicate covers or modify the original artwork solely to add rounded corners or a border.

## 3. Layout Variants

### A. Landing Pages, Categories and Tags

Applies to:

- `/research/`
    
- `/series-and-projects/`
    
- `/studio/`
    
- `/tools/`
    
- `/archive/`
    
- `/categories/{term}/`
    
- `/tags/{term}/`
    

Layout:

- Thumbnail on the left.
    
- Text on the right.
    
- Common left alignment for all thumbnails within the list.
    
- Image and text aligned to the top.
    
- Consistent spacing between consecutive rows.
    
- Missing images must not break the text layout or row spacing.
    

Use CSS Grid or Flexbox for the image/text relationship. Preserve existing selection, sorting, metadata, summaries and navigation.

### B. Universal Hierarchical Child-Page Lists

Applies at every depth when a page displays its immediate children through `{{< section >}}`. The site-local override is `layouts/_shortcodes/section.html`; each nested page renders its own children on its own page. Lists remain hierarchical and are never flattened.

Layout:

- Read `image` and `alt` from each child page.
- Render the linked title, then a short explanation from `description`, falling back to `summary`.
- Flag a child for editorial description when both fields are missing; do not insert placeholder copy.
- Place the thumbnail on the left and child-page information on the right, aligned at the top.
- Use the same responsive size, square crop, border, radius and row spacing as landing-page lists.
- Keep text-only rows when a child has no image.

The shared styling is scoped to `.hierarchical-page-list`. This is independent of sidebar collapse behavior, Series Map navigation, and the section's own cover or article images.

### C. Series Map

Template: `layouts/_partials/series-navigation.html`; scoped styles use `.series-map__item` and `.series-map__thumbnail` in `assets/_custom.scss`.

- Use a 40 × 40px square thumbnail with `object-fit: cover`, a 1px gray border and 3px corner radius.
- Place it left of the existing numbered title link and vertically center the title.
- Read `image` and `alt` from the listed page. If its image is missing, keep the numbered link.
- Show no description, summary or metadata; keep row spacing consistent on desktop and mobile.

### D. Timeline — Visual Archive

Template: `layouts/shortcodes/visual-archive.html`

CSS selectors:

- `.visual-archive-card__image`
    
- `.visual-archive-card__image img`
    

Layout:

- Thumbnail on the left.
    
- Chronological entry content on the right.
    
- Preserve the existing timeline structure, date ordering and visual chronology.
    

Timeline has its own composition, but follows the same square format, border and corner-radius standard.

### E. Site Completion Matrix

Template: `layouts/shortcodes/site-completion-matrix.html`

CSS: `assets/_custom.scss`, scoped to `.site-completion-matrix__thumbnail` and its table cells.

The matrix uses an intentional compact variant at 40 × 40 CSS pixels so its dense status table remains easy to scan. It keeps the square crop, subtle 1px gray border and 3px corner radius. The shortcode reads each page's existing `image` and `alt` Front Matter values. Its image rule overrides the more specific article-image sizing rule only inside the matrix. A fixed 40px thumbnail frame and 64px image cell (including its cell padding) keep both tables aligned. It renders a thumbnail only when the image points to a file present under `static/`; absent or unresolved images leave a blank cell. If a valid image has no `alt` value, the image uses empty alternative text because the adjacent page title supplies the same row's label. When a page has no title, the matrix derives a readable label from its canonical URL path without dropping the row or changing its ordering.

This compact matrix variant is an exception for this table only. It does not change the established 8rem desktop and 5rem narrow-screen thumbnail sizes used by landing-page lists, category and tag lists, or the Timeline.

## 4. Data Requirements

For list thumbnails, use the existing page Front Matter fields:

```
image: "/images/example.webp"
alt: "Descriptive alternative text"
```

Requirements:

- The image path must resolve to an existing asset.
    
- `alt` must describe the meaningful visual content.
    
- Read the values from the relevant page's Front Matter; do not hardcode image paths in list templates.
    
- Preserve the existing content-selection and ordering logic.
    
- If a page has no image, handle that case without breaking the layout.
    

## 5. Implementation Rules

Before adding thumbnails to a new component:

1. Identify its template, partial or shortcode.
    
2. Reuse the existing thumbnail styling where appropriate.
    
3. Keep CSS scoped to the relevant component or shared thumbnail class.
    
4. Reset conflicting inherited image properties, including `float`, `width`, `height` and margins where necessary.
    
5. Do not introduce a new thumbnail size or visual variant without a clear technical reason.
    
6. Do not modify theme files or global article-image rules merely to style list thumbnails.
    

Keep image styling separate from layout composition: the thumbnail standard is shared, but each component controls its own placement.

## 6. Validation Checklist

Before publishing changes:

- Image paths resolve in the generated site.
    
- All thumbnails are square and retain the shared border and radius.
    
- Images and associated text are aligned correctly.
    
- Desktop and narrow-screen layouts work as intended.
    
- Missing images do not break list spacing.
    
- Existing ordering, metadata, links and navigation remain unchanged.
    
- Hugo builds succeed for all active languages.
    
- `git diff --check` passes.
    
- Unrelated components remain visually unchanged.
    

## 7. Reference Files

| Component                     | Implementation                                                                           |
| ----------------------------- | ---------------------------------------------------------------------------------------- |
| Landing-page lists            | `layouts/_partials/series-*-list.html`                                                   |
| Categories and tags           | `layouts/term.html`                                                                      |
| Shared site-local styling     | `assets/_custom.scss`                                                                    |
| Timeline — Visual Archive     | `layouts/shortcodes/visual-archive.html`                                                 |
| Site Completion Matrix        | `layouts/shortcodes/site-completion-matrix.html`; scoped styles in `assets/_custom.scss` |
| Hierarchical Child-Page Lists | `layouts/_shortcodes/section.html`                                                       |
| Series Map                    | `layouts/_partials/series-navigation.html`                                               |

**Core principle:** one thumbnail standard, multiple layout compositions. Reuse the established styling, render only immediate children at each level, and preserve each component's existing hierarchy and selection logic.
