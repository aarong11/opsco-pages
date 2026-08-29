# opsco-pages

The public site for OpsCo. **Everything in this repository is generated** — there is no
source here, and no history connecting it to the repository it is generated from.

Site: <https://aarong11.github.io/opsco-pages/>

## What is published, and what is not

| Published | Not published |
|---|---|
| Module names, purpose, and public signatures | Any function body |
| First line of each public docstring | Private names, defaults, literals |
| SHA-256 per module, and a root digest | Tests, fixtures, deployment configuration |
| Ceremony behaviour and design guidance | Any client name, live record, or production figure |

Default values are withheld deliberately: a default can carry a threshold, a path, or a
host that belongs on the private side.

## Verifying that the site describes the running code

Given a copy of the source under NDA, this reproduces the root digest:

```sh
find service opsco -name '*.py' ! -name '__init__.py' \
  | sort | xargs sha256sum -t | sha256sum
```

`-t` is text mode. Binary mode writes ` *path` instead of two spaces and yields a
different digest. On macOS use `xargs shasum -a 256 | shasum -a 256`.

Root digest for the current build:

```
5e2024bff00b2d041fbbc915c258e73563f3d1eafce096e5eb8ab275853c38fa
```

If it differs from the one on the [audit index](https://aarong11.github.io/opsco-pages/audit.html), you were not
given the code this site describes — which is worth knowing before reading anything
else on it.

## How it gets here

Pushed by CI from the private repository, after the test suite, the scenario rehearsal,
and a redaction scan have all passed. The deny list the scan runs against is never
published; a client name reaching a public page is a failed build rather than a
discovery.

Do not edit these files here — they are overwritten on the next build.

Build 2026.08.
