# opsco-pages

The public site for OpsCo. **Everything in this repository is generated** — there is no
source here, and there is no history connecting it to the repository it is generated
from.

## What is published, and what is not

| Published | Not published |
|---|---|
| Module names, purpose, and public signatures | Any function body |
| First line of each public docstring | Private names, defaults, literals |
| SHA-256 per module, and a root digest | Tests, fixtures, deployment config |
| Ceremony behaviour and design guidance | Any client name, live record, or production figure |

Default values are withheld deliberately: a default can carry a threshold, a path, or a
host that belongs on the private side.

## Verifying that the site describes the running code

The site publishes a root digest over the modules it describes. Given a copy of the
source under NDA, this reproduces it:

```sh
find service opsco -name '*.py' ! -name '__init__.py'   | sort | xargs sha256sum -t | sha256sum
```

`-t` is text mode. Binary mode writes ` *path` instead of two spaces and yields a
different digest. On macOS use `xargs shasum -a 256 | shasum -a 256`.

Root digest for the current build:

```
aabc9c6a8f86452d4d86be60c6d57ad91541a7fc0d962b491aa065547629089a
```

If it differs from the one on the [audit index](https://aarong11.github.io/opsco-pages/audit.html),
you were not given the code this site describes — which is worth knowing before reading
anything else on it.

## How it gets here

Pushed by CI from the private repository after the test suite, the scenario rehearsal,
and a redaction scan all pass. The scan runs against a deny list that is never published;
a client name reaching a public page is a failed build rather than a discovery.

Do not edit these files here. Changes are overwritten on the next build.
