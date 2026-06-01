# zed-local-schema

This repo showcases a bug in Zed, where local JSON schemas will trigger `Invalid schema URI` on Windows.

## Reproduction Steps

1. Clone this repo.
2. Open this repo in Zed on Windows.
3. Open `data.json` and observe the warning.

```
Unable to load schema from 'C:\path\to\zed-local-schema\./schema.json': Invalid schema URI: C:\path\to\zed-local-schema\./schema.json. (768)
```

And if `schemas.url` is set to `schema.json` (instead of `./schema.json`):

```
Unable to load schema from '\schema.json': ENOENT: no such file or directory, open 'D:\schema.json'. (768)
```

## Data Source

Example data taken from [json-schema.org](https://json-schema.org/learn/getting-started-step-by-step#validate-json-data-against-the-schema).
