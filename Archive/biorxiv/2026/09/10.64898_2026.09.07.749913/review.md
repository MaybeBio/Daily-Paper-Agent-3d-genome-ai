## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no methods, figures, tables, or supplementary materials were provided
- **Shared manuscript claim summary** The authors present TransBind2, a deep learning model that predicts transcription factor (TF)–DNA binding by integrating DNA sequence, DNase-seq accessibility, genome mappability, and TF sequence and structure via a bidirectional cross-attention mechanism. The model is framed as binary classification of individual <DNA bin, TF, cell type> triplets. Reported performance includes a macro AUROC of 0.9648 and AUPR of 0.4215 across 690 human ChIP-seq experiments (161 TFs, 91 cell types), a ≥12.67% relative AUPR improvement over baselines, cross-species zero-shot transfer to mouse data, saliency-based peak identification with median error of 12–38 bp, and ablation studies supporting the contribution of TF structure, chromatin accessibility, and bidirectional attention.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or supplementary data were supplied
- **Missing materials affecting confidence** Full methods, model architecture details, training and evaluation protocols, baseline descriptions, statistical significance tests, ablation results, saliency analysis methodology, cross-species evaluation details, and all quantitative results beyond those stated in the abstract

## Reviewer
- **Overall assessment** The abstract describes a plausible and potentially valuable extension of a prior model, with a clear motivation and a set of design choices that are well aligned with current trends in TF–DNA binding prediction. However, the evidence base available for this review is limited to the abstract, which prevents verification of the core claims. Several claims are stated without supporting detail, and the performance metrics, while strong, cannot be assessed for statistical validity, generalizability, or comparability without the underlying methods and results. The work is likely of interest to the computational genomics community, but the case is not fully established from the supplied material.
- **Who would be interested in the results, and why** Computational biologists and bioinformaticians working on regulatory genomics, TF binding site prediction, and deep learning applications to genomics. Researchers developing multimodal models that integrate sequence, chromatin state, and protein structure would also find the approach relevant. The cross-species zero-shot result may appeal to those studying model transferability across organisms.
- **Major strengths** The abstract clearly identifies a limitation in existing models (overreliance on DNA sequence) and proposes a concrete multimodal solution. The inclusion of TF structure via a protein language model and bidirectional cross-attention is a thoughtful design choice. The evaluation across a large number of ChIP-seq experiments and the reported cross-species generalization are notable. The saliency analysis, despite window-level training, suggests the model may learn positionally informative features.
- **Major Concerns**  
  - **Concern ID** R1-M1  
    **Severity** Major  
    **Blocking** Yes  
    **Axis** Technical soundness  
    **Claim pointer** The model achieves a macro AUROC of 0.9648 and AUPR of 0.4215, outperforming TransBind and other baselines with a ≥12.67% relative AUPR gain.  
    **Evidence pointer** Abstract only; location not provided  
    **Concern** The abstract reports aggregate performance metrics but does not describe the evaluation protocol, the number of train/test splits, the nature of the baselines, or whether the reported gains are statistically significant. Without these details, the performance claims cannot be independently assessed.  
    **Why it matters** The central claim of the paper is that TransBind2 outperforms existing methods. If the evaluation is not rigorous or the baselines are not comparable, the reported gains may be misleading.  
    **Resolution test** Provide a detailed description of the evaluation setup, including data partitioning, baseline configurations, and statistical tests (e.g., confidence intervals or significance testing across replicates).  
  - **Concern ID** R1-M2  
    **Severity** Major  
    **Blocking** Yes  
    **Axis** Technical soundness  
    **Claim pointer** The model generalizes to new TFs and cell types via binary classification of individual <DNA bin, TF, cell type> triplets.  
    **Evidence pointer** Abstract only; location not provided  
    **Concern** The abstract claims generalization to new TFs and cell types, but no results are shown for held-out TFs or cell types. The cross-species zero-shot result on mouse data is mentioned, but it is unclear whether this constitutes evidence for generalization to unseen human TFs or cell types.  
    **Why it matters** Generalization to unseen factors and contexts is a key stated advantage of the framing. Without explicit evaluation on held-out TFs and cell types, this claim is unsupported.  
    **Resolution test** Include results from experiments where TFs and cell types are held out during training and report performance on those held-out sets.  
  - **Concern ID** R1-M3  
    **Severity** Major  
    **Blocking** Yes  
    **Axis** Technical soundness  
    **Claim pointer** Saliency analysis identifies TF-binding peaks with a median error of 12–38 bp despite window-level training.  
    **Evidence pointer** Abstract only; location not provided  
    **Concern** The saliency analysis is described in a single sentence. The method for deriving peak positions from saliency maps, the definition of error, and the range of the reported median error are not specified. It is also unclear how this result compares to existing peak-calling methods or whether it is a meaningful contribution.  
    **Why it matters** This claim suggests the model has fine-grained positional accuracy, which would be a notable result. Without methodological detail, the claim cannot be evaluated.  
    **Resolution test** Describe the saliency-based peak identification procedure, define the error metric, and provide a comparison to standard peak-calling approaches.  
  - **Concern ID** R1-M4  
    **Severity** Major  
    **Blocking** No  
    **Axis** Reproducibility  
    **Claim pointer** The model uses a biomodal protein language model (ProstT5) to capture both TF sequence and structure.  
    **Evidence pointer** Abstract only; location not provided  
    **Concern** The abstract does not specify how TF structure is represented or how ProstT5 is used. It is unclear whether the model uses predicted structures, experimental structures, or a structural latent space.  
    **Why it matters** The contribution of TF structure is a central design element. Without clarity on the structural input, the method cannot be reproduced or compared to other structure-aware approaches.  
    **Resolution test** Provide details on the structural data source, the ProstT5 embedding procedure, and how structure is integrated into the cross-attention mechanism.
- **Minor Comments**  
  - **Concern ID** R1-m1  
    **Severity** Minor  
    **Axis** Clarity  
    **Affected element** Abstract wording  
    **Evidence pointer** Abstract; location not provided  
    **Issue** The term "biomodal protein language model" appears to be a typo or nonstandard phrasing. The intended term is likely "bimodal."  
    **Required correction** Replace "biomodal" with "bimodal" or clarify the intended meaning.  
  - **Concern ID** R1-m2  
    **Severity** Minor  
    **Axis** Completeness  
    **Affected element** Ablation summary  
    **Evidence pointer** Abstract; location not provided  
    **Issue** The ablation studies are summarized in one sentence without quantitative results. The relative contribution of each component is not reported.  
    **Required correction** Provide the ablation results in the abstract or indicate where they are presented in the full manuscript.  
  - **Concern ID** R1-m3  
    **Severity** Minor  
    **Axis** Clarity  
    **Affected element** Performance metric  
    **Evidence pointer** Abstract; location not provided  
    **Issue** The abstract reports macro AUROC and AUPR but does not define the averaging procedure or the class balance.  
    **Required correction** Define "macro" in this context and describe the class distribution in the evaluation set.
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4
- **Assessment against Nature-style criteria**  
  - Originality: The combination of TF structure, chromatin accessibility, and bidirectional cross-attention is a reasonable extension of prior work, but the abstract does not clearly differentiate TransBind2 from other multimodal models in the field. The originality is moderate.  
  - Scientific importance: Accurate TF–DNA binding prediction is a longstanding problem in regulatory genomics, and improvements in generalization and positional accuracy would be valuable. The potential importance is high, but it is not yet demonstrated.  
  - Interdisciplinary readership: The work is primarily of interest to computational biologists and machine learning researchers. The abstract is written in a way that is accessible to these groups, but the broader biological significance is not articulated.  
  - Technical soundness: The technical claims cannot be assessed from the abstract alone. The evaluation protocol, structural input, and saliency methodology are not described in sufficient detail.  
  - Readability for nonspecialists: The abstract is concise and generally clear, but terms such as "mappability tracks" and "biomodal" may be unclear to nonspecialists. The abstract does not explain the biological relevance of the results in accessible terms.
- **Recommendation posture** Currently not established from the provided evidence. The abstract presents a promising approach, but the core claims regarding performance, generalization, and positional accuracy require the full manuscript for verification. The review is supportive in principle, provided the technical concerns are resolved.

## Risk / unsupported claims
- The claim of outperforming TransBind and other baselines with a ≥12.67% relative AUPR gain is unsupported without details on baselines, evaluation protocol, and statistical significance.
- The claim of generalization to new TFs and cell types is unsupported without held-out evaluation results.
- The claim of identifying TF-binding peaks with a median error of 12–38 bp is unsupported without methodological detail.
- The cross-species zero-shot performance on mouse data is mentioned but not quantified, making it unassessable.
- The ablation study claims are unquantified and cannot be evaluated.