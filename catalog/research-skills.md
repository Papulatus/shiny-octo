# 调研与研究 Skills

> 本页收录「把外部信息变成可交付成果」这一层的能力：调研方法论、文献工作流、报告生成、数据核对。与其他分类的区别是——这里收的是 **Skill（方法/工作流）**，不是数据源或框架本体。

## Deep Research Anything（本库维护的原创 Skill）

| 字段 | 信息 |
| --- | --- |
| 上游 | [Papulatus/deep-research-anything](https://github.com/Papulatus/deep-research-anything)（本库维护） |
| 许可证 | MIT |
| 形态 | 纯 Skill（`SKILL.md` + 6 个 `references/` 模块），无运行时、无内置服务、无第三方代码 |
| 方法来源 | 合并自 [bytedance/deer-flow](https://github.com/bytedance/deer-flow)（MIT）的六个研究类技能，已去重重构并补齐数据源契约 |
| 文档语言 | 中英双语（`README.md` / `README.zh-CN.md`） |
| 收录时星标 | 新仓库（自有） |

**定位**：一个技能覆盖六类调研任务——网络调研、论文精读、系统性文献综述、咨询级报告、表格与 SQL 分析、开源仓库尽调。六者共享同一套五阶段流程（定界 → 取证 → 校验 → 综合 → 交付）、同一道质量闸门（结论可追溯、不编造数据）和同一个数据源接入契约。

**为什么合并**：真实任务很少是"纯"的（调研完要出报告、读完论文要写综述、自己的数据要支撑结论）。分开维护六套技能会导致质量要求各写一遍且漂移、引用与数据纪律不一致、私有数据无处安放。合并后 `SKILL.md` 只做路由与公共纪律，六套方法论按需加载。

**核心能力**

- **路由表**：按任务信号自动选模式，支持组合（调研+报告、综述+精读、数据+报告、仓库+生态口碑）。
- **五条硬纪律**：任何无法溯源的数字写 `Data not available`；至少 3–5 个角度且正反面覆盖；时效按问题精度对齐；结论挂来源与日期；跨源指标先声明口径。
- **数据源契约**（`references/data-sources.md`）：支持 SQL / HTTP API / 文件 / MCP / 脚本五种形态，适配器只需实现 `describe()`、`query()`、`provenance()`、`freshness()`；凭据只从环境变量读。
- **数据到手三条硬规则**：不插值补齐、不跨源混算、差异必须留痕（幅度 + 原因 + 适用边界）。
- **可直接用的模板**：论文评审（S/W/Q 结构）、文献综述（APA/IEEE/BibTeX）、咨询报告骨架（30+ 框架选 2–4 个）、仓库尽调（健康度清单 + 置信度分级）。

**接入方式**

```bash
# Hermes Agent
cp -R deep-research-anything ~/.hermes/skills/
# Claude Code / Codex / Cursor
cp -R deep-research-anything ~/.claude/skills/
# DeerFlow：放到 skills/public/ 下即可
```

**边界与注意事项**

- 只覆盖**公开信息**；内部专有数据必须自行按契约接入，本技能不携带任何数据源。
- 时间精度到"日"，不适用于秒级实时数据（行情、突发新闻请走 API）。
- 不作专业背书：医疗、法律、投资建议场景只产出证据与角度，不替代专业判断与合规审查。
- 不绕过付费墙/登录墙；读不到全文的来源会显式标注，不允许"假装读过"。
- 文献综述单次上限 50 篇；更大规模应按子主题拆分。
- 技能质量取决于模型自身的检索与判断能力，仍需人工复核关键结论与引用。

## DeerFlow 2.0 — 长任务 SuperAgent Harness（上游来源）

| 字段 | 信息 |
| --- | --- |
| 上游 | [bytedance/deer-flow](https://github.com/bytedance/deer-flow) |
| 许可证 | MIT |
| 形态 | 完整应用：Python 3.12+/LangGraph 后端 + Next.js 前端 + Gateway（默认 `:2026`）+ 沙箱 + 技能系统 + 插件 API |
| 收录时星标 | 85,114 |
| 上游最近推送 | 2026-11-07 |
| 开放 issue | 1,061 |
| 最新版本 | v2.2.0（2026-11-04） |

**定位**：字节开源的长任务智能体运行框架，编排子代理、记忆、沙箱与技能，跑分钟级到小时级任务。2026-02-28 发布 2.0 当天登上 GitHub Trending 第一。

**v1 与 v2 的关系（重要）**

- **v2 是从零重写**，与 v1 不共享代码；v1 冻结在 `main-1.x` 分支（无 tag/release，`git clone -b main-1.x`）。
- v1 是"社区驱动的 Deep Research 框架"，采用固定多角色研究流程；v2 是通用 harness + 可插拔技能 + 四档执行模式（`flash` / `standard` / `pro` 规划 / `ultra` 多子代理）。
- 想复刻 v1 那套固定研究流水线 → 用 `main-1.x`；想要"调研 + PPT/播客/视频/图表 + MCP + 私有知识库"→ 用 v2。

**内置研究类技能**（本库的 Deep Research Anything 即由这六个合并而来）

`deep-research`、`academic-paper-review`、`systematic-literature-review`、`consulting-analysis`、`data-analysis`、`github-deep-research`

**运行时依赖（最小集）**

| 项 | 必需性 | 说明 |
| --- | --- | --- |
| LLM 端点（OpenAI 兼容） | 必需 | 默认火山方舟 + `doubao`；可换 Ollama 或 Gemini AI Studio |
| 搜索 API key（Tavily / InfoQuest / Brave） | 必需 | 没有信息源，研究流程不成立 |
| Python 3.12+（uv） | 必需 | 后端 |
| Node.js 22+（pnpm） | 仅 Web UI | 纯 API 使用可省 |
| Docker | 可选 | 仓库自带 `Dockerfile` + `docker-compose.yml`（后端 `:8000`、前端 `:3000`） |
| Python REPL / MCP server / TTS / RAGFlow | 默认关闭 | 研究流程不需要 |

**工程与安全边界**

- 沙箱与产出物目录会承载用户文件，需限制网络出口与访问权限。
- 技能支持社区 `.skill` 归档导入，**导入前必须审查内容**（上游提供 `review_skill_package` 仅审查不激活）。
- 插件 API 可提供整页 UI 与后端操作，第三方插件等同代码执行，须审查后安装。
- 付费搜索/模型调用会产生实际成本，建议设预算与速率上限。
- 上游迭代极快（v2.0.0 → v2.2.0 三个月内），自建部署应锁定 tag，不要跟 `main`。


## Marketing Skills（Corey Haines）— 营销策略、获客、文案与增长执行技能包

| 字段 | 信息 |
| --- | --- |
| 官方上游 | [coreyhaines31/marketingskills](https://github.com/coreyhaines31/marketingskills)，Corey Haines 维护 |
| 官网与接入 | [marketing-skills.com](https://marketing-skills.com/) · [工具连接指南](https://github.com/coreyhaines31/marketingskills/blob/main/tools/SETUP.md) |
| 许可证 | 已读根 LICENSE：MIT，© 2025 Corey Haines；第三方数据、账户、广告平台、图片/视频模型与服务收费另核 |
| 技术形态 | Agent Skills Markdown、参考文档、模板与可选工具/CLI 集成；不是营销数据供应商或自动获得授权的广告投放服务 |
| 收录快照 | 2026-11-14 CST；60,529 stars、8,823 forks；未归档 |
| 维护快照 | 最新 Release v2.14.12（2026-11-11 UTC）；main 提交 `1f837447b20b`（2026-11-11 UTC）；递归实核 skills/ 下 53 个 SKILL.md |

### 是什么

给 Claude Code、Codex、Cursor 等 Agent 使用的营销工作手册集合，覆盖策略、转化优化（CRO）、文案、SEO/AI 搜索可见性、广告、分析归因、邮件与 B2B 外联、销售支持和增长。核心不是让模型泛泛写营销话术，而是先建立 `product-marketing` 产品上下文（目标客户 ICP、定位、竞争、品牌语气、客户原话），其他技能再按此工作。

### 核心能力与适用场景

- **策略与调研**：product-marketing、marketing-plan、customer-research、competitor-profiling、reverse-engineer-marketing、offers、pricing、launch、marketing-ideas/psychology。
- **B2B 获客与销售**：prospecting、cold-email、sales-enablement、revops、events、co-marketing、public-relations；可用于出口企业目标客户画像、客户开发信、展会评估与销售资料，但公开资料不能代替有效采购线索。
- **内容与搜索**：copywriting/editing、content-strategy、seo-audit、ai-seo、programmatic-seo、site-architecture、schema、link-building、aso。
- **转化和留存**：cro、signup、onboarding、popups、paywalls、churn-prevention、referrals、lead-magnets、community-marketing、free-tools。
- **渠道与测量**：ads、ad-creative、emails、sms、social、analytics、attribution、conversion-tracking、ab-testing；image/video 技能指导素材工作流，**不附送图像模型权限、第三方订阅或投放预算**。
- **持续工作流**：marketing-loops 可设计周期任务，但持续执行依赖宿主调度与授权；marketing-council 的多视角讨论不等于真实专家背书。

### 推荐接入方式

1. 上游支持 `npx skills add coreyhaines31/marketingskills --list` 先看清单，再按需选择：例如 `--skill product-marketing prospecting cold-email sales-enablement`。Claude Code 的非交互安装可显式指定 `-a claude-code`，避免只写入其他 Agent 使用的 `.agents/skills/`。Hermes 需按当前 Profile 的技能目录适配，不假设该 CLI 自动支持。
2. 不需要把 53 个技能全部全局启用；先建立 `.agents/product-marketing.md` 并人工确认事实。营销计划默认有 `~/marketing-plans/<slug>/` 写入约定，采用前检查与自己的项目存储规范是否冲突，**未经同意不向家目录新建任务树**。
3. 库自带 Claude Code / Codex 插件入口，也可使用技能目录与参考资料；安装插件不自动完成工具账号授权。`tools/SETUP.md` 要求先选单一工具与账户、最小 scope、先做只读结果，再决定是否开放写操作。
4. 可选仓库 CLI 需要 Node ≥18；文档中的 `--env-file` 用法要求 Node ≥20.6。密钥使用已有 Secret/环境管理，不粘贴到聊天，不默认创建全套账号连接。

### 安全、隐私、商业与效果边界

- 对广告预算变更、邮件/短信发送、CRM 批量写入、网页发布、账号 OAuth 和自动任务分别授权；默认只读、草稿、测试账户及预算上限，不把“能运行 CLI”当作可花钱/可群发。
- 客户访谈、CRM、转化标识、广告账户与产品上下文可能由宿主发给模型或第三方 API。先确认数据最小化、授权、脱敏、地域与保留策略；本地存 Markdown 不代表数据不外发。
- 冷邮件、短信和 WhatsApp 的联系名单来源、同意/合法依据、退订、地区规则与平台条款需另核，不用于批量猜邮箱、刷量、垃圾信息或未经授权抓取个人资料。
- 转化跟踪代码会影响网站行为与隐私；上线前核验 consent、重复上报、测试流量、归因口径和回滚方案。A/B 测试不因套用方法就自动统计显著。
- README 有明确披露的商业合作伙伴，作者声称核心推荐不受赞助影响；这是上游声明而非本库独立审计结论，选择工具仍按需求、权限、成本和现有系统评估。
- 主要面向技术营销与软件/创业产品，工业定制品的验证周期、渠道与订单模式需重新校准，不能直接套 SaaS 漏斗并承诺营收、SEO 排名或获客效果。
- 本条只收录与审阅文档，不安装技能、不接营销账户、不发送邮件或投放广告。


## Sparkling — 以证据、反常与白板推动业务共创研讨的 Skill

| 字段 | 信息 |
| --- | --- |
| 上游 | [thePlannerIvan/sparkling](https://github.com/thePlannerIvan/sparkling) |
| 许可证 | 已读 LICENSE：AGPL-3.0，README 明确 AGPL-3.0-only；商业定制/其他授权需另谈，不是 MIT。 |
| 技术形态 | 纯工作流协议 Skill、研讨白板与纪要模板，不依赖专属脚本或 DSH 插件。 |
| 收录快照 | 2026-11-16 CST；62 stars、8 forks；未归档；星标不代表质量认证 |
| 维护快照 | 默认分支 main，提交 `73082811bdac`（2026-11-14 UTC）；未发现 GitHub Release |

### 身份与定位

用户提供的 `lawyif` 线索对应作者公开联系方式 Lawyif@163.com；已找到作者“阿祖不看 TVC”的 canonical 仓库 `thePlannerIvan/sparkling`，而不是把 lawyif 擅自当成已证实 GitHub owner。官网 demyth.info，出处见 NOTICE。

用于拿着材料与用户共同推导业务卡点，不是自动输出长篇总结：首轮提出反常点、互斥点和未经检验的默认公理；随后短回合用 PO 挑衅/事实混成检验解释，并维护 `sparkling-whiteboard.md`，避免被否定假设反复出现。最后可输出一页洞察纪要，或关键分歧与取证清单。

### 适合什么与接入

适合有背景材料但判断卡住的产品、营销、组织或商业讨论；不是缺资料时凭空代替市场调研。可先用 Deep Research Anything 取证、Marketing Skills 组织营销事实，再用 Sparkling 协助讨论，但不自动把它加载为所有对话的强制风格。

上游 `npx skills add https://github.com/thePlannerIvan/sparkling --skill sparkling`，按宿主选项目级目录；先确认白板保存位置和覆盖规则，再用“带着这些资料和我讨论，先别写总结报告”触发。外部 `/research` 是可选环境能力，不是此仓库自带可用工具。

### 安全、许可与能力边界

AGPL 的分发、修改和网络服务义务需按实际使用方式评估；COMMERCIAL.md 只说明可讨论定制/其他授权，不表示已获闭源商业授权。TRADEMARK.md 禁止冒充作者或官方背书，修改版注明 fork/来源；默认不往最终客户文件添加项目品牌。

白板可能含经营数据、客户信息和内部假设；确认宿主模型外发及存储权限，事实/推断/待查分开记录，禁止为制造“顿悟”编造因果。250 字短回合、奥卡姆剃刀是讨论方法，不是证明或专业裁决；重大商业决策由用户控制，不替用户确定结论或擅自追加执行任务。本次未安装或创建研讨白板。
