## 01 基本信息

- **标题**：From reference-genome prediction to causal generalization: sequence-to-function models for plant regulatory genomics
- **作者**：Zhan, Mingfang; Wu, Ruigang
- **单位**：未提供
- **期刊/平台**：Frontiers in Plant Science
- **年份**：2026-10-02
- **论文类型**：Mini Review（迷你综述）
- **领域**：植物调控基因组学 × 序列-功能（seq2func）深度学习模型
- **关键词**：sequence-to-function models, plant regulatory genomics, pan-genome, causal generalization, distribution shift, closed-loop AI（基于全文归纳）
- **DOI/ID**：10.3389/fpls.2026.1968878
- **URL**：https://pubmed.ncbi.nlm.nih.gov/42824471/
- **代码**：未提供
- **数据**：未提供
- **阅读日期**：未提供
- **在「三维基因组/染色质组织 × AI 方法/物理模拟」方向中的位置**：本文不直接研究三维基因组或染色质高级结构，而是聚焦植物调控基因组学中的序列-功能预测模型。但其核心关切——从参考基因组观测数据到跨基因型/环境/物种的因果泛化——与三维基因组领域面临的泛化挑战高度同构。文中讨论的分布偏移（distribution shift）评估框架、观测与扰动实验互补、主动学习与持续学习闭环等思路，可直接迁移到染色质构象预测模型的评估与迭代设计中。文中提及的染色质互作信息作为预测基因表达的输入特征（如DeepCBA），也构成与三维基因组方法的直接接口。

---

## 02 一句话总结

本文是一篇迷你综述，系统梳理植物调控基因组学中序列-功能（seq2func）模型的现状与局限，指出基于参考基因组的观测数据训练与评估无法保证对自然单倍型、结构变异、组织、发育阶段、环境及物种的泛化，并提出以生物学有意义的分布偏移为基准的评估框架，以及结合泛基因组、多组学、基因组编辑、报告基因检测、主动学习和持续学习的闭环实验-计算系统作为改进路径。

---

## 03 研究问题

- **具体问题**：seq2func 模型在植物调控基因组学中，从参考基因组预测到跨遗传/环境/物种的因果泛化，面临哪些挑战？如何评估和改进其泛化能力？
- **为什么重要**：植物基因组具有高重复序列含量、转座子丰富、多倍化普遍、长程调控广泛、基因型-环境互作（G×E）复杂等特点。若模型仅在参考基因组上表现良好，则无法有效应用于育种群体中的非参考等位基因、结构变异或工程化调控序列，限制了其在精准育种和气候韧性作物改良中的实际价值。
- **现有方法为何不足**：当前大多数模型在单一或少数参考基因组的观测数据上训练和评估，随机留出位点的测试仅衡量熟悉环境中的插值能力，而非对植物生物学和育种最相关的变异类型的预测能力。观测关联不能确立因果关系，高留出准确率不等于模型恢复了真实的调控规则。
- **精确的「Can ... ?」研究问题**：Can sequence-to-function models trained on reference-genome observational data generalize reliably to non-reference haplotypes, structural variants, tissues, environments, and species in plants, and can their predictions be validated as causal through perturbation assays?

---

## 04 背景与发展脉络

> 注：以下脉络主要基于本文框架构建，标注「仅本文框架」；部分外部引用经文中提及，标注「经外部核验（文中引用）」。

| 阶段 | 代表性方法/事件 | 优点 | 局限 | 本文主张的位置 |
|---|---|---|---|---|
| 早期 seq2func 奠基 | Zhou and Troyanskaya (2015); Kelley et al. (2016) 的深度神经网络映射 DNA 序列到分子输出 | 首次实现端到端序列-功能预测 | 主要在人类/动物系统；输入窗口有限 | 奠定了 seq2func 范式 [经外部核验（文中引用）] |
| 植物 seq2func 初步应用 | Peleke et al. (2024) 跨物种基因-转录本丰度预测；Wang et al. (2024) DeepCBA 整合染色质可及性与互作信息 | 证明植物中可行；跨物种迁移有信号 | 参考基因组依赖；物种间迁移有限 | 植物 seq2func 的可行性证据 [经外部核验（文中引用）] |
| 长上下文架构 | Enformer/Borezoi 风格架构、注意力/状态空间模型 | 可纳入远端调控信息 | 长窗口不必然带来泛化或机制理解 | 需要合适的归纳偏置与训练多样性 [仅本文框架] |
| 植物基础模型/基因组语言模型 | PlantCaduceus, AgroNT, plant-adapted nucleotide transformer | 自监督序列表征 | 表征不等于调控机制；泛化未验证 | 有前景但需功能监督与分布偏移评估 [经外部核验（文中引用）] |
| 因果与泛化转向 | 本文提出的分布偏移评估 + 观测/扰动互补 + 闭环学习 | 明确评估泛化与因果性 | 尚未有完整实现 | 本文的核心主张位置 [仅本文框架] |

---

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|---|---|---|---|
| 参考基因组偏差 | 模型在参考基因组上训练/评估，无法覆盖自然群体中的等位基因多样性 | 参考基因组只是物种序列空间的一种实现；育种相关变异常为非参考等位基因或结构变异 | "A reference genome represents only one realization of a species' regulatory sequence space"（Pan-genomic diversity 节） |
| 转座子与重复序列干扰 | 重复序列富集导致模型利用序列组成或同源性而非可迁移的调控特征 | 转座子可贡献启动子/增强子，但其效应依赖插入位置、序列年龄、表观状态和邻近元件 | "Repeat-rich genomes also increase the risk that models exploit homology or composition rather than transferable regulatory features"（Pan-genomic diversity 节） |
| 多倍体与同源基因混淆 | 同源基因座序列高度相似但调控状态不同，训练标签可能混合不同亚基因组信号 | 短读段多组学数据在同源序列间比对模糊；基因水平聚合标签掩盖亚基因组特异性 | "training labels...can inadvertently mix homeolog-specific regulatory signals, which may inflate aggregate performance while degrading homeolog-specific predictive fidelity"（Polyploidy 节） |
| 远端调控与长程互作 | 仅用近端启动子窗口会遗漏远端增强子等调控元件 | 植物中长程调控广泛存在；长窗口增加计算成本但未必提升机制理解 | "regulatory effects can involve distal cis-regulatory elements, repetitive DNA, and chromatin architecture"（Seq2func models 节） |
| 上下文依赖（组织/发育/环境） | 同一序列在不同条件下功能不同，静态模型无法区分 | 序列定义调控潜力，但输出取决于转录因子丰度、染色质状态、激素信号等上下文 | "DNA sequence defines regulatory potential, but output depends on the cellular and environmental context"（Context dependence 节） |
| 观测关联 ≠ 因果 | 高预测准确率被误读为模型发现了因果调控规则 | 观测数据中的关联可能来自连锁、混杂或序列组成偏差 | "High held-out accuracy on observational data should not therefore be interpreted as evidence that a model has recovered causal regulatory rules"（From observational prediction 节） |
| 评估协议不匹配 | 随机留出位点测试不能反映实际部署场景 | 实际应用面对的是新单倍型、新组织、新环境、新物种——即分布偏移 | "Evaluation based on randomly held-out loci from a reference genome therefore measures interpolation in a familiar setting"（Introduction 节） |

---

## 06 核心思想

### 1) 表面方法
本文是一篇迷你综述，不提出新模型，而是系统性地：
- 梳理植物 seq2func 模型的现状（CNN、Transformer/长上下文架构、基因组语言模型）；
- 列举植物基因组对 seq2func 的独特挑战（泛基因组多样性、转座子、多倍体、远端调控、上下文依赖）；
- 提出以分布偏移（covariate shift / label shift / concept shift）为分类框架的评估基准；
- 提出观测（多组学）+ 扰动（MPRA/STARR-seq/CRISPR 编辑）互补的因果验证路径；
- 提出主动学习 + 持续学习 + 闭环实验-计算系统的迭代框架。

### 2) 核心洞察
- **泛化不是插值**：参考基因组上的随机留出测试衡量的是熟悉环境中的插值能力，而植物育种和调控发现真正需要的是对非参考等位基因、结构变异、新环境和新物种的外推能力。
- **三种分布偏移的区分**：将评估问题分解为 covariate shift（序列分布变化）、label shift（测量过程变化）、concept shift（序列-功能映射关系变化），为设计有意义的基准提供了可操作框架。
- **观测与扰动的互补性**：观测数据（ATAC-seq、ChIP-seq、RNA-seq）提供内源染色质环境中的关联证据，报告基因检测提供分离的序列内在活性，内源编辑提供因果验证——三者构成从关联到因果的证据链。
- **闭环而非一次性预测**：模型不应是静态注释工具，而应作为"虚拟实验"参与迭代——不确定性指导实验选择，实验结果反馈更新模型。

### 3) 可能的普适教训 [Analysis]
- **评估协议决定结论边界**：任何序列-功能（或序列-结构）预测模型的性能声明都必须限定其训练数据覆盖的序列空间和生物学上下文。对三维基因组模型而言，这意味着跨细胞类型、跨物种、跨构象状态的评估应成为标准实践。
- **"上下文"是模型的核心变量而非噪声**：植物中组织/环境/发育对调控的影响提示，染色质结构预测模型同样需要显式编码细胞状态和实验条件，而非仅依赖序列。
- **因果验证是模型可信度的最终标尺**：预测染色质互作或调控效应的模型，其价值最终取决于能否通过扰动实验（如 CRISPR 删除增强子、染色质构象捕获后的编辑验证）得到确认。

---

## 07 方法总览

本文为综述，无原始方法。但文中提出的闭环框架可概括为：

- **输入**：参考基因组与泛基因组序列、多组学观测数据（ATAC-seq、DNase-seq、ChIP-seq、CUT&Tag、RNA-seq、 nascent transcription、染色体构象数据）、报告基因检测数据（MPRA、STARR-seq）、内源编辑结果（CRISPR 删除/替换/碱基编辑/CRISPRi/a）
- **输出**：调控元件注释、变异效应预测、序列设计建议、经实验验证的因果调控机制
- **核心模块**：
  1. **seq2func 预测模型**：CNN 基线、长上下文 Transformer/状态空间架构、基因组语言模型
  2. **分布偏移评估框架**：covariate shift（新单倍型/结构变异/物种）、label shift（不同检测平台/测量类型）、concept shift（不同组织/发育/环境）
  3. **扰动实验模块**：MPRA/STARR-seq 高通量报告基因检测 + CRISPR 内源编辑验证
  4. **主动学习模块**：基于模型不确定性（高不确定性、模型分歧、 underrepresented haplotypes）选择下一轮实验
  5. **持续学习模块**：replay-based rehearsal、参数正则化（EWC）、模块化 adapter 架构，避免灾难性遗忘
- **流程**：观测数据训练模型 → 在分布偏移基准上评估 → 不确定性指导选择扰动实验 → 实验结果验证/修正预测 → 持续学习更新模型 → 循环迭代

---

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|---|---|---|---|---|---|
| seq2func 预测模型（CNN/Transformer/长上下文） | 从 DNA 序列映射到分子功能输出 | 核心预测引擎；CNN 提供局部 motif 识别基线，长上下文架构捕获远端调控 | 输入：one-hot 编码 DNA 序列（可含染色质/表观特征）；输出：可及性、TF 占用、表达等 | 文中引用 Kelley et al. 2016; Avsec et al. 2021; Peleke et al. 2024; Wang et al. 2024 | 移除则无预测能力；但仅靠模型无法保证泛化 [预期效应] |
| 分布偏移评估框架 | 按 covariate/label/concept shift 分类测试泛化 | 随机留出测试不能反映实际部署场景；需要生物学有意义的基准 | 输入：模型预测 + 分层测试集（新单倍型/结构变异/组织/环境/物种）；输出：分层性能与校准报告 | Table 1（文中）；"Benchmarking should include held-out accessions or haplotypes..."（Evaluating generalization 节） | 移除则无法判断模型是否真正泛化，性能声明可能误导 [预期效应] |
| 报告基因检测（MPRA/STARR-seq） | 高通量测量序列内在调控活性 | 提供独立于内源染色质环境的序列活性测量，补充观测数据 | 输入：天然/合成片段文库；输出：定量活性分数 | "MPRAs and STARR-seq allow systematic testing of natural and synthetic fragments"（From observational prediction 节）；Jores et al. 2020 | 移除则缺乏序列内在活性的直接证据，难以区分序列效应与上下文效应 [预期效应] |
| 内源基因组编辑（CRISPR） | 在天然染色质环境中因果验证调控元件 | 报告基因检测无法完全模拟内源染色质环境；编辑提供因果证据 | 输入：候选调控元件/变异；输出：编辑后表型变化 | "CRISPR-based editing enables direct tests in native genomic contexts"（From observational prediction 节）；Rodríguez-Leal et al. 2017 | 移除则无法确证因果关系，预测停留在关联层面 [预期效应] |
| 主动学习 | 基于不确定性选择信息量最大的实验 | 序列空间组合爆炸，无法穷尽实验；需要优先测试最有信息量的候选 | 输入：模型预测 + 不确定性估计；输出：下一轮实验候选集 | "Active learning can prioritize experiments that maximize expected information gain"（Closed-loop 节） | 移除则实验选择无指导，迭代效率大幅降低 [预期效应] |
| 持续学习 | 在累积实验数据上更新模型而不遗忘旧知识 | 实验数据持续产生；朴素微调会导致灾难性遗忘 | 输入：新实验数据 + 旧数据/参数约束；输出：更新后的模型 | 文中提及 replay、EWC、modular adapters 三种策略（Closed-loop 节） | 移除则模型无法持续改进，或更新后丢失已有能力 [预期效应] |

---

## 09 关键公式符号

**不适用。** 本文为综述论文，未提出新的数学模型或算法公式。文中涉及的分布偏移分类（covariate/label/concept shift）为概念性框架而非形式化定义。

---

## 10 实验设计与证据链

本文为迷你综述，不包含原始实验。文中引用的关键实证研究作为支撑证据：

| 实验/研究 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|---|---|---|---|---|---|---|
| Peleke et al. (2024) 跨物种基因表达预测 | seq2func 在植物中可行，存在保守特征 | 拟南芥、番茄、高粱、玉米 | 识别出保守和物种特异性预测特征；近缘物种迁移更强 | 植物 seq2func 的可行性；跨物种迁移有信号 | 不能证明跨物种泛化普遍成立 | "Early studies demonstrate feasibility in plants"（Seq2func models 节） |
| Wang et al. (2024) DeepCBA | 整合染色质可及性和互作信息可改善表达预测 | 玉米 | 整合多模态染色质特征提升预测 | 染色质互作信息对表达预测有价值 | 未证明因果性 | "DeepCBA integrated sequence, chromatin accessibility, and chromatin-interaction information"（Seq2func models 节） |
| Jores et al. (2020) 烟草 STARR-seq | 报告基因检测可识别植物增强子 | 烟草叶片 | 鉴定增强子活性及序列特征 | 报告基因检测在植物中可行 | 未证明内源功能 | "STARR-seq identified plant enhancer activity and functional sequence features"（From observational prediction 节） |
| Rodríguez-Leal et al. (2017) 番茄启动子编辑 | 内源编辑可创造定量性状变异 | 番茄启动子编辑 | 产生连续的表型变异 | 内源编辑是因果验证的有效工具 | 未推广到所有调控元件 | "Promoter editing in tomato has shown that targeted cis-regulatory modifications can create quantitative trait variation"（From observational prediction 节） |

**评测协议**：文中未提供具体数据集、指标或基准实现，但明确提出了评估泛化的分层测试要求（held-out accessions, structural variants, tissues, environments, species）和校准报告要求。

---

## 11 结论正确解读

- **任务范围**：本文讨论的是植物调控基因组学中的 seq2func 模型，即从 DNA 序列预测分子调控输出（可及性、TF 占用、表达等）。不涉及蛋白质编码序列的功能预测，也不涉及三维基因组结构预测本身。
- **oracle/真值输入**：文中强调观测数据（ATAC-seq、ChIP-seq 等）作为训练标签的局限性——它们反映的是内源染色质环境中的关联而非因果。报告基因检测和 CRISPR 编辑被视为更接近因果真值的实验来源，但各自也有边界（报告基因缺乏内源染色质上下文；编辑成本高、通量低）。
- **端到端状态**：文中明确指出，从序列到分子功能的预测已初步可行，但从分子功能到有机体表型（如产量、抗逆性）的桥接仍是最困难的一步。seq2func 分数可作为 GWAS 精细定位和基因组预测的特征或先验，但不等同于表型预测。
- **算力成本**：文中未讨论具体算力需求，但指出长上下文架构和基因组语言模型计算成本高，且"更长上下文不保证机制洞察或泛化"。
- **历史依赖**：模型性能依赖训练数据的参考基因组偏差；持续学习需要应对数据分布漂移和灾难性遗忘。
- **最难情形**：结构变异（尤其是转座子插入和拷贝数变异）、多倍体中的亚基因组特异性调控、以及未观测环境（如田间胁迫组合）下的预测。
- **群体/领域边界**：结论主要针对植物系统，但分布偏移评估框架和闭环学习思路可推广到其他物种和调控预测任务。文中明确建议以拟南芥、水稻、玉米、高粱、番茄、大豆、小麦等作为锚定物种建立基准。
- **不确定性**：文中强调模型应报告校准的不确定性（calibrated uncertainty）和有效域（domain of validity），但未提供具体实现方法。

**有边界的复述**：本文主张，植物 seq2func 模型的进展不应仅以参考基因组上的准确率衡量，而应通过跨单倍型、结构变异、组织、环境、物种的分布偏移测试来评估其泛化能力，并通过报告基因检测和内源编辑的扰动实验来验证预测的因果性；在此基础上，主动学习和持续学习可支撑闭环的实验-计算迭代系统。

---

## 12 作者自认局限

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|---|---|---|---|
| 观测数据无法确立因果 | "Observational associations do not establish that a nucleotide, motif, or cis-regulatory element causally determines a measured output" | 结合报告基因检测（MPRA/STARR-seq）和内源 CRISPR 编辑进行分层验证 | From observational prediction 节 |
| 报告基因检测的上下文缺失 | 游离基因报告系统可能无法完全再现内源染色质环境（如甲基化、三维互作） | 将报告基因检测视为"内在调控潜力"的测量，与内源编辑互补使用 | From observational prediction 节（隐含） |
| 长上下文架构的收益未验证 | "Longer context alone does not guarantee mechanistic insight or generalization" | 需要合适的归纳偏置、训练多样性和分布偏移评估 | Seq2func models 节 |
| 闭环学习的实际障碍 | 数据共享限制、缺乏标准化扰动数据集、植物世代时间长限制迭代速度 | 设计围绕延迟反馈、跨实验室数据协调和显式不确定性校准的闭环系统 | Closed-loop 节 |
| 可解释性方法（如归因图）的局限 | 归因图等方法可优先化候选变异，但"不提供因果证据" | 将可解释性输出视为假设，需经扰动实验验证 | From observational prediction 节（隐含） |

**作者提及的相关约束**（非正式局限）：
- 植物中长程调控和三维基因组数据的获取比动物系统更具挑战性（文中提及染色体构象检测为可用资源之一，但未展开讨论其局限）。
- 转座子富集的基因组中，序列比对和特征归因的可靠性可能下降（"Repeat-rich genomes also increase the risk that models exploit homology or composition"）。

---

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|---|---|---|---|---|
| 分布偏移框架缺乏形式化定义和量化指标 | 文中将 covariate/label/concept shift 作为概念框架提出，但未给出如何量化这些偏移、如何设定通过/失败阈值 | 若无量化标准，"生物学有意义的基准"难以落地为可操作的评测协议 | 在具体数据集上定义偏移度量（如序列相似性距离、标签分布差异），并比较不同模型在偏移下的性能衰减曲线 | "Benchmarking should include held-out accessions or haplotypes..."（Evaluating generalization 节）——有方向无操作化 |
| 闭环框架的可行性论证不足 | 主动学习和持续学习在植物中的实际应用面临数据稀缺、实验周期长、跨实验室标准化困难等障碍，文中仅简要提及 | 若闭环无法在合理时间尺度内迭代，其实际价值存疑 | 在模式植物（如拟南芥）中建立小规模闭环原型，测量每轮迭代的预测改进幅度和成本 | Closed-loop 节中作者自认"practical barriers are particularly severe in plants" |
| 对三维基因组信息的讨论过于简略 | 文中提及染色质互作信息可改善预测（DeepCBA），但未深入讨论三维基因组数据在 seq2func 中的整合策略和挑战 | 三维基因组是连接序列与调控功能的关键中间层，尤其在远端增强子-启动子互作方面 | 系统比较加入/不加入 Hi-C 或 HiChIP 特征对远端调控预测的增益，并评估跨细胞类型的可迁移性 | "chromosome-conformation assays identify distal contacts"（Seq2func models 节）——仅一句带过 |
| "因果"概念的使用可能过于宽松 | 文中将 CRISPR 编辑和报告基因检测视为因果验证，但这些实验验证的是局部序列-功能因果关系，而非有机体表型层面的因果 | 从分子因果到表型因果的鸿沟可能比文中暗示的更大 | 追踪从编辑变异到表型变化的完整因果链，评估中间环节的丢失或补偿效应 | "the hardest step is often the connection from predicted regulatory activity to organismal phenotype"（Bridging 节）——作者部分承认 |
| 对模型架构选择的建议缺乏实证比较 | 文中列举 CNN、Transformer、基因组语言模型等架构，但未提供在植物数据上的系统比较证据 | 架构选择直接影响可扩展性和可解释性，需要实证指导 | 在统一基准上比较不同架构在分布偏移下的性能、校准质量和计算成本 | 文中仅引用已有研究，无新比较实验 |
| 转座子作为调控元件的正面贡献被低估 | 文中主要将转座子视为挑战（重复序列、比对模糊），但转座子也是新调控元件的来源 | 转座子衍生的调控元件可能为育种提供重要靶点 | 分析转座子插入多态性与调控活性变化的关系，评估模型对转座子携带调控元件的预测能力 | "Transposable elements can contribute promoters, enhancers, transcription factor motifs"（Pan-genomic diversity 节）——作者提及但未展开 |

---

## 14 学到什么

> 标题：Agent 提炼的知识候选

1. **分布偏移分类框架（可直接迁移）**：将模型评估从"随机留出"升级为三类分布偏移——covariate shift（输入序列分布变化，如新单倍型/结构变异/物种）、label shift（测量过程变化，如不同检测平台）、concept shift（序列-功能映射关系变化，如不同组织/环境）。**迁移到三维基因组**：染色质构象预测模型应明确测试跨细胞类型（concept shift）、跨物种（covariate shift）、跨实验技术如 Hi-C vs HiChIP vs Micro-C（label shift）的性能。

2. **观测-扰动互补的证据链设计**：观测数据（ATAC-seq、ChIP-seq、Hi-C）提供内源环境中的关联证据；报告基因检测（MPRA/STARR-seq）提供分离的序列内在活性；内源编辑（CRISPR）提供因果验证。**迁移到三维基因组**：Hi-C 预测的增强子-启动子互作可通过 CRISPR 删除增强子后检测目标基因表达和染色质互作变化来验证；也可用报告基因系统测试特定序列片段的增强子活性。

3. **"上下文"是核心变量而非噪声**：植物中同一序列在不同组织/环境下的功能差异巨大，模型必须显式编码上下文。**迁移到三维基因组**：染色质构象预测模型应纳入细胞类型、发育阶段、处理条件等上下文信息，而非仅依赖序列。

4. **不确定性指导实验选择（主动学习）**：模型应输出校准的不确定性，优先选择高不确定性、高信息增益的实验。**迁移到三维基因组**：在预测 CTCF 结合位点或增强子-启动子互作时，优先验证模型分歧最大的区域，可最大化每轮实验的信息量。

5. **持续学习的三策略**：replay-based rehearsal（重放旧数据）、参数正则化（如 EWC）、模块化 adapter 架构（新增任务参数而不覆盖共享表示）。**迁移到三维基因组**：随着新物种、新细胞类型的 Hi-C 数据持续产生，模型更新需避免灾难性遗忘。

6. **"性能报告必须分层"**：模型应在独特序列 vs 重复序列、参考 vs 非参考等位基因、近端 vs 远端调控等分层上分别报告性能，而非仅报告聚合指标。**迁移到三维基因组**：应分别报告 TAD 边界、CTCF 环、增强子-启动子互作等不同结构特征的预测性能。

7. **"更长上下文不保证更好泛化"**：架构扩展（更长窗口、更大模型）需要与训练多样性和归纳偏置匹配，否则只是计算成本增加。**迁移到三维基因组**：从局部序列到 1Mb 窗口的扩展需要验证是否真正提升了远端调控预测能力，而非仅增加参数。

8. **锚定物种基准策略**：建议以拟南芥、水稻、玉米、高粱、番茄、大豆、小麦等作为锚定物种建立跨物种基准。**迁移到三维基因组**：可建立跨物种的染色质构象基准集（如人类、小鼠、拟南芥、水稻、玉米），测试模型的可迁移性。

---

## 15 与已有知识连接

- **与人类/动物 seq2func 的联系**：文中引用的奠基工作（Zhou and Troyanskaya 2015; Kelley et al. 2016; Avsec et al. 2021）均来自人类/动物系统。植物 seq2func 的发展路径（CNN → 长上下文 → 基础模型）与动物系统高度平行，但植物特有的基因组特征（转座子丰富、多倍化、G×E 显著）要求专门的评估框架。**可迁移到三维基因组**：人类三维基因组预测模型（如 Enformer、Akita）的架构和经验可直接迁移到植物，但需注意植物特有的染色质组织特征（如更小的 TAD 结构、不同的 CTCF 非依赖绝缘机制）。

- **与三维基因组预测模型的接口**：文中提及 DeepCBA（Wang et al. 2024）整合染色质可及性和染色质互作信息预测基因表达，这直接连接了 seq2func 与三维基因组建模。**可迁移**：三维基因组预测模型（如预测 Hi-C 接触图的深度模型）可作为 seq2func 的中间层或特征提供者，为基因表达预测提供远端调控上下文。

- **与基础模型/基因组语言模型的联系**：文中引用的 PlantCaduceus、AgroNT 等植物基因组基础模型，与动物基因组基础模型（如 Nucleotide Transformer、DNABERT-2）构成平行发展。**可迁移到三维基因组**：基因组基础模型的表征可微调用于染色质构象预测，或作为多任务学习中的共享编码器。

- **与因果推断文献的联系**：文中"观测关联 ≠ 因果"的论点与孟德尔随机化、共定位分析等遗传流行病学方法形成互补——seq2func 提供分子层面的因果候选，遗传学方法提供群体层面的因果证据。**可迁移到三维基因组**：染色质互作预测的因果验证可借鉴这一分层证据策略。

- **与主动学习/持续学习文献的联系**：文中引用的 EWC（Kirkpatrick et al. 2017）和 replay 策略（Parisi et al. 2019）来自持续学习领域。**可迁移到三维基因组**：这些方法可直接应用于跨细胞类型、跨物种的染色质构象模型持续更新。

- **与泛化理论的联系**：文中对分布偏移的分类（covariate/label/concept shift）源自监督学习中的数据集偏移理论（如 Quiñonero-Candela et al. 2008 的框架）。**可迁移到三维基因组**：为三维基因组模型的泛化评估提供了理论语言。

---

## 16 研究想法

> 标题：Agent 生成的研究候选

### 候选 1：植物三维基因组 seq2func 的分布偏移基准集
- **名称**：Plant3D-Gen-Bench：跨物种/跨组织/跨平台的染色质构象预测基准
- **来源局限/观察**：本文提出分布偏移评估框架但未落地；三维基因组领域同样缺乏系统性的跨条件评估基准
- **核心假设**：现有染色质构象预测模型在跨细胞类型（concept shift）、跨物种（covariate shift）、跨实验技术（label shift）上的性能衰减可被量化，且衰减模式可预测
- **初步方法**：收集拟南芥、水稻、玉米、番茄的 Hi-C/HiChIP/Micro-C 数据，按细胞类型、发育阶段、物种、实验平台分层构建测试集；评估现有模型（如 Akita 风格架构）在各分层上的性能；报告校准误差和不确定性质量
- **验证方式**：与随机留出基线对比，展示分层评估揭示的泛化差距；建立公开排行榜
- **创新状态**：unverified（三维基因组领域已有跨细胞类型评估，但缺乏系统性的分布偏移分类框架和植物多物种基准）

### 候选 2：上下文条件化的染色质构象预测模型
- **名称**：ContextFold：显式编码细胞状态与环境的染色质构象预测模型
- **来源局限/观察**：本文强调"上下文决定序列-功能关系"，但现有三维基因组预测模型大多仅以序列为输入，忽略细胞类型/处理条件
- **核心假设**：将细胞类型、发育阶段、处理条件作为显式条件输入，可显著提升跨条件泛化能力，且优于仅增加序列窗口长度
- **初步方法**：在现有长上下文架构（如 Enformer 风格）基础上，增加条件编码器（如细胞类型 embedding、处理条件向量），与序列表征融合后预测 Hi-C 接触图或调控输出；在植物多组织数据上训练
- **验证方式**：与无条件基线在跨组织预测任务上对比；测试在未见组织上的零样本泛化
- **创新状态**：partially checked（人类系统中已有条件模型探索，植物中未见系统实现）

### 候选 3：不确定性引导的染色质互作验证闭环
- **名称**：Active3D-Loop：基于模型不确定性的 Hi-C 互作验证实验选择框架
- **来源局限/观察**：本文提出主动学习选择实验，但未具体化；三维基因组中，Hi-C 预测的互作需要 3C/qPCR 或 CRISPR 验证，成本高，需要优先排序
- **核心假设**：模型不确定性（如 ensemble 分歧、MC-dropout 方差）与预测错误的概率正相关，不确定性最高的互作对包含最多的新信息
- **初步方法**：训练 ensemble 染色质构象预测模型，对候选增强子-启动子互作输出预测均值和不确定性；设计采集函数（如 BALD、uncertainty sampling）排序候选；在拟南芥或水稻中选取 Top-K 进行 3C/qPCR 验证
- **验证方式**：比较不确定性引导选择与随机选择、预测强度排序选择的验证命中率；评估每轮验证后模型性能提升
- **创新状态**：unverified（主动学习在调控基因组学中已有概念验证，但未在三维基因组互作验证中系统应用）

### 候选 4：转座子插入多态性的调控效应预测
- **名称**：TE-Reg-Effect：预测转座子插入对染色质状态和互作影响的 seq2func 模型
- **来源局限/观察**：本文指出转座子可贡献调控元件但效应依赖上下文；现有 seq2func 模型对转座子序列的预测可靠性未经验证
- **核心假设**：转座子插入的调控效应可通过其序列特征、插入位置和表观状态预测，且模型需在重复序列分层上单独评估
- **初步方法**：利用泛基因组中已知的转座子插入多态性，结合对应基因座的 ATAC-seq/甲基化/Hi-C 数据构建训练集；训练模型预测插入后的染色质状态变化；在独立品系中验证
- **验证方式**：在转座子插入位点的预测准确率 vs 非重复区域；跨品系泛化测试
- **创新状态**：unverified（转座子调控功能已有大量实验研究，但系统性的 seq2func 预测模型缺乏）

### 候选 5：多倍体亚基因组特异性调控预测
- **名称**：SubGenome-Seq2Func：面向多倍体作物的亚基因组特异性调控预测框架
- **来源局限/观察**：本文强调多倍体（如小麦、棉花）中同源基因座序列高度相似但调控不同，现有模型无法区分
- **核心假设**：同源基因座的调控差异可由序列差异（如 SNP、indel、TE 插入）和表观状态共同预测，且亚基因组特异性特征可学习
- **初步方法**：利用小麦或棉花的亚基因组分辨的 ATAC-seq/RNA-seq 数据，构建同源基因座对数据集；训练模型区分亚基因组特异性调控；整合 Hi-C 数据预测同源基因座的互作差异
- **验证方式**：同源基因座对的分类准确率；与 aggregate 基因水平模型的对比
- **创新状态**：unverified（多倍体调控已有组学研究，但 seq2func 建模几乎空白）