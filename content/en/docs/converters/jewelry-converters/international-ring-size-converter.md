---
id: international-ring-size-converter
language: en
translation_of: international-ring-size-converter
translationKey: international-ring-size-converter
title: International Ring Size Converter
description: Convert ring sizes between supported international sizing systems using nominal inner circumference as a common reference.
summary: An interactive jewelry reference tool for converting ring sizes between EU / ISO 8653, US / Canada, UK / Australia / Ireland, and the Japanese JCS reference scale, with clearly stated input ranges and matching limitations.
event_date: 2026-10-23T15:00:00
publication_date: 2026-10-23T15:00:00
lastmod: 2026-10-23T15:00:00
slug: international-ring-size-converter
tags: [ring sizing, ring size conversion, jewelry tools, international standards]
keywords: [international ring size converter, ring size conversion chart, EU ISO 8653 ring size, US ring size, UK ring size, Japanese ring size, inner circumference, jewelry sizing]
categories: [Converters, Jewelry]
series: JewelryConverters
series_index: 3
weight: 3
research_origin: Pivtorak.Studio
status: published
featured: true
image: /images/converters-jewelry-converters-international-ring-size-converter.webp
alt: "International Ring Size Converter: gold rings, ring sizing gauges, a world map, and technical diagrams of inner diameter and circumference on an ivory and gold background."
related: [/en/docs/converters/, /en/tools/, /en/docs/timeline/, /en/docs/the-movement-matrix/site-completion-matrix/]
authors: [Anna Pivtorak]
license: CC BY-NC-ND 4.0
timeline: true
tools: [International Ring Size Converter]
visual_archive: true
disciplines: [Jewelry, Precious Metals, Applied Mathematics, Measurement Science]
converter_type: ring-size
converter_model: nominal inner circumference matching
converter_units: [mm, US ring sizes, UK letter sizes, Japanese JCS sizes]
implementation_status: complete
draft: false
canonical: https://pivtorak.studio/en/docs/converters/jewelry-converters/international-ring-size-converter/
toc: true
completion: 100
seo: true
distribution: true
search: indexed
---


<script type="application/ld+json">
{
  "@context": "https://schema.org",
  "@type": "WebApplication",
  "@id": "https://pivtorak.studio/en/docs/converters/jewelry-converters/international-ring-size-converter/#webapplication",
  "name": "International Ring Size Converter",
  "url": "https://pivtorak.studio/en/docs/converters/jewelry-converters/international-ring-size-converter/",
  "description": "Convert ring sizes between supported international sizing systems using nominal inner circumference as a common reference.",
  "applicationCategory": "UtilitiesApplication",
  "applicationSubCategory": "Jewelry Measurement Converter",
  "operatingSystem": "Any",
  "browserRequirements": "Requires JavaScript",
  "inLanguage": "en",
  "isAccessibleForFree": true,
  "isPartOf": {
    "@type": "WebSite",
    "@id": "https://pivtorak.studio/#website",
    "name": "Pivtorak.Studio",
    "url": "https://pivtorak.studio/"
  },
  "author": {
    "@type": "Person",
    "@id": "https://pivtorak.studio/#person",
    "name": "Anna Pivtorak",
    "url": "https://pivtorak.studio/"
  },
  "image": {
    "@type": "ImageObject",
    "url": "https://pivtorak.studio/images/converters-jewelry-converters-international-ring-size-converter.webp",
    "caption": "International ring sizing systems, jewelry rings, and technical diagrams of inner diameter and circumference."
  },
  "featureList": [
    "EU / ISO 8653 ring sizes",
    "US / Canada ring sizes",
    "UK / Australia / Ireland letter sizes",
    "Japanese JCS reference sizes",
    "Nominal inner circumference comparison",
    "Input validation and approximate size matching"
  ],
  "keywords": [
    "international ring size converter",
    "ring size conversion",
    "EU ISO 8653",
    "US ring sizes",
    "UK ring sizes",
    "Japanese ring sizes",
    "jewelry measurement"
  ],
  "creator": {
    "@id": "https://pivtorak.studio/#person"
  }
}
</script>

# International Ring Size Converter

![_Converters. Jewelry Converters. International Ring Size Converter. AP | Pivtorak.Studio. 23.10.2026_ © Anna Pivtorak (Kostyuk)](/images/converters-jewelry-converters-international-ring-size-converter.webp)

Ring sizing systems vary between countries and regions, making it difficult to compare sizes when buying jewellery internationally, working with overseas suppliers or helping customers choose a ring remotely. The International Ring Size Converter helps translate ring sizes between commonly used standards, bringing different sizing conventions into one practical reference tool. It is designed for jewellers, jewellery retailers, designers and anyone who needs to interpret ring sizes across markets. Enter a known size in one of the supported regional systems to find the nearest size in another supported system. Because sizing systems do not always correspond exactly, converted results should be treated as reference values rather than guaranteed fits.

{{< calculator type="international-ring-size" >}}

## How to Use the Converter

Select the regional sizing system you know, enter its size, and choose the target system. To determine the starting size, measure the inner diameter of a well-fitting ring or the circumference of the finger separately, then consult the corresponding regional sizing chart.

## Understanding International Ring Sizes

Different sizing systems use different scales and reference points. Some are based on the inner circumference in millimetres, others use numerical scales, and some employ letter-based sizes. As a result, the same ring may have different size labels depending on the country or standard.

## Measurement and Fit

For more reliable results, measure a ring's inner diameter across its centre or measure the finger circumference with a flexible measuring strip. Measurements should be taken carefully, as small differences can affect the fit. Finger size may also vary with temperature, time of day and individual anatomy.

## Important Notes

- International ring-size conversions are approximate because sizing standards and commercial charts can differ.
- A converted size may fall between two standard sizes; the most suitable choice depends on the ring design and desired fit.
- Wide bands may require a different fit from narrow rings.
- For valuable, custom-made or difficult-to-resize rings, confirm the size using the jeweller's local sizing system before ordering or manufacturing.

This converter is intended as a practical reference for jewellery work and international size comparison. It does not replace professional fitting or the sizing chart specified by a manufacturer or retailer.

## Systems and calculation limits

This version supports EU / ISO 8653 sizes 41–76, US / Canada sizes 3–13 in half-size steps, UK / Australia / Ireland letter sizes A–Z including half-letter steps, and Japanese JCS reference sizes 1–30. Other regional scales, including China / Hong Kong, India, Brazil, France / Switzerland, Germany, Italy / Spain / the Netherlands and Ukraine, are not offered because the sources reviewed did not establish one sufficiently consistent mapping for this tool.

Each supported input is mapped to a nominal inner circumference in millimetres. EU / ISO uses its size number as the circumference. US / Canada uses the approximate chart progression `C = 44.2 + 2.55 × (s − 3)`. UK-style letters use `C = 38.05 + 1.25 × i + 0.625 × h`, where `i` is the letter's position from A starting at zero and `h` is 0 for a whole letter or 1 for a half-letter. The Japanese reference progression uses `C = 40.8 + (s − 1)`. Here, `C` is in millimetres and `s` is the source-system numeric size. The converter returns the target size with the nearest nominal circumference and reports the difference; chart-derived scales are approximate, not exact standard equivalences. A difference of 0.25 mm or less is described as a close physical match.

The ISO system's circumference basis is defined in [ISO 8653:2016](https://www.iso.org/standard/65408.html). The regional chart anchors and notations are compared with [Pandora's ring-size guide](https://us.pandora.net/en/guide-size-rings/guide-size-rings.html) and [440showroom's Japan-based conversion chart](https://440showroom.tokyo/en-eu/pages/ring-size-guide); these commercial charts are reference data, not endorsements. Confirm the required size with the manufacturer or jeweller before production or purchase.

Related: [Ring Diameter & Circumference Converter](/en/docs/converters/jewelry-converters/ring-diameter-and-circumference-converter/).

**Alt-text:**  
International Ring Size Converter: gold rings, ring sizing gauges, a world map, and technical diagrams of inner diameter and circumference on an ivory and gold background.

_Converters. Jewelry Converters. International Ring Size Converter. AP | Pivtorak.Studio. 23.10.2026_    
© Anna Pivtorak (Kostyuk)
