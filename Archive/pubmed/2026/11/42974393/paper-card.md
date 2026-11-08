## 01 基本信息

- **标题**：AI and computational methods for reconstructing cell-state-specific gene regulatory networks from single-cell transcriptome and chromatin accessibility data in cancer: methods, applications, and perspectives
- **作者与单位**：Wang, Jinying; Chen, Fenjuan（单位未提供）
- **期刊/预印本平台**：Frontiers in Genetics
- **年份**：2026-11-03
- **论文类型**：Mini-review（叙述性综述）
- **领域**：单细胞多组学 × 基因调控网络 × 癌症
- **关键词**：gene regulatory network (GRN)、single-cell multi-omics、scRNA-seq、scATAC-seq、cell-state-specific、cancer、AI、chromatin accessibility
- **DOI/arXiv 号**：10.3389/fgene.2026.1982712
- **代码**：未提供
- **数据**：未提供
- **阅读日期**：未提供
- **在课题方向中的位置**：本文是面向「三维基因组/染色质组织 × AI 方法」课题的一篇方法学综述，聚焦于从单细胞转录组与染色质可及性数据重建细胞状态特异性基因调控网络（GRN）。其核心对象是 TF–cis-regulatory element–target gene 调控关系，与三维基因组中 enhancer-promoter 互作、染色质高级结构调控基因表达的问题高度相关。本文提供的输入数据分类学（same-cell paired / matched-unpaired / imputed / single-modality）、证据层级（统计关联→方向性预测→in silico perturbation→实验验证）以及方法家族划分（motif/co-accessibility、深度整合与图学习、动态与细胞状态特异性建模、虚拟扰动），对三维基因组领域的 GRN 建模与染色质构象预测具有直接的方法论参考价值。

---

## 02 一句话总结

本文系统梳理了从单细胞转录组（scRNA-seq）与染色质可及性（scATAC-seq）数据重建细胞状态特异性基因调控网络（GRN）的 AI 与计算方法，按输入数据设计和方法目标进行分类，提出从统计关联到实验验证的证据层级，并总结了这些方法在癌症 EMT、耐药、谱系可塑性和亚型分析中的应用与局限。

---

## 03 研究问题

- **具体问题**：如何从单细胞转录组和染色质可及性数据中重建细胞状态特异性的基因调控网络（GRN），并区分不同方法在输入数据要求、推断目标和证据强度上的差异？
- **为什么重要**：肿瘤异质性由遗传、表观遗传、微环境和随机因素共同塑造，其中细胞状态特异性调控程序是主要决定因素。GRN 提供了连接转录因子、顺式调控元件和靶基因的系统级模型，是理解耐药、转移和谱系可塑性的计算基础。
- **现有方法为何不足**：经典 GRN 推断依赖 bulk 转录组或单模态 scRNA-seq，无法区分 TF 表达与 TF 活性，也无法将远端增强子分配给其靶基因。已有综述多按方法类别组织或覆盖广泛癌症应用，缺乏以「细胞状态特异性 GRN 重建」为核心、以输入数据设计为分类轴的系统梳理。
- **精确研究问题**：Can cell-state-specific GRNs be reliably reconstructed from paired single-cell transcriptome and chromatin accessibility data, and what evidence level can each method family support?

---

## 04 背景与发展脉络

> 注：以下脉络主要基于本文框架，部分代表性方法经外部核验（标注）。

| 阶段 | 代表性方法/技术 | 优点 | 局限 | 本文主张的位置 |
|---|---|---|---|---|
| 经典 bulk GRN 推断 | WGCNA、ARACNe 等（外部核验） | 可处理 bulk 数据、计算成熟 | 混合细胞类型和状态，无法解析细胞状态特异性 | 被本文视为 baseline，不满足细胞状态分辨率需求 |
| 单模态 scRNA-seq GRN | SCENIC（Aibar et al., 2017，外部核验） | 结合共表达与 motif 富集，可识别 regulon 和细胞状态 | 无法区分 TF 表达与 TF 活性，缺乏染色质可及性证据 | 本文归入 motif/co-accessibility 家族，但指出其单模态局限 |
| 配对单细胞多组学技术 | sci-CAR (2018)、SNARE-seq (2019)、SHARE-seq (2020)、Paired-seq (2019)、10x Multiome | 同一细胞中同时测量染色质可及性与基因表达，直接提供 enhancer-promoter-gene 证据 | 数据稀疏、dropout 严重、批次效应强 | 本文的核心数据基础，定义 same-cell paired 设计 |
| 深度生成与图学习方法 | LINGER、scMultiomeGRN、DeepMAPS、GLUE | 可处理高维稀疏数据，显式建模基因-峰-细胞关系 | 依赖先验质量、可解释性差、需大量计算资源 | 本文归入深度整合与图学习家族 |
| 动态与细胞状态特异性建模 | Dictys、inferCSN、scMTNI、scTIGER | 沿轨迹或状态推断网络重连，捕捉调控动态 | 伪时间推断引入额外假设，状态边界模糊 | 本文强调「每状态一个网络」是近似，需报告边权重变化 |
| 虚拟扰动与因果推断 | CellOracle、Pano、GenKI、scTenifoldKnk、scPRAM | 无需实验即可生成因果候选 | 预测不等于因果，需正交实验验证 | 本文将其定位为假设生成工具，非因果证明 |
| 基础模型（foundation models） | scGPT、Geneformer、GET、EpiAgent、RegFormer、ChromBERT | 跨细胞类型迁移、缓解稀疏性 | 注意力分数不等于因果、存在预训练偏置和域偏移 | 本文主张将其纳入方法学分类，输出需与 baseline 比较并实验验证 |

---

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|---|---|---|---|
| 数据稀疏与 dropout | scATAC-seq 尤其稀疏，峰检测信噪比低，peak-to-gene 连接不可靠 | 单细胞染色质可及性测序深度有限，dropout 非随机，低表达基因和低丰度 TF 易缺失 | Introduction 与 Paired data 节：dropout 非随机，低表达 TF 可能从测量矩阵中缺失 |
| 无法区分 TF 表达与 TF 活性 | 单模态 scRNA-seq 中 TF 高表达不等于高活性 | TF 活性受染色质可及性、共因子、翻译后修饰调控，mRNA 丰度不能直接代表调控活性 | Introduction：单模态表达数据无法区分 TF 表达与 TF 活性 |
| 远端增强子-靶基因分配困难 | 可及性峰与基因的共定位不等于功能连接 | 三维基因组中增强子可能接触远端启动子，线性距离不能决定调控关系 | Paired data 节：可及峰靠近基因可能无关，需考虑三维接触 |
| 批次效应与平台差异 | 不同样本/中心合并后产生人工聚类或掩盖真实状态 | 技术差异（测序平台、建库方法、样本处理）与生物学变异混杂 | Paired data 节：批次和平台差异可造成人工聚类 |
| 细胞状态连续性与网络离散化矛盾 | 肿瘤细胞沿连续轨迹变化，单一静态网络无法刻画状态转换 | 细胞状态是连续谱，网络重连是渐进的，「每状态一个网络」是近似 | 动态建模节：单状态网络是近似，应报告边权重变化 |
| 因果证据不足 | 多数方法输出统计关联或方向性预测，不能证明调控因果性 | 缺乏扰动实验，虚拟扰动和注意力分数不等于真实因果 | 证据层级节：虚拟扰动和注意力分数应视为假设生成而非因果证明 |
| 基准测试不统一 | 不同方法在参考网络、预处理、指标上差异大，跨研究比较困难 | 参考网络标签不完整、存在研究偏倚，指标对类别不平衡敏感 | 评估节：参考网络标签缺失严重、存在研究偏倚，指标需报告标签覆盖率和可观测上限 |

---

## 06 核心思想

### 1) 表面方法

本文是一篇叙述性综述，表面方法为：按输入数据设计（same-cell paired、matched-unpaired、imputed、single-modality）和推断目标（静态 GRN、动态 GRN、虚拟扰动）对现有 AI 与计算方法进行分类，并总结其在癌症中的应用。

### 2) 核心洞察

- **输入数据设计决定方法能力边界**：same-cell paired 数据提供同一细胞中调控元件与转录输出的直接对应，是重建 enhancer-promoter-gene 关系的最强数据基础；matched-unpaired、imputed 和 single-modality 设计虽扩展覆盖，但引入额外假设和伪影。
- **证据层级应显式区分**：统计关联 → 方向性预测 → in silico perturbation → 实验支持的因果调控，四层证据强度递增，方法声称的结论不能超出其证据层级。
- **方法选择应由数据与问题共同驱动**：静态网络选 motif/co-accessibility 或图学习方法；轨迹动态选 Dictys、inferCSN、scMTNI；因果假设选虚拟扰动方法并配正交实验验证。

### 3) 可能的普适教训 [Analysis]

- **「数据设计分类学」可迁移**：三维基因组领域同样面临 same-cell 多组学（如 Hi-C + RNA）与 matched-unpaired 数据的选择问题，本文的输入数据分类框架可直接用于染色质构象预测方法的评估。
- **「证据层级」是通用评估框架**：三维基因组中 enhancer-promoter 互作预测同样需要区分共定位、方向性预测、in silico 扰动（如 CTCF 敲除模拟）和实验验证（如 CRISPR 删除增强子），本文的四层证据框架可迁移。
- **「每状态一个网络」的近似警告**：三维基因组中染色质区室（compartment）和 TAD 结构同样随细胞状态连续变化，静态结构预测需警惕过度离散化。

---

## 07 方法总览

- **输入**：单细胞转录组（scRNA-seq）和/或染色质可及性（scATAC-seq）数据，按设计分为四类：
  1. Same-cell paired：同一细胞中同时测量两种模态（如 10x Multiome、SHARE-seq、SNARE-seq、sci-CAR、Paired-seq）
  2. Matched-unpaired：同一样本/供体的不同细胞分别测量两种模态，需锚定或标签迁移
  3. Imputed/transferred：从一种模态生成另一种模态（如 scMVP、scMOG），引入模型依赖伪影
  4. Single-modality：仅使用 scRNA-seq 或 scATAC-seq 之一，常需外部先验
- **输出**：细胞状态特异性 GRN，包含 TF–enhancer–target gene 边、regulon 活性评分、网络重连轨迹、虚拟扰动预测结果
- **方法家族**：
  1. Motif/co-accessibility 推断：SCENIC、SCENIC+、scREG、FigR、DIRECT-NET、MICA
  2. 深度整合与图学习：LIGER、scMultiomeGRN、DeepMAPS、GLUE
  3. 动态与细胞状态特异性建模：Dictys、inferCSN、scMTNI、scTIGER、Inferelator 3.0
  4. 虚拟扰动：CellOracle、Pano、GenKI、scTenifoldKnk、scPRAM
- **流程**（文字描述）：
  1. 数据预处理与质量控制（dropout 处理、批次校正）
  2. 按输入数据设计选择方法家族
  3. 推断 GRN 边（motif 匹配、共可及性、图嵌入）
  4. 沿轨迹或状态解析网络动态
  5. 虚拟扰动生成因果候选
  6. 与实验验证（CRISPR、Perturb-seq）对接
- **工具**：未提供统一软件框架；各方法独立实现
- **假设**：可及性变化可预测基因表达变化（chromatin potential）；motif 保守性可跨物种迁移；图拓扑携带调控信号；轨迹推断可解析状态转换

---

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|---|---|---|---|---|---|
| 数据设计分类（same-cell paired / matched-unpaired / imputed / single-modality） | 明确不同数据设计的能力边界和假设 | 数据设计决定可推断的调控关系类型和伪影来源 | 输入：数据来源描述；输出：方法选择指南 | Paired data 节：四种设计显式区分，imputed 引入模型依赖伪影 | 移除后方法选择失去依据，易混淆不同证据强度的结论 [预期] |
| Motif/co-accessibility 推断（SCENIC、SCENIC+、scREG、FigR、DIRECT-NET、MICA） | 从序列 motif 和峰-基因共可及性推断 TF–enhancer–gene 边 | 提供可解释的调控元件-基因连接，不依赖深度模型 | 输入：scRNA-seq/scATAC-seq、motif 数据库；输出：regulon、enhancer-gene 连接 | SCENIC+ 在黑色素瘤、PBMC、ENCODE 细胞系中验证；DIRECT-NET 用独立功能基因组数据验证 | 移除后失去可解释的调控元件注释，深度模型输出难以生物学解读 [预期] |
| 深度整合与图学习（LINGER、scMultiomeGRN、DeepMAPS、GLUE） | 学习高维稀疏多组数据的统一表示，显式建模基因-峰-细胞关系 | 捕捉非线性关系和全局拓扑，超越共表达/共可及性 | 输入：paired 多组学数据、先验 motif；输出：细胞特异性网络、TF 活性 | LINGER 在报告基准中优于现有方法；DeepMAPS 在肺癌中产生细胞类型特异性网络 | 移除后失去非线性建模能力，但保留可解释方法仍可工作 [预期] |
| 动态与状态特异性建模（Dictys、inferCSN、scMTNI、scTIGER） | 沿轨迹或状态推断网络重连，捕捉调控动态 | 肿瘤细胞状态连续变化，静态网络无法刻画转换 | 输入：scRNA-seq/scATAC-seq、伪时间；输出：状态特异性网络、边权重变化 | Dictys 在发育轨迹中改善重建精度；scTIGER 在前列腺癌中识别条件特异性网络 | 移除后网络无法反映状态转换，回到「每数据集一个网络」的粗粒度 [预期] |
| 虚拟扰动（CellOracle、Pano、GenKI、scTenifoldKnk、scPRAM） | 通过删除边或改变节点状态模拟基因敲除，生成因果候选 | 无需实验即可优先排序候选调控因子 | 输入：GRN、细胞状态；输出：扰动后状态变化预测 | CellOracle 在斑马鱼中预测未报道的脊索表型并获验证 | 移除后失去因果候选生成能力，但虚拟扰动本身不证明因果 [实测：作者明确标注为假设生成] |
| 证据层级框架（统计关联→方向性→in silico→实验验证） | 区分方法声称的结论强度 | 防止将关联或预测过度解读为因果 | 输入：方法输出类型；输出：证据等级标签 | 全文反复强调四层区分，尤其虚拟扰动和注意力分数非因果 | 移除后结论易被过度解读，临床转化失去依据 [预期] |
| 评估与基准（ENCODE、DREAM、BEELINE、Perturb-seq） | 提供参考网络和功能验证数据 | 衡量边恢复性能和下游效用 | 输入：参考网络、扰动数据；输出：AUROC、AUPRC、早期精度等 | 评估节：参考网络标签缺失严重、存在研究偏倚，指标需报告标签覆盖率和可观测上限 | 移除后无法比较方法优劣，性能数字失去意义 [预期] |

---

## 09 关键公式符号

本文为叙述性综述，未提供数学公式。以下为文中隐含的、理解方法所需的概念性「公式」：

- **Chromatin potential**（SHARE-seq 概念）：  
  \( \text{Chromatin potential} = f(\text{accessibility change}, \text{expression change}) \)  
  可及性变化预测尚未发生的基因表达变化。  
  用途：将可及性动态与表达动态关联，用于轨迹推断。  
  直觉：增强子先于基因开放，可及性变化领先于表达变化。

- **Regulon activity score**（SCENIC 概念）：  
  \( \text{Regulon activity} = \text{AUCell}(\text{TF target genes}, \text{cell expression}) \)  
  基于 TF 靶基因集的富集评分，衡量单个细胞中 TF 调控程序的活性。  
  用途：将 GRN 边转化为细胞状态可比较的活性值。  
  直觉：TF 靶基因整体上调/下调反映该 TF 调控程序是否激活。

- **虚拟扰动（CellOracle 概念）**：  
  \( \Delta \text{cell state} = g(\text{GRN}, \text{remove edges of TF } X) - g(\text{GRN}, \text{original}) \)  
  通过删除目标 TF 的所有出边，比较扰动前后细胞状态表示的变化。  
  用途：生成「该 TF 缺失后细胞状态如何改变」的因果候选。  
  直觉：边删除模拟基因敲除，状态变化大的 TF 更可能是关键调控因子。

- **Cross-modal attention（scMultiomeGRN 概念）**：  
  \( \text{attention}(TF, \text{peak}, \text{gene}) = \text{softmax}(Q_{TF} \cdot K_{\text{peak}}^T / \sqrt{d}) \cdot V_{\text{gene}} \)  
  通过注意力机制在转录组和染色质可及性两个模态间建立 TF–peak–gene 三元关系。  
  用途：决定一个 TF 是否通过某个可及峰调控目标基因。  
  直觉：注意力权重高表示该峰对该 TF-基因对贡献大。

---

## 10 实验设计与证据链

本文为综述，无原始实验。以下为文中引用的代表性方法及其验证方式：

| 实验/验证 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|---|---|---|---|---|---|---|
| SCENIC 在肿瘤和脑数据集中的应用 | 共表达+motif 富集可识别 regulon 和细胞状态 | 应用于黑色素瘤、脑数据集 | 识别出与细胞状态相关的 regulon | 共表达+motif 可推断 regulon 活性 | 不能证明 regulon 边是因果调控 | Aibar et al., 2017（文中引用） |
| SCENIC+ 在黑色素瘤、PBMC、ENCODE 细胞系、果蝇视网膜中的基准 | enhancer-driven GRN 可从 paired 数据推断 | 多组织、多物种基准 | 改善 TF 识别和 enhancer-gene 连接 | paired 数据可推断 enhancer-driven GRN | 未在所有癌症类型中验证 | Bravo Gonzalez-Blas et al., 2023（文中引用） |
| DIRECT-NET 用独立功能基因组数据验证 | 梯度提升可识别全基因组 cis-regulatory elements 及其靶基因 | 与现有方法比较 | 提高 cis-regulatory element-to-gene 推断精度 | 可解释的增强子-基因连接可从 paired 数据推断 | 未在三维基因组层面验证增强子-启动子接触 | Zhang et al., 2022（文中引用） |
| CellOracle 在斑马鱼中的虚拟扰动 | 边删除可预测未报道的表型 | 模拟 TF 敲除，与已知表型比较 | 预测未报道的脊索表型，后获验证 | 虚拟扰动可生成可验证的因果候选 | 虚拟扰动本身不证明因果，需实验验证 | Kamimoto et al., 2023（文中引用） |
| Pano 在人脑类器官中验证 GLI3 | 整合 TF 结合预测与多组学可识别关键调控因子 | 与 pooled 遗传扰动比较 | GLI3 被验证为关键调控因子 | 多组学+TF 结合预测可优先排序调控因子 | 仅验证少数基因，泛化性未证明 | Fleck et al., 2023（文中引用） |
| 小鼠皮肤鳞癌 EMT 研究 | paired scRNA-seq + scATAC-seq 可解析 EMT 状态调控 | CRISPR/Cas9 功能实验 | Klf5、Pitx1 控制早期 EMT，Nfatc1、Creb3l1 作用于后期 | 网络推断可识别 EMT 状态特异性调控因子 | 仅一个模型系统，需更多肿瘤类型验证 | Perez-Gonzalez et al., 2026（文中引用） |
| 黑色素瘤耐药研究 | 网络推断可识别耐药状态和组合策略 | in silico 扰动 + 实验验证 | 识别去分化耐药状态，组合策略降低耐药态占据 | GRN 可指导组合治疗设计 | 临床转化需前瞻性验证 | Pillai et al., 2022（文中引用） |
| 胶质瘤干细胞样细胞研究 | 网络拓扑决定耐药/敏感状态转换 | 模拟 + siRNA/联合治疗 | 网络拓扑预测治疗反应 | 网络拓扑可编码治疗逃逸机制 | 仅体外/类器官证据 | Park et al., 2024（文中引用） |
| 基础模型评估（scGPT、Geneformer） | 注意力分数可预测扰动靶点 | 与简单基因统计比较 | 注意力分数对扰动靶点预测增益有限 | 基础模型输出需与 baseline 比较 | 注意力分数不能作为因果证据 | Kendiukhov, 2026c（文中引用） |

---

## 11 结论正确解读

- **任务范围**：本文仅覆盖从单细胞转录组和染色质可及性数据推断 GRN 的方法，不涉及 bulk 数据、不涉及序列-only 预测、不涉及三维基因组构象数据（如 Hi-C）的直接建模。
- **oracle/真值输入**：文中方法依赖的「真值」包括 ChIP-seq 结合位点、ENCODE 调控元件注释、已知 TF-motif 数据库、CRISPR 扰动表型。这些真值本身不完整且存在细胞类型偏倚。
- **端到端状态**：无任何方法实现从原始测序数据到实验验证的端到端流程；所有方法均需人工选择参考网络、阈值和验证实验。
- **算力成本**：文中未报告具体算力需求；深度生成和图学习方法（LIGER、DeepMAPS、GLUE）隐含高计算成本，但未量化。
- **历史数据依赖**：所有方法依赖已有参考基因组注释和 motif 数据库，对新物种或非编码区变异敏感。
- **最难情形**：低丰度 TF、罕见细胞状态、增强子-启动子三维接触未知、反馈环路、非线性和上下文依赖性调控。
- **群体/领域边界**：结论主要基于癌症研究，正常组织、发育和免疫系统的泛化性未系统验证。
- **有边界的复述**：本文提供的不是「哪种方法最好」的结论，而是一个分类框架和证据层级：same-cell paired 数据是重建 enhancer-promoter-gene 关系的最强基础；统计关联、方向性预测、in silico perturbation 和实验验证构成递进的证据强度；方法选择应由数据设计和研究问题共同驱动；基础模型输出需与简单 baseline 比较并经实验验证。

---

## 12 作者自认局限

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|---|---|---|---|
| 叙述性综述而非系统性综述 | 文献检索不穷尽，可能受选择偏倚和发表偏倚影响；未做定量 meta 分析 | 未明确提及 | Discussion 节 |
| 文献检索偏倚 | 可能受选择偏倚、发表偏倚、英语语言偏倚影响 | 未明确提及 | Discussion 节 |
| 方法缺乏独立重复 | 多种方法缺乏独立重复 | 未明确提及 | Discussion 节 |
| 临床转化证据不足 | 多数应用为回顾性或临床前证据 | 需要前瞻性验证 | Conclusion 节 |
| 三维基因组信息缺失 | 未系统纳入 Hi-C、enhancer-promoter 三维接触数据 | 未明确提及 | [Analysis] 作者在 Paired data 节提到三维基因组中增强子可能接触不同启动子，但未将其作为方法分类维度 |

**作者提及的相关约束**（非正式局限）：
- 单细胞多组学数据 dropout 非随机，低表达基因和低丰度 TF 可能缺失（Paired data 节）
- 参考网络标签不完整、存在研究偏倚，评估指标需报告标签覆盖率和可观测上限（评估节）
- 虚拟扰动和注意力分数应视为假设生成而非因果证明（证据层级节）

---

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|---|---|---|---|---|
| 综述将「same-cell paired」视为最强数据设计，但未讨论 paired 数据中两种模态的测量相互干扰（如 10x Multiome 中 ATAC 建库可能影响 RNA 捕获） | Paired 数据的优势可能被技术噪声抵消 | 方法选择建议可能高估 paired 数据的实际收益 | 比较 paired vs matched-unpaired 在同一细胞类型上的 GRN 重建精度 | Paired data 节：作者仅讨论信息优势，未讨论技术干扰 |
| 证据层级将「实验支持的因果调控」置于最高层，但未讨论 CRISPR 筛选本身的脱靶效应和补偿机制 | 实验验证也可能产生假阳性和假阴性 | 证据层级可能过度简化验证的复杂性 | 系统比较 CRISPR 验证与 Perturb-seq 验证的一致性 | 证据层级节：作者未讨论验证实验本身的局限 |
| 综述将基础模型（scGPT、Geneformer）的注意力分数视为「假设生成」，但未讨论注意力机制的可解释性是否已被系统验证 | 注意力分数可能反映数据统计规律而非生物学调控 | 基础模型的调控输出可能误导生物学解读 | 在已知调控回路（如 p53 通路）上测试注意力分数与实验验证的一致性 | 评估节：作者引用 Kendiukhov 2026c 指出注意力分数增益有限 |
| 综述未将三维基因组数据（Hi-C、enhancer-promoter 接触）纳入方法分类，尽管作者承认增强子可能接触不同启动子 | 三维基因组信息可能显著改善 enhancer-gene 分配 | 遗漏三维基因组维度可能使分类框架不完整 | 比较加入 Hi-C 约束 vs 仅可及性数据的 GRN 重建精度 | Paired data 节：作者提到三维基因组问题但未展开 |
| 综述的「每状态一个网络」批评适用于静态方法，但未讨论动态方法（Dictys、inferCSN）如何验证网络重连的生物学真实性 | 动态网络可能过度拟合伪时间轨迹 | 动态 GRN 的验证标准不明确 | 在已知谱系转换（如 EMT）中比较动态网络预测与实验时间序列 | 动态建模节：作者建议报告边权重变化，但未给出验证标准 |
| 综述未讨论批次效应校正方法（如 Harmony、scVI）对 GRN 推断的影响 | 批次校正可能消除真实生物学信号或引入人工信号 | 批次处理选择可能显著影响 GRN 结果 | 在不同批次处理流程下比较同一数据集的 GRN 稳定性 | Paired data 节：作者提到批次效应但未讨论校正方法 |

---

## 14 学到什么

### Agent 提炼的知识候选

| 知识候选 | 来源 | 可迁移性 | 迁移到三维基因组课题的具体方式 |
|---|---|---|---|
| **输入数据设计分类学**（same-cell paired / matched-unpaired / imputed / single-modality） | 全文核心框架 | 高 | 三维基因组领域同样面临 Hi-C + RNA 的 same-cell 测量（如 sci-Hi-C）与 matched-unpaired 设计的选择；可据此建立染色质构象预测方法的能力边界分类 |
| **证据层级框架**（统计关联→方向性→in silico 扰动→实验验证） | 全文反复强调 | 高 | 三维基因组中 enhancer-promoter 接触预测同样需要区分共定位、方向性预测（如 CTCF-CTCF 相互作用）、in silico 扰动（如模拟 CTCF 敲除）和实验验证（如 CRISPR 删除增强子） |
| **Chromatin potential 概念**（可及性变化预测表达变化） | SHARE-seq（文中引用） | 高 | 三维基因组中可及性变化与基因表达变化的时间差可用于预测 enhancer-promoter 接触的动态重连 |
| **虚拟扰动作为假设生成工具**（CellOracle 的边删除策略） | CellOracle（文中引用） | 高 | 在三维基因组 GRN 中，可通过删除特定 enhancer-promoter 接触边模拟 3D 基因组扰动，预测细胞状态变化 |
| **基础模型输出需与 baseline 比较**（注意力分数≠因果） | 评估节（Kendiukhov 2026c） | 高 | 三维基因组基础模型（如 Enformer、Borzoi）的注意力/贡献分数同样需与简单共定位 baseline 比较，避免过度解读 |
| **「每状态一个网络」是近似** | 动态建模节 | 中 | 三维基因组中 TAD/compartment 结构随细胞状态连续变化，静态结构预测需报告结构边界的动态变化 |
| **参考网络标签不完整、存在研究偏倚** | 评估节 | 中 | 三维基因组参考数据（如 ChIA-PET、HiChIP）同样存在细胞类型偏倚和标签缺失，评估指标需报告覆盖率 |
| **多组学整合优于单模态** | 全文核心主张 | 高 | 三维基因组预测应整合转录组、染色质可及性、甲基化等多模态信息，而非仅依赖序列或单一组学 |
| **方法选择由数据与问题共同驱动** | 方法选择节 | 高 | 三维基因组课题中，静态结构预测选图学习方法，动态重连选轨迹建模，因果验证选虚拟扰动+实验 |
| **增强子-启动子分配需考虑三维接触** | Paired data 节（作者提及但未展开） | 高 | 这是三维基因组课题的核心切入点：可及性共定位不足以确定 enhancer-promoter 功能连接，需引入 Hi-C/HiChIP 接触信息 |

---

## 15 与已有知识连接

- **SCENIC / SCENIC+**（Aibar et al., 2017; Bravo Gonzalez-Blas et al., 2023）：本文将其归入 motif/co-accessibility 家族。SCENIC+ 的 enhancer-driven GRN 推断与三维基因组中 enhancer-promoter 分配问题直接相关，可视为从可及性数据推断调控关系的 baseline。
- **GLUE**（Cao and Gao, 2022）：本文将其归入深度整合家族。GLUE 的图链接嵌入框架可迁移到三维基因组中 Hi-C 与 RNA 的联合嵌入。
- **CellOracle**（Kamimoto et al., 2023）：虚拟扰动方法，其边删除策略可迁移到三维基因组中模拟 CTCF/cohesin 扰动对基因表达的影响。
- **Pando**（Fleck et al., 2023）：整合 TF 结合预测与多组学，在类器官中验证 GLI3，展示了从预测到实验验证的闭环。
- **Enformer / Borzoi**（外部知识）：序列到表达的深度模型，本文未直接讨论，但其注意力/贡献分数与本文对基础模型的批判一致——需与简单 baseline 比较。
- **Hi-C / HiChIP / ChIA-PET**（外部知识）：三维基因组核心数据，本文未纳入方法分类，但作者在 Paired data 节提到增强子可能接触不同启动子，暗示三维接触信息对 enhancer-promoter 分配的重要性。
- **Perturb-seq / CRISPR 筛选**（Dixit et al., 2016; Replogle et al., 2022）：本文将其作为最高证据层级的验证手段，三维基因组课题中同样需要此类功能验证。
- **EMT 研究**（Perez-Gonzalez et al., 2026）：本文引用的 EMT 案例展示了 paired 多组学在解析状态转换中的应用，可迁移到三维基因组中 EMT 相关的染色质结构重编程研究。

---

## 16 研究想法

### Agent 生成的研究候选

**候选 1：三维基因组增强子-启动子分配的统一基准框架**
- **名称**：3D-GRN-Bench
- **来源局限/观察**：本文指出可及性共定位不足以确定 enhancer-promoter 功能连接，但未提供系统比较框架；三维基因组领域缺乏统一的 enhancer-promoter 分配基准
- **核心假设**：整合 Hi-C/HiChIP 接触信息可显著改善 enhancer-promoter 分配精度，且改善幅度可量化
- **初步方法**：构建包含 same-cell paired（如 10x Multiome + Hi-C）、matched-unpaired、imputed 三种数据设计的基准数据集；比较 motif/co-accessibility 方法（SCENIC+、FigR）与图学习方法（GLUE、DeepMAPS）在 enhancer-promoter 分配上的精度；以 CRISPR 验证和 HiChIP 为真值
- **验证方式**：在黑色素瘤、结直肠癌、胶质瘤等已有 paired 多组学数据上评估；报告标签覆盖率和可观测上限
- **创新状态**：unverified

**候选 2：基于染色质状态转移的细胞状态特异性三维 GRN 动态建模**
- **名称**：Chromatin-State-GRN-Dynamics
- **来源局限/观察**：本文指出「每状态一个网络」是近似，动态方法需报告边权重变化；三维基因组中 TAD/compartment 结构随细胞状态连续变化
- **核心假设**：将染色质可及性状态转移（chromatin potential）与三维接触变化联合建模，可预测 EMT 等状态转换中的调控重连
- **初步方法**：扩展 Dictys 的随机过程网络框架，加入 Hi-C 接触矩阵作为边权重先验；沿伪时间推断 enhancer-promoter 接触的动态重连；以 CRISPR 时序实验验证预测的调控重连
- **验证方式**：在 EMT 小鼠模型和黑色素瘤耐药模型中验证；比较加入三维接触先验 vs 仅可及性数据的动态 GRN 精度
- **创新状态**：unverified

**候选 3：虚拟扰动在三维基因组 GRN 中的因果推断扩展**
- **名称**：3D-Causal-Perturb
- **来源局限/观察**：本文指出虚拟扰动（CellOracle 等）生成因果候选但需实验验证；三维基因组中 CTCF/cohesin 扰动是天然实验
- **核心假设**：在三维 GRN 中删除特定 enhancer-promoter 接触边（模拟 CTCF 敲除）可预测细胞状态变化，且预测精度高于仅删除 TF 表达边
- **初步方法**：在 CellOracle 框架中加入三维接触边作为可删除边；利用 CTCF 降解系统（如 auxin-inducible degron）的 Perturb-seq 数据验证；比较「删除接触边」vs「删除表达边」的预测精度
- **验证方式**：在胶质瘤干细胞样细胞和黑色素瘤细胞中验证；以 CRISPR 表型为真值
- **创新状态**：unverified

**候选 4：基础模型在三维基因组 GRN 中的可解释性评估**
- **名称**：Foundation-GRN-Interpretability
- **来源局限/观察**：本文指出基础模型（scGPT、Geneformer）的注意力分数对扰动靶点预测增益有限；三维基因组基础模型（Enformer 等）的贡献分数同样缺乏系统评估
- **核心假设**：基础模型的注意力/贡献分数在三维基因组 GRN 推断中的增量价值有限，需与简单共定位 baseline 比较
- **初步方法**：在多个癌症 paired 多组学数据集上，比较 Enformer、scGPT、Geneformer 的注意力分数 vs 简单共可及性+motif 匹配的 enhancer-promoter 分配精度；以 CRISPR 验证为真值
- **验证方式**：报告增量价值（incremental value over baseline）、标签覆盖率和可观测上限
- **创新状态**：unverified

**候选 5：三维基因组 GRN 的临床转化评估框架**
- **名称**：3D-GRN-Clinical-Framework
- **来源局限/观察**：本文指出临床转化需前瞻性验证，但未提供具体框架；三维基因组 GRN 预测的靶点缺乏临床评估标准
- **核心假设**：将三维 GRN 预测的调控因子与药物反应数据关联，可识别可操作的联合治疗靶点
- **初步方法**：在黑色素瘤和胶质瘤的 paired 多组学数据上构建三维 GRN；将网络预测的耐药驱动因子与药物筛选数据（如 GDSC、CTRP）关联；在类器官中验证联合治疗策略
- **验证方式**：以类器官药物反应为真值；报告预测靶点的实验验证率
- **创新状态**：unverified