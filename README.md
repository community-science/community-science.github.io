# Leibniz Pages

This repository is a thin GitHub Pages deployment for the Leibniz console.

It owns only deployment policy:

- which Leibniz checkout to build,
- which Hugging Face result repositories to include,
- when the static page rebuilds,
- the GitHub Pages publishing workflow.

The Leibniz application code, result validation, console data generation, and
web UI live in `community-science/leibniz`.

## Sources

Edit `sources.json` to change the public result repositories included in the
published console.

Each enabled Hugging Face source is cloned during the Pages workflow and passed
to the Leibniz console build as a result-view root. The workflow treats dispatch
payloads as rebuild notifications only; every run rebuilds from the current
configured sources.

## Triggers

The Pages workflow runs on:

- pushes to this repository,
- manual dispatch,
- repository dispatch events from `community-science/leibniz`,
- repository dispatch events sent by an external Hugging Face webhook bridge,
- an hourly schedule as a reliability backstop.

`community-science/leibniz` must define `LEIBNIZ_PAGES_DISPATCH_TOKEN` with
permission to dispatch events to this repository.

If any configured Hugging Face repositories are private or rate-sensitive, add
`HF_TOKEN` as an Actions secret in this repository.
