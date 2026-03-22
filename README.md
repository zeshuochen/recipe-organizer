# cooking-skills

**Agent Skills for turning recipe videos and posts into structured Obsidian notes.**

> Follows the [Agent Skills specification](https://agentskills.io/specification) — works with Claude Code, Codex CLI, and any skills-compatible agent.

---

## Skills

| Skill | Description |
|-------|-------------|
| [recipe-organizer](skills/recipe-organizer) | Fetch recipes from Xiaohongshu, YouTube, or Bilibili, extract ingredients & steps, and save clean notes to your Obsidian vault — in English or Chinese |

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
VAULT_PATH=C:\Users\you\MyVault     # your Obsidian vault
RECIPES_FOLDER=Recipes              # folder for recipe notes
INDEX_FILE=Recipes/index.md         # optional: delete this line if you don't use an index
```

2. **Share a link** and ask your agent to organize the recipe:

```
https://www.youtube.com/watch?v=...   organize recipe
```

3. The skill auto-detects language — share a Chinese link and get a Chinese note; share an English link and get an English note.

---

## Supported platforms

| Platform | Language | Notes |
|----------|----------|-------|
| Xiaohongshu (小红书) | Chinese | Steps often in images; inferred from comments |
| Bilibili (哔哩哔哩) | Chinese | Description + pinned comments |
| YouTube | English | Description box + pinned comments |

---

## How it works

1. **Fetch** — open each link in Chrome and extract the post body, description, and comments
2. **Classify** — distinguish recipe posts from technique videos (e.g. deboning demos); merge techniques as steps into the related recipe
3. **Write** — create a structured Markdown note in your Obsidian vault using the matching language template
4. **Index** — append a wikilink to your recipe index file (skipped if `INDEX_FILE` is not configured)

---

## Output examples

### English

```markdown
# Cola Chicken Legs

> **Description**: Sweet, sticky, and deeply savoury — a crowd-pleasing one-pan rice topper.
> **Prep time**: 15 min | **Cook time**: 20 min | **Serves**: 2

## Ingredients
- [ ] Chicken legs: 2
- [ ] Cola: 330 ml
- [ ] Light soy sauce: 1 tbsp
- [ ] Dark soy sauce: ½ tbsp
- [ ] Oyster sauce: 1 tbsp
- [ ] Starch: 1 tsp
- [ ] White sesame seeds: to garnish

## Steps
1. **Marinate**: Slice deboned chicken into 2 cm pieces, pat dry. Mix with soy sauces, oyster sauce, starch and a little oil. Rest 10 min.
2. **Sear**: Heat a little oil over medium heat. Stir-fry chicken until the surface is lightly charred.
3. **Braise**: Pour in cola (use half cola, half water if you prefer less sweet). Bring to a boil, then simmer 10 min.
4. **Finish**: Reduce the sauce slightly, sprinkle with white sesame seeds. Serve over rice.

## Tips
- Pat chicken dry before searing — it browns better and won't splatter.
- Half cola + half water gives a less sweet, more savoury result.

## Source
- [可乐鸡腿饭](https://www.xiaohongshu.com/explore/67e0ef8e000000001e00b1f8)
```

### 中文

```markdown
# 菜名：可乐鸡腿饭

> **描述**：香甜浓郁的拌饭神器，鸡腿肉焦香入味，可乐赋予独特甜香，厨房小白也能轻松搞定。
> **准备时间**：15分钟 | **烹饪时间**：20分钟 | **份量**：1-2人份

## 食材清单
- [ ] 鸡腿：2个
- [ ] 可乐：1罐（330ml）
- [ ] 生抽：1汤匙
- [ ] 老抽：半汤匙
- [ ] 蚝油：1汤匙
- [ ] 淀粉：1茶匙
- [ ] 白芝麻：适量（装饰用）
- [ ] 食用油：少许

## 制作步骤
1. **去骨切块**：鸡腿去骨后切成约2cm小块，用厨房纸擦干水分。
2. **腌制**：加入生抽、老抽、蚝油、淀粉，抓匀后喷少许油，腌制10分钟。
3. **煎制**：锅中少量油热后，中火下入鸡腿肉，翻炒至表面微焦上色。
4. **焖煮**：倒入可乐（怕太甜可半可乐半开水），大火烧开后转小火焖煮10分钟。
5. **收汁**：开盖略微收汁，撒上白芝麻，浇在米饭上即可。

## 小贴士
- 鸡腿肉一定要擦干水分，煎时不溅油、更容易上色。
- 半可乐半开水口味更清爽，不那么甜腻。
- 油不用多，鸡腿肉有自身油脂。

## 来源
- [可乐鸡腿饭](https://www.xiaohongshu.com/explore/67e0ef8e000000001e00b1f8)
- [30秒鸡腿去骨技巧](https://www.xiaohongshu.com/explore/67518a240000000002029feb)
```

---

## 简介（中文）

**从小红书、哔哩哔哩、YouTube 食谱视频一键生成结构化 Obsidian 笔记的 Agent Skill。**

自动识别语言——中文链接输出中文笔记，英文链接输出英文笔记。

### 安装

```
/plugin marketplace add zeshuochen/cooking-skills
/plugin install cooking@cooking-skills
```

### 配置

编辑 `skills/recipe-organizer/SKILL.md`，修改以下三项：

```
VAULT_PATH=    # Obsidian vault 的绝对路径
RECIPES_FOLDER=   # vault 内食谱文件夹
INDEX_FILE=    # 可选：食谱索引文件路径，不需要索引则删除此行
```

---

## License

MIT © [zeshuochen](https://github.com/zeshuochen)
