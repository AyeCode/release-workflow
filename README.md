# release-workflow

Shared GitHub workflow that releases an AyeCode plugin to api.ayecode.io when a tag is pushed.

Each add-on repo carries a one-file caller (`.github/workflows/release.yml`) naming its slug; see `ayecode-platform/release/caller.yml`. The tagged tree is the product: it is zipped with `git archive` (export-ignore honoured) and `.distignore` applied, the plugin header `Version` must equal the tag, and the zip plus `readme.txt` are posted to `POST /v1/releases` with the org secret `AYECODE_RELEASE_TOKEN`. The API stores the zip in R2 and updates the product's version and changelog. Tags containing `-beta` set the beta version only.
