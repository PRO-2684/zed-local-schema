# zed-local-schema

This repo showcases a bug in Zed, where local JSON schemas specified in `settings.json` won't work.

## Reproduction Steps

1. Clone this repo.
2. Open this repo in Zed on Windows. (version 1.4.4, commit 1d0b482638588e5507184d91631e30596339ee1b)
3. Open `data.json` and observe the warning.

## Problem

On Windows, the following warning is shown:

```
Unable to load schema from 'C:\path\to\zed-local-schema\./schema.json': Invalid schema URI: C:\path\to\zed-local-schema\./schema.json. (768)
```

And if `schemas.url` is set to `schema.json` (instead of `./schema.json`):

```
Unable to load schema from '\schema.json': ENOENT: no such file or directory, open 'D:\schema.json'. (768)
```

On Linux, there's no warning, but the schema feature is not activated (like auto-completion). With `$schema` key, however, is correctly resolved in both platforms.

## Summary Table

| Platform | Method          | Result         |
| -------- | --------------- | -------------- |
| Windows  | `settings.json` | 🔴 Warning     |
| Linux    | `settings.json` | 🔴 Silent Fail |
| Windows  | `$schema`       | 🟢 Success     |
| Linux    | `$schema`       | 🟢 Success     |

## Data Source

Example data taken from [json-schema.org](https://json-schema.org/learn/getting-started-step-by-step#validate-json-data-against-the-schema).
