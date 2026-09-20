## Review setup
- **Input scope** Full manuscript text including summary, introduction, results and discussion, methods, and supplemental information descriptions
- **Assessment boundary** Methodological soundness, validation rigor, biological claims, and reproducibility of the DeepDive framework as presented
- **Shared manuscript claim summary** The authors present DeepDive, a deep-learning framework for disentangling known and unknown sources of variation in single-nucleus ATAC-seq data, with capabilities for counterfactual prediction and covariate effect estimation, validated on simulated and real datasets including a pancreatic islet application nominating transcription factors linked to type 2 diabetes
- **Visible evidence base** Main text figures 1 and 2, methods section, simulation framework description, benchmarking details, and supplemental figure/table descriptions
- **Missing materials affecting confidence** Supplemental figures S1–S6, Note S1, Tables S1–S3, and the full code repository were not provided for review; detailed model architecture specifics are deferred to Note S1

## Reviewer
- **Overall assessment** The manuscript presents a timely and potentially valuable framework for addressing multicollinearity in single-cell epigenomic data, a problem of growing importance as cohort-scale atlases become common. The dual-network architecture combining adversarial learning with a conditional variational autoencoder is conceptually sound, and the application to pancreatic islet cells demonstrates practical utility. However, the provided evidence base is incomplete, with key validation details and architectural specifics relegated to supplemental materials that were not available for review. The claims of superiority over existing methods require closer scrutiny given the limited comparative analysis presented, and the biological conclusions, while plausible, rest on assumptions about disentanglement quality that are not fully established from the visible evidence.
- **Who would be interested in the results, and why** Computational biologists developing methods for single-cell epigenomic analysis, researchers working on cohort-scale atlases (e.g., human cell atlas projects) who face multicollinearity challenges, and investigators studying pancreatic islet biology and type 2 diabetes mechanisms. The counterfactual prediction capability would also interest methodologists working on causal inference in genomics.
- **Major strengths** The problem addressed is well-motivated and practically important. The dual-network architecture is a thoughtful design choice that explicitly separates known and unknown variation. The multi-decoder framework for uncertainty quantification is a useful innovation. The application to pancreatic islets provides a concrete demonstration of biological utility, and the integration with human genetics and functional data (GSIS, eQTL colocalization) strengthens the biological claims. The framework is designed to be user-friendly with accessible documentation.
- **Major Concerns** See detailed items below.
- **Minor Comments** See detailed items below.
- **Technical failings that need to be addressed before the case is established** R1-M1 (incomplete validation evidence), R1-M2 (insufficient comparative analysis), R1-M3 (unclear biological validation logic), R1-M4 (limited real-data disentanglement validation)
- **Assessment against Nature-style criteria** **Originality**: The approach of combining adversarial learning with conditional VAEs for covariate disentanglement in single-cell epigenomics is a novel contribution, though it builds on established concepts from representation learning. The counterfactual prediction capability for epigenomic data is a distinctive feature. **Scientific importance**: The problem of multicollinearity in cohort-scale single-cell studies is significant and growing, making this a potentially important methodological contribution. The pancreatic islet application addresses questions of direct relevance to diabetes research. **Interdisciplinary readership**: The work bridges computational methodology, epigenomics, and diabetes biology, with potential appeal across these communities. However, the presentation assumes substantial familiarity with deep learning concepts and single-cell analysis, which may limit accessibility. **Technical soundness**: The core architecture is reasonable, but the visible evidence is insufficient to fully assess technical soundness. Key details are deferred to supplemental materials, and the comparative analysis is limited. The simulation framework is described but its validation properties are not fully demonstrated. **Readability for nonspecialists**: The main text is generally clear, but the methods section is dense and assumes significant background knowledge. The biological application section is more accessible than the methodological sections.
- **Recommendation posture** Supportive if technical concerns are resolved. The framework addresses an important problem with a plausible approach, but the current evidence base is insufficient to fully establish the claims. The authors should provide the complete supplemental materials, strengthen the comparative analysis, and clarify the biological validation logic.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence completeness
- **Claim pointer** The manuscript claims DeepDive "accurately reconstructs chromatin accessibility, outperforms state-of-the-art methods with incomplete covariate information, and robustly recovers true biological signals from even highly entangled covariates"
- **Evidence pointer** Figures 1B–1H, S1–S5; location not provided for supplemental figures
- **Concern** The central performance claims are supported primarily by supplemental figures and tables that were not included in the review materials. Figure 1B shows reconstruction quality on one dataset, but the quantitative comparisons, ablation studies, and robustness analyses are all in the supplemental materials. The claim of outperforming state-of-the-art methods is only partially visible in the main text, with the full benchmarking results deferred to Table S1 and Figures S4–S5.
- **Why it matters** The core contribution of the manuscript is the claimed performance advantage of DeepDive. Without access to the full validation evidence, it is impossible to assess whether these claims are justified. The review process requires transparency in the evidence base.
- **Resolution test** Provide the complete supplemental materials including all figures and tables for review. The authors should ensure that all performance claims in the main text are directly supported by visible evidence or clearly referenced to accessible supplemental content.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Comparative analysis
- **Claim pointer** The manuscript claims DeepDive "outperforms state-of-the-art methods with incomplete covariate information"
- **Evidence pointer** Figures 1D–1E, S4–S5; location not provided for supplemental figures
- **Concern** The comparative analysis against existing methods is limited in the visible text. The benchmarking appears to focus primarily on differential accessibility detection (Figure 1D) and average precision under multicollinearity (Figure 1E), but the comparison set is not clearly enumerated in the main text. The integration benchmarking (Figure 1F) compares against several methods, but the results are only summarized as an average metric. The claim of superiority requires a more comprehensive and transparent comparison.
- **Why it matters** The field has multiple established methods for single-cell epigenomic analysis, and the claim of superiority is a key selling point. A limited or unclear comparison undermines confidence in this claim and does not provide the community with sufficient information to choose between methods.
- **Resolution test** Clearly enumerate all methods compared, provide full benchmarking results in the main text or accessible supplemental materials, and discuss the criteria for method selection. The authors should also address potential confounders in the comparison, such as differences in preprocessing or hyperparameter tuning.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Biological validation logic
- **Claim pointer** The manuscript claims that counterfactual prediction "nominates high-confidence transcriptional regulators" and that supported regulators are "more enriched among proteins linked to type 2 diabetes through genetic evidence" and "correlated with glucose-stimulated insulin secretion"
- **Evidence pointer** Figures 2D–2F, S6G; location not provided for supplemental figures
- **Concern** The logic of the "supported" versus "unsupported" classification for transcription factors is unclear. The manuscript states that motifs reversing the beta-subtype effect in T2D-to-ND counterfactuals are "supported," but the biological rationale for this classification is not fully explained. Specifically, it is not clear why a transcription factor whose activity difference between beta subtypes is reversed in the counterfactual should be considered "supported" rather than simply reflecting the expected direction of the diabetes effect. The enrichment analyses in Figures 2E–2F compare supported versus unsupported factors, but the baseline expectation is not clearly defined.
- **Why it matters** The biological conclusions are a major component of the manuscript's significance. If the validation logic is circular or the classification scheme is arbitrary, the biological claims are weakened. The enrichment results could reflect the classification scheme rather than genuine biological signal.
- **Resolution test** Provide a clear biological rationale for the supported/unsupported classification, ideally with a pre-specified hypothesis. The authors should also present the enrichment analyses with appropriate statistical controls and discuss what the results would mean under alternative classification schemes.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Real-data disentanglement validation
- **Claim pointer** The manuscript claims DeepDive "robustly recovers true biological signals from even highly entangled covariates" and demonstrates this in the pancreatic islet application
- **Evidence pointer** Figures 2B–2C, S6B; location not provided for supplemental figures
- **Concern** The validation of disentanglement in real data is indirect. The manuscript shows that DeepDive identifies beta cells as most affected by BMI and diabetes status, and that BMI-associated and diabetes-associated peaks are orthogonal (Jaccard index = 0.1). However, there is no ground truth for disentanglement in real data, and the orthogonality result could reflect the model's architecture rather than true biological separation. The simulation studies provide ground truth, but their realism is unclear.
- **Why it matters** The claim of robust disentanglement in real data is central to the manuscript's utility. If the model simply imposes orthogonality through its architecture, the biological interpretation of the separated effects could be misleading.
- **Resolution test** Provide additional validation of disentanglement in real data, such as comparison with independent biological knowledge, replication in independent datasets, or sensitivity analyses that vary the strength of the adversarial component. The authors should also discuss the limitations of validating disentanglement without ground truth.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity of model description
- **Affected element** Methods section, DeepDive model description
- **Evidence pointer** Methods, "DeepDive" section
- **Issue** The model description is high-level and defers critical details to Note S1. The description of the adversarial component is particularly brief, and the training procedure, while outlined in three phases, lacks specific details on loss functions, hyperparameter selection, and convergence criteria.
- **Required correction** Provide a more complete description of the model architecture and training procedure in the main text or ensure Note S1 contains all necessary details for reproduction.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical methodology
- **Affected element** Differential analysis and effect size estimation
- **Evidence pointer** Methods, "Effect size estimation and differential analysis" section
- **Issue** The use of Fisher's method for combining p-values across decoders assumes independence, which may not hold given that decoders are trained on the same data. The manuscript mentions Cauchy's method as an alternative but does not discuss the implications of p-value dependence.
- **Required correction** Discuss the potential for p-value dependence across decoders and justify the choice of Fisher's method, or provide sensitivity analyses using alternative combination methods.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Simulation realism
- **Affected element** Simulation framework
- **Evidence pointer** Methods, "Simulating count data with controllable covariate dependence" section
- **Issue** The simulation framework assumes independent effects of covariates on features, which may not reflect the complex interactions seen in real biological data. The realism of the simulation is critical for validating the disentanglement claims.
- **Required correction** Discuss the limitations of the simulation framework and consider additional simulations that incorporate interaction effects or more complex dependency structures.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Computational cost
- **Affected element** Model training and resource requirements
- **Evidence pointer** Methods, "Model architecture and training procedure" section
- **Issue** The manuscript notes that training time increases linearly with the number of decoders and that performance saturates at 20 decoders, but does not provide concrete runtime or resource requirements for typical datasets.
- **Required correction** Provide benchmark runtime and resource information for representative dataset sizes to help users assess feasibility.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Code availability
- **Affected element** Reproducibility
- **Evidence pointer** Data and code availability section
- **Issue** The code is available on GitHub and Zenodo, but the manuscript does not specify the software dependencies, versioning, or whether the code has been tested across different computing environments.
- **Required correction** Provide a detailed software environment specification and testing information to ensure reproducibility.

- **Concern ID** R1-m6
- **Severity** Minor
- **Axis** Terminology
- **Affected element** "Counterfactual" terminology
- **Evidence pointer** Throughout the manuscript
- **Issue** The use of "counterfactual" prediction is appropriate but could be clarified. In the context of this model, counterfactual prediction involves manipulating covariate embeddings while holding others fixed, which is a form of intervention in the latent space. The manuscript could benefit from a brief explanation of how this relates to causal inference concepts.
- **Required correction** Add a brief clarification of the counterfactual prediction concept in the context of the model's architecture.

## Risk / unsupported claims
- The claim that DeepDive "outperforms state-of-the-art methods" is not fully supported by the visible evidence, as the complete benchmarking results are in supplemental materials not provided for review.
- The claim that counterfactual prediction "nominates high-confidence transcriptional regulators" is based on a validation logic that is not fully explained and may be circular.
- The claim that DeepDive "robustly recovers true biological signals from even highly entangled covariates" is supported by simulations, but the realism of the simulations and the generalizability to real data are not fully established.
- The biological conclusions regarding specific transcription factors (e.g., HNF1A, NKX6.1, PAX6) are presented as validation but are based on known biology, which could introduce confirmation bias.
- The performance comparison with Biolord in the counterfactual prediction task (Figure 1G) is presented without discussion of potential differences in model complexity or training requirements.
- The claim that DeepDive "offers a powerful and unbiased tool" is not fully supported, as the potential biases in the disentanglement procedure are not thoroughly discussed.