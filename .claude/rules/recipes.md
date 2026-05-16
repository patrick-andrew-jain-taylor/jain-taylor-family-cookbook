---
paths:
  - "_recipes/**/*.md"
---

# Recipe File Rules

## Frontmatter

```yaml
---
author: pjt
title: <Title Case Recipe Name>
image:
  path: /assets/img/<slug>.jpg
  thumbnail: /assets/img/<slug>-300x400.jpg
  caption: "<Short description of the image>"
categories: [<Category>]
tags: [<Tag>]
---
```

Omit the `image:` block entirely if there is no photo.

**Valid categories** (must match `_config.yml` exactly):
Appetizers, Breakfast, Desserts, Drinks, Entrees, Miscellaneous, Seasonings, Side Dishes, Soups

**Valid tags** (must match `_config.yml` exactly):
Meat, Vegan, Vegetarian

## Kramdown table rule

Always put a blank line between a heading and a markdown table. Without it, Kramdown renders the table as raw pipe-separated text.

**Correct:**
```markdown
### Juice

| Ingredient | Quantity |
|:-:|:-:|
| Apple | 1 |
```

**Broken:**
```markdown
### Juice
| Ingredient | Quantity |
|:-:|:-:|
| Apple | 1 |
```

This applies to every `##` and `###` heading that precedes a table, including multi-section recipes with separate ingredient tables per section.

## File naming

Filename must be the recipe title lowercased with spaces replaced by hyphens: `my-recipe-name.md`. This slug is also used for image filenames and the URL permalink.

## Permalink pattern

`/recipes/<category-lowercase>/<slug>/` — derived automatically by Jekyll from the frontmatter.
