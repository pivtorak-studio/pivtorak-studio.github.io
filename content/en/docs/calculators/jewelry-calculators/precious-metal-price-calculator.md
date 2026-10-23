---
id: precious-metal-price-calculator
language: en
translation_of: precious-metal-price-calculator
translationKey: precious-metal-price-calculator
title: Precious Metal Price Calculator
description: Estimate the indicative price of precious metals based on metal mass, fineness, and a user-supplied market quote per troy ounce.
summary: Calculate the indicative fine-metal content value using mass, fineness, and a manually entered price per troy ounce.
event_date: 2026-10-20T08:00:00
publication_date: 2026-10-20T08:00:00
lastmod: 2026-10-20T08:00:00
slug: precious-metal-price-calculator
tags:
  - precious-metals
  - metal-pricing
  - jewelry-calculators
  - precious-metal-value
keywords:
  - precious metal price calculator
  - gold price calculation
  - silver price calculation
  - platinum price calculation
  - fine-metal content
  - fineness
  - troy ounce
  - metal quote
categories:
  - Calculators
  - Jewelry
series: JewelryCalculators
series_index: 3
research_origin: Pivtorak.Studio
status: published
featured: true
image: /images/calculators-jewelry-calculators-precious-metal-price-calculator.webp
alt: Precious Metal Price Calculator with gold, silver, and platinum bars, a precision scale, a market price chart, and the fine-metal content valuation formula.
related:
  - /en/docs/calculators/jewelry-calculators/
  - /en/tools/
  - /en/timeline/
  - /en/docs/the-movement-matrix/site-completion-matrix/
authors:
  - Anna Pivtorak
license: CC BY-NC-ND 4.0
timeline: true
tools: true
visual_archive: true
disciplines:
  - Jewelry
  - Precious Metals
  - Applied Mathematics
calculator_type: market-quote-based-fine-metal-content-value
calculator_model: m_fine = m × (f / 1000); \(P_{\mathrm{item}}\) = (m_fine / 31.1034768) × P
calculator_units: "mass: g; fineness: ‰; price: currency/troy oz; value: currency"
implementation_status: client-side
draft: false
canonical: https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/
toc: true
weight: 3
completion: 100
seo: true
distribution: true
search: indexed
---


<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@graph": [
    {
      "@type": "WebPage",
      "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/#webpage",
      "url": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/",
      "name": "Precious Metal Price Calculator",
      "description": "Estimate the indicative price of precious metals based on metal mass, fineness, and a user-supplied market quote per troy ounce.",
      "inLanguage": "en",
      "isPartOf": {
        "@type": "WebSite",
        "@id": "https://pivtorak.studio/#website"
      },
      "mainEntity": {
        "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/#software"
      },
      "datePublished": "2026-10-20T08:00:00",
      "dateModified": "2026-10-20T08:00:00",
      "image": {
        "@type": "ImageObject",
        "url": "https://pivtorak.studio/images/calculators-jewelry-calculators-precious-metal-price-calculator.webp"
      },
      "author": {
        "@type": "Person",
        "name": "Anna Pivtorak"
      },
      "license": "https://creativecommons.org/licenses/by-nc-nd/4.0/",
      "breadcrumb": {
        "@type": "BreadcrumbList",
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
            "name": "Calculators & Converters",
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
            "name": "Precious Metal Price Calculator",
            "item": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/"
          }
        ]
      }
    },
    {
      "@type": "SoftwareApplication",
      "@id": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/#software",
      "name": "Precious Metal Price Calculator",
      "description": "Calculate the indicative fine-metal content value using mass, fineness, and a manually entered price per troy ounce.",
      "applicationCategory": "UtilitiesApplication",
      "applicationSubCategory": "Jewelry Calculator",
      "operatingSystem": "Any",
      "browserRequirements": "Requires JavaScript enabled in a modern web browser.",
      "inLanguage": "en",
      "isAccessibleForFree": true,
      "isPartOf": {
        "@id": "https://pivtorak.studio/#website"
      },
      "url": "https://pivtorak.studio/en/docs/calculators/jewelry-calculators/precious-metal-price-calculator/",
      "image": "https://pivtorak.studio/images/calculators-jewelry-calculators-precious-metal-price-calculator.webp",
      "author": {
        "@type": "Person",
        "name": "Anna Pivtorak"
      },
      "license": "https://creativecommons.org/licenses/by-nc-nd/4.0/",
      "featureList": [
        "Estimate fine-metal mass from gross mass and fineness.",
        "Calculate indicative metal content value using a user-supplied market quote.",
        "Support calculations for precious metals quoted per troy ounce.",
        "Use manually entered prices without live market data."
      ],
      "keywords": [
        "precious metal price calculator",
        "gold price calculation",
        "silver price calculation",
        "platinum price calculation",
        "fine-metal content",
        "fineness",
        "troy ounce",
        "metal quote"
      ]
    }
  ]
}
</script>

# Precious Metal Price Calculator

![_Calculators. Jewelry Calculators. Precious Metal Price Calculator. AP | Pivtorak.Studio. 20.10.2026_ © Anna Pivtorak (Kostyuk)](/images/calculators-jewelry-calculators-precious-metal-price-calculator.webp)

Estimate the indicative price of the fine precious metal contained in an item using its gross mass, fineness and a manually entered market quote per troy ounce. The calculator determines the proportion of fine metal in the item and uses the supplied quote to estimate the corresponding metal price. It can support preliminary assessments of precious-metal content in jewellery, scrap metal and other objects made from gold, silver, platinum or similar materials. The result is an indicative calculation based on the values entered by the user, not a live market quote or a guaranteed buying or selling price. It does not include dealer spreads, refining costs, commissions, taxes, workmanship, gemstones or other factors that may affect the price of a finished item.

{{< calculator type="price" >}}

## Model and limits

$$
\begin{gathered}
\text{Fine-metal mass}=\text{gross mass}\\\\
\times\frac{\text{fineness}}{1000}\\\\[4pt]
\text{Indicative price of the fine-metal content}\\\\
=\frac{\text{fine-metal mass}}{31.1034768}\\\\
\times\text{quote per troy ounce}.
\end{gathered}
$$

Enter the quote and currency manually. No live market data is used. The result excludes dealer spreads, fees, taxes, workmanship, gemstones and the overall value of finished jewellery.

Related: [Precious Metal Reference Value Calculator](/en/docs/calculators/jewelry-calculators/precious-metal-reference-value-calculator/).

**Alt-text:**  
Precious Metal Price Calculator with gold, silver, and platinum bars, a precision scale, a market price chart, and the fine-metal content valuation formula.

_Calculators. Jewelry Calculators. Precious Metal Price Calculator. AP | Pivtorak.Studio. 20.10.2026_    
© Anna Pivtorak (Kostyuk)
