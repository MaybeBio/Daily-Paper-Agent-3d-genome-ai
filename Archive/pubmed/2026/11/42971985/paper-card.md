## 01 基本信息

- **标题**：PSHIC reveals allele-specific chromatin organization by phasing-free structural modeling
- **作者**：Liu, Wei; Wang, Xueying; Zhang, Yuwei; Li, Shuaicheng（通讯作者）
- **单位**：未提供（Li Shuaicheng 所属机构未在摘要中列出）
- **期刊/平台**：Nature Communications
- **年份**：2026
- **论文类型**：方法学（计算生物学/生物信息学）
- **领域**：三维基因组学、Hi-C 数据分析、等位基因特异性染色质结构建模
- **关键词**：phasing-free、allele-specific、Hi-C、structural modeling、manifold learning、X-chromosome inactivation、genomic imprinting
- **DOI/arXiv**：10.1038/s41467-026-78098-4
- **代码**：未提供
- **数据**：公开数据（GM12878 in situ Hi-C: GSE63525；小鼠 Patski 细胞 DNase Hi-C: GSM2863686, GSM2863688, GSM2863689；单细胞 Hi-C: GSM3691018；Dip-C 参考结构: GSM3271347）
- **阅读日期**：未提供
- **在课题方向中的位置**：本文属于「三维基因组 × 物理/几何建模」交叉方向，提出一种无需 phasing 的等位基因特异性染色质结构解析方法，将二倍体 Hi-C 反卷积问题转化为流形嵌入与逆问题求解，是该方向中首个直接输出等位基因特异性 contact maps 和 3D 结构的 phasing-free 框架。

## 02 一句话总结

PSHIC 将二倍体 Hi-C 观测矩阵建模为两条同源染色体 contact maps 之和，通过流形学习（manifold learning）与幂律距离-接触转换函数，在无需 SNP phasing 的前提下同时求解两条同源染色体的 3D 结构和等位基因特异性 contact maps，并在模拟和真实数据（X 失活、基因组印记、RNAPII 调控网络）中验证了其准确性与生物学可解释性。

## 03 研究问题

- **具体问题**：如何在不依赖 SNP phasing 的情况下，从混合的二倍体 Hi-C 数据中解析出两条同源染色体各自的 3D 结构和等位基因特异性 contact maps？
- **为什么重要**：等位基因特异性染色质组织（如 X 染色体失活、基因组印记、等位基因特异性增强子-启动子互作）是二倍体基因组功能的核心，但传统方法依赖高质量 phased SNP 数据，在非模式生物、低杂合度样本或缺乏 trio 信息的场景中不可用。
- **现有方法不足**：
  - SNP-based 方法（allele-certain、mate-rescue、ASHIC）依赖 phasing 质量，数据利用率低（大量 reads 因无法分配等位基因而被丢弃），对 phasing 错误极度敏感；
  - Diploid-PASTIS 虽为 phasing-free，但仅输出结构而非 contact maps，且精度有限；
  - 现有方法将问题视为"标签-排序"（tag-and-sort），缺乏对染色质物理连续性和全局几何约束的建模。
- **精确研究问题（Can ... ?）**：Can a phasing-free structural modeling approach, which treats diploid Hi-C as a superposition of two homologous chromosome contact maps and leverages manifold geometry and polymer physics constraints, accurately recover allele-specific chromatin organization without any SNP information?

## 04 背景与发展脉络

> 注：此脉络基于本文框架整理，未经外部系统核验。

| 阶段 | 代表方法 | 核心思路 | 优点 | 局限 |
|------|----------|----------|------|------|
| 群体平均结构 | Hi-C 3D 建模（如 PASTIS、MEGABASE） | 从聚合 contact map 重建单一 3D 结构 | 计算成熟、可解释 | 忽略等位基因差异，混合信号 |
| SNP-based 等位基因解析 | allele-certain、mate-rescue | 利用 phased SNP 将 reads 分配到亲本 | 直接、直观 | 数据丢失严重（>90% reads 无法分配）、对 phasing 错误敏感 |
| 概率模型 | ASHIC-PM / ASHIC-ZIPM | 层次贝叶斯建模所有 read 类别 | 数据利用率提高 | 仍依赖 phased SNP 作为 anchor，phasing 错误时性能崩溃 |
| Phasing-free 结构推断 | Diploid-PASTIS | 从聚合矩阵直接推断两条同源结构 | 无需 SNP | 精度有限，不输出 contact maps，无法直接用于下游 loop/TAD 分析 |
| **本文（PSHIC）** | **流形嵌入 + 幂律转换 + 正则化逆问题** | **将二倍体 Hi-C 分解为两条同源 contact maps 之和，联合优化结构与转换参数** | **完全 phasing-free、输出 maps + 结构、对 phasing 错误免疫、数据利用率 100%** | **依赖流形假设与幂律模型；分辨率受限于 bin size** |

**本文主张的位置**：PSHIC 填补了 phasing-free 方法在"输出等位基因特异性 contact maps"这一关键空白，将问题从"标签分配"提升为"全局几何逆问题"，是该方向的方法论升级。

## 05 核心痛点

| 痛点 | 表现 | 成因或作者解释 | 文中证据 |
|------|------|----------------|----------|
| SNP 依赖 | 非模式生物、低杂合度样本无法进行等位基因分析 | 现有方法将 SNP 作为唯一等位基因信息来源 | Introduction 第 3 段："most SNP-driven haplotype-resolved contact-map reconstruction methods..." |
| 数据大量丢失 | 高达 94.1% 的 Hi-C reads 因两端无法同时匹配 SNP 而被丢弃 | 双端 reads 同时覆盖 SNP 的概率低 | Introduction 第 3 段："up to 94.1% of Hi-C read pairs are both-end allele-ambiguous" |
| Phasing 错误敏感 | 0.05% 的 phasing 错误即可导致性能显著下降 | 错误分配的 reads 产生系统性偏差 | Results "PSHIC is insensitive to SNP phasing errors" 节 |
| 无法输出 contact maps | Diploid-PASTIS 仅输出结构，无法直接用于 loop/TAD 等下游分析 | 结构推断与 map 重建未联合建模 | Discussion："Diploid-PASTIS...outputs homolog-specific 3D structures rather than allele-specific contact maps directly" |
| 局部决策 vs 全局几何 | tag-and-sort 方法忽略染色质的物理连续性和全局几何约束 | 将问题简化为局部标签分配 | Introduction 第 3 段："treats reconstruction as a simple tag-and-sort problem" |

## 06 核心思想

**1) 表面方法**：
PSHIC 将观测到的二倍体 Hi-C 矩阵 C_obs 分解为两条同源染色体 contact maps（C_m + C_p）之和，每条同源染色体被嵌入到一个 k 维流形（manifold）中，通过幂律距离-接触转换函数（λ_ij = β·d_ij^(−α)）将流形上的欧氏距离映射为接触概率，然后联合优化两条同源染色体的嵌入坐标和转换参数（α, β），使预测的混合 contact map 与观测数据最佳匹配。

**2) 核心洞察**：
- **逆问题视角**：将等位基因特异性解析从"标签分配"（需要 SNP）重构为"信号分解"（不需要 SNP）——给定混合信号，找到两个分量信号及其对应的几何结构，使二者之和最优解释观测数据。
- **全局约束替代局部标签**：流形假设（染色质是连续的低维几何对象）和物理正则化（同源染色体结构相似性、空间体积约束）提供了不依赖 SNP 的等位基因区分信号。
- **多起始点 + 谱聚类**：由于问题非凸，PSHIC 通过多次随机初始化探索解空间，并利用谱聚类筛选有效解，保证解的稳定性和生物学一致性。

**3) 可能的普适教训 [Analysis]**：
- 在生物信息学中，当"标签"不可得时，可以尝试将问题转化为"信号分解 + 物理约束"的逆问题，利用全局几何/物理先验替代局部标签信息。
- 流形学习（manifold learning）不仅适用于降维可视化，也可以作为生成模型（generative model）的一部分，直接参与逆问题求解。
- 多起始点 + 聚类筛选是处理非凸优化问题的实用策略，尤其适用于生物数据中缺乏唯一 ground truth 的场景。

## 07 方法总览

- **输入**：二倍体 Hi-C contact matrix（C_obs，经 KR 归一化）、bin 数量 n、嵌入维度 k、随机初始化次数 S
- **输出**：两条同源染色体的 contact maps（C_m, C_p）、3D 结构坐标（X_m, X_p）、转换函数参数（α, β）
- **模块**：
  1. **预处理**：KR 归一化；去除低覆盖度 outlier bins（row-sum < μ − 2σ）
  2. **初始化**：C_θ = C_obs/2 + ξ（ξ ~ U(0,1)），通过逆转换函数 D_θ = (β/(C_θ+1))^(1/α) 计算距离矩阵，经典 MDS 得到初始嵌入
  3. **优化**：迭代更新 X_m, X_p, β（内层循环），再更新 α, β（外层循环），最小化对数压缩的平方误差损失
  4. **后处理**：谱聚类筛选有效解，去除同一 trial 中两条 map 落入同一聚类的无效解；对有效解取平均
- **损失函数**：L = L_stress + λ₁·L_consistency + λ₂·L_volume
  - L_stress：对数压缩的预测-观测接触计数平方误差
  - L_consistency：同源染色体近基因组距离 bins 的空间距离一致性正则化
  - L_volume：空间体积正则化（惩罚超出球体边界的坐标）
- **可选模式**：inter-homolog contact modeling mode，显式加入 C_inter 分量（适用于减数分裂等高 inter-homolog 接触场景）
- **工具**：Python 3.8.10, NumPy, scikit-learn, PyTorch（GPU 加速）；Juicer v1.6 用于 Hi-C 预处理；HiCRep、Fit-Hi-C 用于评估
- **文字流程**：C_obs → 预处理 → 多次随机初始化 → 迭代优化（内层结构 + 外层参数）→ 谱聚类筛选 → 平均 → 输出 C_m, C_p, X_m, X_p

## 08 核心模块拆解

| 模块 | 功能 | 为何需要 | 输入输出 | 支撑证据 | 移除后的已知或预期影响 |
|------|------|----------|----------|----------|------------------------|
| KR 归一化 + outlier 去除 | 标准化 contact matrix，去除低质量 bins | Hi-C 数据存在系统性偏差和低覆盖区域 | 输入：raw C_obs；输出：归一化 C_obs | Methods "Learning Hi-C manifold embedding" 节 | 预期：低覆盖 bins 引入噪声，降低 SCC 和 F1 |
| 随机初始化 + MDS | 生成初始嵌入，打破对称性 | 问题非凸，需要多起始点探索 | 输入：C_obs, k；输出：初始 X_m, X_p | Methods "Learning Hi-C manifold embedding" 节 | 预期：单一初始化可能陷入局部最优，导致两条 map 无法分离 |
| 幂律转换函数 | 将距离映射为接触概率 | 物理上接触频率与空间距离呈幂律关系 | 输入：d_ij, α, β；输出：λ_ij | Methods 公式 (4) | 预期：错误 α 导致距离-接触关系失真，降低结构保真度 |
| 对数压缩损失 | 平衡近/远距离 bins 的贡献 | 原始平方误差被高接触 counts 主导 | 输入：C_pred, C_obs；输出：L_stress | Methods 公式 (7) | 预期：移除后近对角线 bins 主导损失，远距离结构信息丢失 |
| 一致性正则化 | 约束同源染色体近基因组距离 bins 空间距离相似 | 同源染色体在局部应具有相似的空间折叠 | 输入：X_m, X_p；输出：L_consistency | Methods 公式 (8) | 预期：移除后可能出现一条染色体过度紧凑、另一条过度分散的非物理解 |
| 体积正则化 | 惩罚超出球体边界的坐标 | 防止结构无限膨胀 | 输入：X_θ；输出：L_volume | Methods 公式 (9) | 预期：移除后结构可能发散，β 估计不稳定 |
| 谱聚类筛选 | 区分有效/无效解 | 部分 trial 可能收敛到两条 map 相似的退化解 | 输入：所有 trial 的 C_m, C_p；输出：有效 trial 集合 V | Methods "Learning Hi-C manifold embedding" 节 | 预期：移除后退化解污染平均结果，降低等位基因特异性分辨率 |
| Inter-homolog 模式 | 显式建模同源染色体间接触 | 减数分裂等场景 inter-homolog 接触显著 | 输入：C_obs；输出：C_m + C_p + C_inter | Methods "Optional inter-homolog contact modeling mode" 节 | 预期：默认模式在 inter-homolog 高场景下产生系统性偏差 |

## 09 关键公式符号

**1) 观测模型（公式 2）**：
C_obs = Σ_{θ∈{m,p}} C_θ
- C_obs：观测到的二倍体 Hi-C contact matrix
- C_m, C_p：母源、父源同源染色体的 contact matrices

**2) 幂律距离-接触转换（公式 4）**：
λ_ij(θ) = E[f_ij(X_θ)] = β · d_ij(X_θ)^(−α)
- λ_ij(θ)：同源染色体 θ 上 bin i、j 之间的期望接触频率
- d_ij(X_θ) = ‖x_θ,i − x_θ,j‖₂：嵌入空间中 bin i、j 的欧氏距离
- α：幂律指数（初始化为 3，基于聚合物物理理论）
- β：比例常数（反映测序深度、实验条件）

**3) 损失函数（公式 7-9）**：
L = L_stress + λ₁·L_consistency + λ₂·L_volume

L_stress = ‖ log(1 + (Σ_θ β·d_ij(X_θ)^(−α) − C_obs,ij)²) ‖₂

L_consistency = (1/R) Σ_{r=1}^{R} (1/r²) ‖ (|diag_r(D_m) − diag_r(D_p)|) / ((diag_r(D_m) + diag_r(D_p))/2) ‖₂

L_volume = Σ_θ Σ_{u=1}^{n} [max(0, ‖x_θ,u‖₂ − l)]²

- diag_r(·)：提取距离矩阵的第 r 条对角线（对应基因组距离为 r 的 bin 对）
- R：考虑的对角线范围（短程基因组距离）
- l：球体半径边界
- λ₁, λ₂：正则化权重

**4) 初始化（公式 11）**：
D_θ = (β / (C_θ + 1))^(1/α)
- 通过逆转换从初始 contact map 估计距离矩阵，再进行 MDS

## 10 实验设计与证据链

- **数据集**：
  - 模拟数据：基于 Dip-C 得到的 GM12878 单细胞 3D 结构（GSM3271347）生成 ground-truth 二倍体 contact maps，再模拟 Poisson 采样
  - 真实数据：小鼠 Patski 细胞 DNase Hi-C（GSM2863686, GSM2863688, GSM2863689）；人 GM12878 in situ Hi-C（GSE63525）；小鼠早期胚胎单细胞 Hi-C（GSM3691018）
- **规模**：模拟中每个参数设置 10 个重复；真实数据覆盖 X 染色体、7 号染色体、11 号、12 号染色体区域
- **指标**：SCC（HiCRep）、F1（loop 检测）、DER（距离误差率）
- **基线**：Diploid-PASTIS、ASHIC-PM、ASHIC-ZIPM、allele-certain、mate-rescue
- **评测协议**：模拟中所有方法共享相同的幂律转换函数和 α=3，确保公平比较；真实数据中与 ChIP-seq、4C-seq、3D-FISH、ChIA-PET 等正交实验数据对比

| 实验 | 检验的 claim | 对比与条件 | 结果 | 支持的结论 | 不支持更强的结论 | 来源 |
|------|-------------|------------|------|-------------|-------------------|------|
| 测序深度敏感性 | PSHIC 在低深度下保持性能 | 深度从 25% 到 100% β̂，10 重复 | SCC 0.989–0.994，F1 0.959–0.967，DER 0.010–0.023 | PSHIC 对深度不敏感 | 未测试低于 25% 深度的极端场景 | Results 图 2C |
| SNP 密度敏感性 | PSHIC 不依赖 SNP 密度 | SNP 密度 1/100bp 到 1/1000bp | PSHIC 性能不变；SNP-based 方法随密度下降而恶化 | PSHIC 在 SNP 稀疏场景中具有优势 | 未测试完全无 SNP 的极端场景 | Results 图 2C |
| Phasing 错误鲁棒性 | PSHIC 对 phasing 错误免疫 | 错误率 0–2% | PSHIC 性能恒定；ASHIC 在 0.05% 错误时 SCC 从 0.936 降至 0.514 | PSHIC 消除了 phasing 错误的影响 | 未测试 >2% 错误率 | Results "PSHIC is insensitive to SNP phasing errors" 节 |
| X 失活 bipartite 结构 | PSHIC 能恢复 Xi 的双超结构域 | 小鼠 Patsik WT/Del/Inv-Dxz4 | WT 和 Inv 保留 bipartite 结构，Del 丧失；Inv 边界向端粒侧偏移 | PSHIC 能检测等位基因特异性结构变异 | 未与单细胞 Hi-C 直接对比 | Results 图 3 |
| H19/Igf2 印记 | PSHIC 能恢复等位基因特异性印记互作 | 小鼠 7 号染色体 1Mb 区域 | 母源染色体 H19-DMR 与 CTCF 簇互作更强，母源特异性 sub-TAD 边界 | PSHIC 能检测印记位点的等位基因特异性组织 | 未验证功能后果 | Results 图 4 |
| 人 GM12878 验证 | PSHIC 结果与 ChIA-PET 一致 | 3 个区域（12 号、11 号、X 染色体） | RNAPII 互作、IGF2/H19 印记、X 失活结构均与 ChIA-PET 一致 | PSHIC 跨物种、跨区域泛化 | 未覆盖全基因组 | Results 图 5 |
| 单细胞数据 | PSHIC 无需 phasing 即可处理单细胞 Hi-C | 小鼠早期胚胎 2-cell 单细胞 Hi-C | 重建的 diploid maps 与 SNP-based 方法高度一致，且信号更强 | PSHIC 可推广至单细胞场景 | 样本量有限 | Results "PSHIC reconstructs single-cell diploid contact maps" 节 |

## 11 结论正确解读

- **任务范围**：PSHIC 解决的是"从聚合二倍体 Hi-C 中恢复等位基因特异性 contact maps 和 3D 结构"这一特定任务，不涉及全基因组从头组装或变异检测。
- **Oracle/真值输入**：模拟中使用了 Dip-C 导出的真实 3D 结构作为 ground truth；真实数据中使用了 ChIP-seq、4C-seq、3D-FISH、ChIA-PET 等正交实验作为验证参考。PSHIC 本身不需要任何 oracle 输入。
- **端到端状态**：PSHIC 是端到端的——输入 raw Hi-C contact matrix，输出等位基因特异性 maps 和结构。但预处理（Juicer 流程）仍需标准 Hi-C 分析步骤。
- **算力成本**：GPU 加速下，染色体尺度（28–1334 bins）单次运行 10–55 分钟；无 SNP 预处理需求，节省约 25.9 小时（对比 SNP calling 流程）。
- **历史数据依赖**：不依赖任何历史数据或预训练模型，完全基于当前输入的 contact matrix。
- **模型依赖**：依赖幂律距离-接触假设（α=3 初始化）和流形连续性假设；在不符合这些假设的场景（如极端重排）中可能失效。
- **最难情形**：低测序深度 + 高 phasing 错误 + 低 SNP 密度的组合场景；全基因组 10kb 分辨率的系统验证尚未完成。
- **群体/领域边界**：验证限于人类（GM12878）和小鼠（Patsik、早期胚胎）细胞系/组织，未覆盖其他物种或疾病样本。
- **不确定性**：PSHIC 输出的是群体平均的等位基因特异性结构，不反映单细胞异质性；inter-homolog 接触在默认模式中被视为噪声，仅在可选模式中显式建模。
- **有边界的复述**：PSHIC 在模拟和真实数据中证明，无需任何 SNP 信息即可从聚合 Hi-C 中恢复等位基因特异性 contact maps 和 3D 结构，在低深度、低 SNP 密度和高 phasing 错误场景下显著优于现有方法，并能检测 X 失活、基因组印记和等位基因特异性调控互作等已知生物学特征。

## 12 作者自认局限

| 局限 | 具体表现 | 作者提出的未来方向 | 来源 |
|------|----------|---------------------|------|
| 仅限染色体内 | 当前框架主要聚焦于染色体内（intra-chromosomal）二倍体重建，未显式建模染色体间（inter-chromosomal）长程互作 | 未来扩展将纳入染色体间接触和全基因组空间约束 | Discussion 第 2 段 |
| 分辨率受限 | 系统分辨率基准测试限于 20kb，因为 Dip-C 导出的 ground truth 坐标最细为 20kb；10kb 全基因组重建未系统验证 | 需要更高分辨率的 ground truth 数据来验证 10kb 重建 | Discussion 第 2 段 |
| 分辨率-效率权衡 | 250kb–1Mb 在重建精度和计算效率间提供最佳平衡，10–20kb 更适合靶向区域或深度测序数据 | 优化算法以支持更高分辨率的全基因组分析 | Discussion 第 2 段 |

## 13 批判性分析

| [Analysis] 观察 | 潜在问题或替代解释 | 为何重要 | 如何检验 | 依据 |
|-----------------|---------------------|----------|----------|------|
| 模拟中所有方法共享相同的幂律转换函数（α=3） | 这可能有利于 PSHIC，因为其优化框架与模拟生成模型完全一致；其他方法（如 ASHIC）可能因模型不匹配而处于劣势 | 模拟基准的公平性直接影响结论的普适性 | 使用不同的 ground-truth 生成模型（如非幂律、含 domain 结构）重新模拟，检验 PSHIC 是否仍占优 | Methods "Hi-C manifold embedding" 节 |
| 真实数据验证依赖已知生物学特征（XCI、印记） | 这些特征是强先验，PSHIC 可能只是"重新发现"已知模式，而非发现新等位基因特异性结构 | 需要验证 PSHIC 能否发现未知的等位基因特异性结构 | 在缺乏先验知识的区域（如常染色体非印记区域）检验 PSHIC 的等位基因特异性预测是否与独立实验一致 | Results 图 3-5 |
| 谱聚类筛选可能引入选择偏差 | 丢弃"无效" trial 的标准可能偏向于与已知生物学一致的解，导致过度拟合先验 | 如果筛选标准隐含生物学先验，PSHIC 的"发现"可能只是先验的反映 | 在模拟中检验筛选标准是否偏向 ground truth；在真实数据中比较筛选前后结果的差异 | Methods "Learning Hi-C manifold embedding" 节 |
| 与 Diploid-PASTIS 的性能差距 | 作者归因于 PSHIC 的联合优化和正则化，但 Diploid-PASTIS 可能因实现细节（如收敛标准、初始化）而表现不佳 | 需要排除实现差异导致的性能差距 | 使用 Diploid-PASTIS 的原始实现和调优参数重新基准测试；检查 PSHIC 是否在相同计算预算下仍占优 | Results 图 2C |
| 未报告统计显著性 | 模拟结果以均值和 SD 呈现，但未提供方法间差异的统计检验 | 性能差距可能不显著，特别是在高深度、高 SNP 密度场景 | 对每个参数设置进行配对统计检验（如 Wilcoxon 检验），报告效应量和置信区间 | Results 图 2C |
| 单细胞验证样本量有限 | 仅使用 2-cell 胚胎数据，且未报告细胞数量 | 单细胞场景的结论可能不稳健 | 在更多单细胞数据集上验证，报告细胞数量和重复 | Results "PSHIC reconstructs single-cell diploid contact maps" 节 |

## 14 学到什么

**Agent 提炼的知识候选**：

1. **Phasing-free 信号分解范式**：将等位基因特异性解析从"标签分配"重构为"信号分解"——C_obs = C_m + C_p。这一思路可迁移到其他缺乏标签信息的二倍体/多倍体基因组分析任务（如等位基因特异性甲基化、ATAC-seq 等）。

2. **流形学习作为生成模型**：MDS/manifold embedding 不仅用于降维可视化，还可以作为生成模型直接参与逆问题求解。在三维基因组建模中，将结构坐标作为可优化变量、通过幂律转换生成 contact map 的思路，可迁移到单倍型分辨的 3D 基因组建模、多细胞类型结构比较等任务。

3. **多起始点 + 谱聚类筛选**：对于非凸优化问题，多次随机初始化 + 基于结构相似性的谱聚类筛选是获得稳健解的实用策略。这一策略可迁移到其他生物信息学优化问题（如结构预测、网络推断）。

4. **物理正则化的重要性**：一致性正则化（同源染色体局部结构相似）和体积正则化（空间边界约束）显著提升了求解稳定性。在三维基因组建模中，引入聚合物物理约束（如排除体积、链连通性）可以改善解的生物学合理性。

5. **评估指标的组合设计**：SCC（map 相似性）+ F1（loop 检测）+ DER（结构距离误差）三者互补，分别评估 contact map 保真度、功能特征恢复和结构精度。这种多维度评估框架可迁移到其他结构预测方法的基准测试。

6. **模拟-真实双轨验证策略**：模拟实验隔离方法差异（共享生成模型），真实实验验证生物学可解释性（与 ChIP-seq、4C-seq、FISH、ChIA-PET 正交验证）。这种"受控模拟 + 正交实验验证"的评估范式值得借鉴。

## 15 与已有知识连接

- **PASTIS / Diploid-PASTIS**：PSHIC 的幂律距离-接触转换框架直接继承自 PASTIS 系列，但将单倍体扩展为二倍体联合优化，并增加了 consistency 和 volume 正则化。可对比阅读 PASTIS 原文以理解增量贡献。
- **ASHIC-PM / ASHIC-ZIPM**：ASHIC 是 SNP-based 概率框架的代表，PSHIC 在模拟中与之对比。两者互补——ASHIC 在高质量 phasing 可用时可能更精确，PSHIC 在 phasing 不可用时是唯一选择。
- **HiCRep / Fit-Hi-C**：评估指标 SCC 来自 HiCRep，loop 检测使用 Fit-Hi-C，均为三维基因组分析的标准工具。
- **Dip-C**：模拟 ground truth 来自 Dip-C 单细胞 3D 结构，连接了单细胞 Hi-C 与群体 Hi-C 分析。
- **Juicer / HiC-Pro**：数据预处理流程，标准 Hi-C 分析工具链。
- **聚合物物理模型**：幂律指数 α=3 的初始化基于 fractal globule 和 equilibrium globule 模型的理论预测，连接了三维基因组学与聚合物物理。
- **X 失活与基因组印记**：生物学验证场景，连接了三维基因组结构与表观遗传调控。
- **可迁移方向**：PSHIC 的"信号分解 + 物理约束"框架可迁移到单细胞 Hi-C 的等位基因解析、多倍体基因组 3D 建模、以及空间转录组与 Hi-C 的整合分析。

## 16 研究想法

**Agent 生成的研究候选**：

1. **候选名称**：PSHIC-3D Genome-wide phasing-free allele-specific TAD/loop annotation
   - **来源局限/观察**：PSHIC 目前聚焦于染色体内重建，未系统评估等位基因特异性 TAD 边界和 loop 的注释精度；作者也承认未纳入 inter-chromosomal 互作。
   - **核心假设**：PSHIC 输出的等位基因特异性 contact maps 可直接用于等位基因特异性 TAD/loop 注释，且比 SNP-based 方法在低 phasing 质量场景下更稳健。
   - **初步方法**：在 PSHIC 输出的 C_m 和 C_p 上运行 TAD 识别算法（如 TopDom、Armatus）和 loop 调用工具（如 Fit-Hi-C、HiCCUPS），与 SNP-based 方法的结果对比；在模拟中引入已知的等位基因特异性 TAD 差异，检验检测灵敏度。
   - **验证方式**：使用已发表的等位基因特异性 Hi-C 数据（如 GM12878 phased 数据）作为 benchmark；与 ChIA-PET、3D-FISH 等正交实验对比。
   - **创新状态**：unverified

2. **候选名称**：PSHIC-single-cell：phasing-free 单细胞等位基因特异性结构解析
   - **来源局限/观察**：作者在补充材料中展示了 PSHIC 在单细胞 Hi-C 上的初步结果，但未系统评估。
   - **核心假设**：PSHIC 的流形学习框架对稀疏单细胞数据具有天然鲁棒性，可在无需 phasing 的情况下解析单细胞水平的等位基因特异性结构。
   - **初步方法**：将 PSHIC 应用于单细胞 Hi-C 数据，与 SNP-based 单细胞等位基因解析方法对比；评估不同细胞周期阶段、不同细胞类型中的表现。
   - **验证方式**：使用已知等位基因特异性结构的单细胞数据（如 X 失活细胞）；与 scHi-C 结构重建方法（如 Higashi）对比。
   - **创新状态**：unverified

3. **候选名称**：PSHIC-phylo：跨物种等位基因特异性结构比较
   - **来源局限/观察**：PSHIC 不依赖物种特异性 SNP 资源，天然适用于非模式生物。
   - **核心假设**：PSHIC 可在缺乏 phasing 资源的非模式生物中解析等位基因特异性染色质结构，揭示跨物种保守的等位基因特异性组织模式。
   - **初步方法**：将 PSHIC 应用于多个物种（如小鼠、大鼠、猪、鸡）的 Hi-C 数据，比较等位基因特异性结构的保守性和差异性。
   - **验证方式**：与已知的印记基因座结构对比；与系统发育分析结合。
   - **创新状态**：unverified

4. **候选名称**：PSHIC-3D genome-wide phasing-free allele-specific enhancer-promoter interaction prediction
   - **来源局限/观察**：PSHIC 在 RNAPII 调控网络和印记基因座中展示了等位基因特异性增强子-启动子互作检测能力，但未系统评估其作为预测工具的性能。
   - **核心假设**：PSHIC 输出的等位基因特异性 contact maps 可预测等位基因特异性增强子-启动子互作，且比基于 SNP 的方法在非编码区更有效。
   - **初步方法**：在 PSHIC 输出的 maps 上运行增强子-启动子互作预测工具（如 TargetFinder、DeepTACT），与 SNP-based 方法对比；在已知等位基因特异性表达基因座中验证。
   - **验证方式**：使用 eQTL 和等位基因特异性表达数据；与 CRISPR 验证的增强子-启动子互作对比。
   - **创新状态**：unverified

5. **候选名称**：PSHIC-3D genome-wide phasing-free allele-specific structural variant detection
   - **来源局限/观察**：PSHIC 能检测 Dxz4 编辑引起的结构变化，提示其可能用于检测等位基因特异性结构变异。
   - **核心假设**：PSHIC 输出的等位基因特异性 contact maps 可检测等位基因特异性结构变异（如倒位、易位、拷贝数变异），且不依赖 SNP phasing。
   - **初步方法**：在模拟中引入已知的等位基因特异性结构变异，检验 PSHIC 的检测灵敏度；在真实数据中与已知结构变异对比。
   - **验证方式**：使用已知结构变异的细胞系（如 Dxz4 编辑细胞）；与光学图谱、长读长测序验证对比。
   - **创新状态**：unverified