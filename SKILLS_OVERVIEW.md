# 工作区技能总览（SKILLS_OVERVIEW）

以下为本工作区内所有 skill 的功能、使用场景与简要使用方法汇总，便于快速理解与调用。

**目录**
- json-canvas
- style-library
- obsidian-bases
- web-to-markdown
- skill-creator
- news-content-factory
- obsidian-markdown
- structure-library

---

**json-canvas**
- 功能：创建与编辑 JSON Canvas 格式（.canvas）文件，支持节点（text/file/link/group）、连线（edges）与颜色/布局等属性。
- 使用场景：在 Obsidian 或其他支持画布的工具中构建思维导图、流程图、项目看板、研究画布等可视化笔记；从结构化数据生成可视化布局；程序化生成或批量修改 canvas 文件。
- 使用方法：编辑或生成符合 JSON Canvas 规范的 JSON 对象，包含 `nodes` 与 `edges` 两个顶层数组。典型字段：`id,type,x,y,width,height,text/file/url,label,color`。示例：创建 `text` 节点并在 `edges` 中连接两节点。

**style-library**
- 功能：存储与管理写作风格模板（风格指纹），支持风格分析、保存与加载，并可被 `news-content-factory` 调用。
- 使用场景：需要按特定文风生成文章时（如财经深度、轻松解读、个人随笔、国际视角、犀利评论等）；在生成流程里快速切换或复用风格模板。
- 使用方法：可使用内置命令：`/style list`（列出模板）、`/style load [name]`（加载风格）、`/style analyze [text]`（分析范文提取指纹）、`/style save [name]`（保存模板）。在自动化流程中，调用 style-library 返回风格指纹并将其作为生成参数。

**obsidian-bases**
- 功能：创建与编辑 Obsidian Bases（.base）文件，定义视图（table/cards/list/map）、过滤器、公式、属性显示与汇总函数，类似于可视化数据库视图配置。
- 使用场景：为 Obsidian 笔记构建动态查询与可视化面板（任务看板、项目跟踪、统计报表、位置地图等）；用 YAML 配置复杂过滤与汇总逻辑。
- 使用方法：编写 .base 文件（YAML），包含 `filters`, `formulas`, `properties`, `summaries`, `views` 等。示例：定义 `formulas` 计算天数、`views` 选择 `table` 或 `cards` 并指定 `order` 与 `summaries`。

**web-to-markdown**
- 功能：将网页（包含微信公众号文章）转换为标准 Markdown 文档，抽取标题、作者、来源、时间、标签、核心观点与正文，并生成供 Obsidian 使用的结构化输出。
- 使用场景：做信息收集、知识管理时把外部文章归档到 Obsidian；快速生成阅读笔记与写作素材；把网页内容规范化为可编辑的 Markdown。
- 使用方法：提供 URL 后，执行抓取与解析（工具链：web_fetch 等），输出必须遵循模板：标题、作者、来源、日期、标签、Core Ideas、Content、我的心得（留空供笔记）。对微信文章做特殊清理（去 UI 垃圾、识别公众号名）。

**skill-creator**
- 功能：关于如何创建有效 skill 的指导与流程文档，包括 SKILL.md 的结构、脚本/引用/资源组织、初始化与打包流程（`init_skill.py`、`package_skill.py`）。
- 使用场景：当需要新增或改进技能（skill）时，按推荐步骤建立、组织并打包；为团队制定统一的 skill 编写规范。
- 使用方法：参照文档中的步骤：规划资源（scripts/references/assets）、运行 `scripts/init_skill.py <skill-name>` 生成模板、编辑 `SKILL.md` 并通过 `scripts/package_skill.py` 打包与验证。

**news-content-factory**
- 功能：从新闻搜索到最终文章生成的一整套工作流：领域确认 → 新闻搜索 → 候选展示 → 组合/角度选择 → 风格与结构配置 → 最终生成。深度整合搜索、解读、结构与风格模块，支持交互式流程与自动化。
- 使用场景：写热点分析、新闻解读、行业纵览等需要“搜集事实 + 形成角度 + 按风格生成文章”的任务，适用于编辑、内容团队与独立作者。
- 使用方法：按 8 步工作流交互操作（或在自动化脚本中调用）：Step1 选择领域；Step2 搜索并去重排序；Step3 展示候选并选择组合；Step4 关联性分析；Step5 生成多个解读角度；Step6 确认方向与标题；Step7 选择风格（可调用 `style-library`）与结构（可调用 `structure-library`）；Step8 生成文章并支持后续微调命令（如 `/style`, `/structure`, `/extend` 等）。

**obsidian-markdown**
- 功能：生成与编辑符合 Obsidian 扩展语法的 Markdown（包含 wikilinks、block 引用、callouts、embed、frontmatter、任务列表、Mermaid、LaTeX 等）。
- 使用场景：在 Obsidian 笔记系统中创建或修正笔记内容，使其兼容 Obsidian 特性；把普通 Markdown 升级为 Obsidian 风格笔记；生成可直接嵌入 Obsidian 的笔记模板。
- 使用方法：输出遵循 Obsidian 语法示例：`[[Wikilink]]`、`![[Embed]]`、`> [!note]` callout、代码块与 Math/KaTeX，支持 block id（`^id`）与查询块（```query```）。可按需要生成带 frontmatter 的笔记头部。

**structure-library**
- 功能：存储并调用文章结构模板（论证框架），例如问题-方案-展望、对比-冲突-融合、时间线-演变、人物故事-启示、现象-本质-影响、问题-证据-结论等。
- 使用场景：需要快速选择或应用标准文章结构以保证逻辑清晰、层次分明；与 `news-content-factory` 配合用于文章生成时确定大纲。
- 使用方法：调用命令形式 `/structure list` 列出模板，`/structure [name]` 应用模板，或 `/structure custom [description]` 生成自定义结构。每个模板包含分段写作要点与字数建议。

---

附：如何调用与推送（给使用者的快速操作示例）

- 在本地打开工作区根目录（已与远程仓库绑定）：

```bash
# 查看仓库状态
git status

# 查看远程
git remote -v
```

- 若需要在仓库中添加/更新说明文档：

```bash
# 编辑或创建文件（例如本文件）
# 然后提交并推送
git add SKILLS_OVERVIEW.md
git commit -m "Add skills overview"
git push
```

---

如果你需要，我可以接着：
- 把每个 skill 的示例与常用命令补充为单个 README（我可以为每个子目录生成 `README.md`），或
- 在 GitHub 仓库启用 CI/发现（例如添加简单的 GitHub Actions 用于 lint 或文档部署）。

要我继续哪一项？
