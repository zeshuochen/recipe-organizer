---
name: recipe-organizer
description: Fetch recipes from Xiaohongshu, YouTube, or Bilibili links, extract ingredients and steps, and save structured notes to an Obsidian vault. Use when the user shares recipe links and asks to organize or save a recipe.
---

# Recipe Organizer

Fetch recipes from recipe posts or videos (Xiaohongshu, YouTube, Bilibili), extract structured content, and save clean recipe notes to an Obsidian vault.

## Configuration

Edit these values before first use:

```
VAULT_PATH=C:\Users\you\MyVault     # absolute path to your Obsidian vault
RECIPES_FOLDER=Recipes              # folder inside the vault for recipe notes
INDEX_FILE=Recipes/index.md         # optional: index file listing all recipes; delete this line to skip indexing
```

## Workflow

### Step 1 — Detect language

Determine the output language from context:
- User writes in **Chinese**, or source is primarily Chinese (Xiaohongshu / Bilibili) → use the **Chinese template**
- User writes in **English**, or source is primarily English (YouTube / English sites) → use the **English template**
- When in doubt, match the language the user wrote in

### Step 2 — Fetch page content

Use `mcp__claude-in-chrome__tabs_context_mcp` to check current tabs, create a new tab per link (`mcp__claude-in-chrome__tabs_create_mcp`), and navigate (`mcp__claude-in-chrome__navigate`).

Try `mcp__claude-in-chrome__get_page_text` first; fall back to `mcp__claude-in-chrome__read_page` (depth=5) if content is sparse.

**Platform-specific notes:**

- **Xiaohongshu**: Steps are often only in images — infer from comments and visible body text
- **YouTube**: Description box usually contains full ingredient list and timestamps; also check pinned comments
- **Bilibili**: Description and pinned comments are the main sources; step details may be in video chapters

### Step 3 — Analyse and consolidate

- Classify each link as a **recipe** or a **technique** (e.g. knife skills, deboning). Technique posts are not saved separately — merge their content as steps or tips into the related recipe.
- Extract: dish name, ingredients + quantities, steps, prep/cook time, serving size, tips
- Multiple links may combine into one dish (e.g. technique video + recipe video)

### Step 4 — Write the note

Use the `Write` tool to create `<VAULT_PATH>/<RECIPES_FOLDER>/<dish name>.md`.

**Chinese template:**

```markdown
# 菜名：[菜名]

> **描述**：[一句话描述，突出特色]
> **准备时间**：[X分钟] | **烹饪时间**：[X分钟] | **份量**：[X人份]

## 食材清单
- [ ] [食材]：[用量]
- [ ] [食材]：[用量]

## 制作步骤
1. **[步骤名]**：[具体操作]
2. **[步骤名]**：[具体操作]

## 小贴士
- [关键注意事项或技巧]

## 来源
- [标题](链接)
```

**English template:**

```markdown
# [Dish Name]

> **Description**: [One-line description highlighting the dish's character]
> **Prep time**: [X min] | **Cook time**: [X min] | **Serves**: [X]

## Ingredients
- [ ] [Ingredient]: [Quantity]
- [ ] [Ingredient]: [Quantity]

## Steps
1. **[Step name]**: [Instructions]
2. **[Step name]**: [Instructions]

## Tips
- [Key tips or cautions]

## Source
- [Title](link)
```

### Step 5 — Update the index (optional)

Skip this step if `INDEX_FILE` is not configured.

`Read` the index file first, then use `Edit` to append at the end:

Chinese: `## [[菜名]]`
English: `## [[Dish Name]]`

## Notes

- If quantities are not stated, use reasonable estimates and note "adjust to taste" (or "可根据口味调整") in tips
- Bold every step name for scannability
- Always keep the original source link
- If multiple posts support one dish, list all links in the source section
