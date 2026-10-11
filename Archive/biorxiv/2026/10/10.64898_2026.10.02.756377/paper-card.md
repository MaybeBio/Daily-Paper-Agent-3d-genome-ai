## 01 基本信息

- **标题**：Cerberus: bidirectional state space blocks improve accuracy and efficiency of regulatory sequence models
- **作者**：Kelley DR; Yuan H; Huang X; Linder J
- **单位**：未提供
- **期刊/平台**：bioRxiv（预印本）
- **年份**：2026-10-09
- **论文类型**：预印本（方法学 + 基准评测）
- **领域**：调控基因组学 / 序列-功能预测 / 深度学习架构
- **关键词**：state space models, Mamba-2, regulatory genomics, variant effect prediction, Borzoi, Cerberus
- **DOI/arXiv**：10.64898/2026.10.02.756377
- **代码**：作者声明发布模型、训练数据、训练与评估代码、基准集（具体链接未提供）
- **数据**：GTEx v11 fine-mapped eQTL/sQTL/paQTL；augmented track collection（具体构成未提供）
- **阅读日期**：未提供
- **在课题方向中的位置**：本文属于「序列-功能预测 × 深度学习架构」方向，核心贡献是用双向状态空间模型（Mamba-2）替代 transformer 自注意力，在长序列调控建模中同时提升效率与精度。对三维基因组/染色质组织 × AI 方向而言，其可迁移点在于：长程相互作用建模的线性复杂度架构、多尺度交互范围的可解释性分析（block depth vs. interaction range）、以及变异效应预测的基准评测协议。

---

## 02 一句话总结

本文用基于 Mamba-2 的双向状态空间块（Hydra）替换 Borzoi 的 transformer 块，在保持训练数据与其余架构不变的前提下，以 5.7 倍更快的速度、32 bp 分辨率（去掉 U-net decoder）获得更准确的调控活性预测与 eQTL 分类，并扩展为 786 kb 输入的八模型集成 Cerberus，在 GTEx v11 三类 QTL 基准上优于 Borzoi。

---

## 03 研究问题

- **具体问题**：在参考基因组提供的唯一训练序列有限、新实验只增加标签不增加序列的条件下，如何设计序列-功能模型的架构，使其从有限的序列多样性中学到更多、更准的调控规则？
- **为什么重要**：长程调控相互作用（enhancer-promoter、CTCF 边界等）对基因表达预测和变异效应解释至关重要；现有 SOTA 模型（Borzoi）依赖 self-attention，其计算成本随序列长度二次增长，限制了分辨率和可处理的输入长度。
- **现有方法为何不足**：transformer 的 self-attention 在长序列上计算昂贵，迫使 Borzoi 使用较低分辨率（如 128 bp）和 U-net decoder 来折中；这限制了模型对精细调控元件的分辨能力，也限制了从有限序列中提取信息的效率。
- **精确研究问题**：Can a bidirectional state space block (Mamba-2-based) replace transformer blocks in a regulatory sequence model to improve both accuracy and efficiency on held-out sequence prediction and variant effect classification, while enabling higher input resolution?

---

## 04 背景与发展脉络

> 注：以下脉络基于本文框架，未经外部系统核验。

| 阶段 | 代表方法 | 优点 | 局限 | 本文位置 |
|------|----------|------|------|----------|
| 第一代：卷积模型 | DeepSEA, Basenji | 可处理局部 motif；计算高效 | 感受野有限，难以捕捉长程调控 | 本文保留卷积前端作为局部特征提取 |
| 第二代：transformer 长程模型 | Enformer, Borzoi | self-attention 可建模长程交互；borzoi 在变异效应预测上 SOTA | 二次复杂度限制分辨率与输入长度；训练数据有限时参数效率低 | 本文用 SSM 替代 transformer 作为长程块 |
| 第三代：状态空间模型 | Mamba, Mamba-2 | 线性复杂度；选择性扫描可建模长程依赖 | 单向扫描可能遗漏双向上下文 | 本文提出 Hydra（双向 SSM 块），在调控序列上验证优于 transformer |
| 集成与扩展 | AlphaGenome 等 | 更大模型、更多数据 | 计算成本高；未必在有限数据下最优 | Cerberus 在 786 kb 输入上集成 8 模型，在 QTL 基准上部分超越 AlphaGenome |

---

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|------|------|----------------|----------|
| 训练序列有限 | 参考基因组提供唯一序列集合；新实验只加标签不加序列 | 基因组序列是固定的，无法像 NLP/CV 那样无限扩充数据 | 引言部分（未提供具体节号） |
| Transformer 计算成本高 | 长序列上 self-attention 二次复杂度；Borzoi 被迫用低分辨率（128 bp） | 自注意力对每对 token 计算交互，长度平方增长 | 作者在引言/方法中对比 Hydra 与 transformer 速度（5.7× faster on 8,192 tokens） |
| 分辨率受限 | 低分辨率（如 128 bp）无法分辨精细调控元件 | 计算预算限制下需在分辨率与输入长度间取舍 | 作者用 32 bp 分辨率运行 Hydra 块并去掉 U-net decoder |
| 有限数据下参数效率低 | transformer 在大规模预训练数据上表现好，但在基因组有限数据下可能过拟合或欠拟合 | 自注意力参数多，需要更多数据拟合 | 作者在固定训练数据下对比 Hydra 与 transformer 块，Hydra 更优 |

---

## 06 核心思想

**1) 表面方法**：将 Borzoi 的 transformer 块替换为 Hydra——一种基于 Mamba-2 的双向状态空间块；在固定其余架构与训练数据的条件下对比；随后将 Hydra 模型扩展到 32 bp 分辨率、去掉 U-net decoder，并集成 8 个模型形成 Cerberus。

**2) 核心洞察**：双向状态空间模型（SSM）在线性复杂度下能有效建模长程依赖，且其选择性扫描机制天然适合调控基因组学中「少数关键远距离元件决定表达」的稀疏交互模式。双向性弥补了单向 Mamba 的上下文缺失，使模型在有限数据下比 transformer 更高效地利用序列信息。

**3) 可能的普适教训 [Analysis]**：在数据量有限但序列长度极长的领域（如三维基因组中 Hi-C 接触图预测、enhancer-promoter 交互预测），二次复杂度的注意力机制可能不是最优选择；线性复杂度的 SSM 架构配合双向扫描，可能在精度与效率上同时超越 transformer。此外，「固定数据与其余架构、只换核心块」的消融对比设计，是评估架构贡献的干净范式。

---

## 07 方法总览

- **输入**：DNA 序列（Cerberus 为 786 kb 输入窗口；Hydra 对比实验为 8,192 token 输入）
- **输出**：binned coverage 预测（调控活性）；变异效应预测（eQTL/sQTL/paQTL 分类与效应量估计）
- **模块**：
  1. 卷积前端（保留 Borzoi 设计）：局部 motif 特征提取
  2. Hydra 块（替代 transformer）：双向 Mamba-2 状态空间块，线性复杂度
  3. 输出头：binned coverage 预测头（去掉 U-net decoder，直接以 32 bp 分辨率输出）
  4. 集成：8 个模型组成 Cerberus 集成
- **训练**：在 augmented track collection 上训练（具体构成未提供）；对比实验固定训练数据与其余架构
- **工具/框架**：未提供（推测为 PyTorch 生态，但未在材料中说明）
- **假设**：双向 SSM 能比 self-attention 更高效地从有限序列中学习长程调控规则；32 bp 分辨率比 128 bp 提供更多精细信息
- **文字流程**：DNA 序列 → 卷积前端提取局部特征 → Hydra 双向 SSM 块逐层处理（交互范围随层深增加）→ 直接输出 32 bp 分辨率 binned coverage → 对变异进行 in silico 突变扫描 → 预测调控活性变化 → 用于 QTL 分类与效应量估计

---

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|------|------|----------|----------|----------|------------------------|
| 卷积前端 | 提取局部序列 motif 特征 | 为 SSM 提供有意义的局部表示；保留 Borzoi 已验证的设计 | 输入：one-hot DNA；输出：局部特征图 | 作者保留 Borzoi 前端设计（未提供单独消融） | 预期：局部 motif 检测能力下降 [Analysis] |
| Hydra 双向 SSM 块 | 建模长程序列依赖；双向扫描捕捉上下游上下文 | 替代 transformer 以降低计算复杂度并提升有限数据下的精度 | 输入：卷积特征；输出：上下文增强的特征 | 对比实验：Hydra 块 vs. transformer 块，固定其余架构与数据，Hydra 更优（5.7× faster, 更高 eQTL AUPRC） | 实测：替换回 transformer 会降低精度与速度 |
| 32 bp 分辨率输出（去 U-net） | 直接输出高分辨率 binned coverage | 更高分辨率可分辨精细调控元件；SSM 线性复杂度使高分辨率可行 | 输入：Hydra 块输出；输出：32 bp coverage | 作者称去掉 U-net 后模型更小且更准（具体数值未提供） | 预期：若用 128 bp 分辨率，精细调控元件分辨能力下降 [Analysis] |
| 8 模型集成（Cerberus） | 集成多个模型提升稳健性与精度 | 单模型可能对特定变异/区域有偏；集成可平均化偏差 | 输入：786 kb 序列；输出：集成预测 | 在 GTEx 三类 QTL 基准上优于 Borzoi | 预期：减少单模型方差，提升泛化 [Analysis] |
| 变异效应预测头 | 从 coverage 预测推导变异效应 | 核心应用场景：eQTL/sQTL/paQTL 分类与效应量 | 输入：参考/变异序列的 coverage 预测；输出：效应分数 | eQTL AUPRC 0.692 vs. Borzoi 0.668；Spearman ρ 0.379 vs. 0.321 | 未提供单独消融 |

---

## 09 关键公式符号

不适用。本文为架构与基准评测论文，材料中未提供形式化数学公式（如 SSM 状态更新方程或损失函数的具体表达式）。作者仅描述 Hydra 基于 Mamba-2 的双向状态空间块，但未在提供的材料中给出具体公式。

---

## 10 实验设计与证据链

**数据集/群体**：
- 训练：augmented track collection（具体构成、规模未提供）
- 基准：GTEx v11 fine-mapped eQTL、sQTL、paQTL
- 负样本匹配：allele frequency、gene expression、phenotype-specific positional annotations

**规模**：eQTL 覆盖 48 个组织；变异距离范围包括 3–100 kb 与 <3 kb 分层

**指标**：AUPRC（eQTL 分类）、Spearman ρ（效应量估计）

**基线**：Borzoi（transformer 架构）、AlphaGenome

**评测协议**：held-out sequences 上的 binned coverage 预测；fine-mapped QTL 分类与效应量排序

| 实验 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|------|-------------|------------|------|-------------|-------------------|------|
| Hydra vs. transformer 块（固定其余架构与数据） | SSM 块在相同条件下优于 transformer | 8,192 token 输入；相同训练数据 | Hydra 5.7× faster；eQTL 分类更准 | SSM 块在效率与精度上均优于 transformer | 未提供具体 AUPRC 数值；未说明是否在所有组织上一致 | 摘要/方法（未提供节号） |
| 32 bp 分辨率 + 去 U-net | 高分辨率直接输出可行且更优 | 对比 Borzoi 的 128 bp + U-net | 模型更小、更准 | SSM 线性复杂度使高分辨率成为可能 | 未提供具体数值；未单独消融分辨率 vs. 去 U-net 的贡献 | 摘要 |
| Cerberus vs. Borzoi（GTEx eQTL） | 集成模型在 eQTL 上优于 Borzoi | 48 组织；匹配负样本 | AUPRC 0.692 vs. 0.668；Spearman ρ 0.379 vs. 0.321 | Cerberus 在 eQTL 分类与效应量上均更优 | 未提供显著性检验；未说明组织间方差 | 摘要 |
| Cerberus vs. AlphaGenome（eQTL） | 与 SOTA 大模型对比 | 分层：<3 kb、3–100 kb | 3–100 kb 区间领先；<3 kb 与编码区落后 | Cerberus 在中长距离调控变异上更强 | 短距离/编码区变异不如 AlphaGenome | 摘要 |
| Cerberus vs. Borzoi（sQTL/paQTL） | 在其他 QTL 类型上同样更优 | GTEx v11 sQTL/paQTL | 均优于 Borzoi | 架构优势跨 QTL 类型泛化 | 未提供具体数值 | 摘要 |
| 可解释性分析（block depth vs. interaction range） | 深层块捕获更长程交互 | 分析各层 Hydra 块的交互范围 | 从第 1 块 0.9 kb 中位半衰期到第 7 块 79 kb；深层锚定 promoter/enhancer/CTCF | 模型分层捕获多尺度调控；CTCF 锚定提示绝缘子/边界相关机制 | 未与三维基因组数据（如 Hi-C）直接对比 | 摘要 |

---

## 11 结论正确解读

- **任务范围**：本文结论限于调控序列建模（binned coverage 预测）与 QTL 变异效应预测（eQTL/sQTL/paQTL），不涉及三维基因组结构预测或染色质构象建模。
- **oracle/真值输入**：fine-mapped QTL 来自 GTEx v11，属于实验推导的因果变异集合；负样本匹配策略（allele frequency、gene expression、positional annotations）旨在减少混淆，但无法完全排除残余混淆。
- **端到端状态**：Cerberus 是端到端训练的序列-功能模型，但变异效应预测依赖 in silico 突变扫描（从 coverage 预测推导），属于间接预测。
- **算力成本**：未提供训练/推理的具体算力需求；仅报告 Hydra 比 transformer 快 5.7 倍（8,192 token 输入）。
- **历史数据依赖**：训练数据为 augmented track collection，具体构成未提供；无法评估数据偏差。
- **模型依赖**：结论基于 Mamba-2 双向 SSM；不保证其他 SSM 变体（如 S4、Hyena）有同样效果。
- **最难情形**：编码区与 <3 kb 变异上落后于 AlphaGenome；短距离调控变异的预测仍是短板。
- **不确定性**：未提供置信区间、显著性检验或跨组织方差分析；预印本未经同行评审。
- **有边界的复述**：在固定训练数据与其余架构的条件下，双向 SSM 块（Hydra）在 8,192 token 输入上比 transformer 快 5.7 倍且 eQTL 分类更准；扩展到 32 bp 分辨率并集成为 Cerberus 后，在 GTEx v11 三类 QTL 基准上整体优于 Borzoi，但在短距离/编码区变异上不如 AlphaGenome。

---

## 12 作者自认局限

在提供的材料（摘要）中，作者明确承认的局限如下：

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|------|----------|---------------------|------|
| 短距离/编码区变异预测不足 | Cerberus 在 <3 kb 与编码区变异上落后于 AlphaGenome | 未在摘要中明确说明 | 摘要 |
| 与 AlphaGenome 互有胜负 | eQTL 分类上互有领先，非全面超越 | 未在摘要中明确说明 | 摘要 |

**作者提及的相关约束**（非正式局限）：
- 训练数据为 augmented track collection，但摘要未说明其构成与规模，暗示数据工程是模型性能的一部分。
- 模型以 786 kb 输入运行，但未说明该长度选择的依据或对更短/更长输入的敏感性。

---

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|-----------------|----------------------|----------|----------|------|
| 对比实验「固定其余架构与数据」的公平性 | 仅替换核心块，但 Hydra 块可能隐式改变了梯度流或正则化效应；「5.7× faster」可能依赖特定序列长度（8,192 token），不代表所有长度 | 若速度优势仅在特定长度成立，则推广性受限 | 在不同输入长度（如 1k、16k、32k token）下重复速度对比；报告 FLOPs 而非仅 wall-clock | 摘要仅报告 8,192 token 下的速度 |
| 32 bp 分辨率提升的归因 | 精度提升可能来自分辨率提升、去 U-net 的架构简化、或两者交互；未单独消融 | 若仅分辨率贡献，则去 U-net 可能不是必要改动 | 设计 2×2 消融：{128 bp, 32 bp} × {with U-net, without U-net} | 摘要称「去掉 U-net 后模型更小且更准」，但未分离变量 |
| 负样本匹配的充分性 | 匹配 allele frequency、gene expression、positional annotations 可减少混淆，但 fine-mapped QTL 本身存在 LD 结构，可能仍有残余混淆 | 若负样本仍有系统偏差，AUPRC 差异可能被夸大 | 使用独立验证集（如 MPRA、CRISPR 扰动数据）交叉验证变异效应预测 | 摘要描述匹配策略但未提供验证 |
| 可解释性分析的解释力度 | 「深层锚定 CTCF」被解释为边界/绝缘子相关，但未与 Hi-C 或 3D 基因组数据直接对比 | 若 CTCF 锚定不代表真实 3D 交互，则对三维基因组课题的迁移价值有限 | 将 Cerberus 的注意力/SSM 交互权重与 Hi-C 接触图、CTCF loop 数据直接对比 | 摘要仅报告 motif 锚定，无 3D 数据验证 |
| 集成 vs. 单模型贡献 | Cerberus 是 8 模型集成；单模型 Hydra 的绝对性能未与 Borzoi 单模型对比 | 若集成是主要增益来源，则架构贡献被高估 | 报告单模型 Hydra vs. 单模型 Borzoi 的对比；再报告集成增益 | 摘要仅报告 Cerberus（集成）与 Borzoi 的对比 |

---

## 14 Agent 提炼的知识候选

**标题：Agent 提炼的知识候选**

1. **线性复杂度长程建模架构（SSM）**：Hydra 基于 Mamba-2 的双向状态空间块，在 8,192 token 输入上比 transformer 快 5.7 倍且精度更高。**可迁移到三维基因组**：Hi-C 接触图预测、enhancer-promoter 交互预测通常需要处理百万级 bin 的序列或矩阵，transformer 的二次复杂度是瓶颈；SSM 的线性复杂度天然适合超长序列建模。迁移路径：将 Hydra 块用于序列-接触图联合预测模型，或用于处理 1 Mb+ 的调控序列窗口。

2. **「固定其余架构与数据、只换核心块」的消融范式**：本文最干净的贡献是严格隔离了架构变量的影响。**可迁移到三维基因组**：在比较不同长程建模架构（transformer vs. SSM vs. Hyena）对 Hi-C 预测的影响时，应采用同样的消融设计，避免数据增强或 decoder 改动混淆归因。

3. **高分辨率直接输出替代 U-net decoder**：32 bp 分辨率直接输出（去掉 U-net）在更小模型下获得更高精度。**可迁移到三维基因组**：Hi-C 预测中常使用 U-net 式 decoder 从低分辨率恢复高分辨率接触图；本文证据提示，若骨干网络足够高效，直接高分辨率输出可能更优。

4. **分层交互范围分析（block depth vs. interaction range）**：从第 1 块 0.9 kb 到第 7 块 79 kb 的中位交互半衰期，且深层锚定 CTCF。**可迁移到三维基因组**：这一分析范式可直接用于检查模型是否学习到多尺度染色质组织（TAD、compartment、loop）；若模型深层交互锚定 CTCF/cohesin motif，则提示模型隐式学习了 3D 基因组结构特征。

5. **负样本匹配协议**：匹配 allele frequency、gene expression、positional annotations 的 QTL 基准设计。**可迁移到三维基因组**：在评估 3D 基因组变异效应预测（如 Hi-C 差异、TAD 边界破坏）时，应采用类似的匹配策略减少混淆。

6. **集成策略**：8 模型集成在 786 kb 输入上运行。**可迁移到三维基因组**：3D 基因组预测模型通常计算量大，集成策略需权衡；但若单模型方差大，集成可提升稳健性。

---

## 15 与已有知识连接

- **Borzoi（Kelley 2024, bioRxiv）**：本文直接基于 Borzoi 架构，替换其 transformer 块。Borzoi 是当前调控序列预测的 SOTA 之一，其 128 bp 分辨率与 U-net decoder 设计是本文的对比基线。**与三维基因组关联**：Borzoi 的预测已被用于 eQTL 与 sQTL 效应解释，但其分辨率限制了对精细调控元件的分辨。
- **Mamba / Mamba-2（Gu & Dao 2023/2024）**：状态空间模型在长序列 NLP 中已展示线性复杂度的优势。本文将其引入调控基因组学，验证了 SSM 在 DNA 序列上的有效性。**与三维基因组关联**：SSM 在 Hi-C 接触图预测中已有初步应用（如 Enformer 的替代），本文提供了更系统的验证。
- **AlphaGenome（2025, bioRxiv）**：大规模基因组模型，本文与其对比显示互有胜负。**与三维基因组关联**：AlphaGenome 类模型通常包含 3D 基因组特征（如 Hi-C）作为输入或辅助任务，本文未使用 3D 数据，但 CTCF 锚定分析提示模型隐式学习了绝缘子相关特征。
- **Enformer（Avsec 2021, Nature Methods）**：transformer 架构的调控预测先驱，本文的对比隐含了「transformer vs. SSM」的架构演进。**与三维基因组关联**：Enformer 的注意力权重已被用于分析 enhancer-promoter 交互，本文的 SSM 交互分析可类比迁移。
- **CTCF/绝缘子与 TAD 边界（外部知识）**：本文发现深层 Hydra 块锚定 CTCF motif，与三维基因组中 CTCF 定义 TAD 边界的已知机制一致。**候选方向**：将 Cerberus 的交互权重与 Hi-C 数据直接对比，验证模型是否隐式学习 3D 结构。

---

## 16 Agent 生成的研究候选

**标题：Agent 生成的研究候选**

1. **候选名称**：SSM-based Hi-C contact prediction from DNA sequence
   - **来源局限/观察**：Cerberus 的 SSM 架构在长序列上高效且准确；Hi-C 接触图预测需要处理超长序列且计算量大。
   - **核心假设**：双向 SSM 能比 transformer 更高效地从 DNA 序列预测 Hi-C 接触图，尤其在 TAD/loop 尺度。
   - **初步方法**：将 Hydra 块嵌入序列-接触图预测模型（如替代 Enformer 的注意力层），输入 1 Mb 序列，输出 Hi-C 接触图；对比 transformer 基线。
   - **验证方式**：在 GM12878 等细胞系的 Hi-C 数据上评估接触图预测准确率（如 Pearson/Spearman 相关），并分析各层交互范围与 TAD 边界的一致性。
   - **创新状态**：unverified

2. **候选名称**：Cross-species transfer learning for 3D genome structure prediction
   - **来源局限/观察**：Cerberus 支持 transfer learning；三维基因组数据在非模式物种中稀缺。
   - **核心假设**：在人类上预训练的 SSM 调控模型可迁移到小鼠等物种的 3D 结构预测，且比从头训练更高效。
   - **初步方法**：用 Cerberus 的预训练权重初始化，微调于小鼠 Hi-C 数据；对比随机初始化。
   - **验证方式**：评估小鼠 Hi-C 接触图预测准确率，并检查 CTCF 锚定是否跨物种保持。
   - **创新状态**：unverified

3. **候选名称**：Interaction range analysis as a diagnostic for 3D structure learning
   - **来源局限/观察**：Cerberus 的分层交互范围分析（0.9 kb → 79 kb）揭示了多尺度学习；三维基因组模型缺乏类似的诊断工具。
   - **核心假设**：通过分析模型各层的交互半衰期，可以判断模型是否学习到 TAD/compartment 等多尺度结构。
   - **初步方法**：对任意序列-结构预测模型，提取各层交互权重，计算中位交互距离；与 Hi-C 数据的 TAD 尺度对比。
   - **验证方式**：在多个模型（transformer, SSM, CNN）上运行该诊断，比较其与 Hi-C 结构尺度的对齐程度。
   - **创新状态**：unverified

4. **候选名称**：Variant effect prediction for 3D structure-disrupting mutations
   - **来源局限/观察**：Cerberus 在 QTL 变异效应预测上优于 Borzoi，但未涉及 3D 结构破坏变异（如 TAD 边界破坏）。
   - **核心假设**：Cerberus 的变异效应预测可扩展到 3D 结构相关变异（如 CTCF motif 破坏），且比 Borzoi 更准。
   - **初步方法**：构建包含已知 TAD 边界破坏变异的基准集，用 Cerberus 与 Borzoi 分别预测效应，对比准确率。
   - **验证方式**：与实验验证的 3D 结构变异（如 Hi-C 验证的 TAD 融合）对比。
   - **创新状态**：unverified

5. **候选名称**：Bidirectional SSM for enhancer-promoter loop prediction
   - **来源局限/观察**：Cerberus 的双向设计捕获上下游上下文；enhancer-promoter 交互本质上是双向的。
   - **核心假设**：双向 SSM 比单向模型或 transformer 更擅长预测 enhancer-promoter 交互方向与强度。
   - **初步方法**：在 enhancer-promoter 交互数据集（如 ABC model 输出）上微调 Cerberus，输出交互概率。
   - **验证方式**：与 CRISPR 验证的 enhancer-promoter 对对比，评估 AUPRC。
   - **创新状态**：unverified