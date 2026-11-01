## 01 基本信息

- **标题**：XChrom: A Cross-Cell Chromatin Accessibility Prediction Model Integrating Genomic Sequence and Cellular Context
- **作者与单位**：Miao, Yuanyuan; Liang, Xuan; Zhang, Wenwen; Han, Dongmei; Li, Yurun; Wang, Zhen（单位未在提供材料中列出）
- **期刊/预印本平台**：Advanced Science (Weinheim, Baden-Wurttemberg, Germany)
- **年份**：2026-10-28（在线发表日期）
- **论文类型**：研究论文（含方法开发与基准测试）
- **领域**：单细胞表观基因组学 / 计算生物学 / 深度学习
- **关键词**：染色质可及性预测、单细胞、深度学习、跨细胞预测、序列建模
- **DOI/arXiv 号**：10.1002/advs.78456
- **代码**：https://github.com/Miaoyuanyuan777/XChrom（分析代码：https://github.com/Miaoyuanyuan777/XChrom_analysis）
- **数据**：10x Multiome 数据集（h_PBMC, m_brain, h_brain）、E-MTAB-11708（h_gonads）、GSE218576（m_palates）、GSE194122（BMMC）、GSE229169（跨物种运动皮层）、COVID-19 数据集（Helmholtz Berlin 存储库）、PBMC10k；处理后数据已上传 Zenodo: https://doi.org/10.5281/zenodo.16959681
- **阅读日期**：未提供
- **在「三维基因组/染色质组织 × AI 方法/物理模拟」方向中的位置**：该文属于「序列 → 染色质可及性」的深度学习预测方法，核心创新在于将细胞身份（来自 scRNA-seq）与 DNA 序列联合建模，实现跨细胞、跨区域、跨样本乃至跨物种的染色质可及性预测。与三维基因组方向的关联在于：染色质可及性是三维基因组功能读段之一，该文的方法论（序列编码 + 细胞上下文编码 + 矩阵乘法融合）可迁移至 3D 基因组结构预测（如 Hi-C 接触图的条件生成），但其本身不预测三维结构。

## 02 一句话总结

XChrom 通过将 DNA 序列编码（CNN）与 scRNA-seq 衍生的细胞身份嵌入（MLP）做矩阵乘法融合，在统一框架中同时实现跨区域（未见序列）、跨细胞（未见细胞）和跨样本/跨物种的染色质可及性预测，并在 COVID-19 单核细胞数据上验证了其对新型细胞状态和疾病相关调控变化的捕捉能力。

## 03 研究问题

- **具体问题**：能否构建一个统一的深度学习模型，同时预测 (i) 训练中未见的基因组区域（cross-region）、(ii) 训练中未见的细胞（cross-cell）、以及 (iii) 两者均未见的组合（cross-both）的染色质可及性？
- **为什么重要**：单细胞染色质可及性（scATAC-seq）是理解转录调控的关键，但配对的多组学数据（同一细胞的 RNA + ATAC）稀缺且昂贵。若能仅从 scRNA-seq（数据丰富）推断染色质可及性，将极大扩展表观基因组研究的覆盖范围，尤其在疾病样本中。
- **现有方法不足**：
  - 第一类（如 Seurat、LS_Lab、MultiVI）基于 RNA-ATAC 流形映射/共享潜空间，不利用 DNA 序列信息，因此无法预测训练数据中未定义的基因组区域。
  - 第二类（如 scBasset）是纯序列模型，能预测未见区域，但无法泛化到未见细胞——因为模型没有细胞身份的输入通道。
- **精确研究问题（Can ... ?）**：Can a deep learning model that jointly encodes genomic sequence and cell identity predict chromatin accessibility for unseen genomic regions and unseen cells simultaneously, and generalize across samples and species?

## 04 背景与发展脉络

> 注：此脉络基于本文框架整理，部分外部引用经核验（标注），整体判断为「经外部核验 + 本文框架」混合。

| 阶段 | 代表方法 | 优点 | 局限 | 本文位置 |
|---|---|---|---|---|
| 多组学整合（流形映射） | Seurat [5]（外部核验：Seurat v4 参考映射）、LS_Lab [6]、MultiVI [7] | 利用 RNA-ATAC 共享结构，可预测已有细胞类型 | 不利用序列，无法预测未见区域；依赖配对数据 | 本文在 cross-cell 任务中作为基线 |
| 序列模型 | scBasset [9]（外部核验：Calico 开源）、Basenji 类模型 | 捕捉序列-功能规则，可预测未见区域 | 无细胞上下文通道，无法泛化到未见细胞 | 本文的序列模块直接继承其 CNN 架构 |
| 多模态融合（本文） | XChrom | 序列 + 细胞身份联合建模，同时实现 cross-region / cross-cell / cross-both | 需要配对数据训练；细胞身份来自 RNA 可能引入模态偏差 | 本文提出的新位置 |

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|---|---|---|---|
| 配对多组学数据稀缺 | scATAC-seq 与 scRNA-seq 配对数据远少于单模态数据 | 实验成本高，难以大规模获取 | Introduction 第 2 段（"paired datasets of these two modalities remain relatively scarce"） |
| 现有跨模态方法无法预测未见区域 | Seurat/LS_Lab/MultiVI 仅能在训练中定义的基因组区域内预测 | 不利用 DNA 序列信息，缺乏序列-功能映射 | Introduction 第 3 段（"constrained to predicting chromatin accessibility only within the predefined genomic regions"） |
| 纯序列模型无法泛化到未见细胞 | scBasset 对未见细胞的预测无细胞特异性 | 模型无细胞身份输入，输出为平均/共享可及性 | Introduction 第 4 段（"cannot generalize to unseen cells"） |
| 跨样本/跨物种时批次效应干扰 | 直接迁移模型到新样本时性能下降 | scRNA-seq 数据存在技术性批次差异 | Results "XChrom can Predict New Samples..." 节（需批次校正，图 S10） |
| 训练集中稀有细胞类型难以学习 | 细胞类型占比过低时预测性能下降 | 数据不平衡导致细胞嵌入欠拟合 | Results 图 4c,d（B 细胞比例消融实验） |

## 06 核心思想

### 1) 表面方法

XChrom 是一个双通道神经网络：
- **序列通道**：以 1344 bp DNA 序列（one-hot 编码）为输入，经 7 层 CNN（卷积+BN+池化+GELU）输出 32 维 peak embedding。
- **细胞通道**：以 scRNA-seq 衍生的细胞嵌入（如 PCA 32 维）为输入，经 LayerNorm + 两层全连接（64→32）输出 32 维 cell embedding。
- **融合**：peak embedding 与 cell embedding 做矩阵乘法（外积），经 sigmoid 输出每个 peak × 每个细胞的二值可及性概率。
- **训练**：二元交叉熵损失，Adam 优化器（β1=0.95, β2=0.9995），学习率指数衰减，早停机制。

### 2) 核心洞察

- **可及性 = 序列潜能 × 细胞状态**：一个基因组区域的可及性由两部分决定——该区域编码的顺式调控信息（序列通道）和该细胞中反式调控环境（细胞通道）。矩阵乘法融合恰好建模了这种「乘法交互」而非「加法交互」，即序列特征在不同细胞状态下被差异化解读。
- **细胞嵌入作为条件变量**：将 scRNA-seq 衍生的细胞身份作为条件输入，使模型在推理时可以对任意新细胞（只要有 RNA 数据）预测其全基因组可及性，无需该细胞的 ATAC 数据。
- **跨物种泛化源于保守调控规则**：模型在人类数据上训练后能预测小鼠、猕猴、狨猴的可及性，说明其捕捉的是进化保守的序列-调控关系，而非物种特异记忆。

### 3) 可能的普适教训 [Analysis]

- **乘法融合优于拼接融合**：当两个输入模态存在「门控/调节」关系（如序列特征被细胞状态调制）时，外积/乘法融合比简单的向量拼接更符合生物机制，且能自然产生 peak×cell 的输出矩阵。
- **条件生成框架的通用性**：将「预测目标」分解为「固有属性编码器 × 上下文编码器」的框架，可迁移至其他条件预测任务（如 Hi-C 接触图按细胞类型条件生成、增强子-启动子互作按组织条件预测）。
- **消融实验设计范式**：通过替换/移除单一模块（如用细胞索引替代 RNA 嵌入、用简化 CNN 替代默认序列编码器）来归因各模块功能，是深度学习生物学方法验证的清晰范式。

## 07 方法总览

- **输入**：
  - 序列：peak 中心 ± 672 bp（共 1344 bp），one-hot 编码为 (1344, 4) 矩阵。
  - 细胞：scRNA-seq 经 PCA 降维后的 32 维嵌入（经 Z-score 归一化 + LayerNorm）。
  - 可选：测序深度（每个细胞的 Z-score 归一化值）作为可学习校正项。
- **输出**：每个 peak × 每个细胞的二值可及性概率矩阵（0-1 连续值）。
- **模块**：
  1. 序列编码器：7 个卷积块（Conv1D + BN + MaxPool + GELU），输出通道数递增（288→512），最后经 Conv1D + GELU 降维至 256 通道，再经全连接输出 32 维 peak embedding。
  2. 细胞编码器：LayerNorm → Dense(64, ReLU) → Dense(32, linear)。
  3. 融合层：peak embedding (P×32) × cell embedding (32×C) → P×C 矩阵 → 加测序深度校正项 → sigmoid。
- **训练**：二元交叉熵，Adam（β1=0.95, β2=0.9995），学习率 0.01 指数衰减（每 10000 步 ×0.9），早停（训练集 AUROC 50 轮无改善则停），最大 1000 epochs。
- **数据增强**：随机反向互补（50% 概率）、随机平移 ±3 bp。
- **推理**：输入新细胞的 RNA 嵌入 + 任意基因组坐标序列，输出该细胞的全基因组可及性预测。
- **工具**：Python 3.8, TensorFlow-GPU 2.6.0, Keras 2.6.0；预处理用 Scanpy 1.9.5, AnnData 0.9.2, scikit-learn 1.0.2。
- **基线方法**：scBasset（序列-only）、Seurat、LS_Lab、MultiVI（跨模态映射）。
- **评测协议**：三种测试集划分（cross-region / cross-cell / cross-both），指标为 AUROC/AUPRC（overall / per-cell / per-peak 三个层级）；细胞状态保真度用 NS、LS、ARI、AMI、ASW。

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|---|---|---|---|---|---|
| 序列编码器（7 层 CNN） | 从 DNA 序列提取顺式调控特征 | 使模型能预测未见基因组区域 | 输入：(1344,4) one-hot；输出：32 维 peak embedding | Results 图 2b：cross-region 任务与 scBasset 相当 | [实测] 替换为简化 3 层 CNN（simpler_CNN）后 cross-region AUROC 显著下降（图 4b） |
| 细胞编码器（2 层 MLP） | 将 scRNA-seq 嵌入变换为可与其他模态融合的细胞表示 | 使模型能泛化到未见细胞 | 输入：32 维 PCA 嵌入；输出：32 维 cell embedding | Results 图 2c：cross-cell 任务显著优于 Seurat/LS_Lab/MultiVI | [实测] 替换为细胞索引（cell_index）后 cross-cell 性能大幅下降（图 4a） |
| 矩阵乘法融合层 | 建模序列特征与细胞状态的乘法交互 | 可及性是序列潜能与细胞环境的乘积关系 | 输入：P×32 与 32×C；输出：P×C 概率矩阵 | Results 图 2d：cross-both 任务可行 | [预期] 若改为拼接+全连接，可能降低跨细胞泛化能力 [Analysis] |
| 测序深度校正项 | 校正单细胞测序深度对可及性检测的影响 | scATAC-seq 数据存在深度异质性 | 输入：每细胞 Z-score 深度；输出：加到 logit 的偏置项 | Methods "XChrom Architecture" 节 | [预期] 移除后低深度细胞预测偏差增大 [Analysis] |
| 数据增强（随机翻转/平移） | 增加序列输入的多样性，促进链/位置不变性 | 可及性不应依赖链方向或微小位移 | 训练时对序列做 50% 翻转和 ±3 bp 平移 | Methods "XChrom Architecture" 节 | [预期] 移除后可能降低 cross-region 泛化 [Analysis] |

## 09 关键公式符号

> 仅列理解模型所必需的公式。

**1. 序列编码**：
\[
h_{peak} = \text{Flatten}(\text{CNN}_{7}(X_{seq}))
\]
- \(X_{seq} \in \mathbb{R}^{1344 \times 4}\)：one-hot 编码的 DNA 序列
- \(h_{peak} \in \mathbb{R}^{32}\)：peak embedding

**2. 细胞编码**：
\[
h_{cell} = W_2 \cdot \text{ReLU}(W_1 \cdot \text{LayerNorm}(z_{rna}))
\]
- \(z_{rna} \in \mathbb{R}^{32}\)：scRNA-seq PCA 嵌入（Z-score 归一化后）
- \(W_1 \in \mathbb{R}^{64 \times 32}, W_2 \in \mathbb{R}^{32 \times 64}\)：可学习权重
- \(h_{cell} \in \mathbb{R}^{32}\)：cell embedding

**3. 融合与预测**：
\[
P_{ij} = \sigma\left( h_{peak,i}^\top h_{cell,j} + b \cdot d_j \right)
\]
- \(P_{ij}\)：peak \(i\) 在细胞 \(j\) 中的可及性概率
- \(h_{peak,i}^\top h_{cell,j}\)：矩阵乘法（外积）融合
- \(d_j\)：细胞 \(j\) 的测序深度（Z-score 归一化），\(b\) 为可学习标量
- \(\sigma(\cdot)\)：sigmoid 函数

**4. 损失函数**：
\[
\mathcal{L} = -\frac{1}{N}\sum_{i,j} \left[ y_{ij} \log P_{ij} + (1-y_{ij}) \log(1-P_{ij}) \right]
\]
- \(y_{ij} \in \{0,1\}\)：二值化可及性标签（测序计数 ≥ 1 为 1）

**5. 评估指标**：
- AUROC / AUPRC：在 overall（所有 peak-cell 对）、per-cell（按细胞平均）、per-peak（按 peak 平均）三个层级计算。
- NS（Neighbor Score）：\(NS_k = \frac{1}{N}\sum_{i=1}^{N} \frac{|N_k^{true}(i) \cap N_k^{imp}(i)|}{k}\)，衡量预测/去噪后数据与 RNA 空间的邻域一致性。
- LS（Label Score）：\(LS_k = \frac{1}{N}\sum_{i=1}^{N} \frac{1}{k}\sum_{j \in N_k^{imp}(i)} I(y_j = y_i)\)，衡量预测数据的局部标签纯度。

## 10 实验设计与证据链

**数据集**：
- 训练/测试：5 个公开配对 scRNA-seq + scATAC-seq 数据集（人类 PBMC、小鼠脑、人脑、性腺、腭板等），覆盖人类和小鼠。
- 跨样本：人类 BMMC 数据集（GSE194122），含多个供体/批次。
- 跨物种：人类、小鼠、猕猴、狨猴运动皮层数据集（GSE229169）。
- COVID-19：PBMC 数据集（含 mild/severe/convalescent），scRNA-seq 与 scATAC-seq 非配对。

**规模**：未提供具体细胞数/peak 数（原文未在摘要中给出）。

**基线**：scBasset（序列-only）、Seurat、LS_Lab、MultiVI。

**评测协议**：三种测试任务（cross-region / cross-cell / cross-both），指标 AUROC/AUPRC（overall/per-cell/per-peak），NS/LS（k=10,50,100），ARI/AMI/ASW。

| 实验 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|---|---|---|---|---|---|---|
| 三任务基准测试 | XChrom 在 cross-region / cross-cell / cross-both 均有效 | 与 scBasset、Seurat、LS_Lab、MultiVI 对比 | XChrom 在 cross-cell 和 cross-both 显著优于所有基线；cross-region 与 scBasset 相当 | 序列+细胞身份联合建模优于单一模态方法 | 未提供具体数值，无法判断效应量 | Results 图 2b-d |
| 去噪/细胞状态保真度 | XChrom 去噪后数据保留细胞身份 | NS/LS 对比 scBasset 和 raw 数据 | XChrom 在多个 k 值下 NS/LS 最高 | 预测数据具有高细胞状态保真度 | 未提供统计显著性检验细节 | Results 图 3b |
| 跨样本预测 | XChrom 可预测新样本（同组织） | BMMC 5 样本交叉验证，需 Harmony 批次校正 | 批次校正后性能显著提升，优于基线 | 批次校正是跨样本应用的必要预处理 | 未测试无校正时的极限 | Results 图 5a, S10 |
| 跨物种预测 | XChrom 捕捉进化保守调控规则 | 人类/小鼠模型 → 猕猴/狨猴 | 跨物种预测性能良好 | 模型学到保守的序列-调控关系 | 未与物种特异模型对比 | Results 图 6a-c |
| B 细胞比例消融 | 训练集中细胞类型比例影响泛化 | 0%, 1%, 3.7%, 7.3% B 细胞 | 比例越低，B 细胞预测性能越差；但少量比例即可恢复 | 模型需要一定量的细胞类型代表 | 未测试其他细胞类型 | Results 图 4c,d |
| COVID-19 应用 | XChrom 可预测疾病相关新细胞状态 | 训练于健康 PBMC10k，预测 COVID-19 PBMC | 成功预测 novel monocyte 亚群（HLA-DRloS100Ahi）的 TF 活性，与 scATAC-seq 验证一致 | 模型可外推到疾病状态 | 未做前瞻性验证 | Results 图 7 |
| 模块消融 | 序列模块负责 cross-region，细胞模块负责 cross-cell | 替换序列为索引 / 细胞为索引 / 简化 CNN | 细胞索引大幅降低 cross-cell；简化 CNN 降低 cross-region | 两模块功能分离 | 未测试两模块同时移除 | Results 图 4a,b |

## 11 结论正确解读

- **任务范围**：XChrom 预测的是**二值染色质可及性**（开放/不开放），而非可及性程度（连续计数）或三维结构。其输出是 peak × cell 的概率矩阵。
- **输入依赖**：推理时需要该细胞的 scRNA-seq 数据（或至少 PCA 嵌入）。若完全没有 RNA 数据，则无法利用细胞通道——此时退化为类似 scBasset 的序列-only 模型。
- **端到端状态**：模型是端到端训练的（序列+细胞嵌入 → 可及性），但细胞嵌入本身来自外部 scRNA-seq 流程（PCA），并非端到端学习。
- **跨样本/跨物种的前提**：跨样本需要批次校正（Harmony 等）；跨物种需要序列比对到参考基因组，且性能在远缘物种（如人类→小鼠）可能下降。
- **细胞类型外推的边界**：当某细胞类型在训练集中完全缺失时（如 B 细胞 0% 条件），模型无法正确重建该细胞类型的可及性谱——需要至少少量代表。
- **不确定性**：论文未报告预测概率的校准性或不确定性估计；AUROC/AUPRC 的置信区间仅在部分比较中提及。
- **生物学解释**：模型可解释性限于 TF motif 活性推断（通过插入/扰动），不提供因果机制。
- **有边界的复述**：XChrom 在「有配对 RNA-ATAC 训练数据、目标细胞有 RNA 嵌入、目标基因组区域可比对到参考基因组」的条件下，能同时预测未见区域和未见细胞的染色质可及性，并在同组织新样本（经批次校正）和跨物种（保守调控）场景下保持可用性；其预测的 TF 活性在 COVID-19 单核细胞中与独立 ATAC 数据一致。

## 12 作者自认局限

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|---|---|---|---|
| 未显式建模基因组变异 | 模型不包含 SNP/CNV 等样本间序列差异信息 | 未来可引入序列变异作为输入 | Discussion 第 1 段（"does not explicitly account for genomic variation between samples"） |
| 细胞身份与序列嵌入的独立性假设 | peak 和 cell 嵌入被假设为独立，可能忽略二者的耦合 | 未来可建模 peak-cell 交互的依赖关系 | Discussion 第 2 段（"there may be a coupling between these two embeddings"） |
| 无法直接构建完整 GRN | 模型识别 TF 活性，但不捕获 TF-靶基因关系 | 未来可结合 GRN 推断方法 | Discussion 第 3 段（"does not directly capture the relationships between these TFs and their target genes"） |
| 跨样本需批次校正 | 未校正时性能下降 | 未来可开发内置批次校正机制 | Results "XChrom can Predict New Samples..." 节 |

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|---|---|---|---|---|
| 矩阵乘法融合的「乘法交互」解释缺乏直接验证 | 模型性能提升可能来自参数增加而非乘法交互本身；未与拼接+全连接基线对比 | 若乘法非关键，则核心创新点被削弱 | 增加「拼接融合」和「加法融合」消融实验 | Results 图 4 仅对比了替换序列/细胞输入的变体，未对比融合方式 |
| 跨物种性能可能受序列保守性混淆 | 跨物种预测好可能因为测试区域本身序列保守，而非模型学到「调控规则」 | 需区分「序列相似性」与「调控逻辑保守」 | 控制序列同一性后重新评估；或在低保守但功能同源的区域测试 | Results 图 6 未报告序列保守性分层分析 |
| COVID-19 应用缺乏定量验证 | TF 活性差异未与独立 ChIP-seq 或扰动实验交叉验证；仅与同一数据的 ATAC 模态比较 | 若预测的 TF 活性是循环论证（从 RNA 推断），则生物学新发现有限 | 用独立 TF 靶基因集或 CRISPR 扰动验证 | Results 图 7 未提供独立验证 |
| 稀有细胞类型外推的「少量即可」结论可能依赖细胞类型 | B 细胞消融仅测试一种细胞类型；其他稀有类型（如祖细胞）可能更难以少量代表恢复 | 泛化性声明需更多细胞类型验证 | 在多种稀有细胞类型上重复消融实验 | Results 图 4c,d 仅 B 细胞 |
| 未报告训练/推理时间与显存 | 全基因组 × 全细胞预测的计算成本未知 | 影响实际可用性 | 补充 benchmark 数据 | 全文未提供 |
| 与三维基因组方向的连接缺失 | 未讨论可及性预测与 Hi-C/3D 结构预测的关系 | 对三维基因组领域读者，迁移价值需自行推断 | 在讨论中增加与 3D 基因组模型的对比 | Discussion 未提及 3D 基因组 |

## 14 学到什么

> Agent 提炼的知识候选

1. **乘法融合架构（可迁移）**：将「序列特征 × 细胞状态」的矩阵乘法融合作为条件预测框架，可直接迁移至三维基因组任务——例如「序列特征 × 细胞类型嵌入 → Hi-C 接触概率」或「CTCF/ cohesin 基序特征 × 细胞状态 → 环域（loop）概率」。
2. **三任务评估范式（可迁移）**：cross-region / cross-cell / cross-both 的划分方式适用于任何「特征 × 条件」预测模型，可用于评估 3D 基因组模型对未见基因组区域和未见细胞类型的泛化能力。
3. **细胞身份嵌入的替代来源**：本文使用 scRNA-seq PCA 嵌入作为细胞身份，但该框架不限于 RNA——任何细胞状态向量（如 ATAC 自身、甲基化、染色质状态）均可作为条件输入，为多模态 3D 基因组预测提供思路。
4. **去噪能力作为评估维度**：NS/LS 等细胞状态保真度指标可用于评估预测/去噪后的染色质数据是否保留生物学信号，这一评估思路可迁移至 Hi-C 数据去噪或增强。
5. **跨物种迁移的验证策略**：通过训练集与测试集跨物种划分来验证模型是否学到保守调控规则，该策略可用于评估 3D 基因组模型在非模式物种上的可迁移性。
6. **TF motif 活性推断方法（可迁移）**：通过 motif 插入 + 预测差异计算单细胞 TF 活性，可迁移至 3D 基因组模型——例如插入/删除 CTCF motif 预测对接触域边界的影响。
7. **批次校正作为预处理**：跨样本预测需先做 RNA 嵌入的批次校正，提示 3D 基因组跨样本预测同样需要类似的嵌入对齐步骤。

## 15 与已有知识连接

- **scBasset [9]**：XChrom 的序列编码器直接继承 scBasset 的 CNN 架构，可视为 scBasset 的多模态扩展。外部核验：scBasset 为 Calico 实验室开源工具，发表于 Nature Machine Intelligence（2021）。
- **Seurat [5] / LS_Lab [6] / MultiVI [7]**：均为 RNA-ATAC 跨模态映射方法，XChrom 在 cross-cell 任务中作为基线。外部核验：Seurat v4 为 Satija 实验室广泛使用的单细胞分析工具；MultiVI 为 scvi-tools 生态的 multimodal VAE。
- **Enformer / Basenji 系列**：序列-功能预测的经典框架，XChrom 的序列模块属于同一范式，但增加了细胞条件通道。
- **3D 基因组方向的连接点**：
  - **Akita / DeepC / C.Origami**：序列 → Hi-C 接触图预测模型，与 XChrom 共享「序列编码器」思路，但缺少细胞条件通道——XChrom 的「细胞嵌入 × 序列嵌入」融合方式可视为其条件扩展。
  - **单细胞 Hi-C 预测**：当前缺乏从 RNA 推断单细胞 3D 基因组的模型，XChrom 的框架提供了「RNA 嵌入 → 染色质状态」的现成通道。
  - **调控规则保守性**：XChrom 跨物种实验与 3D 基因组领域「CTCF/cohesin 环路进化保守性」研究呼应，其方法可用于跨物种 3D 结构预测。
- **COVID-19 表观调控**：作者发现的 monocyte 亚群 TF 活性变化与已报道的 COVID-19 髓系细胞炎症程序一致（外部核验：Schulte-Schrepping et al., Cell 2020 等），支持模型输出的生物学合理性。

## 16 研究想法

> Agent 生成的研究候选

**候选 1：XChrom-3D——将乘法融合框架扩展至单细胞 Hi-C 接触图预测**
- **来源局限/观察**：XChrom 证明「序列 × 细胞嵌入」可预测染色质可及性；3D 基因组领域缺乏从 RNA 推断单细胞 Hi-C 的模型。
- **核心假设**：染色质三维结构同样由「顺式序列特征 × 反式细胞状态」决定，乘法融合可捕捉这种交互。
- **初步方法**：将 XChrom 的序列编码器替换为 Akita 风格的 CNN，输出改为接触图（bin × bin）；细胞嵌入通道保留，融合层改为「接触图特征 × 细胞嵌入」的条件调制。
- **验证方式**：在 paired scRNA + scHi-C 数据上评估 cross-cell 泛化；与 Akita（无条件）对比。
- **创新状态**：unverified

**候选 2：稀有细胞类型的外推边界系统评估**
- **来源局限/观察**：XChrom 仅测试了 B 细胞一种稀有类型；「少量代表即可恢复」的结论可能不普适。
- **核心假设**：不同细胞类型的外推难度与其转录组独特性（距其他类型的距离）相关。
- **初步方法**：在多种细胞类型上重复 B 细胞消融实验，计算外推性能与细胞类型转录组距离/熵的关联。
- **验证方式**：回归分析外推 AUROC ~ 细胞类型独特性指标。
- **创新状态**：unverified

**候选 3：TF motif 活性推断用于 3D 基因组环路注释**
- **来源局限/观察**：XChrom 的 motif 插入方法可推断单细胞 TF 活性；3D 基因组中 TF 对 loop/domain 的贡献缺乏单细胞分辨率注释。
- **核心假设**：XChrom 推断的 TF 活性可预测细胞类型特异的 TAD/loop 变化。
- **初步方法**：在 paired scRNA + scATAC + Hi-C 数据上，将 XChrom TF 活性与 Hi-C 差异区域关联；用 CTCF/cohesin motif 插入预测 loop 强度变化。
- **验证方式**：与 ChIP-seq 验证的 TF 结合位点比较；与已知 loop 数据库（如 HiChIP）交叉验证。
- **创新状态**：unverified

**候选 4：跨物种 3D 基因组预测的保守性分析**
- **来源局限/观察**：XChrom 跨物种预测成功提示保守调控规则；3D 基因组跨物种预测尚未系统评估。
- **核心假设**：训练于人类 Hi-C 的模型可预测小鼠/猕猴的 TAD/loop，且性能与序列保守性相关。
- **初步方法**：用 XChrom-3D（候选 1）在人类数据训练，测试于小鼠/猕猴/狨猴；分层分析序列保守性对预测性能的影响。
- **验证方式**：与物种内训练的模型对比；分析保守 loop 的序列特征。
- **创新状态**：unverified

**候选 5：XChrom 框架用于非编码变异对染色质可及性影响的预测**
- **来源局限/观察**：XChrom 未建模 SNP/CNV，但序列通道天然支持变异输入。
- **核心假设**：XChrom 可预测 SNP 对可及性的影响（等位基因特异可及性），且优于现有方法（如 deltaSVM）。
- **初步方法**：对 eQTL/GWAS 位点做等位基因替换，比较预测可及性差异；在 matched SNP-ATAC 数据上验证。
- **验证方式**：与实验测定的等位基因特异可及性（如 dsQTL）比较 AUROC。
- **创新状态**：unverified