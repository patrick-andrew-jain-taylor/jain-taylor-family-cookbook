---
paths:
  - "assets/img/**"
---

# Recipe Image Rules

## Required files per recipe

Two image files per recipe, both JPEG:

| File | Purpose |
|:-:|:-:|
| `assets/img/<slug>.jpg` | Full-size image |
| `assets/img/<slug>-300x400.jpg` | Thumbnail (portrait 300×400) |

The slug matches the recipe filename without the `.md` extension.

## Processing with sips (macOS)

Convert a source PNG or JPEG to the required files:

```bash
# Full-size JPEG
sips -s format jpeg <source> --out assets/img/<slug>.jpg

# Thumbnail — portrait 300×400 (note: -z takes height then width)
sips -s format jpeg -z 400 300 <source> --out assets/img/<slug>-300x400.jpg
```

## Frontmatter reference

```yaml
image:
  path: /assets/img/<slug>.jpg
  thumbnail: /assets/img/<slug>-300x400.jpg
  caption: "<Short description of the image>"
```
