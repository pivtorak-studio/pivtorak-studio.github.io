# Front Matter generation rules

## Purpose and scope

Use this note when creating or translating Hugo content for Pivtorak.Studio. Front Matter is page-type-specific: do not copy the large metadata set of a research article onto a landing page or visual work without evidence. Hugo configuration, templates, shortcodes, and established content contracts determine whether a field is used.

Production languages are Ukrainian (`uk`, files under `content/uk`), English (`en`), and European Portuguese (`pt`). Russian files exist, but `ru` is disabled in `hugo.toml`; do not imply that a Russian page is currently part of the production language set. Keep RU metadata coherent if specifically asked to prepare that content.

## Universal rules

- Include a localized `title` for every page and a useful localized `description` for pages intended for discovery. The head emits the page description from Hugo's `.Description` or summary fallback.
- Use YAML values of the correct type: dates as date/date-time values, `weight` and `series_index` as numbers, feature flags as booleans, and one series identifier as a scalar string. Lists such as `tags`, `keywords`, `categories`, `authors`, and `related` are YAML sequences.
- Quote text containing YAML-sensitive punctuation where needed. Avoid zero-padded numeric YAML values (`weight: 08`, `series_index: 02`) and quoted numbers; numeric sorting/formatting expects numbers.
- Hugo generates the canonical link in the active head from `.Permalink`. The legacy `canonical` Front Matter field is present in archived content but is not read by the active templates. When extending a content family whose existing pages carry that field, retain it and keep it aligned with the actual permalink for compatibility with that family's metadata convention; do not add it to new content by default or expect it to override the head-generated canonical. Use Hugo's URL fields such as `slug` or `url` only when intentionally changing the generated page URL.
- For future scheduled publication, use explicit Portugal-local UTC offsets in date-time fields; calculate the applicable seasonal offset for that date. Keep `event_date` distinct when the event and publication occur at different times. See `DEVELOPER_NOTES_publication_dates.md`.
- Do not add metadata fields for SEO merely because they sound useful. A field only affects behavior where a template, shortcode, or workflow reads it.

## Required by content type

| Content type | Required / established metadata |
|---|---|
| Ordinary article or individual work | `title`; `date` where publication ordering/scheduling matters. Use `description`, `image`/`alt`, `series` and `series_index` where relevant to its list, display, or content relationship. |
| Series or project landing page | Localized `title` and `description`; `series` scalar and `series_index: 0` where it participates in Series Map; `weight` when menu/list ordering uses it; `show_in_series_projects: true` only when it belongs in that automated list. A page with a hand-maintained JSON-LD block needs its own correct localized values there. |
| Research / Studio / Tools / Archive section entry | Localized `title`; the matching boolean `show_in_series_research`, `_studio`, `_tools`, or `_archive`; `weight` when ordering is weight-based. `image` and `alt` support list thumbnails. Do not set unrelated inclusion markers. |
| Timeline page | Follow the existing localized `docs/timeline/_index.md` pattern: `series: Timeline`, numeric `series_index: 0`, image and alt, dates, and `show_in_series_archive: true`. Its hand-authored CollectionPage JSON-LD is not generated from these fields. |
| Site homepage | Language root `_index.md` has localized title/description and image/alt conventions. The shared person/organization/website graph is emitted only on the English homepage by `layouts/_partials/schema.html`. |

“Required” above means required by an existing project workflow or feature when that type uses it; the Hugo templates do not enforce one universal Front Matter schema.

## Conditional and optional fields

- Hugo links translations by matching paths and base filenames within configured language content directories. Its built-in `translationKey` Front Matter field provides an alternate linking key: pages with the same value are linked as translations even when their content paths or filenames differ. Use it when the real content structure needs that alternate association, and follow existing family conventions; do not add it universally. Project fields such as `translation_of`, `id`, and `language` may be kept where the content family or a project workflow uses them, but they do not replace Hugo's linking mechanisms. Current templates inspected here do not consume those project fields.
- `series` is the exact internal scalar identifier consumed by the Series Map and section shortcode. Preserve its spelling across translations; translate the visible title, not the identifier. `series_index` is numeric and used for ordering/zero-padded display. Section/series landing pages commonly use `0`; numbered works use positive sequence values. `series_page` and `series_title` are conditional navigation overrides used by `series-navigation.html`.
- `show_in_series_*` values are YAML booleans. They control generated section lists; list counts and list JSON-LD are generated from selection and must not be entered manually.
- `date`, `publication_date`, `event_date`, and `lastmod` have distinct meanings. `date` is Hugo's built-in content date and can affect publication behavior; `lastmod` is also a built-in Hugo page date, populated from Front Matter under Hugo's default configuration. This project does not configure custom Front Matter date resolution, and the active rendering templates do not read `.Lastmod`; the publication-dates note's instruction to update `lastmod` on edits is an editorial convention, not site automation. `publication_date` feeds the completion matrix and Timeline sorting; `event_date` is project metadata for the represented event. Only set dates when supported by the content/workflow.
- `image` is normally a site-root path such as `/images/work.webp`; `alt` is localized descriptive text. The head's social image output uses `image`; section list cards and visual archive use `image` and `alt`.
- `authors` is commonly a sequence (often `- Anna Pivtorak`) in content. It does not by itself create JSON-LD author markup. The reusable JSON-LD author reference is a shortcode.
- Research/analysis records may use fields such as `knowledge_type`, `disciplines`, `analysis_methods`, `research_status`, `search`, `seo`, and `distribution`. These support specialized records/matrices; add them only when the content type and the relevant workflow call for them. `search` values such as `pending`, `submitted`, and `indexed` are status claims, not SEO instructions; never claim indexing without evidence.
- `keywords`, `tags`, and `categories` are distinct taxonomies/metadata. Use localized, relevant values in sequences only where appropriate; they are not interchangeable and are not all automatically rendered as schema properties.
- `draft`, `toc`, `featured`, `timeline`, `archive`, `visual_archive`, `status`, and `completion` are workflow/display flags or data for particular page families. Do not copy indiscriminately.

## Multilingual and URL rules

- Localize title, description, summary, alt text, tags/keywords/categories and embedded structured-data text. Preserve technical IDs, series identifiers, and shared content meaning.
- Follow the established content directory and matching basename for translations where the project uses Hugo's path-based association. If translations have different paths or filenames, use the same Hugo `translationKey` on each counterpart when needed to associate them. Localized slugs can differ when the corresponding actual path/URL and links are intentionally different.
- The active head creates a canonical from the Hugo page permalink and emits translation alternates from `.AllTranslations`. Do not add manual canonical or `hreflang` tags in Markdown to duplicate this behavior.
- If content includes a JSON-LD script, its URL and `@id` must match that language page's actual permalink (subject to a deliberate stable entity ID), not a guessed slug.
- The site config calls the Ukrainian language code `uk` (display label UA); use `uk` in language metadata and structured data. Portuguese is `pt`; English `en`; Russian `ru` only for requested, disabled-language material.

## Generation checklist

1. Identify the page type and inspect a current sibling in the same content family and language.
2. Check the relevant templates/shortcodes and notes: `DEVELOPER_NOTES_series_map.md`, `DEVELOPER_NOTES_section_lists_jsonld.md`, `DEVELOPER_NOTES_menu_groups.md`, and `DEVELOPER_NOTES_publication_dates.md`.
3. Include only fields consumed or required for that page type; preserve exact scalar/sequence/number/boolean types.
4. Check counterpart language files for shared identifiers and localized text. Remember RU is disabled in the current config.
5. Verify image paths, links, dates, weights and series ordering against real files. Run Hugo and inspect generated URLs/list output when implementation changes or correctness depends on rendering.

## Evidence and known limitation

The active head is `layouts/_partials/docs/html-head.html`; the page layout is `layouts/baseof.html`. Relevant consumers include `layouts/_partials/series-navigation.html`, `layouts/_shortcodes/section.html`, visual archive/list partials, and `layouts/shortcodes/site-completion-matrix.html`. `DEVELOPER_NOTES.md` contains stale language and SEO statements (for example claiming RU indexing can be enabled by only uncommenting config); check current `hugo.toml` and templates instead. The active head does not read the legacy `canonical` param, and project fields `language` and `translation_of` were not found in active template consumers. Hugo itself recognizes `translationKey` for translation association, and recognizes `lastmod` as a built-in page date; those are Hugo semantics rather than project custom template behavior.
