# Google Scholar Indexing Implementation Guide

> Repository: `riasatislam/riasatislam.github.io`  
> Website: `https://riasatislam.com/`  
> Stack: Hugo Blox Academic CV  
> Purpose: implementation handoff for a future AI coding agent  
> Last reviewed: 24 July 2026

## Objective

Make each individual publication page under `/publication/<slug>/` technically eligible for discovery and correct bibliographic parsing by Google Scholar.

This cannot guarantee inclusion. Google Scholar controls crawling, parsing, version grouping, and indexing. The goal is to remove preventable technical barriers and follow Google's published inclusion guidance:

- <https://scholar.google.com/intl/en/scholar/inclusion.html>
- <https://scholar.google.com/intl/en/scholar/help.html>

## Current repository observations

The repository currently uses Hugo Blox Academic CV. Its production URL is configured as `https://riasatislam.com/`, automatic `robots.txt` generation is enabled, and publication records are stored as page bundles such as:

```text
content/publication/islam-critical-thinking-generative-ai-2026/index.md
```

The inspected example contains a title, author, date, conference name, DOI, a short one-sentence abstract, and external DOI/QMRO links. It does not contain a locally hosted PDF. No repository-level implementation of Google Scholar Highwire Press `citation_*` metadata was identified during the initial review.

The production build command is:

```bash
npm run build:site
```

which runs:

```bash
hugo --gc --minify
```

## Core requirements

Each scholarly output must have its own unique HTML landing page. The main `/publication/` page is a browse page and must not be represented as one scholarly paper.

Every individual publication page should contain, in server-rendered HTML:

```html
<meta name="citation_title" content="Exact paper title">
<meta name="citation_author" content="First author">
<meta name="citation_author" content="Second author">
<meta name="citation_publication_date" content="YYYY/MM/DD">
```

Where relevant, also emit:

```html
<meta name="citation_doi" content="10.xxxx/xxxxx">
<meta name="citation_journal_title" content="Journal title">
<meta name="citation_conference_title" content="Conference title">
<meta name="citation_issn" content="....-....">
<meta name="citation_isbn" content="...">
<meta name="citation_volume" content="12">
<meta name="citation_issue" content="3">
<meta name="citation_firstpage" content="101">
<meta name="citation_lastpage" content="119">
<meta name="citation_technical_report_institution" content="Institution">
<meta name="citation_technical_report_number" content="Report number">
```

Rules:

- exactly one `citation_title`;
- one `citation_author` tag per author;
- exactly one `citation_publication_date`;
- no empty tags;
- no invented metadata;
- no duplicate tags from both the theme and a custom override;
- tags must be present in **View Page Source**, not injected later by JavaScript;
- emit tags only on individual publication pages.

## Complete abstracts

Google Scholar requires the full text or the complete author-written abstract to be freely visible on the landing page. A short descriptive sentence is not sufficient.

For every publication:

1. Obtain the official abstract from the manuscript or authoritative publication record.
2. Put it in the front-matter `abstract` field.
3. Keep any short description in `summary`.
4. Ensure the complete abstract is visible without login, accordions, or interstitials.
5. Never use AI to invent or expand a missing official abstract.

The current record below needs this correction:

```text
content/publication/islam-critical-thinking-generative-ai-2026/index.md
```

## Local PDFs

Where legally permitted, store a searchable manuscript PDF in the same page bundle:

```text
content/
└── publication/
    └── <slug>/
        ├── index.md
        └── paper.pdf
```

The deployed URLs should be:

```text
https://riasatislam.com/publication/<slug>/
https://riasatislam.com/publication/<slug>/paper.pdf
```

Then emit:

```html
<meta name="citation_pdf_url" content="https://riasatislam.com/publication/<slug>/paper.pdf">
```

Only emit `citation_pdf_url` for a local PDF in the same publication subdirectory. Do not point it to ResearchGate, QMRO, Zenodo, or a publisher site.

The PDF must:

- be publicly accessible without authentication or interstitials;
- end in `.pdf`;
- contain searchable text;
- normally be under 5 MB;
- show the exact title prominently on the first page;
- list authors immediately below the title;
- contain a `References` or `Bibliography` section where applicable;
- be a version the author is legally allowed to share.

Do not automatically upload publisher-formatted PDFs. Depending on the licence and publisher policy, the permissible version may be the preprint, submitted manuscript, author accepted manuscript, or openly licensed Version of Record. Where rights are unclear, omit the local PDF and document the issue.

## Recommended front matter

Reuse existing Hugo Blox fields where unambiguous. Add an optional `scholar` block for precise Scholar metadata.

```yaml
---
title: "Understanding Critical Thinking Skills with Generative AI in a Transnational Education Setting"
authors:
  - Riasat Islam
date: "2026-04-27"
publishDate: "2026-07-10T00:00:00+01:00"
publication_types:
  - paper-conference
publication: "2026 IEEE Global Engineering Education Conference (EDUCON)"
hugoblox:
  ids:
    doi: 10.1109/EDUCON67543.2026.11574197

abstract: >-
  Replace this with the complete official author-written abstract.

scholar:
  type: conference-paper
  publication_date: "2026/04/27"
  authors:
    - Riasat Islam
  conference_title: "2026 IEEE Global Engineering Education Conference (EDUCON)"
  doi: "10.1109/EDUCON67543.2026.11574197"
  firstpage: "1"
  lastpage: "9"
  pdf: "paper.pdf"

url_pdf: "paper.pdf"
---
```

Notes:

- `date` should be the date used when citing the work, not the date the website record was added.
- `publishDate` may remain the website publication date.
- Omit unknown fields rather than adding placeholders in production.
- Remove Markdown formatting such as `*Journal Name*` from metadata output.

## Hugo template implementation

First inspect the installed Hugo/Hugo Blox version and locate the actual head-end hook:

```bash
hugo mod graph
hugo mod vendor
rg -n "head-end|hooks/head|</head>" _vendor layouts
```

Likely conventions include:

```text
layouts/partials/hooks/head-end/google-scholar.html
```

or:

```text
layouts/_partials/hooks/head-end/google-scholar.html
```

Use only the convention actually invoked by the installed version. Do not create both blindly.

Before adding a custom template, build and check whether the theme already emits Scholar metadata:

```bash
npm install
npm run build:site
rg -n "citation_(title|author|publication_date|pdf_url)" public/publication
```

Suggested logic, to be adapted to the installed Hugo APIs:

```go-html-template
{{- if and .IsPage (eq .Section "publication") -}}
  {{- $scholar := dict -}}
  {{- with .Params.scholar }}{{ $scholar = . }}{{ end -}}

  <meta name="citation_title" content="{{ .Title | plainify | htmlEscape }}">

  {{- $authors := .Params.authors -}}
  {{- with index $scholar "authors" }}{{ $authors = . }}{{ end -}}
  {{- range $authors }}
    <meta name="citation_author" content="{{ . | plainify | htmlEscape }}">
  {{- end }}

  {{- $publicationDate := .Date.Format "2006/01/02" -}}
  {{- with index $scholar "publication_date" }}{{ $publicationDate = . }}{{ end -}}
  <meta name="citation_publication_date" content="{{ $publicationDate }}">

  {{- $doi := "" -}}
  {{- with index $scholar "doi" -}}
    {{- $doi = . -}}
  {{- else -}}
    {{- with .Params.hugoblox -}}
      {{- with .ids -}}
        {{- with .doi }}{{ $doi = . }}{{ end -}}
      {{- end -}}
    {{- end -}}
  {{- end -}}
  {{- with $doi }}
    <meta name="citation_doi" content="{{ . | htmlEscape }}">
  {{- end }}

  {{- with index $scholar "journal_title" }}
    <meta name="citation_journal_title" content="{{ . | plainify | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "conference_title" }}
    <meta name="citation_conference_title" content="{{ . | plainify | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "volume" }}
    <meta name="citation_volume" content="{{ . | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "issue" }}
    <meta name="citation_issue" content="{{ . | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "firstpage" }}
    <meta name="citation_firstpage" content="{{ . | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "lastpage" }}
    <meta name="citation_lastpage" content="{{ . | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "technical_report_institution" }}
    <meta name="citation_technical_report_institution" content="{{ . | plainify | htmlEscape }}">
  {{- end }}
  {{- with index $scholar "technical_report_number" }}
    <meta name="citation_technical_report_number" content="{{ . | htmlEscape }}">
  {{- end }}

  {{- $pdfName := "paper.pdf" -}}
  {{- with index $scholar "pdf" }}{{ $pdfName = . }}{{ end -}}
  {{- with .Resources.GetMatch $pdfName }}
    <meta name="citation_pdf_url" content="{{ .Permalink }}">
  {{- end }}
{{- end -}}
```

The generated output matters more than exact adherence to this sample.

## Crawlability checks

After deployment, verify:

```bash
curl -L https://riasatislam.com/robots.txt
curl -Ls https://riasatislam.com/publication/<slug>/ | rg -i "noindex|nofollow|citation_"
curl -Ls https://riasatislam.com/sitemap.xml | rg "/publication/"
curl -I https://riasatislam.com/publication/<slug>/paper.pdf
```

Requirements:

- no `noindex` on publication pages;
- publications and PDFs not blocked by `robots.txt`;
- every publication page included in the sitemap;
- ordinary HTML links from the browse page to each record;
- one canonical domain, preferably `https://riasatislam.com/`;
- PDF returns HTTP 200 and `Content-Type: application/pdf`.

## Build and validation

Run:

```bash
npm install
npm run build:site
```

Inspect a pilot page:

```bash
PAGE="public/publication/islam-critical-thinking-generative-ai-2026/index.html"

rg -n "citation_title" "$PAGE"
rg -n "citation_author" "$PAGE"
rg -n "citation_publication_date" "$PAGE"
rg -n "citation_doi" "$PAGE"
rg -n "citation_conference_title" "$PAGE"
rg -n "citation_pdf_url" "$PAGE"
```

Check duplicates:

```bash
rg -o 'name="citation_title"' "$PAGE" | wc -l
rg -o 'name="citation_publication_date"' "$PAGE" | wc -l
```

Each should return `1`.

Run locally and inspect **View Page Source**:

```bash
hugo server --disableFastRender
```

## Automated audit script

Add a script such as:

```text
scripts/check_google_scholar_metadata.py
```

It should inspect `public/publication/*/index.html` and report:

- missing or duplicated title/date tags;
- missing authors;
- empty metadata values;
- `noindex` directives;
- missing or suspiciously short visible abstracts;
- non-absolute PDF URLs;
- PDFs outside the publication subdirectory;
- referenced local PDFs that do not exist;
- PDFs larger than 5 MB;
- duplicate canonical URLs;
- accidental duplicate titles.

Missing PDFs should not fail the build where no legal local PDF is available. Missing required HTML metadata should fail.

Suggested workflow:

```bash
npm run build:site
python3 scripts/check_google_scholar_metadata.py public/publication
```

## Publication inventory

Generate an inventory of all directories under `content/publication/` with:

| Field | Meaning |
|---|---|
| Slug | Directory name |
| Title | Exact title |
| Authors complete | Yes/No |
| Citation date present | Yes/No |
| Full abstract present | Yes/No/Review |
| DOI | DOI or blank |
| Output type | Journal/conference/preprint/report/etc. |
| Venue metadata complete | Yes/No/N/A |
| Local PDF present | Yes/No |
| PDF rights checked | Yes/No/Unknown |
| Scholar tags generated | Yes/No |
| Manual action required | Description |

Do not expose private notes or copyrighted material in the public site.

## Rollout plan

### Phase 1: Pilot

Use:

```text
content/publication/islam-critical-thinking-generative-ai-2026/
```

1. Replace the short abstract with the complete official abstract.
2. Add accurate Scholar metadata.
3. Add a legal local PDF only after rights verification.
4. Implement the head metadata partial.
5. Build and validate.
6. Inspect deployed HTML source.

### Phase 2: Audit all records

List records needing human input, especially missing abstracts, dates, authors, page ranges, document types, and PDF rights decisions.

### Phase 3: Safe bulk changes

Bulk-update only information verifiable from front matter, local files, DOI metadata, or authoritative records. Never guess.

### Phase 4: Deploy and request recrawling

After deployment:

1. submit the sitemap in Google Search Console;
2. request indexing for a small sample of pages and PDFs;
3. search Google Scholar using exact paper titles after allowing time for crawling;
4. do not use Scholar's `site:` count as the sole coverage measure.

Search Console helps diagnose ordinary Google crawling. It is not a direct Google Scholar submission system.

## Instructions for a future AI coding agent

1. Read this file completely.
2. Inspect installed Hugo and Hugo Blox versions.
3. Build the current site before editing.
4. Check generated metadata to avoid duplicates.
5. Find the correct local head-end hook.
6. Add server-rendered Highwire Press metadata only to individual publication pages.
7. Use existing front matter as fallbacks and `scholar` for precise values.
8. Update one pilot publication first.
9. Add an automated audit script.
10. Run the production build and audit.
11. Produce an inventory of records requiring human-supplied metadata or copyright decisions.
12. Never invent metadata or upload PDFs without verified rights.
13. Preserve the existing design and publication functionality.
14. In the pull request, summarise changed files, validation results, and unresolved records.

## Pull-request checklist

- [ ] Site builds before and after changes.
- [ ] Correct Hugo Blox head hook identified.
- [ ] No duplicate `citation_*` tags.
- [ ] Required title, author, and date tags are generated.
- [ ] DOI, venue, pagination, and report tags are accurate where applicable.
- [ ] `citation_pdf_url` is emitted only for a legal local PDF.
- [ ] PDF URL is absolute and in the same publication subdirectory.
- [ ] Complete official abstract is visible on the pilot page.
- [ ] No `noindex` on publication pages.
- [ ] Publication pages appear in the sitemap.
- [ ] Browse page uses ordinary HTML links.
- [ ] Automated metadata audit passes.
- [ ] Historical records requiring manual work are documented.
- [ ] No publisher PDF was added without permission.
- [ ] Deployed HTML source was inspected.

## Expected architecture

```text
/publication/                         # Browse page, not a paper record
/publication/paper-one/               # Scholar-compatible landing page
/publication/paper-one/paper.pdf      # Optional legal manuscript
/publication/paper-two/               # Scholar-compatible landing page
/publication/paper-two/paper.pdf      # Optional legal manuscript
```

The key principle is to optimise for accurate, stable, machine-readable scholarly records rather than merely adding many metadata tags.
