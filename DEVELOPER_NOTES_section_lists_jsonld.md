# Developer Notes — Section Lists and JSON-LD

This document describes how automated section lists and their corresponding JSON-LD are generated on Pivtorak.Studio.

It defines the Front Matter requirements for section entries and the rules that must be preserved when adding or editing content.

## 1. Purpose

The section-list system automatically generates visible lists and matching Schema.org structured data for:

- Series & Projects
    
- Research
    
- Studio
    
- Tools
    
- Archive
    

The same content selection and ordering rules are used to generate the visible HTML list and its corresponding JSON-LD.

The item count is generated automatically. It must not be maintained as a separate manual value.

## 2. How the system works

The system has three main parts:

1. **Front Matter** defines which section entries belong to each list and, where applicable, their order.
    
2. **Hugo partials and shortcodes** select the entries and generate the visible lists, item counts, and JSON-LD.
    
3. **Section landing pages** call the appropriate shortcodes in their content and structured-data blocks.
    

The landing pages retain their author-written introductions, descriptions, and other explanatory content. Only the automated list and structured-data portions are generated.

### Rendering flow

1. Hugo reads the content and its Front Matter.
    
2. The relevant template selects pages using the appropriate `show_in_series_*` marker.
    
3. Entries are sorted according to the implemented ordering rules.
    
4. The visible list and JSON-LD are generated from the corresponding selection.
    
5. The item count reflects the generated list.
    

A successful Hugo build alone does not guarantee that the visible list and JSON-LD agree. Both outputs must be checked.

## 3. Front Matter for section entries

The `show_in_series_*` properties determine whether a section entry is included in a particular automated list.

Use the appropriate property for the destination list:

|Destination|Front Matter property|
|---|---|
|Series & Projects|`show_in_series_projects`|
|Research|`show_in_series_research`|
|Studio|`show_in_series_studio`|
|Tools|`show_in_series_tools`|
|Archive|`show_in_series_archive`|

The property must be a YAML boolean, not a string.

Correct:

```
show_in_series_research: true
```

Incorrect:

```
show_in_series_research: "true"
```

Incorrect:

```
show_in_series_research: "yes"
```

Only add the marker corresponding to the intended destination. A section can be included in multiple lists when that is intentional.

### Example: Research section

```
---
title: "Knowledge Base"
weight: 30
show_in_series_research: true
---
```

This example illustrates the relevant fields. Preserve the actual title, weight, identifiers, language metadata, and other required properties of the existing page.

The marker controls inclusion; the title supplies the visible name, and the weight participates in ordering where the implementation uses weight sorting.

## 4. Front Matter for a section landing page

The five landing pages are maintained separately for each active language:

```
content/{en,pt,ru,uk}/series-and-projects/_index.md
content/{en,pt,ru,uk}/research/_index.md
content/{en,pt,ru,uk}/studio/_index.md
content/{en,pt,ru,uk}/tools/_index.md
content/{en,pt,ru,uk}/archive/_index.md
```

Each landing page contains its own metadata and explanatory content. Its list, item count, and JSON-LD are generated using the corresponding shortcodes.

Do not manually maintain a second copy of the list inside the landing page's JSON-LD. Do not replace an automated count with a fixed number.

When editing a landing page, preserve its existing Front Matter and author-written text unless the task explicitly requires changing them.

## 5. Shortcodes and partials

The section landing pages use dedicated shortcodes for visible lists, item counts, and JSON-LD generation.

The principal visible-list shortcodes are:

```
series-projects-list
series-research-list
series-studio-list
series-tools-list
series-archive-list
```

The item-count shortcode is:

```
series-item-count
```

The JSON-LD helpers include section-specific generators, such as:

```
projects-jsonld-items
research-jsonld-items
archive-jsonld-items
studio-jsonld-items
tools-jsonld-items
```

The implementation is distributed between `layouts/_shortcodes/` and `layouts/_partials/`. Shortcodes provide the content-facing interface; partials contain reusable rendering logic.

Keep the selection rules consistent between the visible-list and JSON-LD implementations. When changing a filter, sorting rule, or URL-generation rule, review both outputs.

## 6. Ordering rules

Ordering is part of the output contract.

Where the implementation sorts entries by `weight`, use the intended numeric weight values. For multilingual content, keep corresponding section weights aligned when the same relative order is required across languages.

Do not assume that filenames, alphabetical order, or publication dates determine the list order.

When adding an entry, verify its position in the generated list rather than relying only on the Front Matter value.

## 7. JSON-LD and Schema.org

The landing pages expose structured data using JSON-LD, the JSON-based serialization format for structured data.

For a section represented as an ordered list, the relevant Schema.org structure is `ItemList`.

Its important properties include:

- `@context`: the Schema.org vocabulary.
    
- `@type`: the structured-data type, such as `ItemList`.
    
- `numberOfItems`: the automatically generated number of entries.
    
- `itemListElement`: the generated list of entries.
    
- `ListItem.position`: the position of an entry in the list.
    
- `ListItem.name`: the entry's displayed name.
    
- `ListItem.url`: the corresponding page URL.
    

The exact schema structure must follow the existing implementation on the relevant landing page.

### Required consistency

The following values must agree between the rendered HTML and JSON-LD:

1. Number of entries.
    
2. Entry names.
    
3. Entry order and positions.
    
4. Entry URLs.
    

Do not hard-code `numberOfItems` or duplicate a manually maintained array of entries when the corresponding generated shortcode is available.

Valid JSON is necessary, but it is not sufficient: the structured data must also describe the content actually displayed on the page.

## 8. Adding a new section entry

When adding a new Research, Studio, Tools, Archive, or Series & Projects entry:

1. Create or update the relevant section page.
    
2. Add the appropriate `show_in_series_*: true` property.
    
3. Set the title and any required metadata.
    
4. Set the appropriate weight if ordering is weight-based.
    
5. Add the marker to each language version that should include the entry.
    
6. Confirm that the intended landing page includes the new entry.
    
7. Confirm that the visible list and JSON-LD contain the same entry in the same position.
    
8. Rebuild the site and inspect the rendered output.
    

A page is not included merely because its filename or title suggests that it belongs to a section. The expected Front Matter marker must be present.

## 9. Verification checklist

Before committing changes to the section-list system:

- The appropriate `show_in_series_*` property is present.
    
- The property is a boolean `true`.
    
- Corresponding language versions have the correct marker.
    
- Titles and URLs are correct.
    
- Ordering is correct.
    
- `numberOfItems` matches the generated list.
    
- JSON-LD parses as valid JSON.
    
- Visible list entries and JSON-LD agree on count, names, positions, and URLs.
    
- The Hugo build succeeds.
    
- The affected landing pages render correctly.
    
- Git changes contain only the intended edits.
    

## 10. Maintenance rule

When changing the selection, ordering, count, URL, or JSON-LD generation logic, review all affected visible lists and their structured-data counterparts.

Test every affected active language. Do not assume that success in one language proves that all language versions are correct.

Keep this document synchronized with changes to the implementation. Document stable architecture and content requirements rather than the history of individual debugging sessions.