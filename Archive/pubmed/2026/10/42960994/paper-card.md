## 01 基本信息
- 标题：Cross-task benchmarking reveals variable transferability of deep learning models across molecular quantitative trait loci
- 作者与单位：Chen, Sihan; Wang, Xiaoyu; Peleg, Anton Y; Xu, Shuting; Li, Fuyi; Webb, Geoffrey I; Song, Jiangning（具体单位未在提供材料中列出；通讯与监督为 J.S., G.W., F.L.）
- 期刊/预印本平台：Briefings in Bioinformatics
- 年份：2026-10-30（按提供日期）
- 论文类型：Benchmarking / 方法学评估研究（跨任务迁移性评测）
- 领域：基因组学 × 深度学习 × 调控变异功能预测（xQTL）
- 关键词：未提供（可据摘要概括：xQTL、eQTL、cross-task transferability、genomic foundation models、variant prioritization）
- DOI/arXiv 号：10.1093/bib/bbag599
- 代码：https://github.com/SihanChen-bioinfo/xQTL-ModelBenchmarking
- 数据：GTEx v10 及既往发表数据集（apaQTL、bQTL、caQTL、clQTL、eQTL、hQTL、miQTL、pQTL、sQTL）；1000 Genomes Project 作为负对照来源；GWAS Catalog CAD-SNPs（2492 个）
- 阅读日期：未提供
- 在「三维基因组/染色质组织 × AI/物理模拟」方向中的位置：本文并非三维基因组建模论文，而是对染色质相关调控变异（含 clQTL，即 chromatin looping QTL）预测模型的跨任务迁移性评测。对本课题的价值在于：① 直接给出 clQTL（染色质环化）在当前主流序列/注释模型下的可预测性下限证据；② 提供「长程上下文表征 vs 局部序列」在染色质高级结构相关任务上的对比结论；③ 提供可迁移的 benchmark 设计范式（统一预处理、染色体划分、类别不平衡敏感性、共识预测策略）。

## 02 一句话总结
该研究用统一的预处理与评测流程，将六个代表性调控变异预测模型（GWAVA、DeepSEA、ExPecto、Enformer、Borzoi、AlphaGenome）的预训练特征迁移到九类 xQTL 的二分类任务上，发现迁移性随分子表型显著变化——染色质可及性/转录因子结合/组蛋白 QTL 易预测，而染色质环化（clQTL）与 microRNA QTL 难预测，长程表征的基础模型（AlphaGenome、Borzoi）整体更优且更抗类别不平衡，并据此在 CAD GWAS 位点上给出 337 个共识候选 caQTL。

## 03 研究问题
- 具体问题：以 eQTL 为中心训练的调控变异预测模型，其预训练特征能否迁移到其他分子表型（xQTL）的变异优先级排序任务？迁移性由什么因素决定？
- 为什么重要：>90% 复杂性状相关变异位于非编码区，实验鉴定 xQTL 成本高、依赖组织/细胞类型；若模型只能预测 eQTL，则无法覆盖更广的调控架构。
- 现有方法为何不足：计算工作过度集中于 eQTL，对其他调控表型泛化性有限；早期方法（GWAVA）依赖注释可得性，序列模型（DeepSEA、ExPecto）受限于短序列上下文，难以捕捉长程调控互作。
- 精确研究问题（Can ... ?）：Can pretrained regulatory features from eQTL-centric sequence- and annotation-based models transfer across nine classes of xQTLs, and which model/feature properties determine the degree of transferability?

## 04 背景与发展脉络
- 阶段一：基于注释的方法（GWAVA）——利用人工整理功能注释做变异优先级排序；优点：生物学信息直接；局限：受注释可得性约束，不直接从 DNA 序列学习，难捕捉上下文依赖与长程效应。
- 阶段二：短上下文序列模型（DeepSEA、ExPecto）——直接从原始 DNA 序列预测多种调控活性；优点：可解释 eQTL；局限：序列上下文短，难捕捉长程调控互作。
- 阶段三：基因组基础模型（Enformer、Borzoi、AlphaGenome）——自监督建模长程依赖，统一框架同时捕捉局部序列决定因素与远端调控互作；优点：长程表征、跨细胞上下文；局限：模型规模、算力、预训练数据依赖。
- 本文主张的位置：在上述脉络中，本文不提出新模型，而是主张「跨表型迁移性被系统性高估」，并给出迁移性梯度（chromatin-activity-linked 表型 > 高阶/转录后表型）的实证框架。
- 脉络标注：以上阶段划分与代表性方法定位来自本文 Introduction 的叙述（仅本文框架）；其中 Enformer/Borzoi/AlphaGenome 长程优势与既往工作一致的说法由作者引用 [20,21,25] 支撑，但未在提供材料中做外部独立核验。

## 05 核心痛点
| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|---|---|---|---|
| 计算研究过度集中于 eQTL | 其他调控表型缺乏稳健预测器 | 作者称该窄焦点限制了基因组调控架构理解 | Introduction 段 4；引用 [10,11,18,19,21,22] |
| 跨表型迁移性未知 | 模型在 eQTL 表现好，其他 xQTL 表现差异大 | 作者归因于不同分子表型调控复杂度不同、与染色质特征关联直接程度不同 | Results「Cross-xQTL prediction performance」；Discussion 段 2 |
| clQTL/miQTL 难预测 | 所有模型一般 AUROC < 0.71，MCC 低 | 作者解释为其机制更 context-specific 或间接，现有数据与架构表征不足 | Results 图 3A、Fig. S3、Table 1；Discussion 段 2 |
| 类别不平衡下指标虚高 | AUROC 稳定但 AUPRC/F1/MCC 随负样本比例上升显著下降 | 作者指出 AUROC 在功能变异稀疏的真实场景下可能高估实用性 | Results「Factors influencing...」；图 5、Fig. S9、Table S7 |
| 线性分类器失效 | L1/Enet 在多个 xQTL 上 AUROC 接近 0.5、MCC 近 0 | 作者解释为序列模型表征含大量非线性交互 | Results 图 4、Fig. S8、Table S6 |
| 特征维度不一致 | 六个模型输出特征维度不同 | 作者承认这可能是性能比较的潜在混杂因素 | Discussion 段 1（作者自述） |

## 06 核心思想
1) 表面方法：固定统一预处理与评测管线，把六个模型的变异级染色质特征抽出，统一训练 XGBoost 等下游分类器，在九类 xQTL 上做二分类，并做不平衡、随机种子、染色体划分、阈值四类敏感性分析。
2) 核心洞察：模型迁移性不是模型固有属性，而是「预训练表征与目标分子表型之间对齐程度」的函数——与染色质活性直接相关的表型（caQTL/bQTL/hQTL）可迁移，涉及高阶染色质构象（clQTL）或转录后过程（miQTL）的表型不可迁移。
3) 可能的普适教训 [Analysis]：在评测跨任务泛化时，必须把「表征对齐度」与「分类器容量」分离考察；仅报告 AUROC 会系统性掩盖稀疏正例场景下的实用性衰减；共识预测（多模型一致）可作为无标签条件下的候选提纯手段。

## 07 方法总览
- 输入：九类 xQTL 的显著变异（正例）+ 1000 Genomes 抽样的非 xQTL 变异（负例，1:10，另做 1:5、1:1）；MAF ≥ 0.01；CAD-SNPs 2492 个。
- 输出：各模型在各 xQTL 上的 AUROC/AUPRC/F1/MCC/Brier；特征重要性富集；337 个共识 CAD 相关候选 caQTL。
- 模块：① 数据收集与负对照构建（含严格匹配敏感性集：≥500 kb、排除已知 xQTL、MAF 差 <0.05、按调控元件注释匹配）；② 六模型特征抽取；③ 下游分类器（XGBoost 主，RF/L1/Enet 对照）；④ 评测指标；⑤ 特征重要性→组织注释映射 + 10 000 次置换检验 + FDR；⑥ g:Profiler 富集（KEGG、HP）；⑦ 等位特异 DNase-seq 信号差异评估。
- 训练：染色体划分（每数据集随机选测试染色体保留约 20%），同一划分用于全部六模型；训练集内 5 折交叉验证调参；固定随机种子 seed=0（另做 42、68）。
- 工具：XGBoost、Random Forest、L1、Elastic Net；g:Profiler；GENCODE v38。
- 反馈回路：无显式迭代反馈回路（单轮 benchmark）。
- 假设：模型输出的变异级染色质特征是可比且可迁移的；负对照抽样能代表非功能变异；固定阈值 0.5 在跨模型比较中公平。
- 文字流程：收集九类 xQTL 与负对照 → 按染色体划分训练/测试 → 六模型抽取变异级特征 → 训练 XGBoost（5 折调参）→ 在测试染色体上算 AUROC/AUPRC/F1/MCC/Brier → 做不平衡/种子/染色体/阈值敏感性 → 特征重要性富集与组织映射 → 迁移到 CAD-SNPs 做共识候选 → 富集分析与等位特异 DNase 验证。

## 08 核心模块拆解
| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|---|---|---|---|---|---|
| 统一预处理与评测管线 | 保证跨模型公平比较 | 六模型架构与特征表示不同 | 输入 xQTL 变异集；输出统一特征矩阵与划分 | Fig. 1；Materials and methods | 移除则跨模型比较不可比（预期效应） |
| 负对照构建（1:10，另 1:5/1:1） | 构造类别不平衡的真实场景 | 功能变异稀疏 | 1000G 抽样 → 负例集 | Table S1；Results | 移除则无法评估不平衡鲁棒性（预期效应） |
| 严格匹配负对照敏感性集 | 排除 LD 与注释混杂 | 主分析负对照可能引入偏差 | ≥500 kb、MAF 匹配、注释匹配 → 敏感性结果 | Fig. S7 | 实测：主结论趋势被复现，未改变结论 |
| 六模型特征抽取 | 提供迁移表征 | 比较不同表征范式 | 变异 → 染色质特征 | Table S2；Fig. 2D/E、Fig. S1/S2 | 移除则无迁移性结论（预期效应） |
| XGBoost 下游分类器 | 非线性整合特征 | 表征含非线性交互 | 特征 → 概率 | 图 4、Fig. S8、Table S6 | 实测：换线性模型（L1/Enet）性能大幅下降，部分近随机 |
| 随机种子重复（0/42/68） | 检验初始化稳健性 | 排除随机性 | 三次运行 → 均值/SD | Table S3 | 实测：AUROC SD 0.00012–0.00735，AUPRC SD 0.00004–0.01106，结论稳健 |
| 统一测试染色体分析 | 排除染色体组成影响 | 各 xQTL 原划分不同 | 固定 chr2/12/14/19/21 | Table S4 | 实测：与原始划分基本一致，仅微小差异 |
| 阈值敏感性分析 | 检验固定 0.5 的影响 | 不平衡下阈值敏感 | 训练集 MCC 最优阈值 → 测试 | Table S5 | 实测：F1/MCC 变化，AUROC/AUPRC 基本不变，结论一致 |
| 特征重要性→组织映射 + 置换检验 | 解释生物学相关性 | 连接特征与表型 | 特征 → 组织富集 + 经验 P + FDR | Fig. 2D/E、Fig. S1/S2/S5/S6 | 移除则失去机制解释（预期效应） |
| 共识预测（AlphaGenome ∩ Borzoi） | 提纯候选 | 单模型假阳性 | CAD-SNPs → 337 候选 | Fig. 6B、Fig. S10 | 实测：两模型 PCC 0.807、Spearman 0.746、一致率 89.92%、κ=0.6673 |
| 等位特异 DNase-seq 差异 | 正交功能验证 | 预测需独立支持 | 候选 vs 非 caQTL → 信号差 | Fig. 6C/D/E | 实测：共识候选等位差异显著大于非 caQTL |

## 09 关键公式符号
- F1 与 MCC：文中给出定义式（Materials and methods「Model performance evaluation」），其中 TP/TN/FP/FN 分别为真阳/真阴/假阳/假阴。用途：阈值依赖的二分类性能；直觉：MCC 对类别不平衡更稳健。
- Brier score：$BS = \frac{1}{N}\sum_{i=1}^{N}(f_i - y_i)^2$，其中 $f_i$ 为变异 i 的预测概率，$y_i \in \{0,1\}$ 为真实标签，N 为变异数。用途：评估概率校准；直觉：越低越好。
- Pearson 相关系数（PCC）：用于预测概率与效应大小的相关（Results 图 2F、图 3B/C），以及 AlphaGenome 与 Borzoi 分数相关（Fig. S10）。具体公式未在提供材料中展开。
- 注：F1、MCC 的完整展开式在提供材料中以「calculated as follows」引出但公式体未完整呈现，故不臆造。

## 10 实验设计与证据链
- 数据集/群体：九类 xQTL（apaQTL、bQTL、caQTL、clQTL、eQTL、hQTL、miQTL、pQTL、sQTL），来源 GTEx v10 与既往发表；eQTL 为 14 811 个全血 eQTL；负对照来自 1000 Genomes，比例 1:10（另 1:5、1:1）；MAF ≥ 0.01；CAD-SNPs 2492 个（GWAS Catalog，MONDO_0005090）。
- 规模：各 xQTL 具体数量见 Table S1（提供材料未列数值）。
- 指标：AUROC、AUPRC、F1、MCC、Brier score；MAF 分布一致性；PCC（概率 vs 效应大小）。
- 基线：六模型互为基线；下游分类器以 XGBoost 为主，RF/L1/Enet 为对照。
- 预算：未提供（未报告 GPU/训练成本）。
- 骨干/仪器：GWAVA、DeepSEA、ExPecto、Enformer、Borzoi、AlphaGenome；下游 XGBoost/RF/L1/Enet。
- oracle 输入：无 oracle 输入；标签来自实验鉴定的 xQTL。
- 评测协议：染色体划分，测试染色体保留约 20%；固定阈值 0.5；5 折交叉验证调参；固定 seed=0。

| 实验 | 检验的claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|---|---|---|---|---|---|---|
| eQTL 预测 | 六模型在 eQTL 上的性能排序 | 1:10 不平衡 | AlphaGenome AUROC=0.810/AUPRC=0.389/F1=0.343/MCC=0.292 最佳；Borzoi 0.804、Enformer 0.799；GWAVA 0.775；ExPecto 0.724；DeepSEA 0.688 | 基础模型在 eQTL 上更优 | 不能说明在其他表型同样最优 | Results 图 2、Table 1 |
| 跨 xQTL 预测 | 迁移性是否随表型变化 | 九类 xQTL × 六模型 | caQTL/bQTL/hQTL 高（caQTL AlphaGenome AUROC=0.954、AUPRC=0.757）；clQTL/miQTL 一般 AUROC<0.71；apaQTL/pQTL/sQTL 中等（pQTL Borzoi AUROC=0.794、AUPRC=0.442） | 存在迁移性梯度 | 不能说明 clQTL/miQTL 不可预测（仅当前特征下难） | Results 图 3、Fig. S3、Table 1 |
| 负对照敏感性 | 结论是否受负对照选择影响 | 严格匹配集（≥500 kb、MAF、注释） | 趋势复现 | 主结论稳健 | 不能排除其他未匹配混杂 | Fig. S7 |
| 随机种子 | 结论是否受初始化影响 | seed 0/42/68 | AUROC SD 0.00012–0.00735；AUPRC SD 0.00004–0.01106 | 对初始化稳健 | 不能推广到未测种子 | Table S3 |
| 统一测试染色体 | 结论是否受染色体组成影响 | chr2/12/14/19/21 | 与原始划分基本一致 | 对划分稳健 | 不能排除其他染色体组合 | Table S4 |
| 阈值敏感性 | 固定 0.5 是否影响结论 | 训练集 MCC 最优阈值 | F1/MCC 变化，AUROC/AUPRC 基本不变 | 结论不依赖固定阈值 | 不能说明最优阈值在所有场景最优 | Table S5 |
| 分类器选择 | 下游分类器影响多大 | XGBoost vs RF vs L1 vs Enet | XGBoost 最佳（caQTL AUROC 0.894–0.954、AUPRC 0.652–0.757）；RF 略低（0.887–0.946、0.598–0.733）；线性模型常近随机 | 非线性集成更优 | 不能说明 XGBoost 在所有特征集上最优 | 图 4、Fig. S8、Table S6 |
| 类别不平衡 | 不平衡如何影响指标 | 1:1/1:5/1:10 | AUROC 稳定，AUPRC 显著下降（AlphaGenome caQTL AUPRC 0.954→0.757）；基础模型更稳健 | AUROC 可能高估实用性 | 不能说明基础模型完全免疫不平衡 | 图 5、Fig. S9、Table S7 |
| CAD 候选识别 | 能否迁移到疾病位点 | AlphaGenome ∩ Borzoi | Borzoi 503、AlphaGenome 422，共识 337（11 已知 + 326 新）；PCC 0.807、Spearman 0.746、一致率 89.92%、κ=0.6673 | 共识策略可提纯候选 | 不能建立因果性 | 图 6、Fig. S10 |
| 功能富集 | 候选是否生物学相关 | g:Profiler KEGG/HP | 胆固醇代谢 FDR=5.32×10⁻⁹；atherosclerosis FDR=8.57×10⁻⁹；arteriosclerosis FDR=2.14×10⁻⁸；coronary artery atherosclerosis FDR=7.42×10⁻⁵ | 候选与 CAD 相关过程富集 | 不能证明这些基因因果驱动 CAD | Fig. S11、Fig. S12 |
| 等位特异 DNase | 候选是否有功能信号 | 共识候选 vs 非 caQTL | 共识候选等位差异显著更大；rs11670056 差异明显且在 ELL 基因内 | 提供正交支持 | 不能替代实验验证 | 图 6C/D/E |

## 11 结论正确解读
- 任务范围：二分类变异优先级排序，非效应量回归、非因果推断、非三维结构预测。
- oracle/真值输入：标签来自实验鉴定的 xQTL（GTEx v10 与既往发表），无 oracle 特征输入。
- 端到端状态：不是端到端——预训练模型冻结，仅下游分类器训练；因此结论针对「冻结表征的可迁移性」，不针对微调后的可迁移性。
- 算力成本：未报告；作者在 Discussion 中提及基础模型受模型规模、算力、预训练数据依赖约束，但无量化。
- 历史数据依赖：依赖 GTEx v10 与既往发表数据集的组织/细胞类型覆盖；预训练数据与目标组织匹配度可能影响性能（作者引用 [43]）。
- 模型依赖：结论限于所测六模型；作者明确未评估 Caduceus、HyenaDNA、Nucleotide Transformer 等基因组语言模型。
- 最难情形：clQTL 与 miQTL（一般 AUROC<0.71）；高类别不平衡（1:10）下的 AUPRC/F1/MCC。
- 群体/领域边界：eQTL 为全血，bQTL/caQTL/clQTL 为 HCASMC，hQTL 为 LCL，miQTL/pQTL/sQTL 为全血，apaQTL 为全血；CAD-SNPs 为常染色体；MAF ≥ 0.01。
- 不确定性：特征维度差异为潜在混杂（作者自述）；负对照抽样策略虽做敏感性但仍可能残留混杂；共识候选需 fine-mapping、colocalization 或正交功能实验确认因果。
- 有边界复述：在当前六模型冻结表征 + XGBoost 下游 + 上述数据条件下，跨 xQTL 迁移性存在稳定梯度，长程基础模型在多数表型与不平衡条件下更优，但 clQTL/miQTL 仍难预测，CAD 候选仅为优先级排序而非因果结论。

## 12 作者自认局限
| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|---|---|---|---|
| 特征维度不一致 | 六模型输出特征维度不同，可能混杂性能比较 | 未明确给出解决方向，仅作为潜在混杂提出 | Discussion 段 1 |
| 未评估新兴基因组语言模型 | Caduceus、HyenaDNA、Nucleotide Transformer 未纳入 | 未来扩展纳入以检验结论是否跨范式成立 | Discussion 段 5 |
| 基础模型算力约束 | 模型规模、计算需求、预训练数据依赖 | 大规模或资源受限应用时需权衡 | Discussion 段 5 |
| 候选因果性未建立 | 共识候选需进一步验证 | fine-mapping、colocalization 或正交功能实验 | Results「Identification of novel CAD-associated caQTLs」末段 |

作者提及的相关约束（非正式局限）：预训练数据与目标组织/细胞类型匹配度可能影响性能（Discussion 段 2，引用 [43]）；基因组基础模型领域快速演进，benchmark 范围有时效性（Discussion 段 5）。

## 13 批判性分析
| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|---|---|---|---|---|
| 冻结表征 + XGBoost 的评测范式可能低估基础模型 | 微调或端到端训练可能改变迁移性排序 | 若结论被用于「选模型」，冻结设定可能误导 | 对同一六模型做微调/线性探测对比 | Materials and methods（冻结特征 + XGBoost） |
| 特征维度差异未控制 | 高维特征可能仅因容量优势而表现更好 | 可能把「维度红利」误读为「长程表征优势」 | 维度对齐（PCA/随机投影）后重跑 | Discussion 段 1（作者自述） |
| 负对照来自 1000 Genomes 随机抽样 | 即使严格匹配，仍可能残留功能相关混杂 | 影响 AUPRC 绝对值与跨表型比较 | 使用不变/中性位点或匹配功能注释的负对照 | Materials and methods；Fig. S7 |
| clQTL 难预测的归因未直接检验 | 可能是特征缺失，也可能是标签质量/样本量问题 | 决定后续应改架构还是改数据 | 报告 clQTL 样本量、标签来源、特征覆盖度并做消融 | Results 图 3A；Discussion 段 2 |
| 共识策略（∩）提高精度但可能损失召回 | 两模型共享偏差会同时漏掉真候选 | 影响下游候选清单完整性 | 报告单模型 vs 共识的召回代理指标（如已知 caQTL 回收率） | Fig. 6B、Fig. S10 |
| 等位特异 DNase 验证非因果 | 等位差异可能来自 LD 或细胞类型特异 | 支持相关性而非因果 | fine-mapping/colocalization/MPRA | 图 6C/D/E；Results 末段 |
| 组织匹配度作为解释未量化 | 未给出预训练组织与目标组织的匹配度量 | 使「对齐度」解释停留在定性 | 构造组织匹配评分并与性能做相关 | Discussion 段 2（引用 [43]） |

## 14 学到什么
Agent 提炼的知识候选：
- 可迁移概念：跨任务迁移性应作为「表征-表型对齐度」的函数来评测，而非模型固有属性；迁移性梯度（染色质活性直接相关 > 高阶构象/转录后）可作为本课题的先验假设。
- 可迁移方法：统一预处理 + 染色体划分 + 固定随机种子 + 多类敏感性分析（负对照、种子、染色体、阈值）的 benchmark 范式，可直接迁移到三维基因组预测任务（如 contact map 预测、loop 预测、TAD 边界预测）的评测设计。
- 可迁移公式/指标：Brier score 用于概率校准；MCC 用于不平衡场景；AUROC 与 AUPRC 分离报告以暴露稀疏正例下的实用性衰减。
- 可迁移实验设计：共识预测（多模型交集）作为无标签提纯策略；等位特异信号差异作为正交验证代理。
- 面向本课题的迁移点：clQTL 难预测（AUROC<0.71）提示当前序列/注释表征对染色质环化机制覆盖不足，可考虑引入 Hi-C/Micro-C 衍生特征、结构域上下文或物理模拟先验；长程基础模型优势提示在三维基因组任务中应优先评估长程上下文架构；类别不平衡敏感性提示在 loop/TAD 等稀疏事件预测中必须报告 AUPRC 而非仅 AUROC。

## 15 与已有知识连接
- 相似：本文对 Enformer/Borzoi/AlphaGenome 长程优势的结论与作者引用 [20,21,25] 一致（经本文引用，未在提供材料中独立核验）。
- 组合：本文的 benchmark 范式可与三维基因组预测任务（contact map、loop、TAD）评测组合，形成「调控变异 × 染色质构象」的联合评测。
- 冲突：本文发现 GWAVA（纯注释）在多个 xQTL 上优于 DeepSEA/ExPecto（短序列模型），与「序列模型必然优于注释模型」的直觉冲突；作者以此强调生物学注释仍高度信息量。
- 可迁移领域：基因组语言模型（Caduceus、HyenaDNA、Nucleotide Transformer，作者引用 [23,44,45]）代表不同范式，其表征是否在三维基因组任务上更可迁移，为候选方向（未核验）。
- 用户已有知识连接：若用户熟悉 Hi-C 数据稀疏性与 loop 检测的类别不平衡问题，本文的 AUROC/AUPRC 分离结论可直接类比。

## 16 研究想法
Agent 生成的研究候选：

1) 名称：三维基因组任务上的跨任务迁移性 benchmark（3D-xQTL-Bench）
- 来源局限/观察：本文发现 clQTL 难预测（AUROC<0.71），且未评估三维构象专用表征。
- 核心假设：引入 Hi-C/Micro-C 衍生特征或结构域上下文可提升 clQTL 及 loop/TAD 相关任务的迁移性。
- 相对本文的增量：把 benchmark 从「序列/注释特征」扩展到「构象特征」，并覆盖 loop/TAD 预测任务。
- 初步方法：在本文统一管线上，替换/拼接特征为「基础模型嵌入 + 构象特征」，下游仍用 XGBoost 与线性对照。
- 验证方式：与本文 clQTL 结果对比 AUROC/AUPRC/MCC；做特征消融与不平衡敏感性。
- 可能的失败模式：构象特征与标签循环依赖（Hi-C 数据本身用于定义 clQTL），导致信息泄漏。
- 创新状态：unverified。

2) 名称：表征维度对齐的迁移性归因实验
- 来源局限/观察：作者自述特征维度差异为潜在混杂。
- 核心假设：维度对齐后，基础模型相对局部模型的优势会缩小但不会消失。
- 相对本文的增量：把「长程表征优势」与「维度红利」分离。
- 初步方法：对六模型特征做 PCA/随机投影到统一维度，重跑全部 xQTL。
- 验证方式：比较对齐前后 AUROC/AUPRC 差值；报告置信区间。
- 可能的失败模式：降维破坏非线性结构，导致所有模型同时退化，无法归因。
- 创新状态：partially checked（作者已承认混杂，但未做对齐实验）。

3) 名称：组织匹配度量化与性能预测
- 来源局限/观察：作者定性提出预训练组织与目标组织匹配度影响性能，但未量化。
- 核心假设：组织匹配评分与跨 xQTL 性能正相关。
- 相对本文的增量：把「对齐度」从定性解释变为可计算指标。
- 初步方法：用特征重要性组织富集分布构造匹配评分，与各 xQTL 性能做相关。
- 验证方式：留一表型交叉验证；置换检验。
- 可能的失败模式：匹配评分与性能均由同一特征重要性推导，存在循环。
- 创新状态：unverified。

4) 名称：共识预测的召回-精度权衡分析
- 来源局限/观察：本文用 AlphaGenome ∩ Borzoi 提纯候选，但未报告召回。
- 核心假设：共识策略在提高精度的同时损失可测量的召回，且损失随模型相关性升高而增大。
- 相对本文的增量：给出共识策略的定量权衡曲线。
- 初步方法：用已知 caQTL 作为正例锚点，计算单模型 vs 共识的召回代理；模拟不同模型相关性下的权衡。
- 验证方式：在多个 xQTL 上重复；与随机交集对照。
- 可能的失败模式：已知 caQTL 数量太少，召回估计方差过大。
- 创新状态：unverified。