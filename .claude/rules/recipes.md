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

## Commit messages

Commits are linted with `@commitlint/config-conventional` (see `.github/workflows/commitlint.yml`). Every commit on a recipe PR must use the Conventional Commits format, e.g. `feat: add <recipe> recipe`. Use `feat:` for new recipes/images, `fix:` for corrections, `chore:`/`docs:` for tooling and notes. Keep the subject lowercase.

## PR review workflow

When publishing a recipe, after opening its pull request, subscribe to the PR's activity (`subscribe_pr_activity`) so review comments and CI failures are auto-handled until the PR is merged or closed. Do this for every recipe PR going forward.

Once the required status checks are green — `commitlint` and the Netlify `deploy-preview` build — you have standing permission to merge the PR (squash) and then monitor the GitHub Pages build on `main` to confirm the site builds successfully. Copilot/AI review comments are advisory: address them if valid, but they do not block the merge.

## Minimize pushes per PR

Each push to a PR triggers a fresh Netlify Deploy Preview build (and the `commitlint` check), which costs build minutes and time. Keep pushes lean:

* Assemble all changes locally and push **once** per PR rather than pushing each small commit as you go.
* When addressing review feedback, batch the fixes into a single push.
* Avoid force-push churn; prefer one final amend/rebase over repeated re-pushes.
