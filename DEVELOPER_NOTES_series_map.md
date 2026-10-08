# Developer Notes — Series Map

This document describes how the custom Series Map works on Pivtorak.Studio and defines the Front Matter requirements that must be preserved when creating or editing series articles.

The purpose of this document is to prevent silent failures where an article is published correctly but does not appear in the Series Map.

---

## 1. Purpose

The Series Map is a navigation component that collects articles belonging to the same series and presents them as a sequence.

For example, articles in the `PeacefulLife` series are connected through the Front Matter property:

```yaml
series: PeacefulLife
```

The Series Map uses this value to determine which pages belong to the series.

The filename, article number, or visible title alone does not establish series membership.

---

## 2. The Critical Front Matter Property

The most important property for Series Map membership is:

```
series: PeacefulLife
```

### Required type

`series` must be a **string (scalar value)**.

Correct:

```
series: PeacefulLife
```

Also valid as a string:

```
series: "PeacefulLife"
```

The project standard is to use the unquoted form:

```
series: PeacefulLife
```

---

## 3. DO NOT use an array

The following format must NOT be used for pages that are expected to appear in the Series Map:

```
series:
  - PeacefulLife
```

or:

```
series: [PeacefulLife]
```

These values are YAML arrays/lists, not strings.

Even though they may look semantically equivalent to a human reader, they have a different data type.

The custom Series Map expects the series value in string form.

### Important historical example

The first 15 `Peaceful Life` articles originally contained:

```
series:
  - PeacefulLife
```

while later articles used:

```
series: PeacefulLife
```

As a result, articles 001–015 were not included in the Series Map even though they clearly belonged to the same series.

Changing the property to:

```
series: PeacefulLife
```

restored the complete Series Map.

---

## 4. How Series Map Determines Membership

Conceptually, the Series Map works like this:

1. Hugo builds the site's regular content pages.
2. The Series Map obtains the series value associated with the current article.
3. It searches for other pages whose `series` Front Matter value matches that series.
4. Matching pages are collected into the Series Map.
5. Each entry links to the corresponding article page.

Therefore:

```
series: PeacefulLife
```

is the connection between an article and the `PeacefulLife` series.

The Series Map is therefore **data-driven by Front Matter**, not by filenames alone.

---

## 5. Front Matter contract

For a normal article that must appear in a Series Map, the following distinction should be maintained.

|Property|Required for Series Map|Expected type|Purpose|
|---|---|---|---|
|`series`|YES|string|Connects the article to a series|
|`title`|YES for reliable display|string|Article title displayed by Hugo / navigation|
|`date`|NO for membership|date|Publication/date metadata; may affect ordering elsewhere|
|`id`|NO for membership|string|Stable article identifier used by the site's broader content system|
|`slug`|NO|string|Optional URL control|
|`weight`|NO|integer|Optional Hugo ordering mechanism where explicitly used|
|`tags`|NO|array|Search / taxonomy metadata|
|`keywords`|NO|array|SEO metadata|
|`description`|NO|string|SEO / page description|
|`image`|NO|string|Article image / metadata|
|`draft`|NO|boolean|Hugo publication state|

### The critical rule

Of these properties, **`series` is the property that establishes Series Map membership.**

Other Front Matter fields should not be assumed to substitute for it.

---

## 6. Multilingual content

Pivtorak.Studio contains multilingual versions of the same articles.

Each language version should explicitly contain the appropriate `series` value.

For example:

### English

```
series: PeacefulLife
```

### Portuguese

```
series: PeacefulLife
```

### Russian

```
series: PeacefulLife
```

### Ukrainian

```
series: PeacefulLife
```

The series identifier should remain consistent across translations.

The visible article title may of course be translated, but the internal series identifier should not be translated.

For example, do not use:

```
series: VidaPacífica
```

in Portuguese if the canonical series identifier is:

```
series: PeacefulLife
```

---

## 7. Series identifier is a technical value

The value of `series` should be treated as an internal identifier, not as display text.

For example:

```
series: PeacefulLife
```

is a technical identifier.

The visible localized name of the series can be handled separately by the site's content and navigation system.

This makes multilingual versions consistent and prevents accidental creation of separate series.

---

## 8. Article numbering

Article numbering is useful for human organization and visual ordering.

Examples:

```
001
002
003
...
015
016
...
042
```

However, the number in the filename or title is not what establishes Series Map membership.

For example:

```
peaceful-life-003-the-right-to-work.md
```

does not automatically make the page part of `PeacefulLife`.

The page must still contain:

```
series: PeacefulLife
```

---

## 9. Recommended Front Matter pattern

A typical article in a series should follow the project's established Front Matter structure.

Example:

```
---
title: "003 The Right to Work"
date: 2024-...
id: "..."
series: PeacefulLife
tags: [...]
keywords: [...]
description: "..."
image: "..."
---
```

The exact additional fields may vary between articles.

The important Series Map requirement is:

```
series: PeacefulLife
```

with `series` represented as a scalar string.

---

## 10. Common mistakes

### Mistake 1 — Using an array

Incorrect:

```
series:
  - PeacefulLife
```

Correct:

```
series: PeacefulLife
```

---

### Mistake 2 — Using an inline array

Incorrect:

```
series: [PeacefulLife]
```

Correct:

```
series: PeacefulLife
```

---

### Mistake 3 — Translating the series identifier

Incorrect:

```
series: VidaPacífica
```

Correct:

```
series: PeacefulLife
```

---

### Mistake 4 — Relying on the filename

This is not sufficient:

```
peaceful-life-043-new-article.md
```

The article still needs:

```
series: PeacefulLife
```

---

### Mistake 5 — Assuming Hugo will infer series membership

Hugo does not infer the custom Series Map relationship simply because:

- the file is inside `content/.../peaceful-life/`;
- the filename starts with `peaceful-life-`;
- the title contains "Peaceful Life";
- the article number follows the existing sequence.

Series membership must be explicitly declared.

---

## 11. Debugging a missing article

If an article is visible on the website but missing from the Series Map, check the Front Matter first.

### Step 1 — Check that `series` exists

```
series: PeacefulLife
```

### Step 2 — Check its type

It must be a string/scalar.

Look for accidental:

```
series:
  - PeacefulLife
```

or:

```
series: [PeacefulLife]
```

### Step 3 — Check the exact value

The identifier must match exactly:

```
series: PeacefulLife
```

Do not introduce:

```
series: peacefullife
```

```
series: Peaceful Life
```

```
series: Peaceful-Life
```

unless the Series Map is intentionally changed to use that identifier.

### Step 4 — Check the translated versions

If the site is multilingual, verify the corresponding article in every language.

### Step 5 — Rebuild Hugo

Run:

```
hugo
```

A successful Hugo build does not necessarily mean that the Series Map data is correct, so the rendered Series Map should also be checked.

---

## 12. Verification checklist for a new series article

Before committing a new article that belongs to an existing series:

- [ ] `series` exists in Front Matter
- [ ] `series` is a scalar string
- [ ] The value exactly matches the existing series identifier
- [ ] The series identifier is not translated
- [ ] The article has a valid `title`
- [ ] The article has the expected multilingual counterpart(s)
- [ ] The article appears in the Series Map locally
- [ ] `hugo` completes successfully
- [ ] The rendered article and Series Map are visually checked
- [ ] Git diff contains only the intended changes

---

## 13. Peaceful Life reference

The canonical internal identifier for the Peaceful Life series is:

```
series: PeacefulLife
```

This exact value should be preserved for all language versions.

Current articles include:

```
PeacefulLife 001
PeacefulLife 002
PeacefulLife 003
...
PeacefulLife 042
```

The Series Map should include all articles whose Front Matter contains the matching scalar value.

---

## 14. Important lesson

The Series Map failure demonstrated an important Hugo/content-model principle:

> YAML data type matters.

These two values are not equivalent to the template:

```
series: PeacefulLife
```

and:

```
series:
  - PeacefulLife
```

The first is a string.

The second is an array.

A custom Hugo template may behave differently depending on the type, even when both values appear to represent the same information to a human reader.

Therefore, when a custom Hugo component depends on Front Matter, **the property name, value, and data type are all part of the project's content contract.**

---

## 15. Maintenance rule

If the Series Map implementation is changed in the future, update this document together with the implementation.

If the expected type or matching logic changes, the Front Matter contract described above must be reviewed before modifying existing articles.

Do not silently change:

```
series: PeacefulLife
```

to another structure without testing the complete multilingual Series Map.

---

## 16. Related developer notes

Other site-level implementation documentation is maintained in:

```
DEVELOPER_NOTES.md
DEVELOPER_NOTES_logo_favicon.md
DEVELOPER_NOTES_menu_groups.md
DEVELOPER_NOTES_robots.md
DEVELOPER_NOTES_top_area.md
DEVELOPER_NOTES_visual_archive.md
DEVELOPER_NOTES_series_map.md
```

The Series Map note should be treated as the reference document for the `series` Front Matter contract.

