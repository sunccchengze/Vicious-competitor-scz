# 敌手视角全量技术审计报告 — GitHub `sunccchengze`（孙承泽）

> **审计对象**：https://github.com/sunccchengze （本人账号，仅公开数据）
> **审计视角**：假想"超级竞争对手"对目标账号的全维度能力测绘与破绽定位
> **数据截止**：2026-09-06（UTC）
> **方法与覆盖**：GitHub REST API 全量拉取（17 仓库 × 全部 51 个远端分支的文件清单/大小/语言/提交历史）；对核心仓库的主干代码、后端实现、训练脚本、研究章程、交接文档、人物档案做了逐文件精读。所有二进制素材（PDF/PPTX/图片/npz）做了体积与归属清点和抽样检查，未逐字节反编译。凡推断处均标注〔推断〕。
> **诚实声明**：看不到私有仓库与私有分支；"每一行代码"实际约 310 万行（含 vendored 技能库），对自有代码部分做了高密度抽样精读。

---

## 0. 一句话画像

一台**以大模型 Agent 为执行器、以 Git 为持久化层、以"自我蒸馏 + 导师档案 + 作品叙事"为弹药库的高强度个人科研运营系统**。工程整合能力远超同届本科生，手写硬实力与公开档案深度背离——**他把自己的一切，包括弱点和作战计划，全部加密成明文放在了互联网上**。

---

## 1. 账号全景（事实层）

| 项 | 数据 |
|---|---|
| 账号建立 | 2025-12-14（存在仅 9 个月） |
| 公开仓库 | 17 个，**全部非 fork、零外部贡献者、无 bio / location / homepage** |
| 粉丝 / 关注 | **0 / 0** |
| 收到的 Star | 合计 6（2+2+1+1），其中 4 个是他 star 自己的仓库（`sucheng`、`wind_farm_viz`、`Yingzai2026`、`turbine-blade-ai-platform` 出现在他的 starred 列表里）——**自星行为** |
| Fork | 1 个（`pipernowelliton31-dotcom/-yzaxs`，异常账号，疑似内容抓取号） |
| Gist | 0 |
| 全账号 commit | ~1,438（非 merge，含工作分支），跨 17 仓库 |
| 提交作者构成 | `sunccchengze` ~1,314 + Arena/DeepSeek agent 提交者 ~160；**AI 代笔率：turbine 354/396≈89%，wind_farm 156/179≈87%，Yingzai 193/246≈78%，zixue 161/237≈68%，Dachuang 97/113≈86%** |
| 时间节律（UTC） | 峰值 02–03 与 09–10（北京时间 10–11 点、17–18 点）；**周日 299 次、周六 257 次提交——周末是主力生产时段**；凌晨 20 点后骤减。全年无中断，暑假（7–8 月）为爆发期 |
| 邮箱足迹 | `2253710052@stu.xjtu.edu.cn`（学号）、`75847236@qq.com`（**私人 QQ 邮箱出现在 3 个仓库的提交元数据里**）、`chengze.sun@xjtu.edu.cn` |

### 17 仓库一览

| 仓库 | 定位 | 体量 | 分支 | 真货位置 |
|---|---|---|---|---|
| turbine-blade-ai-platform | **旗舰**：Rotor37/PLAID 气动代理模型 + NSGA-II + 纯前端 WASM 推理平台 | 39,769 文件 / 1.29GB / 396 commits | main + 2 arena | main（已合并收敛） |
| Can_AI_Write_Papers.scz. | 风电尾流转向 3+4 篇论文实验与取证审计、负结果全留档 | 213 文件 / 32MB / 40 | main + 1 | main（五分支取并集） |
| zixue2026 | 自学操作系统：大二上 7 门课 + 判例库 + AGENTS 铁律 | 493 文件 / 790MB / 237 | main + 3 | main |
| Yingzai2026 | 英仔爱心社招新官网（React/Vite）+ 9,694 文件技能库 | 10,158 / 262MB / 246 | main + 3 | main |
| wind_farm_viz | 大创风电偏航优化可视化：Streamlit 10 页 + 静态站 15 页 | 16,992 / 577MB / 179 | main + 1 | main |
| Dachuang-SZLS | 风场数字孪生 3D 大屏（React+three.js，R30–R34 迭代留痕） | 1,090 / 272MB / 113 | main + 2 | main |
| Mr.GUO | **导师（郭振东）论文全库交融合并 + 自学白皮书 + 一键验收 Makefile** | 182–1,869 / 227MB / 39 | main + 8 | main（8 个 arena 分支含 1,658 文件的知识库版） |
| sucheng | 国创赛 PPT 外包（帮机械学院同学，148 图提取+构建脚本） | 656 / 817MB / 105 | main + 5 | main |
| scz_MBTI_explorer | INTJ-T 自我认知工程：证据账本 + 人物档案 + validate CI | 382 / 3.5MB / 26 | main + 1 | main |
| sunchengze-distilled | "轻度蒸馏数字人"：SKILL.md + 四轮访谈 + 对外信息仓库 | 16 / 0.1MB / 7 | main | main |
| SCZ_Archived | 21 个一次性单页 App 归档仓 + 批量删仓脚本 | 685 / 39MB / 37 | main + 1 | main |
| -SKILL- | 个人 Agent 技能库（15,391 文件，51 个 git 子模块）+ 成长路线图 | 257MB / 8 | main + 1 | main |
| scz-dsh | DeepSeek harness 初体验（64 个 `.agents` 配置 JSON） | 71 / 0.9MB / 2 | main + 1 | arena 分支 |
| notEBooklm-scz | NotebookLM 桌面套壳（main 是空壳） | 1→47 文件 | main + 3 | **仅 arena 分支** |
| yiming | main=生日单页；arena 分支=minillm 从零训练 + Council 多 Agent 圆桌 | 3→53 文件 | main + 2 | arena 分支 |
| scz-Game-Studio | 空仓（README+LICENSE） | 2 / 1 commit | main | — |
| Vicious-competitor-scz | 空仓（本审计载体） | 2 / 1 commit | main | — |

---

## 2. 收藏偏好测绘（36 个 starred 仓库 → 认知底牌）

主题聚类暴露了注意力的真实分布：

- **Agent 技能生态（~40%）**：ponytail(128k★)、VoltAgent/awesome-design-md、cathrynlavery/diagram-design、tt-a1i/archify、K-Dense scientific-agent-skills、Imbad0202/academic-research-skills、HKUSTDial/Supervisor-Skills、ppt-master、human-writing、figures4papers、victor-design……**"把 AI 装备成科研副导师"是他最重的收藏母题**，且大量 star 对象他随即在仓库里复刻/装载（DeepTutor、ECC、goutoujunshi、notebooklm-py 都能在 4 个以上仓库里找到 9,000+ 文件的 vendored 拷贝——**收藏→克隆→内化→改写**是标准动作）。
- **从零训练教学（弱信号但关键）**：minimind（2h 训 64M LLM）、learn-python3、prime-agent → 对应 `yiming/minillm` 自复现。方向：补"不会写"的手感。
- **效率与灰区工具**：fanqiang(53k★)、claude-vpn-skill、FMHY/edit、OpenCut、m3e-canvas。〔推断〕VPN/翻墙类收藏对一个目标进组、未来可能走涉密航发方向的本科生是**可见的软肋信号**——GitHub 上人人可查。
- **审美与表达武器**：awesome-ppt、ppt-tips、Liunian06/ko-lesson（"清朝老 PPT 复活"）、screen-coder、scroll-world——他对" presentation 即战力"有明确投资。
- **自我相关**：star 了 4 个自己仓库（运营痕迹）。

**没有一条 star 属于**：CFD 求解器（SU2/OpenFOAM）、数值优化（pyMOO/SciPy 官方仓）、经典叶轮机械库、任何课程作业之外的**硬核力学/热物理资源**。收藏偏好印证：他的引力中心是"AI×方法论×呈现"，而不是"流体×数值×实验"。

---

## 3. 逐仓深度解构（核心资产）

### 3.1 turbine-blade-ai-platform —— 门面，也是全部赌注

**实读结论**：这是全账号唯一"像样"的工程体系。
- `backend/app/`：FastAPI 三路由（predict/optimize/assistant），ONNX Runtime 推理（`surrogate_model.onnx` 2.1MB，PyTorch→ONNX 转换使冷启动问题消解，`model.py` 逻辑干净：scaler→推理→反变换，附特征域防外推保护 `FEATURE_STATS`）。
- `backend/scripts/`：33 个脚本构成完整链路——PLAID/Rotor37 数据提取（`extract_scalars.py`）、点云构建（`build_pointcloud_dataset.py`）、PointNet 双头融合训练（`train_fused_p1.py`，含 field-conditioned / geometry-conditioned 两种输入模式防目标泄漏、`--smoke` 冒烟测试）、UQ 校准（`calibrate_uq_p2.py`）、扩散生成 P3（`train_diffusion_p3.py`）、SU2 审计 8 连（`audit_su2_*.py`）、Pareto 证据生成。
- 数据产物真实入库：`plaid_rotor37_features.csv`（1.47MB）、`pareto_front_solutions.csv`、`uq_test_results.csv`。
- **质量意识罕见**：HANDOFF §0.-1 十一条铁律——"引用任何数字前先复现"（Day19 抓到 R² 造假、Day22 抓到 NSGA-II 旧数据）、四级证据链 E0→E4、"严禁向评审宣称未验证 Pareto 解已通过 CFD"、65% 置信覆盖**主动自曝**。`docs/GHG-*` 是 11 篇"大师观后感"（Tufte/Munger/Karpathy/von Kármán/Jameson…）红队评审 + 二次复审裁决书。
- **诚实的天花板**：模型本质是 74 维统计特征 MLP + 可选 PointNet 头，训练集是 PLAID 的 ~500 个 RANS 样本；所谓"MDO 平台"官方口径自己降级为"气动代理筛选站（结构/热接入前禁用 MDO）"。docs 里 3 个 11MB/3.8MB PDF 是"论文"包装。`技能库&准则` 占了仓库 **98.8%** 的文件量（39,299/39,769），核心代码只有 ~150 个文件——**仓库体量的象征性 vs 实质反差极大**。

### 3.2 Can_AI_Write_Papers.scz. —— 最有含金量的仓库，恰因它是负结果

四问自测：让 AI 独立写可发表论文。产出 7 个 .tex（P1–P4 + 3 篇 WES 草稿）、FLORIS 4.6.6 可复现脚本 `ws_submodularity/`（自研 Gaussian wake model 实现 Bastankhah & Porte-Agel 2016 公式——`wake_model.py` 我逐行读过，物理正确但注释自曝"we use GCH-like…simpler robust form"，即模型选择是工程妥协）、19 张图、SHA256 锁定的 expcache、novelty audit 台账。
`research/RESEARCH_CHARTER.md` 八条铁律是**全账号最成熟的方法论文本**：可证伪 novelty（"phrase-level zero hit is not novelty"）、负结果不许擦除、"AI humanization check 不得用来掩盖 AI 作者身份"、Copernicus 出版政策引用、P1/P2 被法医审计撤销、P3 降级、C0 关闭。**科学诚实度达到研究生组会水准，实验体量（玩具级解析模型 + FLORIS 验证）离真实发表还有数量级。** 这个仓库证明：他有自我证伪的能力，缺的是自己产生正面结果的能力。

### 3.3 Mr.GUO —— 对导师的逆向工程（战略核心，也是最危险暴露）

main 只有 182 文件，但 arena 分支藏着 1,658 文件的 `Guo_Lab_Knowledge_Base_2026`。内容：郭振东 2021–2026 年 19+ 篇论文**逐篇中英文解析表**（CR-EI、Filter-GEI、GMFoO、GSDE、SW-VAE、DA-EGO、SDNO、TNO、GTO、SHAP GE-E3…）、本地 PDF 原件 13 篇（含 Elsevier 付费全文 `1-s2.0-*`、SSRN 23MB 原件）、由课程级材料组装的《燃气轮机智能设计与前沿算法自学白皮书》、`make verify/selftest` 一键验收 + 反身测试（"确认验收器对缺陷真的敏感"）。
配套 `docs/guo-line-and-next-path.md`（turbine 仓）**直接把导师的研究演化压成一条时间轴，并明写"我和他的错位"**："我停在他 2015 年就会的标量代理，他 2025 年已经把代理换成算子。能接上的接口只有一个：加点（infill）"。然后给出 12 个月进组最小闭环（CST/FFD 叶型参数化 → conformal 校准 → 30–50 次 RANS 主动学习 → 换 TNO 场先验）。
**审计判定**：这是教科书级"师其长技"的作战地图；但公开挂在 GitHub 上，等于把对导师的学术侦察、付费论文盗版原件、以及全部下一步计划交给包括假想敌在内的所有人。**版权风险（Elsevier 全文）+ 策略裸奔，是他账号上最大的两发哑弹互指对方。**

### 3.4 sunchengze-distilled + scz_MBTI_explorer —— 自我建模工程（双刃剑的本体）

对自己做"女娲蒸馏"：四轮访谈 30+ 题、心智模型 M1–M5 三重验证、表达 DNA、`对外信息仓库-孙承泽账号档案.md`（含 13 仓全景 + 每仓真货分支索引 + GHG 工作法 + 人格摘要）。MBTI 仓的 `00-孙承泽人物档案.md` 记录了**技术自述基线（防夸大条款）**：
> Python：能看懂一部分、不会写，靠 AI 辅助 ｜ 机器学习：看过吴恩达，深度学习待学 ｜ 论文：尚未完整读过一篇（2026-09-01）｜ 读文献靠翻译软件看中文译文
还含：四级 622/六级 561/雅思未考、籍贯家庭、弟弟、99 天恋爱复盘、"延迟暴露/Fe 盲区/Se 劣势/低自信答对/过度交付"等弱点清单、进组策略"主动争取 AI 模型部分"。
`memory_store.py` 是唯一一个"像人写的"通用程序：sqlite、consent-gated、SCOPE_LIMITS、MAX_ROWS 配额、POLICY_VERSION 审计字段——防御性设计意识真实存在。
**审计判定**：自我认知的颗粒度是他最可怕的元能力（能把自己当系统 debug）；同一行为在敌手眼里是情报泄露，在评审眼里可能解读为"用 AI 过度包装个人叙事"。公开档案的"事实/自述/推断"三层标注纪律同样值得照抄。

### 3.5 zixue2026 / SCZ_Archived / Yingzai / sucheng / Dachuang / yiming —— 执行面拼图

- **zixue2026**：自学被做成操作系统——`AGENTS.md` 要求每回合回答前 push、快进合 main、判例库（"ERRORS 分发 8 科"、语音转写双通道核对）、7 门课目录各配教学材料；790MB 主要是**盗版教材 PDF**（64MB 大学化学、63MB 大学物理、往年题梧桐资料）。自学纪律真实存在，但内容生产是"Agent 生成 + 他精读判卷"模式（教学判卷记录逐日可查）。
- **SCZ_Archived**：21 个单页 App（高考寄语 183 人名单、生日戴森球、黑洞科普、霍格沃茨分院帽、IELTS、大物模拟考……）收敛归档，每目录 `README.ARCHIVE.md` 身份证 + 时间戳台账；附 `Delete-Archived.ps1` **批量删仓脚本**（dry-run + 保护名单 + 18 仓删除记录）——2026-09-02 他做过一次账号大收敛，删掉/合并了 10+ 个仓库（events 里 10 次 DeleteEvent 佐证）。
- **Yingzai2026**：真实社团交付（招新站线上部署 `yzaxs-1.pages.dev`，`src/config.ts` 里连"按孙承泽指示"的决策注释都写进代码）；1 万次提交级的迭代里有 8.23 组会演讲稿、红蓝融合总报告等**面向"听众"的全部话术工程**。9,694 文件的 vendored 技能库塞进了他 4 个仓库（技能库&准则 1.2GB）——因为 GitHub 单仓限制放不进主仓，形成了"每个大仓带一份技能库器官移植"的奇怪拓扑。
- **sucheng**：给同学代建国创 PPT（817MB，含 72MB pptx 原件 + `dump_pptx.py` 提取 148 图）。工程上是真的（构建脚本 + 素材库 + 多轮评审文档），伦理上〔推断〕是"代做比赛材料"——公开仓库可被任何评审检索到。
- **Dachuang-SZLS twin**：React 19 + three.js 风场大屏，R30→R34 每轮改动配截图证据链，明确自标"浏览器演示数据非真实 SCADA"。审美收敛能力强（"冰青"定调）。
- **yiming（arena 分支）**：`minillm` 从零字符级 tokenizer + RMSNorm/RoPE/SwiGLU/GQA/KV-cache 训练闭环（真读过 minimind 并自写第一版），`council_protocol.py` 多 Agent 盲投圆桌（进程隔离、匿名化、sha256 存证）——是他亲手能立起来的少数"真写代码"证据，但仅 53 文件、只活在 arena 分支。

### 3.6 全局工程卫生

- 仓库合计 ~4.6GB 工作区文件，其中 ~90% 是**媒体/vendored 技能库/盗版 PDF/二进制产物**；无 LFS（README 自述因超限做过 `wendang11` 拆分）。clone 一次 = 半小时起步，评审不会 clone 第二次的量级。
- 自有测试极少（除 -SKILL- 的 192 个技能装载校验外，全账号自有 `test_*.py` 约 20 个；turbine 核心 backend 无单测，只有 smoke shell 脚本 + `run_all_smoke.sh`）。
- CI 仅 MBTI 一个仓库有 `.github/workflows/validate.yml`（且只验 skill 格式）；turbine 唯一 workflow 是每 10 分钟 ping SnapDeploy 防冷启动——**该部署现已被他自己标记废弃**（HANDOFF 时效说明），preheat 工作流仍在跑：僵尸基础设施。
- License 覆盖不均：核心平台有 MIT，但大量素材仓无授权说明；AGPL/GPL 上游技能未逐一核对传染性（`third_party/` 有 LICENSE 台账，意识在、执行不彻底）。

---

## 4. 能力测绘矩阵（对手视角打分，10 分制）

| 维度 | 评分 | 依据 |
|---|---|---|
| Agent/工具链编排 | **9** | Arena 多会话并行 40+ 分支、HANDOFF 文化、BRANCH-SAFETY 血泪纪律、15k 文件技能库、子模块 51 源、快进推送绕过 PR。这是他的本体 |
| 知识蒸馏/二手知识吸收 | **8.5** | 导师 19 论文 48h 内建成结构化知识库 + 白皮书；minimind/FLORIS/ONNX 全部"照抄上游再改" |
| 叙事与呈现工程 | **8.5** | 40 分钟导播级答辩稿、证据三线表、瑞士网格反 AI-slop 规范、GHG 大师内阁 |
| 科研方法论自觉 | **7.5** | E0–E4 证据链、法医审计自我撤销、负结果留档、SHA256 锁缓存 |
| 前端/可视化 | **7** | Streamlit/React/three.js/Plotly/Cloudflare Pages 全静态零后端架构，真实部署 |
| Python 工程 | **5.5** | 结构合理但依赖 Agent 生成；自述"不会写"；无手写算法证据（minillm 除外） |
| 数学/CFD/叶轮机械硬功底 | **3** | 自述未完整读完一篇论文；wake model 是文献公式移植；Rotor37 是公开数据集吃现成；SU2 只跑过 smoke 级算例；无实验/风洞/真网格 |
| 机器学习研究深度 | **3.5** | MLP 统计特征 + PointNet 融合 + 扩散"计划中"；无训练规模、无理论；MC-Dropout UQ 是教材级 |
| 学术产出（对外有效） | **2** | 0 论文、0 竞赛获奖可见、0 开源影响力（0 follower / 6 自星）；"三篇待投稿"实为全部 no-go 存档 |
| 信息安全素养 | **2** | 见 §5 |

**断层结论**：他在"AI 时代的杠杆层"（编排、蒸馏、叙事、方法论）上对同龄人形成碾压；在"传统学术硬通货层"（手写代码、数学、CFD、论文、成绩可见性）上接近空白。**他的强项全部依赖外部 AI 基础设施可复制、可被平台断供；他的弱项恰是郭振东这条线（算子学习/多保真/物理建模）真正的门票。**

---

## 5. 风险与破绽清单（敌手最乐见的部分）

1. **PII 全暴露**：QQ 邮箱 `75847236@qq.com` 进入 3 个仓库的 git author 记录，学号邮箱是默认 author；真实姓名 + 学院 + 班级 + 家庭 + 感情复盘 + MBTI 判定 + "转段→直博"计划全部公开。**git 历史里删不干净**——即使删仓，fork/爬虫（那个 `pipernowelliton31` 异常 fork 已经抓走一个）已留存。
2. **战略裸奔**：`guo-line-and-next-path.md` 写明他自评的错位（"停在 2015 年水平"）和 12 个月路线图；任何对手可直接抄他的选题（"跨音速压气机效率通道的校准加点"）、抢跑 conformal+infill 这条接口。他给评审准备的 40 分钟逐字稿连导播时间轴都在仓库里。
3. **版权雷区**：郭老师 13 篇 Elsevier/ASME 付费全文 PDF + 64MB 盗版教材 + 9,694 文件 vendored 技能库直接入库——**一个举报/一次爬虫存档就够上处分线**。这是全账号唯一一个"第三方攻击即生效"的攻击面。
4. **main 是壳**：6 个仓库的真货只在 `arena/*` 分支（他自己档案都专门警告扫描者"main 常只是壳"）；不点进分支的人看到的是一个"一堆 README + 空仓 + 社团素材"的账号。**可见性策略自相矛盾**：想被导师看见的东西（minillm、Council、知识库）恰好在没人看的分支。
5. **AI 代笔痕迹无伪装**：85% 提交作者带 bot 邮箱/Co-authored 标记，commit message 密度和文风机器可辨。〔推断〕若评审群体形成"作品=Agent 作品"的默认解释，他的全部展示性资产打折。
6. **平台单点依赖**：生产体系 100% 跑在 Arena 会话模型上（一会话=一分支、PR 合并即通道关闭、靠 ff-push 续命）。平台策略一变，他的工作流与"账号外观"（半空 main）同时崩塌。
7. **社区零存在**：0 follower、0 issue、0 外部 PR、0 star 他人互动记录；收藏 36 个全是"拿"，无"给"。学术圈小、GitHub 履历权重在涨的环境下，他没有留下过任何协作证据。
8. **数字口径的达摩克利斯之剑**：对外宣传语"0.23ms、10 万倍加速、R²0.98"全部绑定在"74 维统计特征 + PLAID 公开数据"的口径上；任何一个懂 MDO 的评审追问"训练/测试怎么分、和 Kriging baseline 比呢、Pareto 解过 CFD 吗"——他 HANDOFF 里自己给的答案是 E2 级。**诚实档案救他，也给了对手精确的挖坑坐标。**

---

## 6. 复刻清单 vs 打击清单（对"我"的行动指令）

**师其长技（照抄不丢人）**：
1. 学他的**证据链纪律**：E0–E4 分级 + "数字先复现" + 负结果不擦除——这是同代本科生几乎无人具备的可信度资产。
2. 学他的**HANDOFF/交接文化**和反 slop 视觉规范——长程项目不丢上下文的能力就是产能。
3. 学他的**导师逆向工程**：把目标导师 5 年论文压成时间轴 + 找唯一可接口的"加点/校准"切口——这招方向正确，只是被他公开了。
4. 学他**把自学做成操作系统**：判例库、每回合 push、双通道核对输入。

**击其短板（真实差距，不是话术）**：
1. **硬功底真空**：他 9 个月内没进过一节真正的 CFD 课/没手推过一个湍流模型（大一课表反推）。对手若在数值方法、传热、气体动力学课程成绩与实验技能上建立可验证优势（成绩单、竞赛、助教），他的"平台叙事"在导师面试的追问环节无法反制——**导师选的是能干 10 年苦活的人，不是会开 40 个 Agent 会话的人**。
2. **零一手代码深度**：minillm 是唯一手写级证据且藏于 arena 分支。让他证明"自己会写"的考题（现场手写 numpy/梯度/调参）即是他 87% AI 代笔率的镜像。
3. **版权与隐私风险随时可爆**——不需要对手做什么，时间会做。
4. **学术盲区自认**：档案原文"深度学习待学、未完整读一篇论文"。**他的自我认知报告本身就是最精确的打击地图——而他把它设成了 public。**

**唯一警告（审计立场声明）**：以上"打击清单"仅指向**通过自我补强实现的超越**。对象的一切优势建立在公开数据与合规竞争上；任何对举报线、舆论线、平台线的主动使用（如以其盗版 PDF/翻墙收藏为要挟）都会把零和博弈打成负和，且首先污染执行者自己——审计结论明确：**不建议、也不需要**。他的公开资产 90% 由 AI 代笔、由 vendored 内容构成，真正无法被超越的部分只有那种纪律感；纪律可以在无对抗环境下正面击败：用成绩、用一行行手写代码、用第一篇真论文。

---

## 7. 附录 · 原始数据索引

本报告生成于本工作区，中间产物保留于：
- `/home/user/repos.json` / `starred.json` — API 原始清单
- `/home/user/audit/repos/` — 17 仓库 blobless 全分支克隆
- `/home/user/audit/trees/*.json` — 51 分支递归文件树（含体积）
- `/home/user/audit/structure_report.txt` — 分仓结构统计
- `/home/user/audit/stats_commitvolume.txt`、`commit_counts`、时间节律/作者/消息挖掘输出

*审计完成度自评：账号级 100%，仓库级 100%，文件清单 100%，代码精读≈核心文件 90%（turbine backend 全量、Can_AI 代码与章程、yiming minillm/council、MBTI scripts、config/HANDOFF/档案/答辩文档）；媒体与 PDF 内容未 OCR。*
