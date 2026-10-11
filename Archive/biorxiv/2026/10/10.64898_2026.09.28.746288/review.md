## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no figures, tables, methods, or supplementary materials were provided
- **Shared manuscript claim summary** The authors present Kidzoi, a kidney cell-type-specific sequence-to-function deep learning model derived via transfer learning from the pretrained Borzoi model using single-nucleus chromatin accessibility data from human kidney tissue. They claim accurate cell-type-specific chromatin accessibility prediction, 10–23% improvement in regulatory variant effect prediction over existing models, effective prioritization of kidney function GWAS fine-mapped causal variants with cell-type resolution, sufficiency of a 32–64 kbp local flanking context for variant effect prediction, and comparable performance of a multi-task model at reduced computational cost.
- **Visible evidence base** Abstract text only; no quantitative results, performance metrics, model architecture details, or validation procedures are provided
- **Missing materials affecting confidence** Full manuscript, all figures and tables, methods section, model training and evaluation details, dataset descriptions, baseline model specifications, statistical analyses, and any supplementary information

## Reviewer
- **Overall assessment** The abstract presents a potentially valuable contribution to the field of regulatory genomics by addressing the cell-type specificity gap in existing sequence-to-function models. The transfer learning approach from Borzoi to kidney tissue is conceptually sound and timely. However, the abstract lacks sufficient quantitative detail to evaluate the robustness of the claimed improvements, the validity of the benchmarking procedures, and the generalizability of the findings. The core claims are plausible but currently not verifiable from the provided material.
- **Who would be interested in the results, and why** Researchers in regulatory genomics, computational biology, and kidney disease genetics would find these results relevant. Those working on variant effect prediction for clinical interpretation, particularly in the context of kidney function and chronic kidney disease, would benefit from a cell-type-specific model. Additionally, the transfer learning framework and the multi-task efficiency analysis would interest method developers in the deep learning for genomics community.
- **Major strengths** The problem addressed is well-defined and important, as existing S2F models lack cell-type specificity. The transfer learning strategy is pragmatic and leverages existing resources. The focus on kidney function GWAS variants provides a clinically relevant application. The ablation analysis of flanking sequence context addresses a practical question about model input requirements. The multi-task efficiency comparison is a useful practical consideration.
- **Major Concerns** 
  - R1-M1
  - R1-M2
  - R1-M3
  - R1-M4
- **Minor Comments** 
  - R1-m1
  - R1-m2
  - R1-m3
  - R1-m4
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3
- **Assessment against Nature-style criteria** Originality is moderate to high, as transfer learning for cell-type-specific S2F models is a relatively underexplored direction, though the approach builds directly on existing models. Scientific importance is potentially high given the relevance to kidney disease genetics and variant interpretation, but the magnitude of the claimed improvements needs rigorous validation. Interdisciplinary readership is plausible, spanning genomics, nephrology, and computational biology. Technical soundness cannot be fully assessed from the abstract alone, but the described methodology is reasonable in principle. Readability for nonspecialists is adequate, though some terms such as "sequence-to-function" and "fine-mapped causal variants" may require additional context in the full manuscript.
- **Recommendation posture** Currently not established from the provided evidence. The abstract describes a promising approach, but the absence of quantitative results, benchmarking details, and validation procedures prevents a definitive assessment. Supportive if technical concerns are resolved in the full manuscript.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "Kidzoi accurately predicts cell-type-specific chromatin accessibility and improves regulatory variant effect prediction by 10–23% over existing models."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The abstract claims a 10–23% improvement in variant effect prediction but provides no details on the evaluation metrics, baseline models compared, the number of variants tested, or the statistical significance of these improvements. The range of 10–23% is wide, and it is unclear whether this reflects variability across cell types, datasets, or evaluation settings.
- **Why it matters** Without knowing the exact benchmarking protocol, the reader cannot assess whether the improvement is consistent, meaningful, or potentially driven by favorable evaluation choices. The credibility of the central claim depends on transparent and rigorous benchmarking.
- **Resolution test** Provide in the full manuscript the specific evaluation metrics (e.g., AUROC, AUPRC), the list of baseline models, the number and source of test variants, confidence intervals, and statistical tests for the reported improvement range.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Validation rigor
- **Claim pointer** "Kidzoi effectively prioritizes genome-wide association study (GWAS) fine-mapped causal variants associated with kidney function (estimated glomerular filtration rate based on both creatinine and cystatin C; eGFRcr-cys) while resolving their cell-type specificity."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim of effective prioritization of fine-mapped causal variants lacks any quantitative support. No metrics such as enrichment scores, recall at fixed precision, or comparison to null models are provided. The claim of resolving cell-type specificity is also unsupported without showing how cell-type assignments were validated.
- **Why it matters** Prioritization of causal variants is a key translational application. Without quantitative evidence, the reader cannot determine whether the model adds value over existing tools or whether the cell-type resolution is biologically meaningful rather than an artifact of the training data.
- **Resolution test** Include in the full manuscript enrichment analyses against fine-mapped variants, comparison to baseline models, calibration of posterior probabilities, and validation of cell-type assignments using independent functional data.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical completeness
- **Claim pointer** "Systematic ablation of flanking sequence indicates that a local context of 32–64 kbp, representing only 6–12% of the full model input, is sufficient for accurate variant effect prediction."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The ablation analysis is described only in summary form. No details are given on how the ablation was performed, which variants were used, how accuracy was measured, or how the 32–64 kbp window was determined. The claim that this context is "sufficient" requires a clear definition of the accuracy threshold used.
- **Why it matters** This finding has practical implications for model design and computational efficiency. However, without methodological detail, the result cannot be reproduced or evaluated for robustness across different variant types and genomic contexts.
- **Resolution test** Provide a detailed description of the ablation procedure, the accuracy metric and threshold, the number and type of variants tested, and sensitivity analyses to confirm the stability of the 32–64 kbp finding.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Comparative analysis
- **Claim pointer** "A multi-task model achieves comparable performance to single-task models at a substantially reduced computational cost."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The comparison between multi-task and single-task models is stated without quantitative results. The degree of performance difference and the extent of computational savings are not specified.
- **Why it matters** This claim has practical implications for resource allocation in model training. Without numbers, the reader cannot judge whether the trade-off between performance and efficiency is acceptable for their use case.
- **Resolution test** Report performance metrics for both model types across all evaluated tasks, along with training time, memory usage, and inference speed, to substantiate the claim of comparable performance and reduced cost.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Terminology
- **Evidence pointer** Abstract; location not provided
- **Issue** The term "sequence-to-function (S2F)" is used without a brief definition. While specialists may be familiar with it, nonspecialist readers may benefit from a one-sentence explanation.
- **Required correction** Add a brief parenthetical definition of S2F models in the introduction of the abstract or the full manuscript.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Data availability
- **Evidence pointer** Abstract; location not provided
- **Issue** The abstract does not mention whether the model, code, and training data will be made publicly available.
- **Required correction** State in the full manuscript the availability of the model weights, source code, and processed data to enable reproducibility.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Context
- **Affected element** Related work
- **Evidence pointer** Abstract; location not provided
- **Issue** The abstract does not specify which existing models were used as baselines for the 10–23% improvement claim, beyond the general reference to "existing models."
- **Required correction** Name the specific baseline models in the full manuscript and justify their selection.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Generalizability
- **Affected element** Scope
- **Evidence pointer** Abstract; location not provided
- **Issue** The abstract focuses exclusively on kidney tissue. It is unclear whether the transfer learning approach would generalize to other tissues or disease contexts.
- **Required correction** Discuss in the full manuscript the potential generalizability of the approach and any limitations specific to kidney tissue.

## Risk / unsupported claims
- The 10–23% improvement in variant effect prediction is unsupported without benchmarking details.
- The claim of effective prioritization of fine-mapped causal variants is unsupported without quantitative enrichment or calibration metrics.
- The sufficiency of 32–64 kbp flanking context is unsupported without ablation methodology and accuracy thresholds.
- The comparable performance of the multi-task model is unsupported without specific performance and efficiency numbers.
- The claim of resolving cell-type specificity of variants is not verifiable from the abstract alone.