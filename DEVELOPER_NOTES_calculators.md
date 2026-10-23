# Calculator and converter implementation

This note documents the client-side tools under `content/<language>/docs/`. Keep these models small, explicit, localized and free of network dependencies.

## Inventory and language structure

The calculators are available in EN, PT, RU and UK source content. English jewelry calculator pages retain their `jewelry/` directory; other languages use the calculators section root. Russian source pages are intentionally retained while RU is disabled in `hugo.toml`.

| Tool | Established basename | Type / model | Languages |
|---|---|---|---|
| Precious Metal Mass Calculator | `gold-weight-calculator` | `m = ρV`, volume cm³ × density g/cm³ | EN, PT, RU, UK |
| Precious Metal Price Calculator | `metal-price-calculator` | fine mass = gross mass × fineness/1000; value = fine mass/31.1034768 × user quote | EN, PT, RU, UK |
| Stone Dimensions & Proportion Calculator | `stone-size-calculator` | `L/W`; bounding box `L×W×D` | EN, PT, RU, UK |
| Precious Metal Weight & Force Calculator | `precious-metal-weight-force-calculator` | `F = mg`; g converted to kg; default `gₙ = 9.80665 m/s²` | EN, PT, RU, UK |
| Round Brilliant Diamond Carat Weight Estimator | `round-brilliant-diamond-carat-weight-estimator` | average diameter² × total depth × 0.0061 | EN, PT, RU, UK |
| Precious Metal Mass Unit Converter (legacy URL `gold-weight-converter`) | `gold-weight-converter` | known mass converted among mg, g, kg, troy oz, dwt, grains and metric carats | EN, PT, RU, UK |
| AWG Wire Gauge Converter | `wire-gauge-converter` | AWG nominal diameter and solid-round area | EN, PT, RU, UK |
| Ring Metric Diameter/Circumference Converter | `ring-size-converter` | `C = πd` for metric inner diameter | EN, PT, RU, UK |

The legacy `gold-weight-converter` is the same mass-unit converter family; it is not a second tool or a substitute for deriving mass from volume. Keep its public path and use the displayed title to clarify its unit-conversion scope. No country-specific ring-size mapping is currently supported.

All pages use the shared `calculator` shortcode and `static/js/calculators.js`. Each translated page has a stable `id` and shared Hugo `translationKey`. Preserve existing page basenames, language-specific paths, and established translation relationships. Hugo generates canonical and alternate-language links; do not add page-level duplicate canonical/hreflang values.

## Models, factors and limitations

### Mass from density and volume

`m = ρV`; volume is cm³ and density is g/cm³, so mass is g, with kg reported as g/1000. Density is supplied for the actual material. Alloy composition, porosity, temperature and measurement uncertainty affect the result. Mass is not weight force. [NIST Guide to the SI: density](https://www.nist.gov/pml/special-publication-811/nist-guide-si-chapter-8).

### Weight force

`F = m g`; enter mass in grams and acceleration in m/s²; convert mass to kg before reporting N. The default is standard gravity 9.80665 m/s², not a location-specific measurement. [BIPM, 3rd CGPM (1901)](https://www.bipm.org/en/committees/cg/cgpm/3-1901/resolution-2).

### Precious-metal content value

`m_fine = m_gross × fineness/1000`; `value = m_fine/31.1034768 × quote`. Gross mass is g, fineness is parts per thousand (‰), and quote is user-entered currency per troy ounce. `1 troy oz = 31.1034768 g`. This is indicative fine-metal content arithmetic only: no live market feed, currency exchange conversion, dealer spread, tax, workmanship, stones, buyback offer or finished-jewelry valuation is included. [LBMA: the troy ounce](https://www.lbma.org.uk/wonders-of-gold/items/the-troy-ounce).

### Searchable currency selector

The ISO 4217 alphabetic currency codes are a curated static list in `static/js/calculators.js`, reviewed against the [SIX ISO currency-code maintenance information](https://www.six-group.com/en/products-services/financial-information/market-reference-data/data-standards.html) on 2026-10-19. It excludes historic entries, fund units and precious-metal codes. Currency names are supplied by the browser's localized `Intl.DisplayNames` data for EN, PT-PT, RU and UK; the code is always displayed as a fallback. Users can search by code or localized name and must select a listed result. Keyboard support includes Up/Down, Home/End, Enter and Escape; the input exposes combobox/listbox roles and live result announcements.

The selected code formats the indicative result with `Intl.NumberFormat`. It only labels the user-entered quote and result; it does not fetch or calculate exchange rates. Review the maintained list against SIX updates when ISO 4217 changes.

### Stone dimensions

`ratio = L/W`; `V_box = L×W×D`; all dimensions are mm, ratio is dimensionless and box volume is mm³. The box does not represent the volume or carat weight of a faceted stone. Shape-specific factors and material density are necessary for a gemstone weight estimate. [GIA: carat weight and size](https://4cs.gia.edu/en-us/blog/gia-diamond-grading-reports-understanding-carat-weight/).

### Round brilliant diamond estimate

`estimated ct = average girdle diameter² × total depth × 0.0061`; diameter and depth are mm. GIA's Winter 1986 *Gems & Gemology* source states the diameter² × depth × 0.0061 estimate for round brilliant diamonds. GIA's indexed publication excerpt was independently found and checked on 2026-10-19; the linked PDF itself still returns 404 when opened directly. The coefficient and stated round-brilliant scope are supported by the official GIA excerpt, but the inaccessible full text prevents review of its surrounding qualifications. Treat this as an empirical estimate only. Girdle and cut proportions affect accuracy; some grading references apply a weight correction. The current interface does not apply such a correction and says so through its estimate/limitations wording. Do not generalize to fancy shapes or colored gemstones and do not substitute for weighing a loose stone. [GIA, Winter 1986 *Gems & Gemology*](https://www.gia.edu/doc/WN86.pdf).

### Precious-metal mass unit conversion

Factors relative to grams used in `static/js/calculators.js`:

| Unit | Grams |
|---|---:|
| milligram (mg) | 0.001 |
| gram (g) | 1 |
| kilogram (kg) | 1000 |
| troy ounce (oz t) | 31.1034768 |
| pennyweight (dwt) | 1.55517384 |
| grain (gr) | 0.06479891 |
| metric carat (ct) | 0.2 |

The mass-unit conversion uses the troy ounce and grain definitions; 1 dwt = 24 grains. A metric carat is exactly 200 mg and is a gemstone mass unit. It is distinct from karat/fineness, which describes gold purity. [NIST Handbook 44, Appendix C](https://nvlpubs.nist.gov/nistpubs/hb/2026/NIST.HB.44-2026.pdf), [LBMA troy ounce](https://www.lbma.org.uk/wonders-of-gold/items/the-troy-ounce).

### AWG wire gauge

For integer AWG `n` from 0000 through 40 (`0000` through `000` map to −3 through −1 in the formula): `d(mm) = 0.127 × 92^((36−n)/39)`; solid round cross-section `A = πd²/4`. Diameter and area are nominal; actual wire dimensions have tolerances. This is AWG only, not SWG or every international gauge system. Use [ASTM B258](https://store.astm.org/standards/b258) as the nominal AWG reference.

### Ring metric conversion

For circular inner geometry, `C(mm) = π × d(mm)` and `d(mm) = C(mm)/π`. The interface supports either metric input direction. There are no named national size mappings or claims of international equivalence. [ISO 8653](https://www.iso.org/standard/65408.html) provides ring-measurement and designation context; its publicly available summary is not a full cross-country conversion table.

## Implementation and localization conventions

- Keep all user-facing names, notes, input labels, units, validation, currency interaction messages and output names localized in the `ui` object in `static/js/calculators.js`.
- Calculator prose translates the **Model and limits** heading, formula, units and assumptions in all four source languages.
- Use semantic labels and explicit units; accept only finite positive values except AWG's defined integer range. Purity must be at most 1000‰.
- Currency is an accessible searchable combobox. Arbitrary free text is never accepted as a currency selection.
- Keep calculations unrounded internally; round only displayed values. Use locale-aware number and currency formatting.
- Page-specific model/formula metadata should describe the tool honestly. Avoid hand-authored canonical URLs and do not rename existing paths or image assets as part of calculator work.

## Verification cases

Run these against the client-side controls whenever models or shared code change:

| Tool | Input | Expected result |
|---|---|---|
| Mass | 10 cm³, 19.32 g/cm³ | 193.2 g; 0.1932 kg |
| Force | 1 g, 9.80665 m/s² | 0.00980665 N |
| Price | 10 g, 750‰, 2,000 per troy oz | 7.5 g fine; about 482.26 in selected currency |
| Stone | 6 × 4 × 2 mm | ratio 1.5; box 48 mm³ |
| Diamond estimate | 6.5 mm average diameter, 4 mm depth | 1.0309 ct estimate |
| Unit conversion | 1 troy oz to grams | 31.1034768 g |
| AWG | 10 AWG | nominal diameter about 2.588 mm; area about 5.261 mm² |
| Ring | 20 mm inner diameter; 62.831853 mm circumference | circumference about 62.83185 mm; diameter about 20 mm |

Also verify empty, zero, negative, invalid, non-finite and unusually large numbers; purity above 1000‰; AWG strings 0000, 00, 0, 40 and out-of-range/fractional gauges; currency search by code and localized name, no-result and empty searches, invalid/unselected text; combobox keyboard controls; localized output; internal links and generated translations/canonicals. Record the actual Hugo disk-build outcome. Do not describe an unrun browser or mobile visual check as completed.

### Verification recorded 2026-10-19

- `node --check static/js/calculators.js` and `git diff --check`: passed; Git emitted only expected LF-to-CRLF notices for the existing working-copy configuration.
- Independent arithmetic checks for the documented mass, force, metal-content value, stone ratio/box, diamond estimate, troy-ounce/dwt/carat factors, AWG 10 diameter/area and ring circumference: passed. Locale `Intl.DisplayNames`/`Intl.NumberFormat` currency smoke check: passed.
- Source inventory check: all 20 calculator pages and 12 converter pages exist with translation keys; non-English calculator model headings are localized.
- Full Hugo disk build to `public-qa-final`: exit 0 (156.8 seconds). Generated EN/PT/UK output check found 24 tool pages, each with canonical and language-alternate tags; checked local links from those pages all resolved. RU remains unpublished by project configuration. A copied-JavaScript output check was not completed because this build destination did not contain `static/js/calculators.js`.
- Browser-driven currency selection/keyboard test and desktop/mobile visual inspection were not completed. The local Hugo server could not bind to `127.0.0.1:1313` because the environment denied socket access; the available browser expressly rejected `file:` URLs and allows only HTTP(S). Its policy prohibits workarounds for that restriction. No browser or mobile behavior is claimed as verified.
- The full Hugo build warns that `languages.<en/pt/uk>.languageName` and `.Site.Data` are deprecated. It also reproduces duplicate target paths for `/uk/tags/память/` (`index.html`, `index.xml` and paginator page 1). The same `память` term occurs in RU and UK source content; this is a pre-existing content/taxonomy collision, unrelated to calculator pages. It was left unchanged to preserve scope and public URLs.

## Deferred tools

Do not add a universal gemstone carat estimator or jewelry-value estimator. A general gem estimate needs cut-specific factors, density and validated assumptions; finished jewelry valuation requires a professionally defined method and inputs.
