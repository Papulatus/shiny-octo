# 目录

> 各条目独立记录数据快照；本批新增条目核验于 2026-11-16。项目活跃度、星标、版本、许可证和 API 兼容性会变化，请在采用前核验上游文档与条款。

| 分类 | 条目 | 适用场景 |
| --- | --- | --- |
| [金融 AI](catalog/financial-ai.md) | Kronos、FinRL | K线/量价序列预测、金融时间序列研究、金融强化学习实验与回测原型 |
| [量化研究与市场数据](catalog/quant-data.md) | A-Stock Data、stock-api、TA-Lib Python、PineTS、LLMQuant Hermes、QuantSpace、Lumibot、WorldQuant Miner、Vibe-Trading、QuestDB、TSP（tick-stock-panel）、ZenTrade | A 股/美股数据、技术指标、投研、回测、纸面交易与受控连接器 |
| [MCP、API 与 Agent 工具桥接](catalog/mcp-api-tools.md) | mcp2cli、AOCI-CODE、Agent Lightning、ClassCAD AI | MCP/API 桥接、代码认知、Agent 训练及参数化 CAD |
| [Agent 浏览器](catalog/agent-browser.md) | ego lite | Agent 浏览器自动化、复用本机登录态 |
| [浏览器、网页 Agent 与自动化](catalog/browser-web-agent.md) | GitReverse、CloakBrowser、Page Agent、scroll-world、UI-TARS | 仓库/网站反向 Prompt、自家网页 Copilot、浏览器运行时、沉浸式品牌页 Skill、视觉 GUI Agent |
| [网页采集](catalog/web-scraping.md) | Scrapling | 动态站点、反爬场景、自适应选择器、规模化采集 |
| [视觉 AI、CV 与办公](catalog/vision-office.md) | Qwen 多角度 3D Camera、Supervision、Larkboat、patent-disclosure-skill、AI剪口播、衣装集 COSTUME-DB-01、姿势集 POSE-DB-01、Uchinoko Maker | 图像多视角、检测/分割后处理、文档/表格/PPT 办公、专利技术文档、口播转录与剪辑工程、服装/姿态参考图库、宠物插画生成与个人自用周边 |
| [设计资源](catalog/design-resources.md) | Lucide、Phosphor、Tabler、Radix、Uiverse Galaxy、BoardUI、Bencho、Emil Kowalski Skills、Oil UI、IP as Logo、pixelfx、Blender Skills（Arjun）、img2threejs、Stageshow、Godogen、Anatomy、Pixel-art Gaussian Splats | 三维像素风渲染、界面资源、产品动效、三维程序化重建、解释型插画与游戏生成 |
| [资源目录与邮箱](catalog/resources-email.md) | FMHY、Public APIs、邮箱助手、Open source games、ChromeAppHeroes | 资源/API/邮箱服务发现、按类型查游戏源码、查阅 Chrome 扩展中文评测 |
| [调研与研究 Skills](catalog/research-skills.md) | Deep Research Anything（本库维护）、DeerFlow 2.0、Marketing Skills、Sparkling | 研究与取证、营销获客、材料驱动的业务共创研讨 |

## 快速选择

- 想让 Agent 系统性地做调研（不是搜一下就写）：看 [**Deep Research Anything**](catalog/research-skills.md)。一个技能覆盖六类调研任务，共享五阶段流程与"结论可追溯、不编造数据"的硬纪律；自带厂商中立的数据源契约（SQL/API/文件/MCP/脚本），不含任何私有数据源。
- 想要现成的长任务运行环境（沙箱 + 子代理 + Web 工作台）：看 [**DeerFlow 2.0**](catalog/research-skills.md)。注意 v2 与 v1 是两套代码，v1 留在 `main-1.x` 分支；最小依赖是 LLM 端点 + 一个搜索 API key + Python 3.12。
- 想做市场 OHLCV/K线预测或微调金融序列模型：看 **Kronos**。
- 想以 Gym 风格环境比较 A2C、DDPG、PPO、SAC、TD3 等 DRL 策略，或复现教学/研究型 train-test-trade 流程：看 **FinRL**。它是研究框架；新建生产化交易系统应进一步评估上游推荐的 **FinRL-X / FinRL-Trading**，并独立完成风控、合规和实盘验证。
- 想快速给 Agent 增加 A/港/美股查询：看 **stock-api**；想进行多源 A 股研究：看 **A-Stock Data**。
- 想在 Python/Pandas/Polars 管线中计算 RSI、MACD、布林带、ADX 或 K 线形态：看 **TA-Lib Python**；它只做指标计算，仍需自备合规行情、完成验证和风控。
- 想搭建可维护的 AI 量化研究仓库：看 **QuantSpace**；想把自然语言投研、跨市场回测、MCP/Swarm 和连接器放进一个研究工作台：看 **Vibe-Trading**；想做 Python 回测或 paper/live broker 策略：看 **Lumibot**。
- 已部署 Hermes，想将市场数据查询、晨报、财报/13F/持仓观察做成可控的 MCP + 定时工作流：看 **LLMQuant Hermes**；它需要独立的 LLMQuant Data 凭据、预算控制与人工风控。
- 想把受信任的 MCP、OpenAPI 或 GraphQL 服务转换为可筛选、可脚本化的 CLI，降低 Agent 工具 schema 负担：看 **mcp2cli**。先 `--list` 审查，再用只读白名单、最小 OAuth scope 与隔离 Secret；不要把它当作生产权限/审批系统。
- 想让 Codex、Claude Code 等 Agent 在不抢占日常标签页的前提下完成浏览器任务：看 **ego lite**。
- 想快速把公开 GitHub 仓库压缩成供 Coding Agent 参考的合成 Prompt：看 **GitReverse**；它只读取有限公开上下文，不能替代源码、许可证和安全审查。
- 想把自然语言 GUI 助手嵌入自己的网站：看 **Page Agent**。有明确授权的自动化/检测测试需要时再评估 **CloakBrowser**。
- 想写 Python 采集脚本，且目标站点可能改版或有反自动化限制：看 **Scrapling**。
- 想统一产品图标风格：通常先看 **Lucide** 或 **Tabler**；需要字重变化看 **Phosphor**；需要紧凑栅格看 **Radix Icons**；需要现成 CSS/Tailwind 灵感看 **Uiverse Galaxy**。
- 想让 Agent 做更高质量的 UI 动效决策、审查或原型变体：看 **Emil Kowalski Skills**；按任务选择 `animate`、`review-animations`、`improve-animations` 或 `prototype`，并在真实设备与 reduced-motion 场景验收。

- 想搭 React 后台、数据看板或 AI agent 界面，并希望**组件源码归自己**而不是依赖 npm 包：看 [**BoardUI**](catalog/design-resources.md)。免费层 62 个组件 + design tokens + 页面组合模式 Skill 已能搭出完整后台；19 张图表卡与整页模板属 Pro，MIT 只覆盖免费层，Pro 源码不可再分发；`init` 与 stdio MCP 会写文件并安装 npm 依赖，先在受控分支 diff。
- 想给已有 UI 补**高级交互手感与界面音效**（滑块、Toast、Dynamic Island、voice note、AI thinking 指示器）：看 [**Bencho**](catalog/design-resources.md)。免费 47 个 block + 24 个合成音效，复制文件夹即用；它不是组件基座（无表格、分页、图表体系与表单族），Pro blocks 与站点照片不在 MIT 范围。

- 想做模型无关的 CV 后处理、标注、跟踪和区域计数：看 **Supervision**。
- 想发现公共 API、免费资源或邮箱服务：看 **Public APIs / FMHY / 邮箱助手**，但所有外链都必须单独核验。

- 想将研发材料整理为中国专利交底/申请底稿，或建立私有专利解读与地图知识库：看 [**patent-disclosure-skill（中国专利.skill）**](catalog/vision-office.md)。先审核技能与数据外发边界；工具不能替代专业代理审核、全面查新或官方申请，未公开技术须授权和脱敏。

- 想围绕产品探索差异明显的视觉方向、并排比较原型、截图还原并以真实画面迭代：看 [**Oil UI**](catalog/design-resources.md)。它是设计 Skill，不是组件库；区分 MIT 开源版与付费 Pro，审查更新检查、素材外发和宿主权限，不替代业务正确性与无障碍测试。

- 想存储持续流入的 tick、订单簿、成交或遥测事件，并用时间序列 SQL 做实时聚合与 ASOF 对齐：看 [**QuestDB**](catalog/quant-data.md)。它不是数据供应商或交易系统；区分 Apache-2.0 开源版和 Enterprise 的高可用、安全与自动分层能力，先验证数据契约、权限、负载及备份恢复。

- 想让 Agent 跨会话复用 Git 版本化的代码/schema 语义索引，并治理范围、漂移和索引更新：看 [**AOCI-CODE**](catalog/mcp-api-tools.md)。当前为 RC、FSL-1.1-MIT 源码可见而非 OSI 开源；商业竞争性用途受限，各版本提供满两年后另授 MIT。索引不是源码或测试的替代，宿主模型仍可能外发源码。

- 想把有权使用的 Pine Script 指标迁移到 Node.js/浏览器，用自有 OHLCV 做扫描和图表计算：看 [**PineTS**](catalog/quant-data.md)。它不等于 TradingView 完整环境；原生脚本支持仍需逐 bar 验证，AGPL-3.0/商业双许可须在闭源或 SaaS 接入前评估。

- 想自托管 A 股选股、因子/策略回测、盘中监控与带确认卡的数据问答：看 [**TSP（tick-stock-panel）**](catalog/quant-data.md)。先用只读 MCP scope 和隔离数据评估；注意 Compose 的全接口监听及 Codex 凭据挂载，不将研究工作台当作真实交易或收益保证系统。

- 想了解 **Agent Lightning**：看 [Agent Lightning](catalog/mcp-api-tools.md)。先明确训练奖励、GPU 预算与隔离执行权限，v1.0 不沿用旧版接口。

- 想了解 **IP as Logo**：看 [IP as Logo](catalog/design-resources.md)。先确认生成数量、模型费用和品牌权利，不保证生成资产可注册商标。

- 想了解 **UI-TARS**：看 [UI-TARS](catalog/browser-web-agent.md)。先在授权测试设备验证动作和坐标，敏感操作人工批准；模型、客户端和权重许可分别核验。

- 想了解 **AI剪口播**：看 [AI剪口播](catalog/vision-office.md)。音频会上传火山引擎，需人工审核切点；AGPL 与云转录条款分别评估。

- 想找 AI 绘图用的**服装参考图**或**无脸姿势线稿**：看 [衣装集 / 姿势集](catalog/vision-office.md)。两个站点只允许站内浏览，**明文禁止批量下载（含自动获取）、再分发与销售**；只能人工参考，不能当训练数据或素材库。

- 想给像素游戏增加火焰、法术、打击反馈或导出 Godot/Unity 精灵图：看 [**pixelfx**](catalog/design-resources.md)。代码驱动而非模型生图；附 Agent 创作 Skill，MIT 覆盖代码与效果但不包含 Patch Pixel 专有字体，Patch 平台发布需另行授权操作。

- 想让 Agent 在 Blender 中按建模、UV、材质、绑定、优化到引擎导出的流程制作三维资产：看 [**Blender Skills（Arjun）**](catalog/design-resources.md)。94 个 Skill 加共享 references，需另装 BlenderMCP；Python 执行有文件/网络权限，先做副本和最小范围测试，Windows MCP 配置不可直接照搬 Mac。

- 想让 Agent 按产品定位和客户画像完成营销计划、SEO、文案、B2B 客户开发与转化分析：看 [**Marketing Skills（Corey Haines）**](catalog/research-skills.md)。先建 product-marketing 上下文，按需启用技能；广告花费、邮件发送、CRM 写入与数据外发需单独授权，工业出海不能直接套 SaaS 增长承诺。

### 游戏、创作、CAD 与业务研讨

- **[Open source games](catalog/resources-email.md)**：按类型发现完整游戏、重制项目与源码；CC0 仅覆盖目录，部分游戏另需合法原版数据。
- **[img2threejs](catalog/design-resources.md)**：参考图转程序化 Three.js，不是摄影测量或精确工程反求；安装器可能改多个 Agent 的技能链接。
- **[Stageshow](catalog/design-resources.md)**：营销页产品 UI 插画、光标故事与短动效；示意点击不是浏览器自动化，App 图标不在 MIT 范围。
- **[Godogen](catalog/design-resources.md)**：Claude/Codex 多引擎游戏生成与运行证据闭环；素材工具可能需要 NVIDIA/付费 API，--force 会清空目标目录。
- **[Anatomy](catalog/design-resources.md)**：SVG/WebGL 等轴测机械与技术解释图；可选 3D 为 beta，不替代 CAD/工程计算。
- **[Sparkling](catalog/research-skills.md)**：用反常、证据与白板共创业务判断；AGPL-3.0-only，缺资料先取证，不强行给确定答案。
- **[ClassCAD AI](catalog/mcp-api-tools.md)**：约束草图、参数化零件、装配与验证；MCP MIT 不等于引擎免费商用/STEP 导出，分享 relay 另有外发边界。
- **[ZenTrade](catalog/quant-data.md)**：自托管美股研究、回测和纸面交易；Agent 先用只读 key，混合许可需逐项核对，不连接真实券商下单。

- 想让代码场景或已有GLB/glTF骨骼角色呈现可旋转、动态光照的实时像素风：看 [**Pixel-art Gaussian Splats**](catalog/design-resources.md)。Three.js + Spark，不是完整游戏引擎；Kervan示例模型不受MIT覆盖，动画/大地图/移动性能需独立验证。

- 想挑 Chrome 扩展、先读中文说明再决定装不装：看 [**ChromeAppHeroes**](catalog/resources-email.md)。按编号收录上百篇扩展评测，只作候选清单；文章含作者推广，且仓库许可（GPLv3 / Anti-996 / ISC）三处不一致，安装前核商店权限与时效，不得整站转载。

- 想给自己或朋友的猫狗做插画头像：看 [**Uchinoko Maker**](catalog/vision-office.md)。部件拼装、免费、导出 2816×2816 PNG；但**著作权归运营方，仅许可个人与家庭使用**，商业用途、周边销售、名片海报与网站设计都被条款明确禁止。
