# Pivtorak.Studio — Shared Site Footer

The language-aware service and contact footer is maintained in
`layouts/_partials/docs/site-footer.html`. Its text is stored under the
`studio_footer_*` keys in `i18n/en.yaml`, `i18n/uk.yaml`, `i18n/pt.yaml`, and
`i18n/ru.yaml`. The Russian strings are retained for future use; Russian stays
disabled in `hugo.toml`.

Standard Hugo Book pages receive the partial through the theme's
`docs/inject/footer` hook, overridden at
`layouts/_partials/docs/inject/footer.html`. The landing layout suppresses the
standard footer block, so `layouts/landing.html` invokes the same partial in
that block. Keep all footer markup in the shared partial; do not edit the theme.
Its responsive styling lives in `assets/_custom.scss`.

## Approved design rationale

The footer stays within the main content column rather than spanning the
viewport. It is a permanent, understated service and contact block, not a
second promotional banner. The top Research on Request banner and bottom
footer serve different purposes; normal scrolling keeps them at separate
stages, so they do not compete for attention.

For the top banner's role and layout, see
[`DEVELOPER_NOTES_top_area.md`](DEVELOPER_NOTES_top_area.md).
