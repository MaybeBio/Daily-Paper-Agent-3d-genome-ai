## Review setup
- **Input scope** Full manuscript text (abstract, introduction, results, discussion, methods, figure legends) without supplementary files or source data.
- **Assessment boundary** Scientific validity, methodological soundness, clarity of claims, and alignment with Nature-style criteria. No assessment of code availability, reproducibility scripts, or supplementary figures/tables beyond what is referenced.
- **Shared manuscript claim summary** The authors present PSHIC, a computational framework that reconstructs allele-specific (maternal and paternal) Hi-C contact maps and 3D chromatin structures from unphased, aggregated Hi-C data. The method models chromosomes as continuous manifolds, solves an inverse problem to decompose the observed contact matrix into two homolog-specific components, and is claimed to outperform existing SNP-dependent methods across simulations and real datasets, including X-chromosome inactivation, imprinting, and regulatory contexts.
- **Visible evidence base** Main text, Methods section, Algorithm 1 pseudocode, and figure legends for Figures 1–5. References to Supplementary Figures 1–8, Supplementary Tables 1, and Supplementary Notes 1–6 are present but not provided.
- **Missing materials affecting confidence** Supplementary figures, notes, tables, source data, code, and any benchmarking details beyond the main text. Statistical details for real-data analyses (e.g., number of replicates, confidence intervals) are partially reported but not fully verifiable.

## Reviewer
- **Overall assessment** The manuscript addresses a significant and timely problem in 3D genomics: recovering allele-specific chromatin organization without phased SNP data. The conceptual shift from tag-and-sort to structural modeling is appealing and could broaden applicability to non-model organisms. However, the current evidence base is insufficient to establish the method's validity. Key concerns include the lack of a formal identifiability argument, unclear handling of inter-homolog contacts in the default mode, potential circularity in real-data validation, and incomplete reporting of statistical and computational details. The method's claimed advantages over Diploid-PASTIS and SNP-based approaches are not fully supported by the presented data.
- **Who would be interested in the results, and why** Researchers in 3D genome organization, chromatin structure prediction, and computational genomics. The method could be of interest to those studying allele-specific phenomena (imprinting, X-inactivation) in systems where phased data are unavailable, and to developers of Hi-C analysis tools. The phasing-free aspect may also appeal to the broader chromosome conformation capture community.
- **Major strengths**
  - Addresses a real limitation of existing haplotype-resolved methods: dependence on phased SNPs.
  - The manifold-based inverse problem formulation is conceptually novel and distinct from prior tag-and-sort approaches.
  - Validation spans multiple biological contexts (X-inactivation, imprinting, regulatory loops) and species (mouse, human), with orthogonal experimental comparisons.
  - The method includes practical features such as outlier bin removal, KR normalization, and multi-trial averaging with spectral clustering, suggesting attention to robustness.
- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Identifiability and model assumptions
- **Claim pointer** The manuscript claims that PSHIC can "reveal" allele-specific chromatin organization from aggregated Hi-C data without phasing, implying that the decomposition into maternal and paternal contact maps is identifiable from the observed sum.
- **Evidence pointer** Methods, "Problem formulation" and "Hi-C manifold embedding with adaptive loss"; Algorithm 1.
- **Concern** The core assumption is that the observed contact matrix can be uniquely decomposed into two homolog-specific matrices. However, the manuscript does not provide a formal identifiability analysis. The optimization problem is non-convex, and the authors rely on random initialization and spectral clustering to select solutions. It is unclear whether the decomposition is unique, whether different initializations converge to equivalent solutions, or whether the method can distinguish between genuine allele-specific structure and arbitrary splits of the contact matrix. The consistency regularization and volume penalty may bias solutions but do not guarantee identifiability.
- **Why it matters** If the decomposition is not identifiable, the recovered "allele-specific" maps may be artifacts of the optimization procedure rather than true biological signals. This is a fundamental issue that undermines the central claim of the manuscript.
- **Resolution test** Provide a formal identifiability argument or a simulation study where the true allele-specific maps are known and show that PSHIC recovers them uniquely across many random initializations. Demonstrate that the solution is stable and that the loss landscape does not contain multiple equally good but biologically distinct decompositions.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Validation against ground truth
- **Claim pointer** The manuscript claims that PSHIC "consistently outperforms established methods" in simulations, with SCC ≥ 0.987, F1 ≥ 0.952, and DER ≤ 0.04.
- **Evidence pointer** Results, "Diploid Hi-C map Reconstruction for in silico datasets"; Figure 2C.
- **Concern** The simulation setup is described as deriving ground truth from single-cell Dip-C data, but the details of how the aggregated contact matrix was generated, how noise was added, and how the ground truth was defined are not fully specified. The reported metrics are extremely high (SCC near 0.99), which raises questions about whether the simulation is realistic or overly favorable to PSHIC. The comparison to Diploid-PASTIS, which reportedly has much lower performance, may be due to differences in evaluation criteria or implementation rather than genuine methodological superiority.
- **Why it matters** If the simulation is not realistic or is biased, the claimed performance advantage may not translate to real data. The manuscript's central quantitative claims rest on this simulation.
- **Resolution test** Provide full details of the simulation pipeline, including how the aggregated matrix was generated from Dip-C structures, the noise model, and the exact evaluation protocol. Show that the simulation results are robust to variations in noise, coverage, and ground-truth definition. Consider benchmarking on additional independent simulated datasets or on real data with known allele-specific features.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Real-data validation and circularity
- **Claim pointer** The manuscript claims that PSHIC recovers allele-specific features consistent with orthogonal experimental approaches (3D DNA-FISH, 4C-seq, ChIA-PET) in mouse and human datasets.
- **Evidence pointer** Results, sections on X-inactivation, H19/Igf2 imprinting, and GM12878; Figures 3–5.
- **Concern** The real-data validation appears to rely on comparing PSHIC's output to known or expected biological features (e.g., bipartite structure of Xi, imprinted interactions). However, the manuscript does not clearly state whether these features were used to guide the method's parameters or to select among candidate solutions. If the method's output is compared to the same features used for validation, there is a risk of circularity. Additionally, the comparison to SNP-based methods (allele-certain, mate-rescue) in real data is qualitative, and the manuscript does not provide quantitative metrics for how well PSHIC matches the SNP-based results.
- **Why it matters** If validation is circular or only qualitative, the claim that PSHIC accurately recovers allele-specific organization in real data is not substantiated.
- **Resolution test** Clearly state that no biological features were used to guide the method's optimization or solution selection. Provide quantitative comparisons between PSHIC's output and SNP-based methods (e.g., correlation of contact maps, overlap of loops) in real data. For the X-inactivation and imprinting analyses, show that the recovered allele-specific features are not simply a consequence of the method's assumptions.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Inter-homolog contact modeling
- **Claim pointer** The manuscript states that PSHIC's default mode treats inter-homolog contacts as noise, but an optional mode explicitly models them.
- **Evidence pointer** Methods, "Optional inter-homolog contact modeling mode"; Supplementary Notes 1–2.
- **Concern** The default mode's assumption that inter-homolog contacts are negligible may not hold in all biological contexts, and the manuscript does not provide guidance on when the optional mode should be used. The simulation results for the optional mode are only referenced in supplementary materials, which are not provided. It is unclear whether the optional mode improves accuracy or introduces new biases.
- **Why it matters** If the default mode is applied in contexts where inter-homolog contacts are significant, the reconstructed allele-specific maps may be systematically biased. The manuscript's applicability claims may be overstated.
- **Resolution test** Provide the supplementary results for the inter-homolog mode. Show how the choice of mode affects performance in simulations with varying inter-homolog contact fractions. Provide clear guidance on when each mode is appropriate.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Computational cost and scalability
- **Claim pointer** The manuscript claims that PSHIC is computationally feasible at the chromosome scale, with runtimes of 10–55 minutes per run depending on resolution.
- **Evidence pointer** Methods, "Convergence and running time"; Supplementary Table 1.
- **Concern** The runtime analysis is limited to a single chromosome and does not address genome-wide scalability. The number of random initializations (S) and the criteria for selecting the number of trials are not specified. The comparison to SNP-based methods in terms of total wall-clock time (including preprocessing) is only partially reported.
- **Why it matters** If PSHIC does not scale to genome-wide analysis or requires excessive computational resources, its practical utility is limited.
- **Resolution test** Provide runtime benchmarks for multiple chromosomes or a full genome at typical resolutions. Specify the number of random initializations used and the sensitivity of results to this parameter. Provide a more complete comparison of total analysis time, including preprocessing, for PSHIC versus SNP-based methods.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity of notation
- **Affected element** Methods, "Problem formulation" and "Hi manifold embedding with adaptive loss"
- **Evidence pointer** Equations 1–15 and Algorithm 1.
- **Issue** The notation is dense and sometimes inconsistent. For example, the use of \(\hat{\beta}\) in the main text is not clearly defined in the Methods, and the relationship between the embedding dimension \(k\) and the final 3D projection via PCA is not explained in detail.
- **Required correction** Define all symbols clearly at first use, including \(\hat{\beta}\), and explain the role of \(k\) and the PCA projection step in the Methods.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** Results, "Diploid Hi-C map Reconstruction for in silico datasets" and real-data sections
- **Evidence pointer** Figure 2C, Figure 3C, Figure 4B.
- **Issue** The manuscript reports means and standard deviations for some metrics but does not consistently report confidence intervals or statistical tests for comparisons between methods. For real-data analyses, the number of replicates and the variability across replicates are not always clear.
- **Required correction** Report confidence intervals or effect sizes for key comparisons. For real-data analyses, state the number of independent datasets or replicates and how variability was assessed.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Parameter sensitivity
- **Affected element** Methods, "Hi-C Datasets and simulation" and "Convergence and running time"
- **Evidence pointer** Algorithm 1, Supplementary Table 1.
- **Issue** The sensitivity of results to key parameters such as the regularization weights \(\lambda_1\), \(\lambda_2\), the number of trials \(S\), and the convergence criteria is not reported.
- **Required correction** Provide a sensitivity analysis for these parameters, or at least state the values used and justify them.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Comparison to existing methods
- **Affected element** Results, "Diploid Hi-C map Reconstruction for in silico datasets"
- **Evidence pointer** Figure 2C.
- **Issue** The comparison to existing methods is limited to a single simulation setting. The manuscript does not discuss potential limitations of the compared methods or whether the comparison is fair (e.g., same input data, same evaluation metrics).
- **Required correction** Clarify the comparison protocol and discuss any limitations of the compared methods that might affect the results.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Readability
- **Affected element** Introduction and Discussion
- **Evidence pointer** Sections on X-inactivation and imprinting.
- **Issue** The biological background is dense and assumes significant prior knowledge. Some terms (e.g., "bipartite structure," "superdomains") are used without clear definitions for a general audience.
- **Required correction** Provide brief definitions or context for key biological terms to improve accessibility for nonspecialist readers.

- **Technical failings that need to be addressed before the case is established**
  - R1-M1: Lack of identifiability analysis for the core decomposition problem.
  - R1-M2: Incomplete simulation details and potential bias in the benchmarking protocol.
  - R1-M3: Potential circularity in real-data validation and lack of quantitative comparison to SNP-based methods.
  - R1-M4: Unclear handling of inter-homolog contacts and lack of guidance on mode selection.
  - R1-M5: Incomplete computational scalability analysis.

- **Assessment against Nature-style criteria**
  - **Originality** The phasing-free structural modeling approach is conceptually original and distinct from existing SNP-based methods. The idea of treating the decomposition as an inverse problem on manifolds is novel.
  - **Scientific importance** The problem addressed is important: enabling allele-specific analysis in systems where phased data are unavailable. If validated, the method could have broad impact.
  - **Interdisciplinary readership** The topic is of interest to computational biologists, genomicists, and chromatin biologists. However, the dense methods and lack of clear biological context may limit accessibility.
  - **Technical soundness** The technical approach is plausible but not fully validated. The lack of identifiability analysis and incomplete simulation details are significant gaps.
  - **Readability for nonspecialists** The manuscript is technically dense and assumes significant background. The biological significance could be communicated more clearly.

- **Recommendation posture** Currently not established from the provided evidence. The manuscript presents a promising idea but lacks the rigorous validation and analysis needed to support its central claims. Major revisions are required to address the identifiability concern, provide complete simulation and real-data validation, and clarify the method's practical applicability.

## Risk / unsupported claims
- The claim that PSHIC "consistently outperforms established methods" is not fully supported due to incomplete simulation details and potential bias.
- The claim that PSHIC "reveals" allele-specific organization is not supported without an identifiability analysis.
- The claim that PSHIC's real-data results align with orthogonal experiments is qualitative and may be circular.
- The claim that PSHIC is computationally feasible at the chromosome scale is based on limited benchmarks and does not address genome-wide scalability.
- The claim that PSHIC "democratizes diploid chromatin analysis" is overstated given the unresolved technical concerns.