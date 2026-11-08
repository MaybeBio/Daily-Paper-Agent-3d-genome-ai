## Review setup
- **Input scope** Full manuscript text (abstract, introduction, methods, results, discussion) without figures, tables, or supplementary materials
- **Assessment boundary** Scientific validity, methodological soundness, and clarity of claims based on the provided text only; code and data availability statements noted but not independently verified
- **Shared manuscript claim summary** The authors present scSTEC, a computational framework for annotating chromatin subcompartments from individual single-cell Hi-C matrices without imputation, complex upstream processing, or cross-cell information sharing. The method is based on a mathematical observation that the estimated inter-chromosomal matrix used by scGHOST is of rank 2, enabling exact two-dimensional embedding of the relevant geometry. The authors validate scSTEC on bulk Hi-C, downsampled simulations, and multiple real scHi-C datasets, reporting comparable performance to scGHOST with greater interpretability and computational efficiency.
- **Visible evidence base** Main text only; all figures, supplementary figures, and supplementary methods referenced but not provided
- **Missing materials affecting confidence** All figures (Figures 1-5), all supplementary figures (S1-S22), supplementary methods, and supplementary data availability details; without these, quantitative claims and benchmarking results cannot be independently assessed

## Reviewer

- **Overall assessment** The manuscript addresses a relevant problem in single-cell genomics: annotating chromatin subcompartments from sparse scHi-C data without relying on complex deep-learning pipelines or cross-cell information sharing. The central mathematical observation regarding the rank-2 structure of scGHOST's estimated inter-chromosomal matrix is potentially interesting and could provide a useful theoretical justification for dimensionality reduction in this context. However, the manuscript as provided cannot be fully evaluated because all figures and supplementary materials are missing. The claims of comparable performance to scGHOST, robustness to sparsity, and biological validity rest entirely on visual and quantitative results presented in figures that were not available for review. The methodological description is also incomplete in places, with key equations and definitions omitted from the text as provided. The writing is generally clear and the logical structure is sound, but the evidence base is insufficient for a definitive assessment.

- **Who would be interested in the results, and why** Computational biologists and bioinformaticians working on single-cell chromatin conformation analysis, particularly those developing or using tools for compartment and subcompartment annotation. The claim of a mathematically grounded, interpretable alternative to deep-learning-based methods may also interest researchers concerned with reproducibility and transparency in computational genomics. Biologists studying 3D genome organization, cell-type-specific chromatin states, and developmental dynamics could find the downstream applications (cell-type resolution, developmental trajectories) relevant, though the biological findings are presented as validations rather than discoveries.

- **Major Strengths**
  - The core idea is conceptually appealing: identifying a low-rank structure in the estimated inter-chromosomal matrix and exploiting it for direct two-dimensional embedding is elegant and potentially generalizable.
  - The method addresses a genuine limitation of existing approaches (scGHOST's dependence on cross-cell information and complex pipelines), and the goal of per-cell independent annotation is well motivated.
  - The validation strategy is broad, spanning bulk Hi-C, simulations, and multiple real datasets across species and developmental contexts, with attention to both technical performance and biological interpretability.
  - The discussion of limitations is honest and includes practical guidance on data coverage requirements and potential extensions.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence completeness
- **Claim pointer** The manuscript claims that scSTEC achieves subcompartment annotations comparable to scGHOST across bulk Hi-C, downsampled simulations, and real scHi-C datasets, and that it remains robust under severe data sparsity.
- **Evidence pointer** Figures 2A-D, 3A-G, 4A-E, 5A-C; Supplementary Figures S1-S22; location not provided
- **Concern** All quantitative results supporting the central performance claims are presented in figures and supplementary figures that were not included in the provided material. Without these, the claims of comparability to scGHOST, robustness to sparsity, and biological validity cannot be assessed. This includes the benchmarking against ground truth in simulations, the statistical significance of enrichment analyses, the concordance metrics, and the visual comparisons that are central to the paper's conclusions.
- **Why it matters** The core contribution of the manuscript is empirical: demonstrating that a simpler, interpretable method performs comparably to a more complex one. Without access to the actual results, the validity of this claim is unverifiable.
- **Resolution test** Provide all figures and supplementary figures with full legends, including quantitative values, statistical tests, and sample sizes. The reviewer must be able to evaluate the magnitude of reported effects and the strength of statistical support.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Methodological completeness
- **Claim pointer** The methods section describes a two-dimensional genomic representation and embedding procedure, including equations for the representation, distance calculations, and eigenvalue decomposition.
- **Evidence pointer** Section 2.1; location not provided
- **Concern** The key equations defining the 2D representation, the distance calculations, and the eigenvalue decomposition are referenced in the text but not actually displayed in the provided manuscript. The definitions of key variables (e.g., the exact form of the representation, the meaning of the eigenvectors and eigenvalues, the precise construction of the embedding) are therefore incomplete. This makes it impossible to fully understand or reproduce the method.
- **Why it matters** A computational method must be described with sufficient precision to be implemented by others. Missing equations and variable definitions undermine reproducibility and the ability to assess the mathematical claims.
- **Resolution test** Provide the complete methods section with all equations explicitly displayed and all variables defined. The derivation of the rank-2 property and the equivalence of the distance metrics should be shown step by step.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Statistical rigor
- **Claim pointer** The manuscript reports that intra-subcompartment contacts are significantly stronger than inter-subcompartment contacts (one-sided P < 5 x 10^-142) and that variable loci exhibit significantly greater transcriptional variability than stable loci (P = 7 x 10^-6), among other statistical claims.
- **Evidence pointer** Sections 3.1, 3.2; location not provided
- **Concern** The statistical methods used to compute the reported P-values are not described. It is unclear what test was used, how multiple testing was handled, whether the tests account for the spatial autocorrelation inherent in genomic data, and whether the reported P-values are corrected for the number of comparisons performed. The extremely small P-value reported for the contact enrichment analysis raises questions about the effective sample size and whether the test is appropriate for the data structure.
- **Why it matters** Without a clear description of the statistical framework, the reported significance levels cannot be interpreted, and the robustness of the biological conclusions is uncertain.
- **Resolution test** Describe the statistical tests used for each comparison, including the null model, the test statistic, the handling of multiple testing, and any corrections for spatial or technical covariates. Justify the choice of tests given the data structure.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Comparison fairness
- **Claim pointer** The manuscript claims that scSTEC performs comparably to scGHOST and outperforms it in interpretability and computational cost, and that direct clustering on the 2D representation performed worse than the scGHOST framework on simulated datasets.
- **Evidence pointer** Supplementary Figures S1, S22; location not provided
- **Concern** The comparison with scGHOST is described only in terms of final performance metrics. It is unclear whether both methods were evaluated under identical conditions, including the same input data, the same preprocessing, the same evaluation metrics, and the same computational resources. The claim that scSTEC is markedly faster than CPU-based scGHOST is presented without details on the benchmarking setup, such as hardware, data size, and whether both methods were optimized to a comparable degree.
- **Why it matters** Fair benchmarking is essential for claims of comparable performance and improved efficiency. Differences in implementation, optimization, or evaluation protocols could bias the comparison.
- **Resolution test** Provide a detailed description of the benchmarking protocol, including hardware, software versions, input data, preprocessing steps, evaluation metrics, and the number of runs. Discuss any differences in how the two methods were implemented or optimized.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Biological validation depth
- **Claim pointer** The manuscript claims that subcompartments identified by scSTEC show consistent associations with gene expression and epigenetic profiles, and that developmental dynamics are captured in embryonic and olfactory neuron datasets.
- **Evidence pointer** Sections 3.3-3.5, Figures 4A-E, 5A-C; location not provided
- **Concern** The biological validations are described at a high level, but the specific analyses are not detailed. For example, it is unclear how "consistent associations" were defined, what the effect sizes were, whether the associations were compared against a null model, and whether the developmental trajectories were statistically supported. The claim that subcompartment changes precede transcriptional changes for 40% of genes is a strong temporal claim that requires careful analysis of the temporal resolution and the statistical framework used to establish ordering.
- **Why it matters** The biological relevance of the method is a key part of the paper's contribution. Without detailed descriptions of the validation analyses, the strength of the biological claims cannot be evaluated.
- **Resolution test** Provide detailed descriptions of the biological validation analyses, including the statistical models, the definition of "consistent association," the handling of multiple testing, and the methods used to establish temporal ordering in the developmental analyses.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Section 2.1, definition of the 2D representation
- **Evidence pointer** Section 2.1; location not provided
- **Issue** The text states that the representation is defined by equations that are not shown. The intuitive description is helpful but insufficient for understanding the exact construction.
- **Required correction** Display all equations in full and provide a brief numerical example or schematic to illustrate the construction of the representation and embedding.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Parameter justification
- **Affected element** Section 2.1, choice of top and bottom 30% of bins by CpG density
- **Evidence pointer** Section 2.1; location not provided
- **Issue** The choice of 30% thresholds for defining CpG-high and CpG-low bins appears arbitrary. No sensitivity analysis is described.
- **Required correction** Provide a sensitivity analysis for this parameter or justify the choice based on prior work or data-driven criteria.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Methodological detail
- **Affected element** Section 2.2, labeling of clusters by CpG density
- **Evidence pointer** Section 2.2; location not provided
- **Issue** The labeling of the five clusters as A1, A2, B1, B2, and B3 based on decreasing mean CpG density is described, but it is unclear how this labeling relates to the canonical subcompartment definitions from bulk Hi-C data, which are based on chromatin marks and replication timing.
- **Required correction** Clarify the relationship between CpG-density-based labeling and the canonical subcompartment definitions, and discuss any potential discrepancies.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Quality control
- **Affected element** Section 2.3, quality control thresholds
- **Evidence pointer** Section 2.3; location not provided
- **Issue** The quality control thresholds (sparsity above 0.98, fewer than 3,000 total contacts) are described as empirical and based on LiMCA data. It is unclear how sensitive the results are to these thresholds.
- **Required correction** Provide a sensitivity analysis for the QC thresholds or discuss how the choice of thresholds affects the fraction of cells retained and the downstream results.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Data availability statement
- **Evidence pointer** Data availability section; location not provided
- **Issue** The data availability statement indicates that all data are publicly available, but the specific accession numbers or URLs for each dataset are not listed in the provided text.
- **Required correction** List the specific accession numbers or URLs for each dataset used in the study.

- **Concern ID** R1-m6
- **Severity** Minor
- **Axis** Terminology
- **Affected element** Abstract and Introduction, "direct" annotation
- **Evidence pointer** Abstract, Section 1; location not provided
- **Issue** The term "direct" is used to describe the annotation approach, but the method still involves multiple steps (representation, embedding, clustering, labeling, consensus). The contrast with scGHOST is clear, but the term "direct" may overstate the simplicity.
- **Required correction** Consider rephrasing to "annotation from the individual cell's own contact matrix without imputation or cross-cell information" to avoid ambiguity.

- **Technical failings that need to be addressed before the case is established**
  - R1-M1 (missing figures and supplementary materials) must be resolved by providing all visual and quantitative results.
  - R1-M2 (missing equations) must be resolved by providing the complete mathematical formulation.
  - R1-M3 (statistical methods) must be resolved by describing the statistical framework for all reported P-values.

- **Assessment against Nature-style criteria**
  - Originality: The observation of the rank-2 structure in scGHOST's estimated inter-chromosomal matrix and its exploitation for direct two-dimensional embedding is a novel contribution. The idea of per-cell independent annotation without imputation is a meaningful conceptual shift from existing approaches. However, the originality is somewhat tempered by the fact that the method builds directly on scGHOST's framework and uses established techniques (CpG density, K-means clustering, consensus across references).
  - Scientific importance: The problem of subcompartment annotation from scHi-C data is of growing importance as single-cell chromatin conformation technologies become more widespread. A method that is interpretable, computationally efficient, and does not require cross-cell information could be valuable for the community. However, the importance depends on whether the performance claims hold up under scrutiny, which cannot be assessed from the provided material.
  - Interdisciplinary readership: The manuscript is likely to appeal primarily to computational biologists and bioinformaticians. The biological applications (cell-type resolution, developmental dynamics) may attract some interest from experimental biologists, but the presentation is method-centric and the biological findings are presented as validations rather than discoveries. The interdisciplinary reach is therefore moderate.
  - Technical soundness: The mathematical derivation of the rank-2 property and the equivalence of distance metrics is a strength, but the incomplete presentation of equations prevents full evaluation. The benchmarking strategy is broad, but the missing figures and lack of statistical detail undermine confidence. The use of multiple real datasets across species and contexts is commendable.
  - Readability for nonspecialists: The abstract and introduction are accessible and clearly motivate the problem. The methods section is more technical and would be challenging for nonspecialists, but this is expected for a computational methods paper. The discussion is clear and appropriately contextualizes the findings.

- **Recommendation posture** Currently not established from the provided evidence. The manuscript presents a potentially interesting and useful method, and the conceptual contribution is sound. However, the absence of all figures, supplementary materials, and key equations makes it impossible to verify the central claims of comparable performance, robustness, and biological validity. The statistical framework is also insufficiently described. The authors should be invited to resubmit a complete version of the manuscript with all figures, equations, and statistical details, at which point a full assessment can be made.

## Risk / unsupported claims
- The claim that scSTEC achieves subcompartment annotations comparable to scGHOST is unsupported without the benchmarking figures and quantitative results.
- The claim that scSTEC remains robust under severe data sparsity is unsupported without the simulation results.
- The claim that scSTEC-derived subcompartments show consistent associations with gene expression and epigenetic profiles is unsupported without the relevant figures and statistical analyses.
- The claim that subcompartment changes precede transcriptional changes for a subset of genes is unsupported without the temporal analysis details.
- The mathematical derivation of the rank-2 property and the equivalence of distance metrics is referenced but not shown, making it unverifiable.
- The claim of markedly reduced computational cost relative to scGHOST is unsupported without benchmarking details.
- The generalizability of the CpG-density-based labeling to diverse cell types and species is asserted but not systematically evaluated in the provided text.