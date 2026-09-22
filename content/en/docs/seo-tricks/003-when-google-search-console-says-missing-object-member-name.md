---
id: seo-tricks-003-when-google-search-console-says-missing-object-member-name
language: en
translation_of: seo-tricks-003-when-google-search-console-says-missing-object-member-name
title: 003 When Google Search Console Says — Missing } or Object Member Name
description: "A real Google Search Console case: investigating and fixing a structured data parsing error caused by the way JSON-LD was placed after YAML front matter in Hugo Markdown files."
summary: Google Search Console reported that structured data could not be parsed because of a missing } or object member name. The investigation found the underlying issue in the separation between YAML front matter and JSON-LD, affecting 565 Markdown files.
event_date: 2026-09-22T18:00:00
publication_date: 2026-09-22T18:00:00
slug: when-google-search-console-says-missing-object-member-name
tags:
  - Google Search Console
  - structured data
  - JSON-LD
  - Hugo
  - SEO debugging
keywords:
  - Google Search Console structured data
  - missing object member name
  - JSON-LD parsing error
  - structured data parsing error
  - Hugo JSON-LD
categories:
  - SEO
  - Technical SEO
series: SEOTricks
series_index: 3
research_origin: Pivtorak.Studio
status: published
featured: true
image: /images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp
alt: Google Search Console confirming that a structured data parsing issue has been resolved
related:
  - /en/docs/seo-tricks/
  - /en/docs/timeline/
authors:
  - Anna Pivtorak
draft: false
canonical: https://pivtorak.studio/en/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/
toc: true
weight: 3
completion: 100
seo: true
distribution: true
search: indexed
search_intent: troubleshooting Google Search Console structured data parsing errors
article_type: SEO troubleshooting case study
primary_topic: Google Search Console structured data parsing
verification_model: Source → Build → Live
research_status: confirmed
technical_status: verified
lastmod: 2026-09-22T18:00:00
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "TechArticle",
  "headline": "003 When Google Search Console Says — Missing } or Object Member Name",
  "description": "A real Google Search Console case: investigating and fixing a structured data parsing error caused by the way JSON-LD was placed after YAML front matter in Hugo Markdown files.",
  "inLanguage": "en",
  "datePublished": "2026-09-22T18:00:00+01:00",
  "dateModified": "2026-09-22T18:00:00+01:00",
  "author": {
    "@type": "Person",
    "name": "Anna Pivtorak",
    "url": "https://pivtorak.studio/en/"
  },
  "publisher": {
    "@type": "Person",
    "name": "Anna Pivtorak"
  },
  "mainEntityOfPage": {
    "@type": "WebPage",
    "@id": "https://pivtorak.studio/en/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/"
  },
  "url": "https://pivtorak.studio/en/docs/seo-tricks/when-google-search-console-says-missing-object-member-name/",
  "image": "https://pivtorak.studio/images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp",
  "articleSection": "SEO Tricks",
  "keywords": [
    "Google Search Console structured data",
    "missing object member name",
    "JSON-LD parsing error",
    "structured data parsing error",
    "Hugo JSON-LD"
  ],
  "about": {
    "@type": "Thing",
    "name": "Google Search Console structured data parsing"
  },
  "isPartOf": {
    "@type": "CreativeWorkSeries",
    "name": "SEO Tricks",
    "url": "https://pivtorak.studio/en/docs/seo-tricks/"
  }
}
</script>


![_SEO Tricks. When Google Search Console Says: Missing `}` or Object Member Name. AP | Pivtorak.Studio. 22.09.2026_ © Anna Pivtorak (Kostyuk)](/images/seo-tricks-003-when-google-search-console-says-missing-object-member-name.webp)

# When Google Search Console Says: Missing `}` or Object Member Name | SEO Tricks

_One missing character can make perfectly valid-looking structured data invisible to the parser._

## Quick Summary Box

> **Google Search Console reported:**  
> **Issue:** Structured data cannot be parsed  
> **Specific error:** Missing `}` or object member name

The problem was caused by the way JSON-LD was placed immediately after the YAML front matter in Markdown files. A missing blank line caused the generated content to be parsed incorrectly.

We checked the affected source files, corrected the formatting, verified that the accidental encoding damage introduced during the repair was fully restored, rebuilt the site successfully, and deployed the fix. Google Search Console later confirmed that the issue had been resolved.

## The Question

What caused Google Search Console to report that the structured data on the site could not be parsed?

The specific error was:

> **Missing `}` or object member name**

We needed to determine whether the problem was in the JSON-LD itself, in the Hugo templates generating it, or in the way the JSON-LD was placed in the Markdown source files.

## Why It Matters

Structured data helps search engines understand the meaning and structure of a page. If the JSON-LD cannot be parsed, that structured data cannot be reliably processed.

This does **not** automatically mean that the page cannot be crawled or indexed, or that its ranking will be affected. The important issue here is more specific: **the structured data itself may not be available to search engines in the form in which it was intended.**

That makes a parsing error worth fixing, especially when the same source pattern affects many pages across a site.

## The Check

We started by checking the actual source files rather than assuming that the JSON-LD itself was malformed.

The investigation covered four levels:

1. **The Google Search Console report** — to identify the exact problem and error message.  
2. **Hugo templates** — to see where structured data was generated and whether the JSON-LD syntax was being altered during page generation.  
3. **Markdown source files** — to check how the JSON-LD `<script>` blocks were placed relative to the YAML front matter.  
4. **Generated HTML** — to compare the source structure with what Hugo actually produced.  

A search through the site content revealed **565 Markdown files** in which the closing YAML front matter delimiter was immediately followed by the JSON-LD `<script>` block, without a blank line:

```text
---
<script type="application/ld+json">
```

We then tested the same structure after inserting a blank line:

```text
---

<script type="application/ld+json">
```

The generated HTML was checked for the structured-data script and for the presence of escaped JSON characters such as `&quot;`.

The check showed that the formatting change was sufficient to produce correctly separated front matter and JSON-LD in the generated output.

## What We Found

The investigation revealed that the JSON-LD itself was not the problem.

### What we expected

Each Markdown file had a normal YAML front matter block followed by a JSON-LD `<script>` block. Once Hugo processed the Markdown, the structured data should appear as a separate script in the generated HTML.

### What we observed

In **565 Markdown files**, the closing YAML front matter delimiter was immediately followed by the JSON-LD block:

```text
---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

There was no blank line between the end of the front matter and the HTML `<script>` element.

This pattern was repeated across the affected files, so the issue was not an isolated malformed JSON object.

### What the evidence showed

We tested the same content after adding a single blank line:

```text
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

After rebuilding the site with Hugo, the generated HTML contained the JSON-LD as a separate `application/ld+json` script.

For the test page, the structured-data check returned:

```text
application/ld+json: 1 of 1
&quot;: No results
```

This was significant because it showed that the JSON-LD was reaching the generated HTML in the expected form rather than being incorrectly combined with the preceding front matter.

### What caused the problem

The cause was therefore **not a missing `}` inside the JSON-LD object**.

The underlying problem was the **lack of separation between the YAML front matter and the following JSON-LD `<script>` block in the Markdown source**.

Because the same source pattern occurred in 565 files, the problem had the potential to affect structured data across a large part of the site.

The investigation also revealed an important practical lesson: when a search engine reports a JSON parsing error, the visible error message does not necessarily identify the actual source of the problem. In this case, the reported missing `}` pointed toward the JSON object, but the evidence showed that the problem was in the **boundary between the Markdown front matter and the JSON-LD block**.

## The Fix

The fix was deliberately small: **add one blank line between the closing YAML front matter delimiter and the JSON-LD `<script>` block in every affected Markdown file.**

### Before

```text
---
<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

### After

```text
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  ...
}
</script>
```

The affected files were located across the site's content directories. A total of **565 Markdown files** contained this exact source pattern.

Rather than editing the files individually, we performed the correction systematically across the affected files.

### An important complication

During the first mass-edit operation, the Windows PowerShell encoding handling introduced **UTF-8 mojibake** into the affected files. Characters such as:

```text
â€”
â€™
Â©
ðŸ...
```

appeared in place of the original Unicode characters.

We stopped the process, identified the encoding problem, and restored the affected files using the reverse CP1252/UTF-8 transformation. A subsequent verification found:

```text
Залишилося файлів із mojibake: 0
```

We then checked the Git diff to make sure that the intended content had not been altered. The final diff showed that the substantive change was the addition of **one blank line per affected file**.

### Final result

The correction produced:

```text
565 files changed, 565 insertions(+)
```

Hugo then built the site successfully.

After the source files were verified, the change was committed and pushed to GitHub:

```text
915f05fa Add spacing between front matter and JSON-LD
```

The important part of the fix was therefore not changing the JSON-LD objects themselves, but **separating the YAML front matter from the following JSON-LD block in the Markdown source.**

## Verification

The verification followed the full sequence:

**Source → Build → Live**

### Source

After the correction, we checked the affected Markdown files and the Git diff.

The final diff confirmed that the intended source change was limited to the addition of **one blank line** between the YAML front matter and the JSON-LD block in each affected file.

The 565 affected files were committed as:

```text
915f05fa Add spacing between front matter and JSON-LD
```

### Build

The site was rebuilt with Hugo after the correction.

The build completed successfully. The existing Hugo deprecation warnings remained, but they were unrelated to the structured-data problem and did not prevent the build.

We also verified that no mojibake remained after the encoding restoration:

```text
Files with remaining mojibake: 0
```

The corrected content was then pushed to GitHub:

```text
bde59e67..915f05fa  main -> main
```

### Live

The final and most important verification came from **Google Search Console itself**.

Google subsequently sent a confirmation stating that the problem had been resolved:

> **We confirmed that you fixed the issues: Structured data cannot be parsed.**

The specific error Google had previously reported was:

> **Missing `}` or object member name**

Google confirmed the fix for the page it had rechecked.

This is the highest level of verification available in this case: the source was corrected, the site built successfully, the corrected version was deployed, and **Google Search Console independently confirmed that the reported structured-data parsing problem had been resolved.**

### Result

**Source → corrected**  
**Build → successful**  
**Live → verified by Google Search Console** ✅

The important distinction is that the first two checks established that our correction worked technically; the final Google confirmation established that **the search engine accepted the corrected structured data on the live site.**

## Final Takeaway

The key lesson is simple: **when Google reports a structured-data parsing error, do not assume that the JSON-LD object itself is malformed. Check the entire path from source Markdown to generated HTML.**

In this case, one missing blank line between YAML front matter and a JSON-LD `<script>` block was enough to trigger a parsing problem across **565 files**. The fix was small, but finding the real cause required checking the source, the Hugo build, the generated HTML, and finally the live site through Google Search Console.

_Sometimes the error points to the JSON. The real problem may be just before it._

`Google Search Console` · `structured data` · `JSON-LD` · `Hugo` · `SEO debugging`

**Alt-text:**  
Google Search Console confirming that the structured-data parsing issue has been resolved on the live site.

_SEO Tricks. When Google Search Console Says: Missing `}` or Object Member Name. AP | Pivtorak.Studio. 22.09.2026_  
© Anna Pivtorak (Kostyuk)

