# Pivtorak.Studio — Schema Architecture & New Page Workflow

## 1. Purpose

This document describes the current architecture for author identity, publisher identity, multilingual page relationships, and Schema.org structured data on Pivtorak.Studio.

It defines the standard workflow for creating and publishing new pages without duplicating existing infrastructure.

The rules apply to active production languages:

- Ukrainian (`uk`)
    
- English (`en`)
    
- European Portuguese (`pt`)
    

Russian (`ru`) remains disabled in the production Hugo configuration.

## 2. Central entities

### Author: Person

The site's central author entity is defined through:

- `data/seo/author.yaml`
    
- `layouts/_partials/schema.html`
    

Canonical entity identifier:

`https://pivtorak.studio/en/#person`

Content pages should reference this entity rather than create a new, incomplete `Person` definition for the same author.

The existing shortcode `schema-author-reference` provides a reusable reference mechanism for Schema.org markup. Follow its established implementation and usage examples.

### Publisher: Organization

The central publisher entity is defined through:

- `data/seo/organization.yaml`
    
- `layouts/_partials/schema.html`
    

Canonical entity identifier:

`https://pivtorak.studio/en/#organization`

When Pivtorak.Studio is the publisher, content pages should reference this entity using the existing `schema-organization-reference` shortcode.

Do not create a separate embedded `Organization` definition for Pivtorak.Studio when the central reference is appropriate.

### Website: WebSite

The central `WebSite` entity is defined in the JSON-LD graph generated for the English homepage.

Canonical entity identifier:

`https://pivtorak.studio/en/#website`

References to the website entity must use the identifier actually defined by the central graph. Do not derive a different identifier from the current language prefix.

## 3. Active Schema.org infrastructure

The current implementation uses:

- `data/seo/author.yaml` — shared author data.
    
- `data/seo/organization.yaml` — shared publisher data.
    
- `layouts/_partials/schema.html` — central JSON-LD graph.
    
- `layouts/_shortcodes/schema-author-reference.html` — reusable author reference.
    
- `layouts/_shortcodes/schema-organization-reference.html` — reusable publisher reference.
    
- `layouts/_partials/docs/html-head.html` — active document head, including metadata, canonical URLs, language alternatives, and schema integrations.
    

The central graph and reference shortcodes have different responsibilities: the graph defines shared entities; reference shortcodes connect individual content to those entities.

Before introducing another Schema.org partial or shortcode, inspect the existing implementation and reuse it whenever possible.

## 4. Creating a new page

### Step 1 — Create the content

Create the Markdown file in the appropriate language directory and content section.

Use the established Front Matter conventions for the relevant page type.

Provide accurate, localized values for:

- `title`
    
- `date`, where applicable
    
- `description`
    
- `summary`, where applicable
    
- `image` and `alt`, where applicable
    
- `tags`, `keywords`, and other fields required by the relevant content type
    

Preserve the site's existing URL and multilingual conventions.

Do not add new Front Matter fields solely because they sound useful for SEO. A field affects generated output only when the relevant templates or code use it.

### Step 2 — Connect the author and publisher

When the page's structured data identifies Anna Pivtorak as its author, use the existing author reference.

When Pivtorak.Studio is the publisher, use the existing organization reference.

Do not create a separate author identity for each language.

Do not assume that fields such as `author`, `authors`, `seo`, or `search` automatically generate Schema.org markup. Inspect the active templates and follow an existing working example.

### Step 3 — Choose the appropriate page type

Use Schema.org types that reflect the actual purpose and content of the page.

Examples include:

- `Article` for an article;
    
- `CollectionPage` for a page whose primary purpose is to present a collection;
    
- `CreativeWorkSeries` for a series of related creative or editorial works;
    
- `Person` and `Organization` for the corresponding entities.
    

Do not add properties merely to make the graph appear more detailed.

Use `mainEntityOfPage`, `isPartOf`, and `hasPart` when they accurately describe the real relationships.

For a series landing page, include `hasPart` only for actual, relevant component works. For an article belonging to a series, represent that relationship consistently with the established schema implementation.

### Step 4 — Connect translations

For translations of the same content, preserve the established multilingual structure and use the same internal series identifier where applicable.

Translate visible titles, descriptions, and other language-specific content. Do not translate technical identifiers such as the value of `series`.

Ensure that each published language version has the correct URL and canonical.

The active head template generates `hreflang` alternatives from Hugo's `.AllTranslations`, including the current page and available translations.

Do not add manual `hreflang` tags to individual Markdown files unless the existing architecture specifically requires them.

## 5. Creating a new series

When creating a new series:

1. Establish a stable internal series identifier.
    
2. Create the required localized landing pages.
    
3. Use the established series Front Matter and navigation conventions.
    
4. Give each language version its own localized URL, title, description, and appropriate structured data.
    
5. Use a consistent series entity identifier across translations when the pages represent the same series.
    
6. Connect published articles to the series using the established internal series field and appropriate Schema.org relationships.
    
7. Generate component lists from actual content when the existing architecture supports this reliably.
    

Do not invent child articles, URLs, or relationships for works that have not been published.

A series landing page does not need artificial components merely to populate `hasPart`.

## 6. Validation before publication

After creating a page or modifying shared schema infrastructure, run a Hugo build.

Check the generated HTML rather than relying on Front Matter alone.

Verify:

- the expected page URL is generated;
    
- the HTML language attribute is correct;
    
- canonical points to the intended localized URL;
    
- `hreflang` contains the current page and the relevant published translations;
    
- the author reference uses the central `Person` ID;
    
- the publisher reference uses the central `Organization` ID where applicable;
    
- JSON-LD parses correctly;
    
- no conflicting entity definitions were introduced;
    
- no unintended `noindex` directive is present;
    
- the page appears in the appropriate sitemap;
    
- all internal links point to valid pages.
    

Run `git diff --check` and review the final diff before committing.

For changes to shared templates, validate representative pages across all active languages and relevant content types.

## 7. Publication and post-publication checks

Use the repository's established GitHub workflow.

After deployment, verify the live HTML for representative pages and confirm that the deployed output matches the intended build.

For new or materially changed pages, Google Search Console can subsequently be used to inspect discovery, crawling, indexing, and canonical selection.

Keep these outcomes separate:

- a successful Hugo build confirms that the site can be generated;
    
- a successful deployment confirms that the release was published;
    
- valid JSON-LD confirms that the generated structured data can be parsed;
    
- none of these alone confirms that Google has indexed the page or will display it in search results.
    

Do not change internal search-status fields to claim that Google has indexed a page. Record actual indexing observations separately.

## 8. Maintenance principles

- Prefer shared templates and data over duplicated definitions.
    
- Preserve stable entity identifiers.
    
- Keep localized content and technical identity consistent.
    
- Model only relationships supported by actual content.
    
- Avoid unnecessary new files, metadata fields, and structural pages.
    
- Validate generated output before publishing.
    
- Treat indexing and search visibility as observed outcomes, not guaranteed effects of structured data.
    

This document describes the current implementation and the standard workflow for extending it. If the implementation changes, update this document to reflect the verified architecture.