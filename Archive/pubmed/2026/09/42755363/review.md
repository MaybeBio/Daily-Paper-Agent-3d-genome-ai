## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no methods, figures, tables, or supplementary materials were provided
- **Shared manuscript claim summary** The authors present GenoME, a Mixture of Experts based generative model that integrates DNA sequence and cell-type-specific ATAC-seq signals to predict unified genomic profiles including epigenomics, transcriptomics, and chromatin architecture. The model is claimed to generalize to unseen or individualized cell types from a single ATAC-seq input, support in silico perturbation for forecasting multimodal consequences of genetic perturbations, identify functional enhancer-promoter connections with performance exceeding Activity-by-Contact, and enable deciphering of transcription factor grammar in cell-type-specific enhancers.
- **Visible evidence base** Abstract text only; no quantitative results, benchmark details, model architecture descriptions, or validation procedures are available
- **Missing materials affecting confidence** Full manuscript, methods section, all figures and tables, supplementary information, benchmark definitions, statistical analyses, and code or data availability statements

## Reviewer
- **Overall assessment** The abstract describes an ambitious and potentially valuable framework for integrative modeling of the regulatory genome. The scope of outputs, from epigenomics to chromatin architecture, and the claimed cross-cell-type generalization are scientifically compelling. However, the abstract provides no quantitative evidence, no comparison details, and no methodological specifics. The core claims, particularly those of outperforming specialized models and achieving accurate perturbation forecasting, cannot be evaluated from the supplied material. The work may be of interest to computational genomics and regulatory biology communities, but the current evidence base is insufficient to establish the case.
- **Who would be interested in the results, and why** Computational biologists developing generative models for genomics, researchers studying gene regulation and chromatin architecture, and experimentalists seeking in silico tools for perturbation prioritization and enhancer-promoter mapping would find this work relevant. The promise of predicting full regulatory landscapes from a single ATAC-seq experiment could appeal to those working on rare or difficult-to-profile cell types.
- **Major strengths** The proposed framework addresses a recognized gap in integrative modeling of multiscale regulatory outputs. The emphasis on cross-cell-type generalization from a single input modality is a practical and forward-looking design goal. The inclusion of an in silico perturbation component with causal interpretation potential adds translational relevance.
- **Major Concerns**  
  - R1-M1  
  - R1-M2  
  - R1-M3  
  - R1-M4
- **Minor Comments**  
  - R1-m1  
  - R1-m2  
  - R1-m3
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4
- **Assessment against Nature-style criteria** Originality is potentially high given the integration of multiple output modalities within a single generative framework, but this cannot be confirmed without methodological details. Scientific importance is plausible for regulatory genomics, yet the abstract does not demonstrate impact through quantitative outcomes. Interdisciplinary readership is likely, spanning machine learning and molecular biology, but the abstract lacks sufficient technical transparency for either audience to assess rigor. Technical soundness is not assessable from the abstract alone. Readability for nonspecialists is adequate in terms of prose clarity, though the density of domain terms may limit accessibility.
- **Recommendation posture** Currently not established from the provided evidence. The claims are scientifically interesting but require full manuscript review with quantitative results and methodological detail before a supportive posture can be considered.

### Major Concerns

- **Concern ID** R1-M1  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Evidence sufficiency  
- **Claim pointer** GenoME predicts a unified genomic profile encompassing epigenomics, transcriptomics, and chromatin architecture at base-pair to kilobase resolutions.  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The abstract asserts multiscale predictive capability across three distinct data modalities but provides no performance metrics, no resolution benchmarks, and no comparison to existing integrative models.  
- **Why it matters** Without quantitative evidence of prediction accuracy across each modality and resolution scale, the central capability claim is unverifiable.  
- **Resolution test** Provide in the full manuscript prediction accuracy metrics, such as correlation or AUROC, for each modality against held-out experimental data, with resolution-specific breakdowns.

- **Concern ID** R1-M2  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Generalization validity  
- **Claim pointer** GenoME generalizes to predict the full regulatory landscape of unseen or individualized cell types from a single ATAC-seq input.  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The claim of cross-cell-type generalization is central to the work, but the abstract does not specify how unseen cell types are defined, what training and test splits were used, or how performance on unseen cell types compares to seen cell types.  
- **Why it matters** Generalization to unseen cell types is a strong claim that requires careful evaluation to rule out trivial solutions, such as reliance on sequence-only features or leakage from similar cell types in training.  
- **Resolution test** Describe the cell-type split strategy, report performance on held-out cell types, and include ablation analyses that isolate the contribution of ATAC-seq signals versus sequence features.

- **Concern ID** R1-M3  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Comparative rigor  
- **Claim pointer** GenoME outperforms specialized models like Activity-by-Contact in identifying functional enhancer-promoter connections.  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The abstract states superiority over Activity-by-Contact without presenting any comparative metrics, statistical tests, or dataset descriptions.  
- **Why it matters** Outperformance claims require rigorous benchmarking on standardized datasets with appropriate significance testing to be credible.  
- **Resolution test** Provide benchmark datasets, evaluation metrics, and statistical significance results for comparisons against Activity-by-Contact and other relevant baselines.

- **Concern ID** R1-M4  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Perturbation validity  
- **Claim pointer** GenoME accurately forecasts the multimodal consequences of genetic perturbations.  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The perturbation forecasting claim implies causal predictive ability, but the abstract provides no details on how perturbations are simulated, what validation against experimental perturbation data was performed, or what accuracy was achieved.  
- **Why it matters** Causal claims in silico require validation against independent experimental perturbation datasets to establish reliability.  
- **Resolution test** Describe the perturbation framework, validate against published perturbation experiments, and report concordance metrics such as correlation or enrichment of predicted versus observed changes.

### Minor Comments

- **Concern ID** R1-m1  
- **Severity** Minor  
- **Axis** Clarity  
- **Affected element** Model input description  
- **Evidence pointer** Abstract; location not provided  
- **Issue** The abstract states the model uses DNA sequence and ATAC-seq signals but does not clarify whether ATAC-seq is used as a continuous signal or as peak calls, nor how sequence context is encoded.  
- **Required correction** Specify input representations in the methods section.

- **Concern ID** R1-m2  
- **Severity** Minor  
- **Axis** Interpretability  
- **Affected element** Transcription factor grammar claim  
- **Evidence pointer** Abstract; location not provided  
- **Issue** The claim of deciphering transcription factor grammar is vague and lacks definition of what grammar means in this context.  
- **Required correction** Define the specific grammar features extracted and how they are validated.

- **Concern ID** R1-m3  
- **Severity** Minor  
- **Axis** Reproducibility  
- **Affected element** Resource availability  
- **Evidence pointer** Abstract; location not provided  
- **Issue** No mention of code or data availability, which is essential for reproducibility.  
- **Required correction** Include a data and code availability statement in the full manuscript.

## Risk / unsupported claims
- The claim of outperforming Activity-by-Contact is unsupported by any comparative data in the abstract.
- The claim of accurate perturbation forecasting is unsupported by any validation evidence in the abstract.
- The claim of cross-cell-type generalization to unseen cell types is unsupported by any evaluation details in the abstract.
- The claim of predicting unified genomic profiles at base-pair to kilobase resolutions is unsupported by any resolution-specific performance metrics in the abstract.
- The claim of deciphering transcription factor grammar is unsupported by any methodological or validation details in the abstract.