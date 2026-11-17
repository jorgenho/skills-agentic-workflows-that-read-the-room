---
name: update-github-info
description: Propose concise, source-backed updates to Mona's GitHub Info website.
intent: Keep Mona's GitHub Info website current with practical, source-backed GitHub guidance for developers.
strict: true
on:
  schedule: daily
  workflow_dispatch:
permissions:
  contents: read
  pull-requests: read
  copilot-requests: write
engine:
  id: copilot
  copilot-sdk: true
tools:
  edit: true
  web-fetch:
  github:
    mode: gh-proxy
    toolsets: [pull_requests]
network:
  allowed:
    - github.blog
    - github.com
safe-outputs:
  create-pull-request:
    allowed-files:
      - site/content/github-info.md
    draft: false
    max-patch-files: 1
---

# Update Mona's GitHub Info

Read `notes/mona-notes.md` and the existing `site/content/github-info.md` first.
Fetch both https://github.blog/latest/ and https://github.blog/changelog/ with
the web-fetch tool. Use only relevant, verifiable information from those
official sources; include source links for any additions.

Update `site/content/github-info.md` with concise, practical guidance that helps
developers learn GitHub faster. Preserve useful existing content, avoid
repeating information already covered, and make only evidence-backed changes.
Do not edit any other file.

Before proposing a pull request, check for an existing open pull request that
already updates this file and avoid creating a duplicate. Open a pull request for Mona to review.
Do not write changes directly to the default branch. Use only the configured
`create-pull-request` safe output, which is restricted to
`site/content/github-info.md`.

If neither source contains a useful update, the evidence is insufficient, or an
equivalent update is already proposed, make no changes and call `noop` with a
brief reason.
