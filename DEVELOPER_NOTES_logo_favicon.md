# DEVELOPER NOTES — Logo & Favicon

Technical documentation for the Pivtorak.Studio logo, favicon,
their Hugo integration, and related Schema.org / JSON-LD references.

---

## 1. Current Brand Mark

### P.S.

The current Pivtorak.Studio brand mark is:

P.S.

white lettering on a black square with slightly rounded corners.

`P.S.` has two intended readings:

- Pivtorak.Studio
- Post Scriptum

The additional meaning is semantic and is not encoded through separate
graphic elements.

### Visual characteristics

- black background;
- white `P.S.` lettering;
- thin, compact, technical lettering;
- slightly rounded square corners;
- no decorative rays, gradients, or additional graphic elements.

Cyan / turquoise and coral remain secondary colors of the broader
Pivtorak.Studio visual system, but are not part of the current
primary logo or favicon.

---

# 2. Master Logo Asset

The master source of the current brand mark is:

```text
assets/brand/ps-master.svg
```

This is the primary source for the current logo design.

### Rule

When the logo is redesigned, update the master asset first:

```
assets/brand/ps-master.svg
```

Then regenerate the required derivative files.

Do not independently redesign different copies of the logo in different  
directories.

The intended model is:

```
ONE MASTER
     ↓
controlled derivatives
     ↓
different Hugo / JSON-LD / browser uses
```

---

# 3. Current Logo Files

The current source-level WEBP logo files are:

```
images/logo.webp
static/logo.webp
```

Both currently contain the current P.S. logo.

They are separate files because they serve different roles in the  
project structure.

## 3.1 `images/logo.webp`

Path:

```
images/logo.webp
```

This file is referenced directly by Schema.org / JSON-LD content  
and by the publisher schema partial.

Current publisher partial:

```
layouts/_partials/docs/schema/publisher.html
```

Relevant reference:

```
"logo": {
  "@type": "ImageObject",
  "url": "{{ "images/logo.webp" | absURL }}"
}
```

Therefore this file must not be deleted merely because the Sidebar  
uses the SVG master asset instead.

---

## 3.2 `static/logo.webp`

Path:

```
static/logo.webp
```

This is the static/public version of the logo.

It is retained because existing site configuration and content may  
refer to the public `/logo.webp` path.

---

# 4. Important: `pivtorak-studio-logo.webp` Is a Different Asset

Some older JSON-LD blocks use:

```
/images/pivtorak-studio-logo.webp
```

This is NOT the same path as:

```
/images/logo.webp
```

It must therefore be treated as a separate legacy/older asset.

Current references were found in the following series:

```
Independent Researcher Manifesto
  004 — The Right to Simplicity
  005 — The Right to Incompleteness
  006 — The Right to Human Outcomes
```

These references occur in:

```
content/en/...
content/pt/...
content/ru/...
content/uk/...
```

### Important

When the main P.S. logo is replaced, do NOT automatically replace  
`pivtorak-studio-logo.webp` unless a separate decision is made to  
migrate these older JSON-LD references.

This is a separate cleanup / migration task.

---

# 5. Sidebar Logo

The Sidebar logo is controlled by the site-local Hugo override:

```
layouts/_partials/docs/brand.html
```

It loads:

```
assets/brand/ps-master.svg
```

Current implementation:

```
{{- with resources.Get "brand/ps-master.svg" -}}
<img src="{{ .RelPermalink }}" alt="{{ partial "docs/text/i18n" "Logo" }}" />
{{- end -}}
```

### Important

Do not modify the corresponding file inside:

```
themes/hugo-book/
```

The site uses a local override instead.

---

# 6. Sidebar Logo Size

The Sidebar logo size is defined in:

```
assets/_custom.scss
```

Current rule:

```
.book-brand img {
    height: 56px !important;
    width: auto !important;
}
```

Current approved size:

```
56 px
```

A simple replacement of the logo artwork does not require changing  
this CSS rule.

---

# 7. Favicon

The browser favicon is currently configured through:

```
hugo.toml
```

under:

```
[params]
BookFavicon = "images/favicon.svg"
```

The corresponding site-local Hugo partial is:

```
layouts/_partials/docs/html-head-favicon.html
```

Current content:

```
<link rel="icon" href="{{ .Site.Params.BookFavicon | relURL }}">
```

The generated HTML therefore contains:

```
<link rel="icon" href="/images/favicon.svg">
```

### Important

Do not modify:

```
themes/hugo-book/layouts/_partials/docs/html-head-favicon.html
```

The site-local override is intentional.

---

# 8. Current Favicon Files

The current P.S. favicon exists in two source locations:

```
images/favicon.svg
static/images/favicon.svg
```

These two files currently have the same SHA-256 hash and therefore  
are byte-identical.

Current SHA-256:

```
7F717EB1BFD61F0B5513AB4947E962E9A78E272C5A26A323A1AE974E293DC39C
```

Current size:

```
569598 bytes
```

---

# 9. Legacy / Other Favicon Files

Several other `favicon.svg` files exist in the project.

Examples include:

```
favicon.svg
themes/hugo-book/static/favicon.svg
```

and generated copies inside:

```
public/
public/research-validation/
public/series-projects-validation/
```

These files must not automatically be treated as the current browser  
favicon.

The current browser favicon is determined by:

```
hugo.toml
        ↓
BookFavicon
        ↓
layouts/_partials/docs/html-head-favicon.html
        ↓
/images/favicon.svg
```

---

# 10. Legacy Content References to `/favicon.svg`

A separate set of older JSON-LD blocks explicitly references:

```
https://pivtorak.studio/favicon.svg
```

These references occur in:

```
The Majestic Discipline

037 — Zero Navigation
038 — Sum of Vectors
039 — Direct Return
```

in:

```
content/en/
content/pt/
content/ru/
content/uk/
```

Total currently identified:

```
12 content files
```

These references are NOT the same as the current browser favicon  
configuration:

```
/images/favicon.svg
```

They point to the root-level URL:

```
/favicon.svg
```

### Important

Do not silently change these references when replacing the current  
browser favicon.

If these old JSON-LD references are to be migrated to the current  
favicon asset, that should be treated as a separate intentional  
migration.

---

# 11. Why Multiple Logo / Favicon Locations Exist

The project uses several Hugo mechanisms:

```
assets/
images/
static/
content/
layouts/
```

They do not all serve the same purpose.

### `assets/`

Used by Hugo's asset pipeline.

Current master logo:

```
assets/brand/ps-master.svg
```

### `images/`

Contains assets referenced directly by content and structured data.

Current logo:

```
images/logo.webp
```

Current favicon:

```
images/favicon.svg
```

### `static/`

Contains files copied directly to the public site.

Current logo:

```
static/logo.webp
```

Current favicon:

```
static/images/favicon.svg
```

### `content/`

Contains Markdown and embedded JSON-LD references.

Some articles contain explicit references to:

```
/images/logo.webp
/images/pivtorak-studio-logo.webp
/favicon.svg
```

### `layouts/`

Contains Hugo templates and local overrides controlling how these  
assets are used.

---

# 12. Generated Files — DO NOT Edit Manually

Hugo generates additional copies of assets inside:

```
public/
```

and related validation output directories.

Examples:

```
public/logo.webp
public/images/logo.webp
public/research-validation/
public/series-projects-validation/
```

These are generated files.

They should NOT be manually updated when the logo changes.

Instead:

1. update the appropriate source asset;
2. rebuild Hugo;
3. allow Hugo to regenerate `public/`.

---

# 13. What Must Be Updated When the Main Logo Changes

If the P.S. logo is redesigned, use this order.

## Step 1 — Update master

```
assets/brand/ps-master.svg
```

## Step 2 — Regenerate current WEBP logo

Update:

```
images/logo.webp
static/logo.webp
```

Both should represent the same current logo.

## Step 3 — Regenerate favicon

Update:

```
images/favicon.svg
static/images/favicon.svg
```

Both should represent the same current favicon.

## Step 4 — Check configuration

Verify:

```
hugo.toml
```

contains:

```
BookFavicon = "images/favicon.svg"
```

## Step 5 — Check local Hugo overrides

Verify:

```
layouts/_partials/docs/brand.html
layouts/_partials/docs/html-head-favicon.html
```

No change should normally be required if the paths remain unchanged.

## Step 6 — Check Schema.org references

Search for:

```
logo.webp
pivtorak-studio-logo.webp
favicon.svg
```

Do not automatically replace every occurrence.

Determine whether each occurrence refers to:

- the current brand logo;
- an older logo;
- an article image;
- a favicon;
- another organization's logo;
- generated output.

---

# 14. Important Distinction: Current vs Legacy

## Current Pivtorak.Studio brand system

```
assets/brand/ps-master.svg
        ↓
images/logo.webp
static/logo.webp
        ↓
Schema.org / JSON-LD

images/favicon.svg
static/images/favicon.svg
        ↓
BookFavicon
        ↓
browser favicon
```

## Legacy / separate assets

```
/images/pivtorak-studio-logo.webp
/favicon.svg
```

These are currently referenced by older content and should not be  
silently removed or redirected without checking the relevant articles.

---

# 15. Search Before Replacing a Logo

Before changing or deleting any logo/favicons, search the repository.

For example:

```
Get-ChildItem content,layouts -Recurse -File |
Select-String -Pattern 'logo\.webp' |
ForEach-Object {
    "$($_.Path) : $($_.LineNumber) : $($_.Line.Trim())"
}
```

and:

```
Get-ChildItem content,layouts -Recurse -File |
Select-String -Pattern 'favicon\.svg' |
ForEach-Object {
    "$($_.Path) : $($_.LineNumber) : $($_.Line.Trim())"
}
```

Also search specifically for the older logo name:

```
Get-ChildItem content,layouts -Recurse -File |
Select-String -Pattern 'pivtorak-studio-logo\.webp' |
ForEach-Object {
    "$($_.Path) : $($_.LineNumber) : $($_.Line.Trim())"
}
```

---

# 16. Local Verification After a Logo Change

Run:

```
hugo server
```

Check:

1. Sidebar logo;
2. browser tab favicon;
3. page source;
4. Schema.org / JSON-LD references;
5. pages containing older logo references;
6. Hugo build result.

The generated page source should contain:

```
<link rel="icon" href="/images/favicon.svg">
```

---

# 17. Browser Favicon Cache

Browsers may cache favicon images separately from the page itself.

After changing the favicon:

```
Ctrl + Shift + R
```

If the current browser tab shows the new P.S. favicon but an existing  
bookmark still shows the old Hugo Book icon, this may be browser  
bookmark favicon caching rather than a Hugo problem.

Always verify the generated HTML before diagnosing a favicon problem.

---

# 18. Git Verification

Before committing:

```
git status
```

Review the list of changed files.

Then verify the site locally.

Only after successful local verification:

```
git add -A
git commit -m "Update P.S. branding and favicon"
git push
```

---

# 19. Current Brand Architecture

```
                    P.S. MASTER
                         │
                         ▼
              assets/brand/ps-master.svg
                         │
             ┌───────────┴───────────┐
             │                       │
             ▼                       ▼
       Sidebar logo             Derived assets
             │                       │
             ▼               ┌───────┴────────┐
 layouts/_partials/           │                │
 docs/brand.html              ▼                ▼
                         logo.webp        favicon.svg
                             │                │
                    ┌────────┴───────┐        │
                    ▼                ▼        ▼
              images/logo.webp   static/   Browser
                                logo.webp   favicon
```

---

# 20. Current Status

Brand:

```
P.S.
```

Master:

```
assets/brand/ps-master.svg
```

Sidebar:

```
layouts/_partials/docs/brand.html
```

Sidebar size:

```
56 px
```

Current logo:

```
images/logo.webp
static/logo.webp
```

Current favicon:

```
images/favicon.svg
static/images/favicon.svg
```

Favicon configuration:

```
BookFavicon = "images/favicon.svg"
```

Favicon override:

```
layouts/_partials/docs/html-head-favicon.html
```

Theme files:

```
DO NOT EDIT
```

Generated `public/` files:

```
DO NOT EDIT MANUALLY
```

Legacy / separate references:

```
/images/pivtorak-studio-logo.webp
/favicon.svg
```

These require separate review before migration or deletion.

---

# 21. Maintenance Principle

The project follows this principle:

> ONE MASTER → CONTROLLED DERIVATIVES → VERIFIED REFERENCES

When the visual identity changes, do not replace files blindly.

First identify:

1. the master asset;
2. current derivatives;
3. Hugo template references;
4. Schema.org / JSON-LD references;
5. legacy references;
6. generated files.

Then update only the appropriate layer.

This prevents accidental breakage of structured data,  
historical content, and Hugo-generated output.



### Три різні рівні:

**🟢 Поточна система**

ps-master.svg
      ↓
logo.webp
      ↓
Schema.org

і

favicon.svg
      ↓
BookFavicon
      ↓
browser


**🟡 Старі посилання, які існують і не повинні зникнути випадково**

```
pivtorak-studio-logo.webp
/favicon.svg
```

**⚪ Генеровані копії**

```
public/...
```

— їх руками не чіпаємо.

Знайдені старі `logo.webp` у validation-папках:  не означає, що треба бігати й замінювати кожен файл, який називається `logo.webp`.**

Ще одна важлива знахідка: 
у трьох мовних версіях `Independent Researcher Manifesto` використовується саме **`pivtorak-studio-logo.webp`**, а не поточний `logo.webp`. 