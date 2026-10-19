# Academic Research Skills — ZCode 适配版

[![Upstream](https://img.shields.io/badge/upstream-academic--research--skills-blue)](https://github.com/Imbad0202/academic-research-skills)
[![Version](https://img.shields.io/badge/version-3.23.1-blue)](./.zcode-plugin/plugin.json)
[![License: CC BY-NC 4.0](https://img.shields.io/badge/license-CC%20BY--NC%204.0-lightgrey)](./LICENSE)

**ARS(Academic Research Skills)** 的 [ZCode](https://zcode.ai) 插件适配版,基于上游 Claude Code 插件 [academic-research-skills](https://github.com/Imbad0202/academic-research-skills) 改造,内容同步至上游 **v3.23.1** 发布版(main 分支提交 [`cfd081d`](https://github.com/Imbad0202/academic-research-skills/commit/cfd081d8f),2026-10-16,补丁版:写入范围守卫修复与覆盖说明、sr-screener 按 RFC 4180 解析 CSV、routing core 收紧 `[direct-mode]` 逃生舱、Gemini 4 Argon 试运行校验模型),可在 ZCode 插件市场中直接安装。

一套契约审计(contract-audited)的学术研究全流程能力:**调研 → 写作 → 诚信检查 → 同行评审 → 修订 → 复审 → 定稿**。

## 在 ZCode 中安装

### 方式一:从 GitHub 市场安装(推荐)

1. 打开 ZCode 的**插件市场**(Plugin Marketplace)。
2. 点击**添加 → 添加插件市场**(Add → Add Plugin Marketplace)。
3. 粘贴本仓库的 GitHub 地址(例如 `https://github.com/e2mcc/academic-research-skills-zcode`),点击**添加**。
4. 添加成功后,进入**个人(Personal)**页签,找到市场 **academic-research-skills-zcode** 下的 **Academic Research Skills (ZCode)**,核对版本号后点击**安装**。
5. 安装后可在**设置 → 插件**中管理启用/停用。

### 方式二:本地目录安装(测试用)

将本仓库克隆到本地后,在"添加插件市场"时直接粘贴仓库根目录路径(包含 `marketplace.json` 的目录)即可,后续步骤同上。

## 五个技能

| 技能 | 说明 |
|---|---|
| `deep-research` | 13 个代理角色的深度调研流水线:研究问题 formulation、系统性文献检索、来源验证、跨源综合、偏倚风险评估、元分析、APA 7.0 报告编译、事实核查等 8 种模式 |
| `academic-paper` | 12 个代理角色的论文写作流水线,11 种模式(大纲/撰写/摘要/文献综述/格式转换/引用检查/AI 披露/rebuttal 审计等),支持 6 种论文类型、5 种引用格式、LaTeX/Pandoc/PDF 输出 |
| `academic-paper-reviewer` | 多视角模拟同行评审:5 席位角色分离评审团(Journal-Fit Reviewer + 3 位同行评审 + 魔鬼代言人),支持完整评审、复审、快速评估、方法论聚焦、评审者校准等模式 |
| `academic-pipeline` | 端到端编排器:research → write → integrity → review → revise → re-review → finalize 十阶段全流程 |
| `sr-screener` | 系统性/范围/快速综述的研究筛选(v3.23.0 新增,8 种模式):把计划书转为用户确认的纳入/排除规则,两位盲审 AI 审查者 + 第三位裁决者,固定顺序排除代码、批次可续跑、质量控制(种子研究、kappa/PABAK)、PRISMA 2020 数字、EndNote/Zotero RIS 分组,产出交给 `academic-paper` 的 `literature_corpus[]` |

## 斜杠命令(16 个)

安装后可用 `/ars-*` 系列命令:

`/ars-full`(全流程)、`/ars-plan`(研究规划)、`/ars-lit-review`(文献综述)、`/ars-outline`(论文大纲)、`/ars-abstract`(摘要)、`/ars-reviewer`(模拟评审)、`/ars-revision`(修订)、`/ars-revision-coach`(修订教练)、`/ars-rebuttal-audit`(rebuttal 审计)、`/ars-citation-check`(引用检查)、`/ars-disclosure`(AI 使用披露)、`/ars-format-convert`(格式转换)、`/ars-3w`(三段式文献扫描)、`/ars-cache-invalidate`(缓存失效)、`/ars-mark-read` / `/ars-unmark-read`(阅读标记)

## 环境要求

- **Python 3(可选)**:引用校验闸门、文献检索客户端(arXiv / Crossref / OpenAlex / Semantic Scholar)等脚本使用 Python。未安装 Python 时插件优雅降级,核心工作流不受影响。
- **网络**:文献检索与引用校验需要访问学术 API。
- 输出 PDF/LaTeX 时需要相应工具链(如 `pandoc`、LaTeX 发行版),按需安装。

## 与上游的差异(适配说明)

本仓库对上游做了**最小化适配**,技能内容(5 个技能目录、`shared/`、`scripts/`、`docs/`、`examples/`)与上游 v3.23.1(提交 `cfd081d`,2026-10-16)逐字节一致——唯一例外是 sr-screener 的 7 处 agent 引用按本插件命名空间改为 `academic-research-skills-zcode:screening_reviewer_agent`,便于后续同步:

1. **插件清单**:新增 `.zcode-plugin/plugin.json`(ZCode 原生清单),显式声明 skills / commands / hooks / agents 组件。
2. **市场清单**:新增仓库根级 `marketplace.json`(ZCode 支持的目录格式),插件以仓库根为源(`source: "./"`)。
3. **技能引用前缀**:16 个命令文件、会话启动宣告脚本,以及 sr-screener 的 agent 引用(SKILL.md、orchestration/protocol_template 参考、配置模板与示例、根级 `agents/screening_reviewer_agent.md`)中的 `academic-research-skills:<name>` 前缀统一改为 `academic-research-skills-zcode:<name>`。
4. **排除开发资产**:未收录 `evals/`、`plugin-evals*/`、`tests/`、`audits/`、`.claude/`、`.github/`、`pi/` 等仅用于上游开发/CI 的目录(约 21MB),运行时无引用。
5. **符号链接移除**:上游 `skills/` 目录(5 个指向根目录技能的符号链接)未收录,ZCode 清单直接声明五个技能目录。
6. 原版 README 保留为 [README.upstream.zh-CN.md](./README.upstream.zh-CN.md) / [README.upstream.md](./README.upstream.md)(其相对链接均仍有效;固定在 v3.22.2 切点,不随同步更新,最新版见上游仓库)。

钩子兼容性:上游 `hooks/hooks.json` 使用的 `SessionStart` 与 `PreToolUse` 事件、`${CLAUDE_PLUGIN_ROOT}` 变量均为 ZCode 支持的标准格式,未做改动。

## 同步上游更新

```bash
# 拉取上游最新版本后,将技能相关目录覆盖到本仓库(保留 .zcode-plugin/ 与 marketplace.json)
# 需同步检查:commands/*.md 与 scripts/announce-ars-loaded.sh 中的技能前缀
```

同步记录:

- **2026-10-19(v3.23.1)**:同步上游 v3.23.1(main @ `cfd081d`;较 v3.23.1 标签多出的 #984 CHANGELOG 备注与 #985 pi wrapper 修复均属本仓库排除的开发资产,不影响移植内容)。修复:#982 sr-screener 解析 CSV 只嗅探分隔符、引号规则遵循 RFC 4180(#979);#972 写入范围守卫补上插件范围 agent 类型与外来 timeout 二进制两条未检查路径(#970/#971),#973/#974 守卫实际覆盖范围与真实 hook 载荷文档;#961 routing core 明确消息中间出现的 `[direct-mode]` 令牌不是逃生舱(#892);#981 Gemini 4 Argon 列为试运行 Google 校验模型;#963/#978 Windows 路径 lint 修复(as_posix);#965/#977 `exception_reason` 必须为字符串;THIRD_PARTY 收录 md-to-word(#969)。适配:ZCode 打包元数据升至 v3.23.1(plugin.json、marketplace.json、CITATION.cff、README 徽章与同步记录)。
- **2026-10-05(v3.23.0)**:同步上游 v3.23.0(main @ `6ab4b03`)。新增第五个技能 `sr-screener`(#919,由 @erfanz97 贡献):协议驱动的研究筛选,8 种模式(protocol / quick / pilot / ta-screen / ft-screen / adjudicate / audit / report),新增根级插件代理 `screening_reviewer_agent`(共 4 个)。修复:#942 运行记录仅经可信读取访问、#943/#947/#948 checkpoint 证据改由指定文件夹重放、#944 频谱计数、#945/#946 记录解析错误不再引用文件内容、#951 CSV 导出公式中和。适配:sr-screener 的 7 处 agent 引用改为 `academic-research-skills-zcode:` 前缀。
- **2026-10-02(v3.22.3)**:同步上游 main @ `9201425`,补齐 #941(#936:完整性闸门判定 NOT_FOUND 的文献进入 passport 新增的 `excluded_sources[]` 契约,后续写作派发不再引用;C2 内部一致性检查新增摘要与正文比对;独立修订模式声明摘要未再生成)。
- **2026-10-02(v3.22.2)**:首次适配,基线为上游 main @ `471082d`(含 v3.22.2 及其后 #910–#940)。

## 署名与许可
> 注:GitHub 页面侧栏会把许可证显示为 "Other",这是平台限制——GitHub 的自动识别不支持 NonCommercial 系列 CC 许可证(上游仓库同样如此)。本项目的许可证以 [LICENSE](./LICENSE) 文件为准:CC BY-NC 4.0。根据该许可证条款,本演绎版本必须以相同许可证发布,不可更换为 MIT 等宽松许可证(除非获得上游作者授权)。


- 上游作者:[Cheng-I Wu (Imbad0202)](https://github.com/Imbad0202),原项目见 [academic-research-skills](https://github.com/Imbad0202/academic-research-skills)
- 许可证:**CC BY-NC 4.0**(署名-非商业性使用),见 [LICENSE](./LICENSE);本适配版同样以 CC BY-NC 4.0 发布
- 第三方组件:[THIRD_PARTY.md](./THIRD_PARTY.md);引用格式:[CITATION.cff](./CITATION.cff)

## 试用示例

安装后新建任务,输入:

> 帮我对"大语言模型在系统性文献综述中的应用"做一个快速文献调研,输出研究问题、检索策略和 10 篇核心文献。

预期:`deep-research` 技能被触发,按其调研流水线产出结构化调研报告。
