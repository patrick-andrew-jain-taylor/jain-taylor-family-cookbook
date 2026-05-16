# Add a Recipe to the Family Cookbook

Add a new recipe to the jain-taylor-family-cookbook Jekyll site, including image processing, correctly structured markdown, a conventional commit, and a PR ready for Sourcery review.

## Arguments

`$ARGUMENTS` — recipe title and/or details. If not provided, ask the user for the recipe name, ingredients, and instructions before proceeding.

## Steps

### 1. Gather recipe details

If `$ARGUMENTS` doesn't include enough information, ask the user for:
- Recipe title
- Ingredients (can be a list; you'll structure them into a table)
- Instructions (numbered steps)
- Category (one of: Appetizers, Breakfast, Desserts, Drinks, Entrees, Miscellaneous, Seasonings, Soups, Side Dishes)
- Tags (one or more of: Vegetarian, Vegan, Meat)
- Author (`pjt` unless specified otherwise)
- A photo, if they have one (ask them to provide the file path, e.g. via `@/path/to/image.png`)

### 2. Process the image (if provided)

Images go in `assets/img/`. The slug is the recipe title lowercased with spaces replaced by hyphens.

```bash
# Full-size JPEG
sips -s format jpeg <input> --out assets/img/<slug>.jpg

# Thumbnail — portrait 300×400 (note: sips -z takes height then width)
sips -s format jpeg -z 400 300 <input> --out assets/img/<slug>-300x400.jpg
```

### 3. Create the recipe file

Create `_recipes/<slug>.md`. Use this structure exactly:

```markdown
---
author: pjt
title: <Title>
image:
  path: /assets/img/<slug>.jpg
  thumbnail: /assets/img/<slug>-300x400.jpg
  caption: "<Short description of the image>"
categories: [<Category>]
tags: [<Tag>]
---

<One-sentence description of the recipe.>

## Ingredients

**CRITICAL — Kramdown rule:** always put a blank line between a heading (`###`, `##`, etc.) and a table. Without it, the table renders as raw pipe text in the browser.

### <Section name, e.g. "Sauce"> (omit section heading if there's only one ingredient list)

| Ingredient | Quantity |
|:-:|:-:|
| <Ingredient> | <Amount> |

## Instructions

### <Section name> (omit if only one section)
1. Step one.
2. Step two.
```

If there is no image, omit the `image:` block entirely.

### 4. Commit and open a PR

Use conventional commit format:

```
feat: add <recipe title> recipe
```

Branch name: `feat/add-<slug>`

After pushing and opening the PR, monitor for the Sourcery review. When Sourcery comments, retrieve their "Prompt for AI Agents" section and address all feedback before requesting merge.
