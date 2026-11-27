---
name: update-github-info
description: Refresh the GitHub Info page with practical updates from official GitHub sources.
intent: Keep Mona's GitHub Info page current with concise, practical guidance backed by official GitHub sources.
on:
  schedule: daily
  workflow_dispatch:
  skip-if-match: 'is:pr is:open "gh-aw-workflow-id: update-github-info" in:body'
permissions:
  contents: read
  pull-requests: read
checkout:
  fetch-depth: 1
strict: true
engine:
  id: copilot
  copilot-sdk: true
network:
  allowed:
    - github.blog
    - github.com
tools:
  edit: true
  web-fetch: {}
safe-outputs:
  create-pull-request:
    title-prefix: "[github-info] "
    reviewers:
      - monalisa
    draft: false
    max: 1
    allowed-files:
      - site/content/github-info.md
---

# Update GitHub Info

Read `notes/mona-notes.md` and the current `site/content/github-info.md` before
making changes. Follow Mona's editorial guidance: keep updates short and
practical, help developers learn GitHub faster, and cite the source for every
item drawn from the GitHub Blog or Changelog.

Use the web-fetch tool to read both:

- https://github.blog/latest/
- https://github.blog/changelog/

Select only recent, useful items supported by those pages. Update
`site/content/github-info.md` with concise summaries and direct source links,
preserving its existing structure and editorial voice. Edit no other files.

If neither source contains a sufficiently useful update, or the page already
reflects the relevant updates, make no changes and call `noop` with a brief
reason. Otherwise, propose the change through the configured
`create-pull-request` safe output and request review from Mona. Never write
directly to the default branch or create a pull request through shell commands,
GitHub APIs, or other write tools.
