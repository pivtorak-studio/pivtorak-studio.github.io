# DEVELOPER NOTES — Publication Dates and Time Zones

**Project:** Pivtorak.Studio  
**Scope:** Hugo Front Matter, scheduled publications, Timeline  
**Status:** Established working rule  
**Last updated:** 2026-10-09

---

## 1. Purpose

This document defines how dates and time zones must be handled when preparing scheduled publications for Pivtorak.Studio.

The objective is to ensure that:

- scheduled articles become available at the intended local time;  
- local builds and GitHub Actions interpret publication dates consistently;  
- daylight saving time is taken into account;  
- Timeline dates and publication dates remain semantically distinct;  
- existing content is not modified unnecessarily.  

## 2. Core Rule

**Every newly scheduled future publication must include an explicit UTC offset in its date-time fields.**

For publications scheduled according to mainland Portugal local time, use the applicable seasonal offset:

|Period|Offset|Example|
|---|---|---|
|Western European Summer Time (WEST)|`+01:00`|`2026-10-09T03:00:00+01:00`|
|Western European Time (WET)|`+00:00`|`2026-12-09T03:00:00+00:00`|

Do not assume that the same offset applies throughout the year.

The examples above illustrate the seasonal rule for mainland Portugal. The applicable offset must correspond to the intended publication date.

### Why the explicit offset matters

A date-time without an offset, such as:

```
date: 2026-10-09T03:00:00
```

does not explicitly identify the intended time zone.

An explicit offset removes this ambiguity:

```
date: 2026-10-09T03:00:00+01:00
```

Hugo may interpret date-time values differently depending on the configured time zone and build environment. The explicit offset identifies the intended instant independently of the machine's local time zone.

## 3. Front Matter Fields

The following fields have distinct purposes.

|Field|Purpose|
|---|---|
|`date`|Hugo's standard content date; can determine when a page is published.|
|`publication_date`|Project-specific publication metadata used by custom site functionality.|
|`event_date`|Project-specific date of the event or occurrence represented by the article.|
|`lastmod`|Date of the most recent modification.|

For a scheduled article, ensure that `date` contains the intended publication instant. Keep `publication_date` consistent with the actual publication schedule where the project requires it.

Use an explicit offset in the date-time fields when they represent the same scheduled local-time event.

Do not automatically assume that `event_date` must equal `date`: an article may describe an event that occurred at a different time.

Likewise, update `lastmod` when the content is modified rather than treating it as an independent publication scheduler.

## 4. Recommended Front Matter Format

Example: an article scheduled for 03:00 mainland Portugal time on 9 October 2026.

```
event_date: 2026-10-09T03:00:00+01:00
publication_date: 2026-10-09T03:00:00+01:00
date: 2026-10-09T03:00:00+01:00
lastmod: 2026-10-09T03:00:00+01:00
draft: false
```

For an article scheduled for 03:00 on 9 December 2026, use `+00:00` instead.

Preserve the project's existing field names and metadata conventions. Do not introduce a new field merely to store the UTC offset.

## 5. Incident Record: ESMÉE Laboratory Publications

**Date:** 9 October 2026

Three articles were prepared for publication:

- `03-01-world-laboratory`  
- `03-02-problem-laboratory`  
- `03-03-destiny-laboratory`  

Initially, the date-time fields had no explicit UTC offset.

During investigation:

1. GitHub Actions completed successfully.  
2. `hugo list future` identified the third article as a future publication.  
3. A local Hugo build generated the first two articles but did not generate the third article at the expected output path.  
4. The scheduled date-time fields were updated to include `+01:00`.  
5. The changes were committed and pushed.  
6. GitHub Actions completed successfully again.  
7. The first two articles appeared on the published site, while the third remained scheduled for its later publication time.  

This incident established the practical importance of specifying the intended time zone for scheduled publications.

**Operational lesson:** A successful build does not guarantee that a future-dated article has been included in the generated site.

## 6. Publication Workflow

Before pushing a scheduled article:

1. **Check the intended local publication time.** Confirm the date and time in mainland Portugal.  
2. **Determine the applicable seasonal offset.** Use `+01:00` during summer time and `+00:00`   during winter time.  
3. **Check the Front Matter.** Ensure that `date` contains the intended publication instant and that related project-specific fields are consistent.  
4. **Inspect future pages.** Run:  
    ```
    hugo list future
    ```
    Confirm that pages scheduled for later publication remain future-dated and that pages intended for immediate publication are not unexpectedly listed.  
5. **Build the site.** Run:  
    ```
    hugo
    ```
6. **Check the output.** If necessary, verify that the expected HTML file exists in `public`.  
7. **Commit and push.** Confirm that GitHub Actions completes successfully.  
8. **Verify deployment.** Check the published URL when the article is expected to be available.  

Do not rely on the passage of time alone to publish a static Hugo page. A new build and deployment may be necessary after the scheduled publication time.

## 7. Existing Content

This rule applies primarily to newly scheduled future publications.

- Do not mass-edit historical Front Matter solely to append UTC offsets.  
- Do not change existing Timeline data without first verifying how the Timeline interprets and displays its dates.  
- Do not assume that every date field represents a publication schedule.  
- Investigate existing pages individually when a date or time discrepancy is observed.  

The purpose is to establish predictable publication behavior without introducing unnecessary changes across the content archive.

## 8. Relationship with Timeline

Timeline and publication scheduling serve different purposes.

- `date` participates in Hugo's content publication behavior.  
- `publication_date` records publication metadata for project-specific functionality.  
- `event_date` describes the relevant event or occurrence.  
- Timeline rendering and sorting must follow the conventions implemented by the project's Timeline functionality.  

An explicit UTC offset can help preserve the intended instant, but it does not by itself determine how a custom Timeline formats or displays that instant.

Any future changes to Timeline date normalization must preserve the distinction between event time and publication time.

## 9. Maintenance Rule

Whenever the publication workflow, Hugo configuration, or Timeline date processing changes:

- verify the applicable time-zone behavior;  
- test at least one scheduled future article;  
- check `hugo list future` and the generated HTML;  
- verify the deployment result;  
- update this document if the established rule changes.  

**Final rule:** For newly scheduled publications, specify an explicit UTC offset appropriate to mainland Portugal on the intended publication date. Validate the result through Hugo's future-page listing, local build, and deployment checks.