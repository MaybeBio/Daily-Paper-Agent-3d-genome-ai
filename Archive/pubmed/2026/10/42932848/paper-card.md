## 01 基本信息
- 标题：EpiInsula: calibrated regression of the Hi-C insulation score from cell-type-specific epigenomic signal
- 作者与单位：Jin, Yuyu; Chen, Tong; Gao, Jie; Tong, Mengyao; Xu, Guangcheng; Zhang, Xueyu; Liu, Weixu; Shen, Yin（具体单位未在提供材料中列出；资助信息含 Anhui Medical University，暗示单位归属，但未提供明确 affiliation 列表）
- 期刊/预印本平台：Briefings in Bioinformatics
- 年份：2026-10-26（日期字段）
- 论文类型：方法学论文（方法开发 + 基准比较 + 消融/迁移分析）
- 领域：三维基因组 / 染色质组织预测；表观基因组信号 → 连续绝缘分数回归
- 关键词：未提供（正文未列关键词列表）
- DOI/arXiv 号：10.1093/bib/bbag589
- 代码：https://github.com/Yin-Shen/EpiInsula
- 数据：ENCODE（20/24 表观输入 track）、4D Nucleome（4 个 H1-hESC track、insulation targets、Hi-C 矩阵、参考 boundary calls）、GEO GSE225201（GM12878 Micro-C，仅描述性比较，非模型输入）；逐文件 accession 见 Supplementary Table S1
- 阅读日期：未提供
- 在「三维基因组/染色质组织 × AI 方法/物理模拟」方向中的位置：属于「一维表观信号 → 三维染色质组织」的 AI 预测分支，但把预测目标从 boundary classification 改为连续 insulation score 的 calibrated regression，并强调 chromosome-disjoint 评测与 cell-type-specific 对比端点。与 C.Origami / ChromNet / Epiphany / Akita / Orca 等 contact-map 或 boundary 预测方法构成同一问题域的不同输出形式。

## 02 一句话总结
把染色质组织预测从 boundary 二分类改为对 10-kb Hi-C insulation score 的连续回归，用 ±700-kb 窗口内六条 cell-type-specific 表观 track 经 dilated residual CNN 预测，在 chromosome-disjoint 划分下四株细胞系 held-out 相关 0.774–0.860、measured-on-predicted 回归斜率 0.90–0.95，并在 cell-type-specific boundary 对比端点上优于七个同契约方法与三个重训 contact-map 预测器。

## 03 研究问题
- 具体问题：能否从常规可得的 cell-type-specific 表观基因组信号，连续、可校准地预测 10-kb 分辨率的 Hi-C insulation score，而不是只预测 boundary 位置？
- 为什么重要：insulation 决定 enhancer–promoter 可达性，boundary 破坏与肢体畸形、glioma 与 T-ALL 的致癌基因激活相关；10-kb 分辨率 Hi-C 需深度测序，成本随 bin 数平方增长，无法覆盖大量细胞类型。
- 现有方法为何不足：(1) 大量工作把问题表述为 boundary classification，丢弃 insulation profile 的深度与形状；(2) 各研究 boundary label 定义不同，accuracy 不可比；(3) 参考 domain 随 caller、分辨率、normalisation 变化；(4) 域景观在细胞类型间高度保守，pooled accuracy 被共享成分主导，方法可在细胞类型真正不同的位点贡献很小。
- 精确研究问题（Can ... ?）：Can a model predict the continuous 10-kb insulation score, calibrated in the conditional-mean sense, from cell-type-specific epigenomic tracks such that it also recovers the loci where two cell types differ?

## 04 背景与发展脉络
（脉络为「仅本文框架」——本文 Introduction 自述的谱系，未经外部核验）
- 阶段 1：3C 及其衍生（4C、5C、ChIA-PET）→ Hi-C → Micro-C，确立 TAD 与 boundary 概念，boundary 约束 enhancer–promoter 通讯。
- 阶段 2：insulation score 作为连续量（sliding square window 沿对角线求和），boundary 定义为局部极小。
- 阶段 3：机制侧——cohesin loop extrusion 在 convergent CTCF 处停滞解释 boundary 位置与方向；CTCF 降解去除局部 insulation 而保留 compartment。
- 阶段 4：从一维信号预测组织——preciseTAD（transfer learning，bp 分辨率 boundary 预测）、Epiphany（adversarial，从表观 track 预测 contact map）、C.Origami（sequence + cell-type signal）、ChromNet（multi-task，跨细胞类型）。
- 阶段 5：从 sequence 单独预测——Akita、Orca、DeepC；dilated convolution 用于远端信号（sequential regulatory-activity prediction），后续用 self-attention 覆盖更长范围。
- 本文主张的位置：不主张架构新颖（明确声明 assembled from established components），主张在 target（连续 calibrated regression）、evaluation design（chromosome-disjoint + 单一契约 + cell-type-specific 端点）与 fitted model 刻画上的贡献。

## 05 核心痛点
| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|---|---|---|---|
| boundary classification 丢弃 profile 深度与形状 | 只保留极小位置，不保留 insulation 深度 | 作者主张：该表述本身丢弃信息 | Introduction；Discussion 首段 |
| 方法间不可比 | 各研究 boundary label 定义不同，reported accuracy 依赖 target 定义与评测数据 | 作者主张：label 定义与评测数据不一致 | Introduction |
| 参考 domain 不稳定 | 随 caller、分辨率、normalisation 变化 | 作者主张 | Introduction（引 [37,38]） |
| pooled accuracy 被保守成分主导 | 域景观跨细胞类型保守，方法可在细胞类型差异位点贡献很小 | 作者主张 | Introduction；Results「Predicted profiles recover boundaries differing between IMR-90 and K562」 |
| 10-kb Hi-C 测序成本高 | 互作空间随 bin 数平方增长，测序需求超线性上升 | 作者主张 | Introduction（引 [17–19]） |
| 预测深度被压缩 | 最深 1% measured insulation 的预测深度仅为实测的 52.7%–71.0% | 作者以 reverse-regression slope 0.64–0.81 与 depth recovery 量化 | Results「Held-out prediction accuracy and calibration」；Supplementary Table S9 |

## 06 核心思想
1) 表面方法：用 1D dilated residual CNN，输入 6×1400（1-kb bin，±700 kb），输出单个 10-kb bin 的 insulation score；每株细胞系单独拟合，细胞特异性由输入 track 承载。
2) 核心洞察：把预测目标从「boundary 是不是在这里」换成「insulation 有多深」，使输出可作为一个连续 profile 分析；并用 chromosome-disjoint 划分 + 单一评测契约 + 只在细胞类型分歧处定义的端点，把「共享景观」与「细胞类型特异组织」分开评估。
3) 可能的普适教训 [Analysis]：当预测目标存在一个连续 underlying quantity 时，直接回归该量可能比回归其离散派生标签保留更多信息，且更易跨研究比较；评测端点应显式区分「保守成分」与「分歧成分」，否则 pooled 指标会掩盖方法差异。

## 07 方法总览
- 输入：6 条 cell-type-specific processed signal tracks（ATAC-seq、CTCF、RAD21、H3K4me1、H3K4me3、H3K27ac），1-kb bin，±700 kb 窗口 → 6×1400 矩阵。不使用 sequence-derived channel。
- 输出：该 locus 中心 10-kb bin 的 insulation score（连续标量，log2 归一化尺度）。
- 模块：width-7 stem（6→128）→ 8 个 residual block（width-3 conv，dilation 1–128，BN，GELU，pointwise conv，dropout，identity skip）→ read-out（中心位置特征 + 窗口全局均值）→ 两层 MLP → 单标量。583 681 可训练参数。
- 训练：loss = smooth L1 on standardised target + 0.3 × (1 − batch Pearson correlation)，β=1；AdamW，2-epoch warm-up + cosine decay，60-epoch budget，early stopping on validation correlation；每细胞系每 fold 三个 seed（42/13/99），共 60 个主模型。
- 工具：cooltools 生成 4D Nucleome insulation track；block bootstrap（2000 draws）做不确定性；Benjamini–Hochberg 校正。
- 反馈回路：无在线反馈；但有 inference-time 探针（gradient×input 空间归因、CTCF/RAD21 dose response、additivity）与 retrained ablation（240 次拟合）。
- 假设：insulation 由局部表观信号在 ±700 kb 内决定；细胞特异性由输入 track 承载而非模型参数；chromosome-disjoint 划分足以阻断近邻相关 locus 的泄漏。
- 文字流程：ENCODE/4D Nucleome track → 1-kb binning → 每 fold 在训练染色体上拟合 robust scaling + target standardisation → asinh 变换 + clip ±30 → 6×1400 输入 → dilated residual CNN → 中心+全局 read-out → 标量 → 反标准化 → 与 measured insulation 比较（Pearson、OLS slope/intercept、reverse regression、depth recovery、boundary F1、fine-scale 分量、cell-type-specific 对比恢复率）。

## 08 核心模块拆解
| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|---|---|---|---|---|---|
| Dilated residual CNN backbone（8 blocks，dilation 1–128） | 在参数不随范围增长的前提下覆盖远端信号 | 远端表观信号影响中心 insulation | 6×1400 → 128×1400 特征 | Methods「Network architecture」；Supplementary Table S4 | 未做 backbone 消融；预期感受野不足会降低远端依赖的预测（预期效应，未实测） |
| Centre + global read-out | 组合中心位置特征与窗口全局均值 | 中心位置决定目标 bin，全局上下文提供背景 | 特征 → 单标量 | Methods「Network architecture」 | 未单独消融（预期效应） |
| Correlation loss term（weight 0.3） | 使 batch 内预测与 target 的 Pearson 相关进入目标 | 直接优化排序/形状而非仅逐点误差 | 预测与 target → 标量惩罚 | Results「A classification twin and the correlation-term control」；Supplementary Table S11 | 实测：置 0 后所有量变化 ≤0.004，per-seed 范围重叠，回归目标对分类目标的领先保持 |
| 连续回归目标（vs 分类 twin） | 预测 insulation 深度而非 boundary 标签 | 保留 profile 深度与形状 | 同输入 → 连续值 vs logit | Results「A classification twin...」；Supplementary Table S11 | 实测：分类 twin boundary F1 0.506/0.404/0.508/0.471 vs 回归 0.594/0.500/0.597/0.540；AP 0.492/0.371/0.496/0.463 vs 0.596/0.504/0.614/0.537 |
| 输入组消融（去 CTCF / RAD21 / ATAC / 三条 histone） | 刻画预测对哪些 track 依赖 | 判断信号来源 | 重训 240 次拟合 | Results「Input ablation...」；Supplementary Table S13 | 实测：16 个 cell-line×condition 比较中 15 个未校正 200-bin bootstrap 区间排除零；最大变化为 H1-hESC 去三条 histone 与去 RAD21；IMR-90 去 CTCF 近零 |
| 跨细胞类型迁移（zero-shot / label-free BN / fine-tune） | 评估无 target label 与低 label 预算下的可用性 | 扩展到无 contact map 的细胞类型 | source checkpoint → target 输入 | Results「Fine-tuning enables cross-cell-line transfer...」；Supplementary Table S8 | 实测：zero-shot 均值 0.561 vs within-cell 0.801；label-free BN 0.594；1% target loci fine-tune 达 within-cell 的 93.2%–97.7% |

## 09 关键公式符号
- Insulation score 定义：S(i, w) = 第 i 个 bin、半窗 w 下，w 个上游 bin 与 w 个下游 bin 之间的 mean balanced contact frequency；报告值为 S 除以对应染色体臂 mappable 区域中位数后做 base-2 log 变换。用途：定义预测目标；直觉：接近 0 表示典型跨 bin 接触，越负表示绝缘越强。来源：Methods「Insulation score as the prediction target」。
- 校准回归：y = a·ŷ + b（OLS of measured y on predicted ŷ）。符号：y 实测 insulation，ŷ 预测。用途：校准判据——conditional mean 校准成立时 a=1、b=0。直觉：斜率近 1 表示「给定预测值的实测均值等于该预测值」，但不表示逐 locus 幅度被恢复。来源：Methods「Evaluation metrics, estimands, and dispersion」。
- 训练目标：smooth L1 on standardised target + 0.3 × (1 − Pearson(pred, target))，β=1。用途：逐点误差 + batch 内形状/排序。直觉：correlation 项对预测的平移与正缩放不变。来源：Methods「Training objective and optimisation settings」。
- Depth recovery：最深 1% measured insulation 值上，预测均值 / 实测均值。用途：量化最深谷的幅度恢复。来源：Methods「Evaluation metrics」；Results 报 62.5%/63.3%/71.0%/52.7%。
- Cell-type-specific 对比恢复：measured z-score < −1.5 在一株、> −0.3 在另一株定义 contrasting set；predicted z-score < −1.0 / > −0.5 判为 recovered。用途：只在细胞类型分歧处评估。来源：Methods「Boundary calling and cell-type-specific boundaries」。

## 10 实验设计与证据链
数据集/群体：四株 GRCh38 人类细胞系 H1-hESC、GM12878、IMR-90、K562；admitted autosomal loci 254 834 / 258 012 / 256 850 / 258 635（合计 1 028 331）；held-out 评测覆盖 21 条 autosome 的 973 169 loci（chromosome 8 因用于选择 half-width 被排除）。
规模：22 autosome 分 5 个 test block，各带一个 validation chromosome；每细胞系每 fold 三个 seed → 60 个主模型；ablation 240 次拟合；两个 control 各 60 次拟合。
指标：Pearson correlation（主）、OLS slope/intercept、reverse-regression slope、identity-line R²、depth recovery、boundary F1（±10 kb，另有 exact bin 与 ±20 kb 敏感性）、fine-scale component correlation、cell-type-specific contrast recovery、AUROC（Strong vs Weak 排序）。
基线：七个同契约方法（CT-TADB 改编、preciseTAD 改编、pTADS 改编、MLP、plain CNN、ridge、gradient-boosted trees）；三个重训 contact-map 预测器（Epiphany、C.Origami、ChromNet）两种设置（重训 / 释放权重直接应用）。
预算：60-epoch，early stopping；Epiphany 55-epoch budget + patience 12；C.Origami/ChromNet 80-epoch released schedule，单 GPU、per-device batch size 8（原配置四 GPU）。
骨干/仪器：1D dilated residual CNN，583 681 参数；无 GPU 型号信息。
Oracle 输入：无 oracle 输入；但 cell-type-specific 端点由 measured Hi-C 定义（非模型输入），Micro-C 仅作描述性比较且非输入/训练目标。
评测协议：chromosome-disjoint；input scaler、target standardisation、weights、early stopping 仅用训练+验证染色体；boundary prominence 在 validation chromosome 上选后冻结；block bootstrap（2000 draws，chromosome-stratified、gap-aware），方法比较合并 50/100/200-bin 结果并做 BH 校正（28 tests）。

| 实验 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|---|---|---|---|---|---|---|
| Held-out 预测 | 可从表观 track 连续预测 insulation | 四细胞系 × 5 fold × 3 seed，chromosome-disjoint | corr 0.791/0.780/0.860/0.774；seed SD ≤0.004；slope 0.95/0.95/0.91/0.90，intercept 距 0 ≤0.008 | 条件均值校准成立 | 不表示逐 locus 幅度恢复（reverse slope 0.66/0.64/0.81/0.67；depth recovery 52.7%–71.0%） | Results 图 2A–C；Supplementary Table S9 |
| 同契约方法比较 | EpiInsula 优于七个方法 | 同输入/窗口/fold/seed/held-out loci | pooled corr 0.801 vs 0.703（CT-TADB）至 0.548（ridge）；28/28 差异 bootstrap 区间排除零，校正单侧 P<0.001 | 在该契约下排名第一 | 不构成对原论文报告性能的复现或反驳 | Results 图 3A、3C |
| Boundary F1 | 连续回归在 boundary 端点也领先 | prominence 在 validation 上选后冻结 | F1 0.594/0.500/0.597/0.540 vs CT-TADB 0.571/0.457/0.522/0.462；precision 与 recall 均最高 | 连续目标不牺牲 boundary 定位 | 不表示 boundary 定义唯一或跨 caller 稳健 | Results 图 3B、3D；Supplementary Fig. S1 |
| 重训 contact-map 预测器 | 直接预测 insulation 优于从 contact map 派生 | 同 fold/seed/chromosomes，各方法原生输入与代码 | 派生 score corr：Epiphany 0.533/0.377/0.678/0.437；ChromNet 0.511/0.346/0.677/0.424；C.Origami 0.159/0.148/0.280/0.289；EpiInsula 同条件 0.803/0.792/0.877/0.821 | 该端点下直接回归更有支持 | 三方法训练目标是 contact map，此比较衡量其输出对该端点的支持，非方法优劣总评 | Results「Insulation scores derived from three retrained contact-map predictors」；Supplementary Fig. S2 |
| Fine-scale 分量 | 领先不只来自平滑成分 | 250-kb 半宽（另 100/500 kb） | fine-scale corr 0.798/0.774/0.861/0.801；28/28 差异为正，最小 0.042 [0.038, 0.046] | 细尺度信息被保留 | 不排除平滑成分仍贡献大部分方差 | Results「The lead is retained on the fine-scale component」；Supplementary Fig. S3、Table S10 |
| 分类 twin 与 correlation-term control | 连续目标优于二分类目标 | 同 fold/seed/输入/优化配方，仅改 target/loss/checkpoint 选择 | 分类 twin F1 与 AP 均更低；logit track 与 measured insulation 相关 −0.357 至 −0.469；去掉 correlation 项变化 ≤0.004 | 目标形式本身带来增益 | 不表示 correlation 项是增益来源 | Results「A classification twin...」；Supplementary Table S11 |
| Strong vs Weak 排序 | 预测深度携带 boundary 强度信息 | AUROC，predicted vs measured depth | 0.750/0.743/0.699/0.690 vs measured 0.897/0.859/0.793/0.794 | 预测 profile 有分级记录 | 排序锐度低于实测 | Results「Predicted depth orders reference boundaries by strength」；Supplementary Table S12 |
| 输入组消融 | 依赖哪些 track | 重训，16 个 cell-line×condition | 15/16 未校正区间排除零；最大为 H1-hESC 去 histone 与去 RAD21；IMR-90 去 CTCF 近零 | 预测依赖因细胞系而异 | 作者明确：track 相关，消融是条件性的；非因果生物学贡献 | Results「Input ablation...」；Supplementary Table S13 |
| 跨细胞类型迁移 | 无/低 label 下可用性 | 16 个有序 pair × 5 fold × 3 seed；label-free BN；0.5%/1%/5%/25% fine-tune | zero-shot 均值 0.561；label-free BN 0.594；1% loci fine-tune 0.737/0.750/0.840/0.750（within-cell 的 93.2%–97.7%）；随机初始化同预算 0.596/0.556/0.721/0.619 | 有 target label 时 fine-tune 有效 | 作者明确：不建立对未测细胞类型的 label-free 泛化 | Results「Fine-tuning enables...」；Supplementary Table S8 |
| Cell-type-specific 对比 | 在细胞类型分歧处是否领先 | IMR-90/K562 固定阈值 + 25 点网格 + 另 5 对细胞系 | 0.383 vs MLP 0.264、其余 0.024–0.081；25 点全部第一；另 5 对 0.343–0.435，125 点全部第一 | 支持在分歧处评估 | 作者明确：描述性聚合比较，不建立单位点生物学机制 | Results「Predicted profiles recover boundaries differing between IMR-90 and K562」；Supplementary Fig. S6、Table S14/S15 |

## 11 结论正确解读
- 任务范围：预测对象是 10-kb diamond insulation score（log2 归一化），不是 contact map 本身，也不是 boundary 标签；boundary 由预测 profile 的局部极小派生。
- Oracle/真值输入：无 oracle 输入；但 cell-type-specific 端点由 measured Hi-C 定义，Micro-C 比较中一组由模型输出部分定义，作者明确声明非独立验证。
- 端到端状态：从表观 track 到连续 score 是端到端训练的；但 boundary calling 的 prominence 需在 validation chromosome 上选择后冻结，属评测流程的一部分。
- 算力成本：未提供训练总算力、GPU 型号或 wall-clock；仅提到 C.Origami/ChromNet 用单 GPU、batch size 8（原配置四 GPU）。
- 历史数据依赖：依赖 ENCODE 与 4D Nucleome 的 processed track 与 released insulation track（cooltools 生成）；依赖 4D Nucleome 的 boundary calls 作为参考。
- 模型依赖：结论绑定于该 dilated residual CNN 与 smooth L1 + correlation 项的目标；作者声明无架构新颖性，未做 backbone 替换实验。
- 最难情形：最深谷幅度恢复不足（52.7%–71.0%）；zero-shot 跨细胞类型显著低于 within-cell（0.561 vs 0.801）；GM12878 仅 6/21 autosome 达 0.80。
- 群体/领域边界：仅四株人类细胞系（H1-hESC、GM12878、IMR-90、K562），仅 autosome，仅 GRCh38；作者指出六条 track 在原代或临床样本中可能不可得。
- 不确定性：block bootstrap 区间描述「给定观测染色体集下的 locus 级变异」，fold 级离散单独报告；cell-type-specific 端点为描述性。
- 有边界的复述：在四株人类细胞系、chromosome-disjoint 评测、六条 cell-type-specific 表观 track 与 ±700-kb 窗口的条件下，EpiInsula 能连续预测 10-kb insulation score 的条件均值（斜率 0.90–0.95），在该契约下优于七个同契约方法与三个重训 contact-map 预测器派生的 score，并在 IMR-90/K562 等细胞类型分歧位点上恢复率高于对比方法；但最深谷幅度被压缩，跨细胞类型零样本性能明显下降，且所有归因与细胞类型特异分析均为计算性、描述性，不建立调控因果。

## 12 作者自认局限
| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|---|---|---|---|
| 需要六条 cell-type-specific 表观 track | 在原代或临床样本中可能不可得 | 未明确给出方向 | Discussion 末段 |
| 固定 ±700-kb 上下文 | 可能遗漏更长程结构 | 未明确给出方向 | Discussion 末段 |
| 归因、输入缩放与细胞类型特异分析为计算性、描述性 | 不建立调控因果 | 未明确给出方向 | Discussion 末段 |
| 零样本跨细胞类型性能低于 within-cell | 0.561 vs 0.801 | 支持有 target label 时 fine-tune；不建立 label-free 泛化到未测细胞类型 | Discussion |
| 预测幅度压缩 | reverse slope 0.64–0.81；depth recovery 52.7%–71.0% | 未明确给出方向 | Results；Discussion |

作者提及的相关约束（非正式局限）：(a) 三个 contact-map 预测器为任务匹配实现而非原方法复现，比较不反映原论文报告性能；(b) 消融因输入 track 相关而是条件性的，非因果生物学贡献；(c) cell-type-specific 端点为描述性聚合比较；(d) Micro-C 比较中一组由模型输出部分定义，非独立验证；(e) 显示的 locus 为示例，非统计重复。

## 13 批判性分析
| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|---|---|---|---|---|
| 无架构消融 | 增益可能来自 dilated residual backbone 而非「连续目标」这一表述；分类 twin 只改了 target/loss/checkpoint，未改 backbone | 若增益主要来自 backbone，则「回归 vs 分类」的普适教训被高估 | 在同一 backbone 上做 target 形式的正交消融（已部分做）；再在 MLP/plain CNN backbone 上重复回归 vs 分类对照 | Methods「Comparison methods」；Results「A classification twin...」 |
| 七个对比方法中三个是「任务适配」而非原方法 | 适配可能未调优到与原方法同等程度（如 preciseTAD/pTADS 用 capped training subsamples） | 排名第一的幅度可能部分来自适配不对称 | 对适配方法做等预算超参搜索；报告 subsample 上限对结果的影响 | Methods「Comparison methods and the task-matched contract」 |
| ±700-kb half-width 由 validation correlation 在 0.001 容差内选最小 | 该选择标准偏向相关而非幅度；可能系统性限制远端依赖 | 若更长窗口能改善深度恢复，则当前窗口是幅度压缩的部分成因 | 在固定 backbone 下扫描 half-width 并同时报告 depth recovery 与 reverse slope | Methods「Input representation and signal normalisation」；Supplementary Table S3 |
| Cell-type-specific 阈值手工指定（−1.5/−0.3 与 −1.0/−0.5） | 恢复率绝对值依赖阈值；虽然做了 25 点网格，但网格是围绕手工值缩放 | 端点绝对值不宜跨研究直接比较 | 用与阈值无关的度量（如 contrasting set 上的 ranking AUROC 或连续 z-score 差的相关）重做 | Methods「Boundary calling and cell-type-specific boundaries」 |
| 参考 boundary 来自单一 4D Nucleome call set | 作者自己指出参考 domain 随 caller/分辨率/normalisation 变化，但主比较只用一套 call | F1 的绝对值可能对 call set 敏感 | 用多个 caller（如 Arrowhead、TopDom）重复 boundary F1 比较 | Introduction；Methods「Boundary calling」 |
| Zero-shot 使用了 target 自身训练染色体的 input scaler | 作者明确说明这不是 strict source-only application | 「zero-shot」标签可能被读者误读为完全无 target 信息 | 增加 strict source-only（用 source scaler）对照 | Methods「Cross-cell-type transfer and label-efficiency experiments」 |
| 输入消融为 retrain-from-scratch，未做同预算的随机特征对照 | 去掉一组 track 后性能下降可能部分来自输入维度减少而非信息丢失 | 影响「哪些 track 携带预测信息」的解读强度 | 加入等维度的随机/打乱 track 对照 | Results「Input ablation...」；Supplementary Table S13 |
| 三个 contact-map 预测器在单 fold（fold 1）上重训 | 单 fold 结果可能不具代表性；且 C.Origami 派生 score 明显偏低（0.148–0.289） | 该比较的结论强度受 fold 选择影响 | 在全部 5 fold 上重训并报告 fold 间离散 | Methods「Comparison with contact-map prediction methods」；Supplementary Fig. S2 |
| 未报告训练算力与 wall-clock | 无法评估方法在常规实验室的可复现成本 | 影响方法可及性判断 | 报告 GPU 型号、训练时长、总 GPU-hours | 全文未提供 |

## 14 学到什么
### Agent 提炼的知识候选
- 可迁移概念 1：把三维基因组预测目标从离散标签改为连续 underlying quantity（insulation score、compartment strength、contact probability 的连续形式），可保留 profile 深度与形状，并使跨研究比较有共同尺度。迁移方式：在本课题中，凡预测 boundary/loop/TAD 的任务，可同时回归其连续强度量并报告校准斜率。
- 可迁移概念 2：conditional-mean calibration 的判据是 OLS slope≈1、intercept≈0，但它与逐样本幅度恢复是两件事；必须同时报告 reverse-regression slope 与 depth recovery。迁移方式：任何从一维信号回归三维基因组连续量的工作，都应把「校准」与「幅度」分开报告。
- 可迁移概念 3：chromosome-disjoint 划分 + 单一评测契约（同输入、窗口、fold、seed、held-out loci）是把方法差异归因于模型而非评测的必要条件。迁移方式：在本课题做 benchmark 时，固定输入 track 集合与窗口，只变模型。
- 可迁移概念 4：只在细胞类型分歧处定义的端点（measured z-score 阈值 + predicted z-score 阈值 + 阈值网格）能把「共享景观」与「细胞类型特异组织」分开。迁移方式：用于评估任何声称 cell-type-specific 的三维基因组预测器。
- 可迁移方法 1：dilated residual CNN + centre-plus-global read-out，在参数不随范围增长的前提下覆盖 ±700 kb。迁移方式：作为长程表观信号编码器的轻量 baseline（583 681 参数），与 self-attention 方案对比。
- 可迁移方法 2：loss = smooth L1 + 0.3 × (1 − batch Pearson)，其中 correlation 项对平移与正缩放不变。迁移方式：用于任何需要同时优化逐点误差与 profile 形状的回归任务；但本文实测该项对结果影响 ≤0.004，说明其作用可能有限。
- 可迁移方法 3：输入组 retrained ablation（240 次拟合）+ inference-time 探针（gradient×input、dose response、additivity）的组合，用于区分「预测依赖」与「机制」。迁移方式：在本课题中报告 track 依赖时，明确标注为 predictive dependence 而非 causal contribution。
- 可迁移实验设计 1：label-efficiency 曲线（0.5%/1%/5%/25% target loci）与随机初始化同预算对照，量化预训练权重的增量（+0.119 至 +0.194）。迁移方式：评估跨细胞类型/跨物种迁移时，必须报告同预算随机初始化基线。
- 可迁移实验设计 2：label-free BN statistics recomputation 作为零成本适配（0.561→0.594）。迁移方式：在无 target label 场景下作为最低成本 baseline。
- 可迁移概念 5：fine-scale vs smooth 分量分解（moving average 半宽 100/250/500 kb，共用 interior 丢弃两端 50 bins）。迁移方式：用于检验预测是否只捕捉了保守的平滑景观。

## 15 与已有知识连接
- 相似工作（本文引用，可核验）：preciseTAD [24]、Epiphany [25]、C.Origami [26]、ChromNet [27]、Akita [30]、Orca [31]、DeepC [32]、CT-TADB [36]、pTADS [48]——均为「一维信号或序列 → 染色质组织」的预测方法，本文与其在输出形式（连续 score vs boundary label vs contact map）和评测契约上区分。
- 机制侧连接（本文引用，可核验）：cohesin loop extrusion 在 convergent CTCF 停滞 [20,21]，人类 cohesin 挤出活性直接观测 [22]，CTCF 降解去除局部 insulation 而保留 compartment [23]；本文的 RAD21 消融结果与 cohesin–CTCF 在转录绝缘位点的关联 [52,53] 一致，但作者明确声明测的是预测依赖而非该关联本身。
- 生物学意义连接（本文引用，可核验）：boundary 破坏与肢体畸形、glioma、T-ALL 致癌基因激活 [5–7]；boundary 强度与 CTCF occupancy、super-enhancer 绝缘 [54]；boundary 宽度与 CTCF 位点分布 [55]；单 boundary CTCF motif 缺失导致异位 enhancer 接触 [56]。
- 冲突/张力：本文指出 boundary classification 路线 [24,35,36] 丢弃 profile 深度与形状，且各研究 label 定义不同导致不可比——这与该路线自身报告的 accuracy 形成方法论张力，但本文未直接复现这些方法，故不构成对其报告性能的反驳。
- 可迁移领域：sequential regulatory-activity prediction 中的 dilated convolution [33] 与后续 self-attention [34]；本文把 dilated convolution 迁移到染色质组织预测。
- 用户已有知识连接：若本课题已熟悉 C.Origami/ChromNet 的 contact-map 预测范式，本文提供了一个「不预测 contact map 而直接预测其派生连续量」的对照视角，以及一套可复用的评测契约模板。
- 候选方向（标注为候选）：将本文的 calibrated regression 目标与 contact-map 预测器联合训练（多任务），或把 insulation score 回归作为 contact-map 预测器的辅助头——本文未做，属候选。

## 16 研究想法
### Agent 生成的研究候选
1. 名称：Multi-caller boundary F1 稳健性重评
- 来源局限/观察：本文 boundary F1 只用单一 4D Nucleome call set，而作者自己指出参考 domain 随 caller 变化。
- 核心假设：EpiInsula 相对对比方法的 boundary F1 领先在多个 caller 下保持，但绝对 F1 会显著变化。
- 相对本文的增量：把「领先」与「绝对值」分离，检验结论对参考定义的稳健性。
- 初步方法：用 Arrowhead、TopDom、 insulation-based caller 各生成一套参考 boundary，在相同 fold/seed/prominence 冻结流程下重算 F1。
- 验证方式：报告跨 caller 的 F1 排名一致性与绝对 F1 的方差。
- 可能的失败模式：排名在不同 caller 下翻转，说明领先依赖参考定义。
- 创新状态：unverified

2. 名称：Strict source-only zero-shot 对照
- 来源局限/观察：本文 zero-shot 使用 target 自身训练染色体的 input scaler，作者明确说这不是 strict source-only。
- 核心假设：strict source-only（用 source scaler）会进一步降低跨细胞类型相关，量化「input 统计量」本身的贡献。
- 相对本文的增量：把 zero-shot 拆成「权重迁移」与「输入统计迁移」两部分。
- 初步方法：对 16 个有序 pair 分别用 source scaler 与 target scaler 推理，比较相关差。
- 验证方式：配对 block bootstrap 检验差值。
- 可能的失败模式：两设置差异极小，说明 input 统计量不是主要瓶颈。
- 创新状态：partially checked（作者已指出该设置非 strict，但未做对照）

3. 名称：Insulation 回归作为 contact-map 预测器的辅助头
- 来源局限/观察：本文显示直接回归 insulation 优于从 contact map 派生（0.79–0.88 vs 0.15–0.68），但两者是分离训练的。
- 核心假设：在 contact-map 预测器上加入 insulation score 回归辅助头，可提升其派生 insulation 的相关，且不损害 contact map 质量。
- 相对本文的增量：把「直接回归」与「contact map 预测」从竞争关系变为多任务关系。
- 初步方法：在 C.Origami/ChromNet backbone 上加一个从中间特征预测 insulation score 的头，多任务训练，比较 contact map 指标与派生 insulation 相关。
- 验证方式：同 fold/seed/chromosomes 下与本文单任务结果对比。
- 可能的失败模式：辅助头只提升派生 insulation 而损害 contact map，或反之。
- 创新状态：unverified

4. 名称：Half-width 与 depth recovery 的联合扫描
- 来源局限/观察：±700-kb half-width 由 validation correlation 在 0.001 容差内选最小，而深度恢复仅 52.7%–71.0%。
- 核心假设：更长窗口能改善 depth recovery 与 reverse-regression slope，即使 pooled correlation 不变。
- 相对本文的增量：把窗口选择标准从「相关」改为「相关 + 幅度」的多目标。
- 初步方法：在固定 backbone 下扫描 ±100 至 ±1000 kb，同时报告 correlation、reverse slope、depth recovery。
- 验证方式：在四细胞系 × 5 fold × 3 seed 上重复。
- 可能的失败模式：更长窗口不改善幅度，说明压缩来自目标或 loss 而非感受野。
- 创新状态：partially checked（作者已训练七个 half-width，但只按 correlation 选择）

5. 名称：Cell-type-specific 端点的阈值无关版本
- 来源局限/观察：contrast recovery 依赖手工指定的 measured/predicted z-score 阈值，虽做了 25 点网格但围绕手工值缩放。
- 核心假设：用阈值无关度量（如 contrasting set 上 predicted z-score 差的 AUROC，或 predicted 与 measured z-score 差的回归斜率）可得到更稳健的方法排名。
- 相对本文的增量：消除端点对阈值选择的依赖。
- 初步方法：对每对细胞系，用 measured z-score 差连续值作为排序目标，计算 predicted z-score 差的 Spearman/AUROC。
- 验证方式：与本文 25 点网格排名对比一致性。
- 可能的失败模式：阈值无关度量下方法排名与本文不同，说明原端点有阈值偏置。
- 创新状态：unverified

6. 名称：等维度随机 track 对照的输入消融
- 来源局限/观察：输入消融为 retrain-from-scratch，去掉一组 track 后性能下降可能部分来自输入维度减少。
- 核心假设：加入等维度随机/打乱 track 对照后，真实 track 的信息贡献可被更准确估计。
- 相对本文的增量：把「维度效应」与「信息效应」分离。
- 初步方法：对每个消融条件，额外训练一个用等数量随机打乱 track 替换被移除 track 的模型。
- 验证方式：比较真实移除 vs 打乱替换的性能差。
- 可能的失败模式：两者差异极小，说明消融效应主要来自维度而非信息。
- 创新状态：unverified