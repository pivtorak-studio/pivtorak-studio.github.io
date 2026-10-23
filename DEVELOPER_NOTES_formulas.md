# Developer Notes: Mathematical Formulas

## Purpose

Use this document whenever creating or editing calculator pages,
converters, templates, educational articles, or other content that
contains mathematical formulas on Pivtorak.Studio.

The goal is to make formulas mathematically correct, visually clear,
pleasant to read, and consistent with the site's existing rendering
implementation.

## 1. Inspect the Existing Implementation First

-   Reuse the site's existing KaTeX setup and established markup
    conventions.
-   Before changing formula syntax or rendering behavior, inspect the
    current Hugo configuration, relevant templates/shortcodes, and a
    successfully rendered formula on the site.
-   Do not add another math-rendering library, duplicate KaTeX
    initialization, or change global configuration when the existing
    implementation is sufficient.
-   Treat the currently working English Jewelry Calculator articles as
    visual references for well-formatted equations.

## 2. Choose the Appropriate Math Delimiters

The site uses KaTeX auto-render. Use the delimiters that have been
verified to work with the site's Hugo/Goldmark pipeline:

-   Inline mathematics: `$...$`
-   Display mathematics: `$$...$$`

Use inline math for short expressions within a sentence, such as
`$m = \rho V$`.

Use display math for important equations, multi-step calculations,
equations with fractions, or formulas that benefit from their own visual
space:

``` markdown
$$
m = \rho V
$$
```

**Important Markdown/Goldmark compatibility rule:** In the current site
pipeline, Goldmark strips the backslashes from `\(...\)` and `\[...\]`
in affected Markdown contexts. Do not use these delimiters for new or
edited Markdown formulas unless a specific test proves they survive the
actual rendering pipeline correctly.

Do not assume that TeX source in a Markdown file will render correctly
just because the source looks valid. Check the generated HTML or
rendered page.

## 3. Format Equations for Readability

-   Prefer standard mathematical notation over prose-like strings
    containing underscores, slashes, and unformatted operators.
-   Use proper fractions, subscripts, superscripts, Greek letters,
    multiplication signs, summations, and units where they improve
    clarity.
-   Keep equations centered and visually separated when they are the
    main point of a section.
-   Use aligned multi-line equations for derivations or worked
    calculations with several steps.
-   Break long calculations into meaningful intermediate steps rather
    than forcing one extremely wide line.
-   Keep related equations together, but avoid combining unrelated
    formulas into one crowded display.
-   Use explanatory prose before or after an equation to identify what
    it calculates and how to interpret it.
-   Do not add decorative complexity where a short inline formula is
    already clear.

Example:

``` markdown
$$
\begin{aligned}
m_f &= m_g \frac{F}{1000} \\
P_g &= \frac{P_u}{B_u} \\
V_r &= m_f P_g
\end{aligned}
$$
```

This example illustrates presentation only. Choose variables and
relationships appropriate to the actual subject; never copy example
equations as a substitute for the correct model.

## 4. Preserve Mathematical Meaning Exactly

Formatting is not permission to change the calculation.

When improving or translating an existing formula, preserve:

-   the mathematical relationship and operation order;
-   all variables and their definitions;
-   coefficients, constants, conversion factors, and precision;
-   units and unit conversions;
-   assumptions, boundary conditions, and rounding rules;
-   the numerical results of worked examples.

Do not silently simplify, rearrange, approximate, normalize, or
"correct" a formula if that could alter its meaning or interpretation.
If a genuine mathematical error is suspected, report it separately and
ask for authorization before changing the calculation.

Check worked examples against the original formula. A visually
attractive equation with a changed value is a failure.

## 5. Multilingual Content

-   Apply the same mathematical presentation standard to every available
    language version: EN, PT (European Portuguese), RU, and UK.
-   Identify translations using the repository's actual filenames,
    paths, and `translationKey` conventions; do not guess file paths.
-   Keep formulas mathematically equivalent across translations, even
    when surrounding prose and decimal formatting differ by locale.
-   Translate explanatory prose and variable descriptions appropriately,
    but do not translate or rename mathematical symbols without a clear
    reason.
-   Check each language's generated page. Successful rendering in
    English does not prove that formulas render in PT, RU, or UK.

## 6. Multi-Line Equations and Markdown Escaping

Goldmark may process TeX backslashes before KaTeX receives the source.

-   For aligned equations, use TeX environments supported by the site's
    KaTeX version, such as `aligned`, when appropriate.
-   In Markdown source, escape row-break backslashes when necessary so
    that the generated HTML passes the intended TeX `\\` row break to
    KaTeX. The required escaping must be confirmed in generated output;
    do not rely on visual inspection of the Markdown source alone.
-   Verify that each intended equation line remains separate and aligned
    after rendering.
-   If line breaks fail, inspect the generated HTML first. Do not
    repeatedly alter delimiters or rebuild the whole site without
    identifying the cause.

## 7. Formula Previews, Summaries, and Front Matter

Formula previews in section indexes, cards, summaries, or Front Matter
are separate rendering contexts from formulas inside article Markdown.

-   Inspect how the preview is sourced and rendered before editing it.
-   Use the existing KaTeX implementation where supported by that
    context.
-   If a template or shortcode outputs formula metadata as plain text,
    fix the relevant presentation layer or source field narrowly; do not
    assume that formatting the article body will fix the preview.
-   Do not add formula previews to pages where they are inappropriate.
-   Keep Front Matter data types and the expected template contract
    unchanged unless the task explicitly requires a change.

## 8. Scope Protection

When asked to improve formula presentation only:

-   Do not change calculator or converter logic, JavaScript, inputs,
    outputs, validation, or calculations.
-   Do not modify CSS, templates, shortcodes, Front Matter, JSON-LD,
    article prose, or unrelated files unless the task specifically
    requires a change to the formula-rendering presentation layer.
-   If a shared template or shortcode must be changed to fix a formula
    preview, make the smallest targeted change and check all affected
    pages.
-   Preserve existing successful formula formatting. Do not rewrite
    already-correct formulas merely for consistency of editing.

## 9. Validation Checklist

Before finishing, verify the relevant items:

-   [ ] Formula delimiters survive the Hugo/Goldmark pipeline and render
    through the existing KaTeX setup.
-   [ ] Inline and display formulas are visually distinct where
    appropriate.
-   [ ] Fractions, subscripts, superscripts, symbols, units, and
    operators render correctly.
-   [ ] Multi-line equations retain their intended line breaks and
    alignment.
-   [ ] Long equations and worked examples do not cause unwanted
    horizontal page overflow, especially on mobile.
-   [ ] Mathematical meaning and every worked-example result match the
    source.
-   [ ] All available language versions have been checked individually.
-   [ ] Index/card previews have been checked separately from article
    bodies.
-   [ ] No unrelated content or calculator functionality has changed.
-   [ ] Hugo build and targeted checks have been run as appropriate;
    avoid an unnecessary full multilingual rebuild if existing output
    allows reliable targeted validation.
-   [ ] The final report lists modified files, checks performed, and any
    unresolved issues.

## 10. Reporting

When reporting completion, distinguish between:

-   source files edited;
-   generated HTML inspected;
-   pages visually checked in the browser;
-   build status;
-   mathematical correctness checks performed;
-   any checks not performed or issues still unresolved.

Do not claim that formulas render correctly in every language based only
on a successful build or a check of the English version.

## Related Developer Notes

This document complements the site's general developer instructions and
calculator conventions, including `DEVELOPER_NOTES.md` and
`DEVELOPER_NOTES_calculators.md`.

If the site's math-rendering implementation changes, update this
document to reflect the verified behavior of the current
Hugo/Goldmark/KaTeX pipeline.
