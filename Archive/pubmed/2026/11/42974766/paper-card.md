## 01 基本信息

- **标题**：Varied Ensembles of Long-range ChROmatin interactions drive chromatin compartmentalization
- **作者与单位**：Ostwal, Yogesh; Muzzopappa, Fernando; Heurteau, Alexandre; Raffel, Raoul; Veluchamy, Alaguraj; Eswara, Karthik; Boudellioua, Ahlem; Ali, Shakila; Kumari, Reema; Depierre, David; Vadlamani, Satya; Schickele, Naomi; Schaak, Stephane; Erdel, Fabian; Cuvier, Olivier; Fischle, Wolfgang（KAUST 等，具体单位未在摘要中逐一列出）
- **期刊/预印本平台**：Nucleic Acids Research
- **年份**：2026-11-03（在线日期）
- **论文类型**：研究论文（实验 + 模拟）
- **领域**：三维基因组 / 染色质组织 / 表观遗传学
- **关键词**：chromatin compartmentalization, HPL-2, LIN-61, H3K9me2, VELCROs, Hi-C, polymer simulations, C. elegans
- **DOI/arXiv 号**：10.1093/nar/gkag1082
- **代码**：https://doi.org/10.5281/zenodo.22817233
- **数据**：GEO: GSE271747 (Hi-C), GSE271919 (RNA-seq), GSE271927 (ChIP-seq)
- **阅读日期**：未提供
- **该文在课题方向中的位置**：本文属于「三维基因组 × 实验扰动 + 物理模拟」交叉方向，核心贡献是提出 VELCROs（Varied Ensembles of Long-range ChROmatin interactions）作为染色质区室化（compartmentalization）的驱动单元，并通过 Hi-C、ChIP-seq 与粗粒化聚合物模拟相结合，建立"高密度 HPL-2 + LIN-61 + H3K9me2 位点 → 随机长程互作网络 → B 区室形成"的机制模型。对三维基因组 × AI 方向的可迁移点在于：其"密度而非强度"的特征编码思路、区室化作为相变（phase transition）的物理框架，以及 Hi-C 数据驱动的模拟-实验闭环验证策略。

---

## 02 一句话总结

本文通过 C. elegans 突变体 Hi-C 与 ChIP-seq 分析，发现 HPL-2、LIN-61 与 H3K9me2 三阳性位点的高密度（而非单个位点强度）定义了 B 区室互作界面，并利用粗粒化聚合物模拟证明这类"VELCROs"互作网络足以驱动染色质区室化的相变式分离。

---

## 03 研究问题

- **具体问题**：哪些染色质组分（chromatin components）在分子层面驱动真核基因组 A/B 区室化？其互作的组织原则是什么？
- **为什么重要**：A/B 区室化是三维基因组组织的基本层级，与基因调控、复制时序、衰老等密切相关；但驱动区室化的分子机制长期不明，缺乏可遗传扰动的实验证据。
- **现有方法不足**：
  - 还原论模拟（如仅依赖 HP1 或 H3K9me3）无法解释区室化的稳健性；
  - 单基因敲除（如 hpl-2 或 lin-61 单突变）不产生区室化缺陷，提示功能冗余；
  - 缺乏将"位点强度"与"位点密度"区分开来的系统分析框架。
- **精确研究问题**：Can high-density ensembles of HPL-2 + LIN-61 + H3K9me2 sites (VELCROs) drive chromatin compartmentalization in a manner that is independent of individual peak intensity and robust to single-factor loss?

---

## 04 背景与发展脉络

> 注：以下脉络主要基于本文框架，部分经外部核验（标注）。

1. **区室化现象的发现与描述（2012–2015）**：Hi-C 揭示 A/B 区室（Lieberman-Aiden et al., 2009）；C. elegans 中区室化与染色体臂相关（Crane et al., 2015）。[外部核验]
2. **HP1/H3K9me 作为异染色质互作介质的模型（2015–2020）**：HP1 体外相分离（Larson et al., 2017; Strom et al., 2017）；H3K9me 缺失导致异染色质去组织化（Wang et al., 2019）。[外部核验]
3. **弱互作/多价互作驱动区室化的理论（2018–2022）**：block copolymer 模型、相分离框架（Jost et al., 2017; Nuebler et al., 2018）；"多价 bridging" 概念。[外部核验]
4. **本文位置**：在 C. elegans 中提供首个系统性遗传扰动证据，将"位点密度"而非"位点强度"确立为区室化的关键参数，并提出 VELCROs 作为区室化的功能单元，同时用最小聚合物模型验证其充分性。

---

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|------|------|----------------|----------|
| 区室化驱动因子不明 | 已知 HP1/H3K9me 参与异染色质，但单因子缺失不足以破坏区室化 | 功能冗余：HPL-2 与 LIN-61 可能协同工作 | Results 图 2B–C：单突变保留区室化，双突变丧失 |
| 位点强度 vs 密度混淆 | 传统分析聚焦 peak 强度，无法解释区室化稳健性 | 区室化依赖高密度位点的协同互作，而非单个强位点 | Results 图 4A、5E：密度而非强度区分 A/B |
| 模拟缺乏实验锚定 | 聚合物模拟参数缺乏真实染色质组分约束 | 缺乏可遗传扰动的实验数据来约束模拟 | Methods 模拟节：以 ChIP-seq 位点分布为输入 |
| 区室化与转录的耦合不清 | 转录抑制未改变区室化 | 区室化不直接由转录活动驱动 | Results 图 3F、S7：RNA 变化与区室化缺陷不相关 |

---

## 06 核心思想

1. **表面方法**：对 C. elegans 野生型与多种染色质调控因子突变体（hpl-2、lin-61、hpl-2;lin-61、set-32; met-2 set-25、cec-4）进行 Hi-C、ChIP-seq 与 RNA-seq，结合粗粒化聚合物模拟，系统评估区室化缺陷及其分子基础。

2. **核心洞察**：区室化不是由单个强互作位点（peak intensity）决定，而是由高密度的 HPL-2 + LIN-61 + H3K9me2 三阳性位点形成的"随机互作网络"（VELCROs）驱动。这类互作是**组合性、随机性、多价性**的，而非确定性的点对点 loop。其强度由位点密度决定，且对单因子缺失具有冗余缓冲。

3. **可能的普适教训 [Analysis]**：三维基因组中"结构单元"的定义应从"确定性互作"转向"统计性互作集合"；区室化可能本质上是多组分、多价互作的相变现象，而非单一分子事件的总和。这对 AI 建模的启示是：特征工程应关注位点密度/分布统计量，而非仅峰值强度。

---

## 07 方法总览

- **输入**：C. elegans 野生型与突变体胚胎（Hi-C、ChIP-seq、RNA-seq）；ChIP-seq 位点分布（HPL-2、LIN-61、H3K9me2/3 等）
- **输出**：区室化缺陷定量（PC1/PC2 变化）、VELCROs 互作网络特征、模拟 Hi-C 矩阵
- **模块**：
  1. Hi-C 数据处理与区室化分析（HiCExplorer 流程：比对、矩阵构建、KR 归一化、PCA）
  2. ChIP-seq 峰检测与密度分析（MACS2、PyMaSC、IDR）
  3. 差异区室化分析（saddle plot、differential saddle plot）
  4. 粗粒化聚合物模拟（LAMMPS，bead 模型，互作势由 ChIP-seq 位点分布参数化）
  5. FRAP 活体成像（HPL-2 动力学）
- **训练**：不适用（无监督/物理模拟，无神经网络训练）
- **工具**：HiCExplorer、MACS2、PyMaSC、deepTools、LAMMPS、R
- **文字流程**：收集突变体 → Hi-C/ChIP-seq/RNA-seq → 区室化定量（PC1/PC2）→ 鉴定区室化缺陷突变体 → 分析缺陷位点的染色质特征（密度 vs 强度）→ 定义 VELCROs → 以 ChIP-seq 位点分布参数化聚合物模拟 → 模拟 Hi-C 验证 VELCROs 充分性 → FRAP 验证 HPL-2 动力学差异

---

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|------|------|----------|----------|----------|------------------------|
| Hi-C 区室化分析 | 定量 A/B 区室及突变体差异 | 区室化是核心表型 | 输入：Hi-C reads；输出：PC1/PC2、saddle plot | Results 图 1–2 | 无法定量区室化缺陷 |
| ChIP-seq 峰密度分析 | 计算 HPL-2/LIN-61/H3K9me2 位点密度 | 区分密度与强度 | 输入：ChIP-seq reads；输出：峰密度/强度 | Results 图 4–5 | 无法建立分子特征与区室化的关联 |
| 差异 saddle plot | 比较突变体 vs 野生型的互作偏好 | 识别区室化缺陷类型 | 输入：Hi-C 矩阵；输出：差异互作图 | Results 图 3B–C | 无法区分 B–B 丢失与 A–B 增益 |
| 粗粒化聚合物模拟 | 检验 VELCROs 是否足以驱动区室化 | 建立因果充分性 | 输入：位点分布、互作势；输出：模拟 Hi-C | Results 图 6 | 无法区分相关性与因果性 |
| FRAP | 测量 HPL-2 在 A/B 区室的动力学 | 验证互作稳定性差异 | 输入：荧光恢复曲线；输出：扩散时间/不动比例 | Results 图 5H–I | 缺乏互作动态的直接证据 |

---

## 09 关键公式符号

> 本文为实验 + 模拟论文，公式较少，以下为理解模拟部分必需的公式。

1. **FENE 键势**（模拟中连接相邻 bead）：
   \[
   U_{\text{FENE}}(r) = -\frac{1}{2} K_{\text{FENE}} R_0^2 \ln\left[1 - \left(\frac{r}{R_0}\right)^2\right]
   \]
   - \( r \)：相邻 bead 间距
   - \( K_{\text{FENE}} = 30\,k_BT \)：键弹性常数
   - \( R_0 = 1.6\sigma \)：最大键长

2. **Weeks–Chandler–Andersen (WCA) 排斥势**（排除体积）：
   \[
   U_{\text{WCA}}(r) = 4\varepsilon\left[\left(\frac{\sigma}{r}\right)^{12} - \left(\frac{\sigma}{r}\right)^6\right] + \varepsilon, \quad r < 2^{1/6}\sigma
   \]

3. **Kratky–Porod 弯曲势**（纤维刚度）：
   \[
   U_{\text{bend}}(\theta) = K_{\text{BEND}}(1 - \cos\theta)
   \]
   - \( \theta \)：三个相邻 bead 的夹角
   - \( K_{\text{BEND}} = l_p k_BT \)，\( l_p = 1.5\sigma \)（持久长度）

4. **截断 Lennard–Jones 互作势**（位点间吸引）：
   \[
   U_{\text{LJ}}(r) = 4\varepsilon_{1-2}\left[\left(\frac{\sigma}{r}\right)^{12} - \left(\frac{\sigma}{r}\right)^6\right], \quad r < r_{\text{cut}} = 2.5\sigma
   \]
   - \( \varepsilon_{1-2} \)：由位点特征决定（见下）

5. **互作强度参数化**：
   \[
   \varepsilon_{1-2} = \varepsilon_{\text{chromatin}} + \varepsilon_{\text{peak}} N_1^{\text{peaks}} N_2^{\text{peaks}} + \varepsilon_{\text{loop}} N_1^{\text{loops}} N_2^{\text{loops}}
   \]
   - \( N_i^{\text{peaks}} \)：bead i 中 ChIP-seq 峰数
   - \( N_i^{\text{loops}} \)：bead i 中 loop 锚点数
   - \( \varepsilon_{\text{peak}} = 0.24\,k_BT \)，\( \varepsilon_{\text{loop}} = 0.12\,k_BT \)，\( \varepsilon_{\text{chromatin}} = 0.01\,k_BT \)
   - 若仅一个 bead 含峰/loop，额外加 \( \varepsilon_{\text{peak-chromatin}} = 0.075\,k_BT \) 或 \( \varepsilon_{\text{loop-chromatin}} = 0.01\,k_BT \)

6. **FRAP 归一化**：
   \[
   I_{\text{norm}}(t) = \frac{I_B(t) - I_{BG}(t)}{I_{\text{REF}}(t) - I_{BG}(t)}
   \]
   - \( I_B \)：漂白区强度；\( I_{\text{REF}} \)：参考区强度；\( I_{BG} \)：背景

---

## 10 实验设计与证据链

- **数据集/群体**：C. elegans 晚期胚胎（60–200 细胞期）；野生型 N2 与突变体：hpl-2(tm1489)、lin-61(tm2649)、hpl-2;lin-61、set-32(red11); met-2(n4256) set-25(n5021)、cec-4(ok3124)
- **规模**：Hi-C 与 ChIP-seq 各条件生物学重复 2–3 次（Methods 节）；模拟为 3 次独立运行
- **指标**：PC1/PC2 振幅、saddle plot 强度、B–B/A–A/B–B/A–B 互作偏好、TAD 强度、FRAP 不动比例
- **基线**：野生型 N2
- **骨干/仪器**：Hi-C（DpnII 酶切）、ChIP-seq（HPL-2、LIN-61、H3K9me2/3 抗体）、共聚焦显微镜（FRAP）
- **oracle 输入**：模拟中 ChIP-seq 位点分布来自实验数据（非预测）
- **评测协议**：突变体 vs 野生型的差异分析；模拟 vs 实验 Hi-C 的 SSR 比较

| 实验 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|------|-------------|------------|------|-------------|-------------------|------|
| 突变体 Hi-C 区室化分析 | HPL-2/LIN-61 参与区室化 | 单突变 vs 双突变 vs WT | 单突变保留区室化，双突变丧失 | HPL-2 与 LIN-61 功能冗余 | 不能排除其他因子参与 | Results 图 2B–C |
| 位点密度 vs 强度分析 | 密度决定区室化 | 按密度/强度分层比较 | 密度与 PC1 相关，强度不相关 | 密度是区室化的关键参数 | 未测试所有组蛋白修饰 | Results 图 4A、5E |
| VELCROs 缺失验证 | VELCROs 是区室化必要条件 | 区室化缺陷突变体 vs 非缺陷 | 缺陷突变体 VELCROs 消失 | VELCROs 与区室化共变 | 相关性不等于因果 | Results 图 5B |
| 聚合物模拟 | VELCROs 足以驱动区室化 | 有/无 VELCROs 互作势 | 有 VELCROs 时出现区室化 | VELCROs 充分性成立 | 模拟为最小模型，未含全部因子 | Results 图 6 |
| 模拟相变分析 | 区室化为一级相变 | 逐步降低位点密度 | 临界密度 70–80% 处突变 | 相变特征 | 仅限模拟系统 | Results 图 6D–G |
| FRAP | B 区室 HPL-2 更稳定 | 区内 vs 区外 | 区内不动比例更高 | HPL-2 在 B 区室停留更久 | 未直接测量互作亲和力 | Results 图 5H–I |
| α-amanitin 处理 | 区室化不依赖转录 | 处理 vs 未处理 | 区室化无显著变化 | 区室化与转录解耦 | 未检测所有转录类型 | Results 图 S7A–B |

---

## 11 结论正确解读

- **任务范围**：本文结论限于 C. elegans 晚期胚胎的稳态区室化维持，不涉及区室化的从头建立（de novo establishment）或细胞周期动态。
- **oracle/真值输入**：模拟以实验 ChIP-seq 位点分布为输入，属于"实验约束的模拟验证"，非端到端预测。
- **端到端状态**：非端到端。实验与模拟为两阶段闭环，模拟仅验证充分性，未用于预测新突变体。
- **算力成本**：未提供具体算力信息（Not assessable）。
- **历史数据依赖**：依赖 C. elegans 参考基因组 WBcel235 与公开 ChIP-seq 数据集（GEO）。
- **模型依赖**：模拟为粗粒化 bead 模型，忽略序列特异性、loop extrusion 动态、核膜锚定等。
- **最难情形**：X 染色体区室化缺陷较弱，作者归因于其独特的 DCC 介导组织方式；常染色体臂间互作是主要分析对象。
- **群体/领域边界**：结论可能不直接推广到哺乳动物（着丝粒、LAD 组织更复杂）；作者在 Discussion 中明确说明需进一步验证。
- **不确定性**：突变体表型可能受发育时序影响；FRAP 仅测量 HPL-2，未测量 LIN-61 动力学。

**有边界的复述**：在 C. elegans 晚期胚胎中，HPL-2、LIN-61 与 H3K9me2 三阳性位点的高密度区域通过组合性长程互作（VELCROs）驱动 B 区室形成；该过程不依赖单个位点强度，且对单因子缺失具有冗余缓冲；粗粒化模拟表明这类互作足以在临界密度以上驱动区室化相变。

---

## 12 作者自认局限

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|------|----------|---------------------|------|
| 无法排除其他染色质因子参与 | 双突变仍可能保留部分区室化残余 | 需系统性筛选更多染色质调控因子 | Discussion 节 |
| 突变体表型可能受发育时序影响 | 分析限于晚期胚胎稳态 | 需研究区室化的从头建立过程 | Discussion 节 |
| 模拟为最小模型 | 未包含 loop extrusion、核膜锚定等 | 需更复杂、多参数模型 | Discussion 节 |
| 未直接测量互作亲和力 | FRAP 仅间接反映 HPL-2 停留时间 | 需单分子成像或生化重构 | Discussion 节 |
| 哺乳动物推广性未验证 | 着丝粒、LAD 组织更复杂 | 需在哺乳动物系统中验证 VELCROs 概念 | Discussion 节 |
| 未分析所有组蛋白修饰 | 仅聚焦 H3K9me2/3 | 需系统比较多种修饰的贡献 | Results 图 4 相关讨论 |

---

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|-----------------|---------------------|----------|----------|------|
| 密度-区室化相关性可能受基因组结构混淆 | 高密度区域可能同时富集其他特征（如复制时序、基因密度） | 若混淆变量存在，密度可能非因果 | 在控制基因密度、GC 含量后重新分析 | Results 图 4–5 未做多变量控制 |
| VELCROs 的"随机性"缺乏单细胞证据 | 群体 Hi-C 的弥散信号可能来自细胞间异质性 | 随机互作 vs 确定性互作的区分需要单细胞验证 | 单细胞 Hi-C 或成像验证 | Discussion 中作者也承认需进一步实验 |
| 模拟参数可能过拟合 | 能量参数（0.24/0.12 kT）仅对 C. elegans 染色体 I 优化 | 若参数不可迁移，模拟结论泛化性有限 | 用其他染色体或物种数据验证模拟 | Methods 模拟节未提供参数敏感性分析 |
| 冗余性结论可能受等位基因剂量影响 | 单突变体中残余蛋白可能足以维持功能 | 冗余性可能被高估 | 构建条件性双突变或蛋白快速降解系统 | Results 图 2 未做剂量分析 |
| FRAP 的 A/B 区室划分依赖 Hi-C 定义 | 循环论证风险：用 Hi-C 定义区室再验证互作差异 | 需独立的空间定义（如成像） | 结合显微镜空间定位 | Results 图 5H–I |

---

## 14 学到什么

> 标题：Agent 提炼的知识候选

1. **"密度而非强度"的特征编码原则**：在三维基因组建模中，区室化预测的特征应包含位点密度（单位长度内 peak 数），而非仅 peak 强度。可迁移到 AI 特征工程：将 ChIP-seq peak 密度作为图神经网络节点特征。
2. **组合性互作网络的建模思路**：VELCROs 表明区室化源于多对多、随机性互作，而非确定性 loop。AI 模型可考虑用集合/图嵌入表达"互作网络"而非单一边预测。
3. **相变框架用于区室化分类**：模拟显示区室化具有临界密度和一级相变特征。可迁移到 AI：将区室化预测建模为"相变检测"问题，而非连续回归。
4. **实验-模拟闭环验证策略**：以 ChIP-seq 位点分布为输入、Hi-C 为输出约束的模拟验证，可作为 AI 模型的可解释性验证框架。
5. **冗余性对扰动预测的影响**：单因子缺失不改变表型不代表该因子不参与——AI 模型需考虑功能冗余，避免基于单基因扰动的错误因果推断。
6. **FRAP 作为互作动力学的正交验证**：静态 Hi-C 与动态 FRAP 结合，可验证互作稳定性差异。AI 模型若预测互作强度，可用 FRAP 数据作为独立验证集。

---

## 15 与已有知识连接

- **Lieberman-Aiden et al., 2009**：Hi-C 首次揭示 A/B 区室；本文在此基础上将区室化的分子驱动因子具体化为 VELCROs。
- **Crane et al., 2015（C. elegans Hi-C）**：本文延续其 C. elegans 区室化分析框架，但聚焦于分子机制。
- **Larson et al., 2017; Strom et al., 2017（HP1 相分离）**：本文的 VELCROs 概念与 HP1 相分离模型一致，但强调多组分（HPL-2 + LIN-61 + H3K9me2）协同。
- **Nuebler et al., 2018（block copolymer 模型）**：本文模拟框架与其类似，但以实验 ChIP-seq 位点分布为输入，更具生物学约束。
- **Jost et al., 2017（相分离与区室化理论）**：本文的相变分析直接呼应其理论框架。
- **H3K9me2 vs H3K9me3 功能差异**：本文强调 H3K9me2（而非 H3K9me3）与 VELCROs 相关，与经典"H3K9me3 为组成性异染色质标记"的观点形成张力，值得关注。
- **候选方向 [Analysis]**：与哺乳动物 HP1α/HP1β 功能冗余的文献（如 Lachner et al., 2001）可对比；与 AI 驱动的区室化预测工作（如 DeepC、AUC 等）可结合，将 VELCROs 密度作为新特征。

---

## 16 研究想法

> 标题：Agent 生成的研究候选

1. **候选名称**：VELCRO-density 作为区室化预测的通用特征
   - **来源局限/观察**：本文在 C. elegans 中证明密度而非强度决定区室化；哺乳动物中是否成立未知。
   - **核心假设**：H3K9me2 + HP1 + 其他 reader 的三阳性位点密度在哺乳动物中同样预测 B 区室。
   - **初步方法**：在人类 GM12878/K562 Hi-C 与 ChIP-seq 数据上，计算三阳性位点密度，与 PC1 做回归；与现有区室化预测模型（如基于 CTCF/cohesin）比较。
   - **验证方式**：跨细胞类型、跨物种验证；扰动实验（如 HP1 降解）后预测失效。
   - **创新状态**：unverified

2. **候选名称**：基于 VELCROs 的生成式染色质折叠模型
   - **来源局限/观察**：本文模拟为最小模型，未包含 loop extrusion 与核膜锚定。
   - **核心假设**：将 VELCROs 作为"吸引中心"嵌入扩散模型或 GNN，可生成更真实的 Hi-C 矩阵。
   - **初步方法**：以 ChIP-seq 位点密度为节点特征，训练基于图的扩散模型生成 Hi-C；与仅用序列特征的模型对比。
   - **验证方式**：生成 Hi-C 与实验 Hi-C 的 SSR、A/B 区室一致性。
   - **创新状态**：unverified

3. **候选名称**：单细胞 VELCROs 异质性分析
   - **来源局限/观察**：本文 VELCROs 的"随机性"可能来自群体平均或真实单细胞异质性。
   - **核心假设**：单细胞 Hi-C 中 VELCROs 呈现 bimodal 分布（有/无），而非连续强度变化。
   - **初步方法**：分析已发表单细胞 Hi-C 数据（如 sci-Hi-C），计算三阳性位点对的共定位频率。
   - **验证方式**：与本文模拟的相变预测对比；统计单细胞间 VELCROs 的离散度。
   - **创新状态**：unverified

4. **候选名称**：VELCROs 与衰老/疾病中区室化丢失的关联
   - **来源局限/观察**：本文提到衰老中区室化丢失（Discussion），但未深入。
   - **核心假设**：衰老或癌症中 B 区室丢失源于三阳性位点密度下降，而非单个位点强度变化。
   - **初步方法**：分析衰老细胞或癌细胞系的 Hi-C 与 H3K9me2 ChIP-seq，计算密度变化与区室化丢失的相关性。
   - **验证方式**：统计显著性；与已知区室化丢失区域重叠分析。
   - **创新状态**：unverified

5. **候选名称**：多价互作强度的 AI 可学习表征
   - **来源局限/观察**：本文的 Lennard-Jones 参数化依赖人工设定能量值。
   - **核心假设**：神经网络可学习"多价互作势"的隐式表征，替代人工参数。
   - **初步方法**：以 ChIP-seq 位点分布为输入，训练神经势能函数，输出 Hi-C 矩阵；与本文模拟结果对比。
   - **验证方式**：模拟 Hi-C 与实验 Hi-C 的一致性；跨染色体泛化。
   - **创新状态**：unverified