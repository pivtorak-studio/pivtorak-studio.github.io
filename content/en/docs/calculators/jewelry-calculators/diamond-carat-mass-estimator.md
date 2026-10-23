---
id: diamond-carat-mass-estimator
translationKey: diamond-carat-mass-estimator
language: en
title: Diamond Carat Mass Estimator
description: Estimate diamond carat mass from measured dimensions using documented, shape-specific empirical models.
summary: A manual dimensional estimate for round brilliant, oval, pear, marquise, emerald and heart diamonds, with model limits explained.
publication_date: 2026-10-21T06:00:00+01:00
date: 2026-10-21T06:00:00+01:00
lastmod: 2026-10-21T06:00:00+01:00
slug: diamond-carat-mass-estimator
tags:
  - calculator
  - diamond
  - carat mass
  - gemology
keywords:
  - diamond carat mass estimator
  - diamond mass by dimensions
  - diamond shape factor
categories:
  - Jewelry
  - Calculators
series: JewelryCalculators
series_index: 5
research_origin: Pivtorak.Studio
status: published
featured: false
image: /images/calculators-jewelry-calculators-diamond-carat-mass-estimator.webp
alt: Diamond dimensions and a calculator used to estimate carat mass.
related:
  - /en/docs/calculators/
  - /en/tools/
  - /en/docs/timeline/
  - /en/docs/the-movement-matrix/site-completion-matrix/
authors:
  - Anna Pivtorak
license: CC BY-NC-ND 4.0
timeline: true
tools: true
visual_archive: true
disciplines:
  - gemology
  - applied mathematics
  - jewelry
calculator_type: diamond-mass-estimator
calculator_model: shape-specific empirical dimensional estimates; see each model
calculator_units: "dimensions: mm; estimated mass: metric carats (ct)"
implementation_status: client-side
draft: false
toc: true
completion: 100
seo: true
distribution: true
search: indexed
canonical: https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/
event_date: 2026-10-21T06:00:00+01:00
translation_of: diamond-carat-mass-estimator
---

<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "WebPage",
      "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#webpage",
      "url": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/",
      "name": "Diamond Carat Mass Estimator",
      "description": "Estimate diamond carat mass from measured dimensions using documented, shape-specific empirical models.",
      "inLanguage": "en",
      "isPartOf": {
        "@id": "https://pivtorak.studio/#website"
      },
      "mainEntity": {
        "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#software"
      },
      "author": {
        "@id": "https://pivtorak.studio/#person"
      },
      "datePublished": "2026-10-21T06:00:00+01:00",
      "dateModified": "2026-10-21T06:00:00+01:00",
      "image": "https://pivtorak.studio/images/calculators-jewelry-calculators-diamond-carat-mass-estimator.webp",
      "breadcrumb": {
        "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#breadcrumb"
      },
      "workTranslation": [
        {
          "@id": "https://pivtorak.studio/pt/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#webpage"
        },
        {
          "@id": "https://pivtorak.studio/ru/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#webpage"
        },
        {
          "@id": "https://pivtorak.studio/uk/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#webpage"
        }
      ]
    },
    {
      "@type": "SoftwareApplication",
      "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#software",
      "name": "Diamond Carat Mass Estimator",
      "description": "A browser-based calculator for estimating the carat mass of round brilliant, oval, pear, marquise, emerald step-cut and heart-shaped diamonds from measured dimensions.",
      "applicationCategory": "UtilitiesApplication",
      "applicationSubCategory": "Gemological calculator",
      "operatingSystem": "Any",
      "inLanguage": "en",
      "isAccessibleForFree": true,
      "creator": {
        "@id": "https://pivtorak.studio/#person"
      },
      "url": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/"
    },
    {
      "@type": "BreadcrumbList",
      "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/#breadcrumb",
      "itemListElement": [
        {
          "@type": "ListItem",
          "position": 1,
          "name": "Home",
          "item": "https://pivtorak.studio/en/"
        },
        {
          "@type": "ListItem",
          "position": 2,
          "name": "Calculators",
          "item": "https://pivtorak.studio/en/docs/calculators/"
        },
        {
          "@type": "ListItem",
          "position": 3,
          "name": "Jewelry Calculators",
          "item": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/"
        },
        {
          "@type": "ListItem",
          "position": 4,
          "name": "Diamond Carat Mass Estimator",
          "item": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/diamond-carat-mass-estimator/"
        }
      ]
    }
  ]
}
</script>


# Diamond Carat Mass Estimator

![_Calculators. Jewelry Calculators. Diamond Carat Mass Estimator. AP | Pivtorak.Studio. 21.10.2026_ © Anna Pivtorak (Kostyuk)](/images/calculators-jewelry-calculators-diamond-carat-mass-estimator.webp)

Estimate a diamond's carat mass from measured dimensions when the loose stone cannot be weighed. These empirical models turn millimetre measurements into approximate mass in metric carats. Select a cut shape and enter the dimensions requested for that model. The result is a dimensional estimate, not a measurement, appraisal, market value or offer from Pivtorak.Studio.

One metric carat (ct) is exactly 0.2 g. Estimates are rounded to three decimal places. For round brilliant diamonds, enter the average of the minimum and maximum girdle diameters; for fancy shapes, enter length, width and total depth. Measure in millimetres with a suitable gauge. Input dimensions must be greater than 0 and no more than 100 mm. For non-round cuts, total depth must not exceed the larger face dimension.

{{< calculator type="diamond" >}}

## Calculation models and limitations

Each coefficient belongs to its stated shape model. Four fancy-shape models also require selecting a published reference length-to-width ratio. Compare that reference with the measured ratio shown in the result. The calculator does not interpolate between coefficient rows. It does not calculate an estimate when the measured ratio is outside the listed range. Girdle thickness, outline, facet pattern, pavilion geometry, culet and other proportions can still make a stone differ from its model. Weigh a loose diamond on a suitable calibrated balance to determine its mass.

### Round brilliant: average-diameter model

Use this model for a standard round brilliant when two girdle diameters are available. It squares their average and multiplies it by total depth and the round-brilliant coefficient.

**Formula:**

$$
m_{\mathrm{ct}}=D_a^2\times h\times k_r,\qquad k_r=0.0061
$$

- `m_ct`: estimated mass, in metric carats (ct).
- `D_a`: average girdle diameter, in millimetres (mm), entered as the mean of the minimum and maximum diameters.
- `h`: total depth, in mm.
- `k_r`: empirical round-brilliant coefficient, 0.0061.

Enter the already averaged diameter, not the two readings separately. This approximation does not correct for an unusually thick or thin girdle or atypical proportions. Do not use it for other outlines or gemstones.

**Worked example.** If $D_a=6.50\ \mathrm{mm}$ and $h=3.90\ \mathrm{mm}$:

**Worked calculation:**

$$
\begin{aligned}
6.50\ \mathrm{mm}\times6.50\ \mathrm{mm}&=42.25\ \mathrm{mm}^2,\\\\
42.25\ \mathrm{mm}^2\times3.90\ \mathrm{mm}&=164.775\ \mathrm{mm}^3,\\\\
164.775\ \mathrm{mm}^3\times0.0061\\\\
&=1.0051275\ \mathrm{ct},\\\\
&\approx1.005\ \mathrm{ct}
\end{aligned}
$$

The displayed value is rounded, not weighed. Sources: [GCAL instructional diamond grading](https://www.gcalusa.com/instructional-diamond-grading.html); [CISGEM diamond dimensions and mass](https://www.cisgem.com/gemmologia/diamante/le-4c).

### Oval brilliant: ratio-specific model

Use this for an oval brilliant. Multiply length, width and depth by the factor for the selected reference length-to-width ratio. Select the closest listed ratio and compare it with the measured ratio shown by the calculator.

**Formula:**

$$
m_{\mathrm{ct}}=L\times W\times h\times k_o(r),\qquad r=\frac{L}{W}
$$

| Reference ratio (r) | Factor `k_o(r)` |
|---:|---:|
| 1.25:1 | 0.00625 |
| 1.50:1 | 0.00640 |
| 2.00:1 | 0.00670 |

- `m_ct`: estimated mass, in ct.
- `L`: maximum outline length, in mm.
- `W`: maximum outline width, in mm.
- `h`: total depth, in mm.
- `r=L/W`: measured length-to-width ratio, dimensionless.
- `k_o(r)`: empirical oval factor for the selected reference ratio.

These are discrete models, not a continuous curve; no interpolation is performed. Girdle and profile differences are not corrected.

**Worked example.** For $L=7.00\ \mathrm{mm}$, $W=5.00\ \mathrm{mm}$, and $h=3.20\ \mathrm{mm}$, the measured ratio is 1.40:1. Using the 1.50:1 reference factor:

**Worked calculation:**

$$
\begin{aligned}
7.00\ \mathrm{mm}\times5.00\ \mathrm{mm}&=35.00\ \mathrm{mm}^2,\\\\
35.00\ \mathrm{mm}^2\times3.20\ \mathrm{mm}&=112.00\ \mathrm{mm}^3,\\\\
112.00\ \mathrm{mm}^3\times0.00640&=0.7168\ \mathrm{ct},\\\\
&\approx0.717\ \mathrm{ct}
\end{aligned}
$$

The selected 1.50:1 model does not claim that 1.40:1 and 1.50:1 outlines are identical. Source: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html).

### Pear brilliant: ratio-specific model

Use this for a pear brilliant with a measured length-to-width ratio between 1.25:1 and 2.00:1. Multiply length, width and depth by the factor for the selected reference ratio. The selected row is a discrete empirical model, not an automatically fitted correction.

**Formula:**

$$
m_{\mathrm{ct}}=L\times W\times h\times k_p(r),\qquad r=\frac{L}{W}
$$

| Reference ratio (r) | Factor `k_p(r)` |
|---:|---:|
| 1.25:1 | 0.00615 |
| 1.50:1 | 0.00600 |
| 2.00:1 | 0.00575 |

- `m_ct`: estimated mass, in ct.
- `L`: maximum length from point to rounded end, in mm.
- `W`: maximum width, in mm.
- `h`: total depth, in mm.
- `r=L/W`: measured length-to-width ratio, dimensionless.
- `k_p(r)`: empirical pear factor for the selected reference ratio.

The outline and shoulders vary, so the ratio alone does not describe the full geometry. No girdle or shape-specific correction is applied.

**Worked example.** For $L=7.50\ \mathrm{mm}$, $W=5.00\ \mathrm{mm}$, and $h=3.20\ \mathrm{mm}$, $r=1.50:1$:

**Worked calculation:**

$$
\begin{aligned}
7.50\ \mathrm{mm}\times5.00\ \mathrm{mm}&=37.50\ \mathrm{mm}^2,\\\\
37.50\ \mathrm{mm}^2\times3.20\ \mathrm{mm}&=120.00\ \mathrm{mm}^3,\\\\
120.00\ \mathrm{mm}^3\times0.00600&=0.720\ \mathrm{ct}
\end{aligned}
$$

This is an estimate for the selected ratio model. Source: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html).

### Marquise brilliant: ratio-specific model

Use this for a marquise brilliant with a reference ratio from 1.50:1 to 2.50:1. Select the closest listed ratio and compare it with the measured ratio displayed by the calculator.

**Formula:**

$$
\begin{aligned}
m_{\mathrm{ct}}&=L\times W\times h\times k_m(r),\\\\
r&=\frac{L}{W}
\end{aligned}
$$

| Reference ratio (r) | Factor `k_m(r)` |
|---:|---:|
| 1.50:1 | 0.00565 |
| 2.00:1 | 0.00580 |
| 2.50:1 | 0.00585 |

- `m_ct`: estimated mass, in ct.
- `L`: maximum length between the two points, in mm.
- `W`: maximum width, in mm.
- `h`: total depth, in mm.
- `r=L/W`: measured length-to-width ratio, dimensionless.
- `k_m(r)`: empirical marquise factor for the selected reference ratio.

The factor does not model point shape, wing width, girdle thickness or pavilion bulge. The choices are discrete and no interpolation is done.

**Worked example.** For $L=8.00\ \mathrm{mm}$, $W=4.00\ \mathrm{mm}$, and $h=3.20\ \mathrm{mm}$, $r=2.00:1$:

**Worked calculation:**

$$
\begin{aligned}
8.00\ \mathrm{mm}\times4.00\ \mathrm{mm}&=32.00\ \mathrm{mm}^2,\\\\
32.00\ \mathrm{mm}^2\times3.20\ \mathrm{mm}&=102.40\ \mathrm{mm}^3,\\\\
102.40\ \mathrm{mm}^3\times0.00580&=0.59392\ \mathrm{ct},\\\\
&\approx0.594\ \mathrm{ct}
\end{aligned}
$$

This does not replace weighing. Source: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html).

### Emerald step cut: ratio-specific model

Use this for a rectangular emerald step cut with a measured ratio from 1.50:1 to 2.50:1. The factor is higher than for brilliant shapes and varies with the reference ratio. Select a documented ratio model and compare it with the measured ratio shown by the calculator.

**Formula:**

$$
m_{\mathrm{ct}}=L\times W\times h\times k_e(r),\qquad r=\frac{L}{W}
$$

| Reference ratio (r) | Factor `k_e(r)` |
|---:|---:|
| 1.50:1 | 0.00920 |
| 2.00:1 | 0.01000 |
| 2.50:1 | 0.01060 |

- `m_ct`: estimated mass, in ct.
- `L`: maximum length, in mm.
- `W`: maximum width, in mm.
- `h`: total depth, in mm.
- `r=L/W`: measured length-to-width ratio, dimensionless.
- `k_e(r)`: empirical emerald-cut factor for the selected reference ratio.

Corner truncation, step arrangement, girdle and pavilion geometry affect the result. No corner or girdle correction or coefficient interpolation is applied.

**Worked example.** For $L=8.00\ \mathrm{mm}$, $W=4.00\ \mathrm{mm}$, and $h=3.20\ \mathrm{mm}$, $r=2.00:1$:

**Worked calculation:**

$$
\begin{aligned}
8.00\ \mathrm{mm}\times4.00\ \mathrm{mm}&=32.00\ \mathrm{mm}^2,\\\\
32.00\ \mathrm{mm}^2\times3.20\ \mathrm{mm}&=102.40\ \mathrm{mm}^3,\\\\
102.40\ \mathrm{mm}^3\times0.01000&=1.024\ \mathrm{ct}
\end{aligned}
$$

The result does not account for corner shape or girdle correction. Source: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html).

### Heart brilliant: fixed-factor model

Use this for a heart brilliant. Multiply maximum length, maximum width and total depth by the published heart-shape factor. This model has no ratio-specific table.

**Formula:**

$$
\begin{aligned}
m_{\mathrm{ct}}&=L\times W\times h\times k_h,\\\\
k_h&=0.0059
\end{aligned}
$$

- `m_ct`: estimated mass, in ct.
- `L`: maximum length along the cleft-to-point axis, in mm.
- `W`: maximum width across the lobes, in mm.
- `h`: total depth, in mm.
- `k_h`: empirical heart factor, 0.0059.

The fixed factor cannot represent every outline, cleft, lobe, girdle or pavilion profile. Treat the result as a rough estimate, not measured mass.

**Worked example.** For $L=7.00\ \mathrm{mm}$, $W=5.00\ \mathrm{mm}$, and $h=3.20\ \mathrm{mm}$:

**Worked calculation:**

$$
\begin{aligned}
7.00\ \mathrm{mm}\times5.00\ \mathrm{mm}&=35.00\ \mathrm{mm}^2,\\\\
35.00\ \mathrm{mm}^2\times3.20\ \mathrm{mm}&=112.00\ \mathrm{mm}^3,\\\\
112.00\ \mathrm{mm}^3\times0.0059&=0.6608\ \mathrm{ct},\\\\
&\approx0.661\ \mathrm{ct}
\end{aligned}
$$

Sources: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html); [CISGEM](https://www.cisgem.com/gemmologia/diamante/le-4c).

### Converting metric carats to grams

The shape-specific model estimates mass in metric carats. When a gram value is useful, convert that estimate using the exact metric-carat relationship.

**Formula:**

$$
m_{\mathrm{g}}=m_{\mathrm{ct}}\times0.2\ \mathrm{g/ct}
$$

- `m_g`: estimated mass in grams (g).
- `m_ct`: selected shape model's estimated mass rounded to the displayed precision of 0.001 ct.
- `0.2 g/ct`: exact conversion factor; one metric carat equals 0.2 g.

This changes only the unit used to express the same estimated mass. It does not make a dimensional estimate more accurate or turn it into a measurement. Here, carat means the gemstone mass unit, not gold fineness in karats.

**Worked example.** For an estimated $1.005\ \mathrm{ct}$:

**Worked calculation:**

$$
1.005\ \mathrm{ct}\times0.2\ \mathrm{g/ct}=0.201\ \mathrm{g}
$$

The gram result is derived from the rounded displayed carat estimate. Source: [NIST, Precious Metals Conversion Information](https://www.nist.gov/pml/owm/metric-si/unit-conversion/precious-metals-conversion-information).

### Why princess cut is not included

The consulted references disagree: GCAL's formula text gives 0.0082 while its selector lists 0.0085; a training table attributed to IDC rules and the GIA Gem Reference Guide gives 0.0083. Without a consistent documented basis, this page does not present a princess-cut estimate as verified. Sources: [GCAL](https://www.gcalusa.com/instructional-diamond-grading.html); [Jewelers Training Resources, cut lesson](https://jtr.org/us/en/books/certified-diamond-expert/cut).

## General limitations

These are empirical dimensional models for the specified diamond cuts only. Factors summarize typical proportions; they do not derive the exact faceted volume from outside dimensions. Actual mass varies with cut proportions, girdle, culet, facet geometry, outline and measurement position. Fancy-shape estimates also vary with length-to-width ratio; hence the calculator requires a reference model for four shapes. Mounted stones can be difficult to measure accurately. Do not apply these equations to other gemstones. Weigh a loose diamond on a suitable calibrated balance to determine actual mass. One metric carat is 0.2 g; carat here denotes mass, not gold fineness.

## Sources

- [GCAL by Sarine, Instructional Diamond Grading](https://www.gcalusa.com/instructional-diamond-grading.html) — dimensional formula, shape factors, ratio tables and correction discussion.
- [CISGEM, Le 4C dei diamanti](https://www.cisgem.com/gemmologia/diamante/le-4c) — approximate dimensional formulas, ratio-dependent fancy-shape factors and measurement guidance.
- [Jewelers Training Resources, Certified Diamond Expert: Cut](https://jtr.org/us/en/books/certified-diamond-expert/cut) — simplified shape factors, attributed to IDC Rules and the GIA Gem Reference Guide.
- [GIA, Observations of Oval-, Pear-, and Marquise-Shaped Diamonds](https://www.gia.edu/gems-gemology/fall-2024-fancy-shaped-diamonds) — research on variation in fancy-shape outlines and proportions.

The factors are empirical approximations; sources differ in their model structure and corrections. The selected factor set is identified here, without claiming universal factors or professional certification.

Related: [Gemstone Dimensions & Geometry](/en/docs/calculators/jewelry-calculators/gemstone-dimensions-and-geometry/).

**Alt-text:**  
Diamond dimensions and a calculator used to estimate carat mass.

_Calculators. Jewelry Calculators. Diamond Carat Mass Estimator. AP | Pivtorak.Studio. 21.10.2026_    
© Anna Pivtorak (Kostyuk)
