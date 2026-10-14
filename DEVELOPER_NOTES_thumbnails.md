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

### B. Timeline — Visual Archive

Template: `layouts/shortcodes/visual-archive.html`

CSS selectors:

- `.visual-archive-card__image`
    
- `.visual-archive-card__image img`
    

Layout:

- Thumbnail on the left.
    
- Chronological entry content on the right.
    
- Preserve the existing timeline structure, date ordering and visual chronology.
    

Timeline has its own composition, but follows the same square format, border and corner-radius standard.

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

|Component|Implementation|
|---|---|
|Landing-page lists|`layouts/_partials/series-*-list.html`|
|Categories and tags|`layouts/term.html`|
|Shared site-local styling|`assets/_custom.scss`|
|Timeline — Visual Archive|`layouts/shortcodes/visual-archive.html`|

**Core principle:** one thumbnail standard, multiple layout compositions. Reuse the established styling and preserve each component's existing structure.