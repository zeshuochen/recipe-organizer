# cooking-skills

**Agent Skills for turning recipe videos and posts into structured Obsidian notes.**

> Follows the [Agent Skills specification](https://agentskills.io/specification) — works with Claude Code, Codex CLI, and any skills-compatible agent.

---

## Skills

| Skill | Description |
|-------|-------------|
| [recipe-organizer](skills/recipe-organizer) | Fetch recipes from any recipe link, extract ingredients & steps, and save clean notes to your Obsidian vault — in English or Chinese |

---

## Installation

### Claude Code

```
/plugin marketplace add zeshuochen/cooking-skills
/plugin install cooking@cooking-skills
```

### Manual

Clone this repo and copy the `skills/` directory to your agent's skills path.

---

## Quick start

1. **Configure** your vault path in `skills/recipe-organizer/SKILL.md`:

```
VAULT_PATH=C:\Users\you\MyVault
RECIPES_FOLDER=Recipes
INDEX_FILE=Recipes/index.md
```

2. **Share a link** and ask your agent to organize the recipe:

```
https://www.xiaohongshu.com/explore/...   organize recipe
```

3. The skill auto-detects language — share a Chinese link and get a Chinese note; share an English link and get an English note.

---

## How it works

1. **Fetch** — open each link in Chrome and extract the post body and comments
2. **Classify** — distinguish recipe posts from technique videos (e.g. deboning demos); merge techniques as steps into the related recipe
3. **Write** — create a structured Markdown note in your Obsidian vault using the matching language template
4. **Index** — append a wikilink to your recipe index file

### Output example (English)

```markdown
# Cola Chicken Legs

> **Description**: Sweet, sticky, and deeply savoury — a crowd-pleasing one-pan rice topper.
> **Prep time**: 15 min | **Cook time**: 20 min | **Serves**: 2

## Ingredients
- [ ] Chicken legs: 2
- [ ] Cola: 330 ml
...

## Steps
1. **Marinate**: Slice chicken, add soy sauce, oyster sauce, starch. Rest 10 min.
2. **Sear**: Pan-fry over medium heat until golden on all sides.
3. **Braise**: Pour in cola, bring to boil, simmer 10 min, reduce sauce.

## Tips
- Pat chicken dry before searing for a better crust.

## Source
- [可乐鸡腿饭](https://www.xiaohongshu.com/...)
```

### Output example (中文)

```markdown
# 菜名：可乐鸡腿饭

> **描述**：香甜浓郁的拌饭神器，焦香入味，厨房小白也能搞定。
> **准备时间**：15分钟 | **烹饪时间**：20分钟 | **份量**：1-2人份

## 食材清单
- [ ] 鸡腿：2个
- [ ] 可乐：330ml
...
```

---

## 简介（中文）

**从食谱视频链接一键生成结构化 Obsidian 笔记的 Agent Skill。**

支持小红书、YouTube 等平台，自动识别语言——中文链接输出中文笔记，英文链接输出英文笔记。

### 安装

```
/plugin marketplace add zeshuochen/cooking-skills
/plugin install cooking@cooking-skills
```

### 配置

编辑 `skills/recipe-organizer/SKILL.md`，将以下三项改为你自己的路径：

```
VAULT_PATH=    # Obsidian vault 的绝对路径
RECIPES_FOLDER=   # vault 内食谱文件夹
INDEX_FILE=    # 食谱索引文件路径
```

---

## License

MIT © [zeshuochen](https://github.com/zeshuochen)
