---
name: recipe-organizer
description: Fetch recipes from any recipe video or post link (Xiaohongshu, YouTube, etc.), extract ingredients and steps, and save structured notes to an Obsidian vault. Use when the user shares recipe links and asks to organize or save a recipe.
---

# Recipe Organizer

Fetch recipes from recipe posts or videos, extract structured content, and save clean recipe notes to an Obsidian vault.

## Configuration

The user must configure these values in this file before first use:

```
VAULT_PATH=E:\Obsidian\ob库\电脑仓库        # absolute path to your Obsidian vault
RECIPES_FOLDER=Atlas-Knowledge/厨艺          # folder inside the vault for recipe notes
INDEX_FILE=Atlas-Knowledge/厨艺/0 食谱.md   # index file that lists all recipes
```

## Workflow

### Step 1 — Detect language

Determine the output language from context:
- If the user writes in **Chinese**, or the source content is primarily Chinese → use the **Chinese template**
- If the user writes in **English**, or the source content is primarily English → use the **English template**
- When in doubt, match the language of the recipe source

### Step 2 — Fetch page content

Use `mcp__claude-in-chrome__tabs_context_mcp` to check current tabs, create a new tab per link (`mcp__claude-in-chrome__tabs_create_mcp`), and navigate (`mcp__claude-in-chrome__navigate`).

- Try `mcp__claude-in-chrome__get_page_text` first for the main body text
- Fall back to `mcp__claude-in-chrome__read_page` (depth=5) if content is insufficient
- Note: video posts often have steps only in images — infer from comments and any visible text

### Step 3 — Analyse and consolidate

- Classify each link as a **recipe** or a **technique** (e.g. deboning, knife skills). Technique posts are not saved as separate notes — merge their content as steps or tips into the related recipe.
- Extract: dish name, ingredients + quantities, steps, prep/cook time, serving size, tips
- Multiple links may combine into one dish (e.g. technique video + recipe video)

### Step 4 — Write the note

Use the `Write` tool to create `<VAULT_PATH>/<RECIPES_FOLDER>/<dish name>.md`.

**Chinese template** (use when language is Chinese):

```markdown
# 菜名：[菜名]

> **描述**：[一句话描述，突出特色]
> **准备时间**：[X分钟] | **烹饪时间**：[X分钟] | **份量**：[X人份]

## 食材清单
- [ ] [食材]：[用量]

## 制作步骤
1. **[步骤名]**：[具体操作]

## 小贴士
- [关键注意事项或技巧]

## 来源
- [标题](链接)
```

**English template** (use when language is English):

```markdown
# [Dish Name]

> **Description**: [One-line description highlighting the dish's character]
> **Prep time**: [X min] | **Cook time**: [X min] | **Serves**: [X]

## Ingredients
- [ ] [Ingredient]: [Quantity]

## Steps
1. **[Step name]**: [Instructions]

## Tips
- [Key tips or cautions]

## Source
- [Title](link)
```

### Step 5 — Update the index

`Read` the index file first, then use `Edit` to append at the end.

Chinese: `## [[菜名]]`
English: `## [[Dish Name]]`

## Notes

- If quantities are not stated, use reasonable estimates and note "adjust to taste" (or "可根据口味调整") in tips
- Bold every step name for scannability
- Always keep the original source link
- If multiple posts support one dish, list all links in the source section
