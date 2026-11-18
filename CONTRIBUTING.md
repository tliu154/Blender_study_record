---
tags:
  - "#course/Blender"
  - "#type/资料"
created: 2026-11-18
---
# 新增章节规范

给自己看的约定。加一章走 5 步，保证整个仓库风格统一、链接不烂、随时能自检。

**状态只改 [SYLLABUS.md](SYLLABUS.md)**，篇 README 和根 README 不重复维护章节清单。
术语与名词见 [NOTATION.md](NOTATION.md)。

## 0. Obsidian / GitHub 双兼容约定

- 一律 `.md`，UTF-8，相对超链（不要绝对路径、不要用 `[[wikilink]]`），这样 GitHub 和 Obsidian 都能点开
- **打 tags**：frontmatter 按 0.5 节标签规范填写（course/type/topic/source 四类），用 `tools/add_tags.py` 幂等生成
- 章节互引用相对 Markdown 链接，例：`[ch08](02_blender_basics/docs/ch08_mesh_cleanup.md)`
- 锚点引用用显式 ID（见下），不依赖 GitHub 自动 slug
- **跨仓库链接**：指向 ComfyUI 主仓库时用完整 URL（`https://github.com/tliu154/ComfyUI_study_record/blob/main/...`），
  因为相对路径跨仓库无效；本仓库内部一律相对超链

## 0.5 标签规范（每篇必打）

沿用知识库标签规范，**每篇笔记 frontmatter 都要有 `tags:`**：

```markdown
---
tags:
  - "#course/Blender"
  - "#type/笔记"
  - "#topic/网格"
  - "#source/官方文档"
created: YYYY-MM-DD
---
```

规则：层级 `英文/中文/中文`、无空格、最多 3 层、统一单数；标签带引号带 `#`。
本仓库取值：

| 类别 | 本仓库取值 |
|---|---|
| `#course/` | 一律 `Blender`（本仓库主题，大写特例）|
| `#type/` | docs → `笔记`；tasks → `练习`；框架/README → `资料` |
| `#topic/` | 按章号映射（ch08 网格 / ch11 导出 …），见 `tools/add_tags.py` 的 `TOPIC_BY_CH` |
| `#source/` | 教学笔记 → `官方文档` |

**已移除**（不要再出现）：`#statu/等待复习`、`#flag/重要`、`标签有哪些` 字段。脚本会自动清理。

**不要手动逐个加标签**：写完一批笔记后跑 `python tools/add_tags.py`，它按路径规则自动打、
幂等（重跑无副作用）、清理旧标签，并保留 `created` 等其它 frontmatter 字段。
`_templates/` 是复制源，跳过不打。

## 1. 命名：全局章号

```
<篇目录>/docs/chNN_<短名>.md     教学
<篇目录>/tasks/chNN_task.md      实操
```

- `NN` 是 [SYLLABUS.md](SYLLABUS.md) 里分配的**两位章号**，全仓库唯一
- 篇目录只是分组（`01_comfyui_3d/` / `02_blender_basics/`），不参与编号
- `[待写]` 章节不建文件；开写时才建 docs + tasks

## 2. 章节模板规则

复制 `_templates/chapter_template.md`，保留：
- frontmatter（标签由脚本生成）
- 顶部「前置 / 对应实操 / 状态 / 所属篇」四行
- 一句话定位 + 「本篇一条线」导航
- **子概念索引表**（每概念一个锚点链接）
- 每节 `<a id="cNN-MM"></a>` + `### NN.M ...（English）`
- **每节四段**：概念定义 → 直觉类比 → 界面/参数 → 常见误区
- 每节结尾「够用边界」「和已有认知的差异」两个引用块
- 小结 + 实操/下一步链接

## 3. 锚点规则

- 显式锚点：`<a id="c08-02"></a>`，紧接 `### 8.2 ...`
- 索引用 `[文字](#c08-02)`，同文件；跨文件用 `[文字](path/to/file.md#c08-02)`
- 只校验 `cNN-MM` 形式；其它内部跳转请用普通标题或链接文本，不要用 `#自定义`
- 代码块里的示例锚点不算数（`verify_all.py` 会剥离代码块）

> 模板里的链接是**占位**，复制后逐个替换；`verify_all.py` 自动跳过 `_templates/`。

## 4. 校验（不能跳过）

在仓库根目录跑（脚本按自身位置推断仓库根）：

```bash
python tools/verify_all.py
```

任一检查失败，退出码 1。脚本做两件事：

| 检查项 | 做法 |
|---|---|
| 相对链接 | 检查所有 `.md` 的链接目标存在；跳过代码块与行内代码；`http(s)` 外链不查 |
| 显式锚点 | 检查 `#cNN-MM` 链接在目标文件里确有 `<a id="cNN-MM"></a>` |
| 路径写错 | 目标文件名在仓库已存在、只是相对路径层级写错 → 报 `链接失效` |

若报 `链接失效` 且是路径层级写错（跨篇常用 `../` 写成 `../../`、tasks 引用 docs 漏 `../docs/`），
先 dry-run 预览再一键修：

```bash
python tools/fix_links.py           # 预览改法
python tools/fix_links.py --apply   # 确认后写回
```

> 「预定未写」豁免只在目标章节文件**确实还不存在**时生效；章节写完后再有失效链接一律报错。

另外人工检查一次：

- [ ] 子概念索引里每个链接都能跳到对应 `<a id>`
- [ ] **无非标准锚点链接**：`grep -n '](#' 新文档.md | grep -v '#c'` 应为空
- [ ] 章号、文件名、实操文件三者一致
- [ ] ComfyUI / Blender 名词与 [NOTATION.md](NOTATION.md) 一致
- [ ] 没有重复定义同一个概念（先在 SYLLABUS 里搜一遍）

## 5. 更新状态

- [SYLLABUS.md](SYLLABUS.md)：该章状态改 `[已完成]`，填实际文件列
- 根 README：只更新「进度」里的汇总
- 一篇收口时，在该篇 README 补一句实际产出

## 6. 实操任务写法

每章一份 `tasks/chNN_task.md`，复制 `_templates/task_template.md`，包含：
目标、前提、步骤（可照做）、验收标准、改一改会怎样（小实验表）、可复现记录、常见问题。
Blender 后处理类任务可分 A/B 档：A 档真跑，B 档跑不动时看懂结构即可。

## 7. 与 ComfyUI 主仓库的关系

- 本仓库第 1 篇讲「ComfyUI 里怎么生成 3D」，会引用主仓库的 2D 基础概念（采样/提示词/模型）
- 引用方式：完整 GitHub URL 超链，**不复制**主仓库内容
- 主仓库附录 D 有一条外链指回本仓库；两边正文互不嵌入

## 8. 提交习惯

- 按「一块一篇」推进：填完一篇 → 自检 → 更新状态 → commit → push
- 提交信息：`add chNN-NN: 第X篇主题 教学与实操`
- 推送：
  ```bash
  GIT_TERMINAL_PROMPT=1 git -c credential.helper=manager \
    -c credential.helperselector.selected=manager push origin main
  ```
