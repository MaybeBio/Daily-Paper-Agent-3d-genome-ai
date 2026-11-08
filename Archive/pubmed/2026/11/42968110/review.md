## Review setup
- **Input scope** Full manuscript text (Introduction, Literature review, Methodology, Results, Discussion, Limitations) as provided.
- **Assessment boundary** Scientific and technical evaluation of the proposed MT-AAE framework, its validation, and the claims made, based solely on the supplied text. No external data, code, or supplementary materials were accessed.
- **Shared manuscript claim summary** The authors propose a Multi-Task Adversarial Autoencoder (MT-AAE) that generates variable-length functional genomic elements (e.g., promoters) while preserving biophysical properties (GC-content, k-mer frequencies) and functional class identity. Claims include: (1) the architecture alleviates mode collapse and posterior divergence; (2) a context-aware length normalization strategy handles variable-length inputs; (3) an interpretable latent space is achieved; (4) the model outperforms VAE, GAN, and shuffled controls on Train-on-Synthetic Test-on-Real (TRTS) accuracy and biophysical fidelity metrics.
- **Visible evidence base** Tables 1-17, Figures 1-10 (described in text), equations (1)-(9), and algorithmic descriptions (Algorithms 1-2). Quantitative results are reported for TRTS accuracy (74.7%), RTSR accuracy (70.1%), GC MAE (0.010), k-mer JSD values, ablation study outcomes, and efficiency metrics.
- **Missing materials affecting confidence** The actual figures (1-10) and supplementary materials were not provided. Code, hyperparameter details beyond Table 6, dataset preprocessing scripts, and full per-class confusion matrices were not available. Statistical significance tests for the reported improvements over baselines are not described in the text.

## Reviewer
- **Overall assessment** The manuscript addresses a relevant and timely problem in generative genomics: producing synthetic regulatory elements that are not only sequence-valid but also biophysically plausible and functionally classifiable. The proposed MT-AAE architecture is a reasonable synthesis of adversarial training and multi-task learning, and the evaluation framework (TRTS/RTSR, k-mer JSD, GC MAE) is thoughtful. However, the evidence presented is insufficient to fully support the central claims. Key weaknesses include: a small and synthetic Phase I dataset (1,850 sequences) with no clear biological validation; a Phase II dataset that is drastically reduced from 27,346 to 1,910 sequences without adequate justification; a lack of statistical significance testing; and an ablation study that shows severe performance collapse at intermediate stages, raising questions about the stability and robustness of the final model. The interpretability claim is not substantiated with any quantitative or qualitative analysis of the latent space. The cross-species generalization failure, while honestly reported, is framed as expected but undermines the broader utility claim. The manuscript is well-written and structured, but the technical case is not yet established.

- **Who would be interested in the results, and why** Researchers in computational genomics, synthetic biology, and deep generative modeling would find this work of interest. The problem of generating functional DNA sequences with controlled biophysical properties is directly relevant to designing promoters, enhancers, and other regulatory elements for therapeutic and biotechnological applications. The TRTS/RTSR evaluation protocol and the multi-task regularization approach could be adopted by others working on sequence generation. The work may also appeal to those studying latent space interpretability in biological sequence models.

- **Major strengths**
  1. The problem is well-motivated and addresses a genuine gap: most generative models for DNA focus on sequence statistics or motif recovery but rarely jointly enforce biophysical constraints and functional class separability.
  2. The evaluation protocol is more rigorous than typical in this field, incorporating TRTS/RTSR bidirectional testing, k-mer JSD at multiple orders, GC-content MAE, and class-wise generation ratios to assess mode collapse.
  3. The ablation study is a valuable addition, as it systematically isolates the contribution of each component (classification, GC regression, balanced sampling) and reveals non-trivial interactions.
  4. The honest reporting of the cross-species generalization failure, including a plausible mechanistic explanation (GC distribution mismatch), is commendable and adds credibility.
  5. The writing is clear, and the mathematical formulations (loss functions, metrics) are presented in a reproducible manner.

- **Major Concerns**

  - **Concern ID** R1-M1
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Technical soundness / Validation
  - **Claim pointer** The authors claim that the MT-AAE "generates variable-length genomic elements with high functional and biophysical fidelity" and that the model "alleviates mode collapse and posterior divergence."
  - **Evidence pointer** Section "Phase I: Synthetic benchmark for mechanistic validation", Table 2, Table 7, Table 14
  - **Concern** The Phase I dataset is entirely synthetic (1,850 sequences) with deterministic motif placement. This is a reasonable starting point, but the claim of "high functional fidelity" is only demonstrated on this artificial corpus. The Phase II dataset, which is the only real-world test, is reduced from 27,346 to 1,910 sequences after filtering, and the filtering criteria are not fully described. More critically, the reported TRTS accuracy of 74.7% is not accompanied by any confidence intervals or statistical significance tests against the baselines (VAE: 44.0%, GAN: 41.0%). The shuffled control (50.7%) is also not tested for significance. Without such tests, it is impossible to determine whether the observed improvements are robust or within noise, especially given the small per-class sample sizes (e.g., snoRNA n=3).
  - **Why it matters** The central claim of the paper is that MT-AAE outperforms existing methods. Without statistical validation, this claim is not established. The small sample sizes for minority classes make the reported recall values (e.g., snoRNA 0.33 at S5) highly unstable and potentially misleading.
  - **Resolution test** Provide confidence intervals or p-values for the TRTS/RTSR accuracy differences between MT-AAE and each baseline. Report per-class results with error bars. Justify the filtering criteria for the Phase II dataset and describe the final class distribution in detail.

  - **Concern ID** R1-M2
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Technical soundness / Ablation interpretation
  - **Claim pointer** The authors state that "the full MT-AAE training reconciles these objectives, achieving synergistic performance" and that the ablation demonstrates "task interference" that is resolved in the final model.
  - **Evidence pointer** Section "Ablation study: architectural component contributions", Figure 8, Table 16
  - **Concern** The ablation results show a dramatic performance collapse at intermediate stages: adding GC regression drops TRTS accuracy from 0.450 to 0.350, and adding balanced sampling further drops it to 0.170. The final model recovers to 0.747. This pattern suggests that the loss landscape is highly unstable and that the final performance may be sensitive to initialization, hyperparameter choices, or training order. The authors provide a post-hoc hypothesis for the GC regression interference but do not test it. Moreover, the per-class recall at S5 shows severe degradation for snoRNA (1.00 to 0.33) and moderate degradation for ncRNA (0.875 to 0.48), which is not fully explained by the "small sample size" argument alone. The claim of "synergistic performance" is not supported by a mechanistic understanding of why the full model succeeds where intermediate stages fail.
  - **Why it matters** If the final model's performance is contingent on a fragile balancing act that is not well understood, the method is not reproducible or generalizable. The ablation study, as presented, raises more questions than it answers about the robustness of the architecture.
  - **Resolution test** Perform multiple training runs with different random seeds to assess variance. Provide a more detailed analysis of the loss landscape, including gradient norms and latent space visualizations at each ablation stage. Test the hypothesis that GC regression over-regularizes the latent space by, for example, removing the GC head and instead adding a fixed penalty.

  - **Concern ID** R1-M3
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Interpretability claim
  - **Claim pointer** The authors claim "an interpretable latent space representation designed to enhance trust in synthetic sequences for therapeutic use."
  - **Evidence pointer** Section "Latent space design and regularization", Figure 9
  - **Concern** The only evidence for interpretability is a t-SNE projection showing clustering by functional class. This is a weak form of interpretability. The authors do not demonstrate that specific latent dimensions correspond to biologically meaningful features (e.g., GC-content, motif presence, or class identity). There is no analysis of what the latent space encodes beyond class separability, nor any comparison to latent spaces of baseline models. The claim that this "enhances trust" is not substantiated.
  - **Why it matters** Interpretability is a stated contribution and a key differentiator from prior work. Without a concrete demonstration of what the latent dimensions represent and how they can be used for biological insight or quality control, this claim is overstated.
  - **Resolution test** Provide a systematic analysis of the latent space, such as: (a) correlation of individual latent dimensions with biophysical properties (GC, k-mer frequencies); (b) interpolation experiments showing smooth transitions between functional classes; (c) a comparison of latent space structure with a standard VAE or AAE baseline.

  - **Concern ID** R1-M4
  - **Severity** Major
  - **Blocking** No
  - **Axis** Technical soundness / Baseline fairness
  - **Claim pointer** The authors claim MT-AAE outperforms VAE and GAN baselines, and that the baselines were "implemented using their original published architectures and default hyperparameters without validation-set tuning."
  - **Evidence pointer** Section "Baseline models for comparison", Table 14
  - **Concern** The baseline comparison is potentially unfair. The MT-AAE's hyperparameters were tuned via grid search on the validation set (Table 6), while the baselines were not tuned at all. This is a classic "tuned model vs. untuned baseline" comparison, which can inflate the apparent improvement. Additionally, the WGAN-GP baseline is reported with a TRTS accuracy of 0.21, which is below the shuffled control (0.507). This is suspicious and suggests the WGAN-GP may have been poorly configured or undertrained. The authors do not provide training curves or convergence diagnostics for any of the baselines.
  - **Why it matters** The claim of superiority over baselines is a core contribution. An unfair comparison undermines the validity of this claim and the practical value of the proposed method.
  - **Resolution test** Either tune the baselines using the same validation-based grid search procedure, or clearly state that the comparison is against default-configuration baselines and discuss the implications. Provide training curves and final loss values for all models to demonstrate convergence.

  - **Concern ID** R1-M5
  - **Severity** Major
  - **Blocking** No
  - **Axis** Scientific importance / Generalizability
  - **Claim pointer** The authors state that the model "does not generalise to Mus musculus sequences" and frame this as expected due to species-specific regulatory grammar.
  - **Evidence pointer** Section "Cross-species generalisation assessment", Figure 10
  - **Concern** The cross-species failure is reported as a limitation, but it also reveals a fundamental constraint of the approach: the model learns species-specific and potentially dataset-specific biases. The authors suggest future work on multi-species training, but this is not explored. The claim that the model is useful for "data augmentation for underrepresented functional classes" is questionable if the model cannot generalize across species or tissue types. The GC distribution mismatch explanation is plausible but not tested (e.g., by retraining on a GC-matched subset of mouse data).
  - **Why it matters** The practical utility of the model depends on its ability to generate useful sequences beyond the exact training distribution. The reported failure mode is significant and deserves deeper investigation, not just a forward-looking statement.
  - **Resolution test** Conduct a controlled experiment to test the GC-mismatch hypothesis, such as training on a GC-matched subset of mouse sequences or applying a domain adaptation technique. Discuss the implications for the claimed utility in data augmentation.

- **Minor Comments**

  - **Concern ID** R1-m1
  - **Severity** Minor
  - **Axis** Clarity / Reproducibility
  - **Affected element** Section "Phase II: NCBI human gene corpus for empirical evaluation"
  - **Evidence pointer** Table 3
  - **Issue** The reduction from 27,346 to 1,910 sequences is drastic, but the filtering criteria are only briefly mentioned ("length filtering... removal of sequences with ambiguous nucleotide content exceeding 5%"). The class distribution after filtering is not shown, and it is unclear if the filtering introduced bias.
  - **Required correction** Provide a detailed description of the filtering pipeline, including the number of sequences removed at each step. Report the final class distribution and compare it to the original distribution to assess potential bias.

  - **Concern ID** R1-m2
  - **Severity** Minor
  - **Axis** Technical soundness
  - **Affected element** Section "Biophysical property preservation"
  - **Evidence pointer** Table 13
  - **Issue** The k-mer JSD values are reported with confidence intervals, but the methodology for computing these intervals is not described. It is unclear if they are bootstrap intervals, standard errors across folds, or something else.
  - **Required correction** Describe how the confidence intervals were computed. If they are bootstrap intervals, specify the number of resamples.

  - **Concern ID** R1-m3
  - **Severity** Minor
  - **Axis** Clarity
  - **Affected element** Section "Case study: promoter sequence generation"
  - **Evidence pointer** Figure 4
  - **Issue** The case study of Sample 3 is presented as evidence of motif recovery, but only one example is shown. The claim that the model "recovers canonical regulatory motifs" is based on a single instance and the population-level analysis in Table 11.
  - **Required correction** Clarify that the case study is illustrative. Consider showing additional examples or a summary of motif recovery rates across all generated promoters.

  - **Concern ID** R1-m4
  - **Severity** Minor
  - **Axis** Reproducibility
  - **Affected element** Section "Reproducibility and implementation details"
  - **Evidence pointer** Table 6
  - **Issue** The hyperparameter grid search is described, but the search ranges for some parameters (e.g., dropout rate, learning rate) are not fully specified. The text mentions "learning rate 0.001" but does not state if this was part of the grid or a fixed choice.
  - **Required correction** Provide the full grid search space for all hyperparameters, including the learning rate, and state which parameters were fixed vs. tuned.

  - **Concern ID** R1-m5
  - **Severity** Minor
  - **Axis** Clarity
  - **Affected element** Section "Discussion"
  - **Evidence pointer** Paragraph on cross-species generalization
  - **Issue** The discussion of the cross-species failure is somewhat repetitive with the Results section. The explanation of the GC mismatch is plausible but could be more concise.
  - **Required correction** Streamline the discussion to avoid redundancy and focus on the implications and potential solutions.

- **Technical failings that need to be addressed before the case is established**
  1. Lack of statistical significance testing for all primary comparisons (TRTS/RTSR accuracy, k-mer JSD, GC MAE) between MT-AAE and baselines.
  2. Unfair baseline comparison: MT-AAE hyperparameters tuned, baselines not tuned.
  3. Ablation study shows severe performance collapse at intermediate stages, with no mechanistic explanation or robustness analysis (e.g., multiple seeds).
  4. Interpretability claim is not substantiated beyond t-SNE clustering.
  5. Cross-species generalization failure is reported but not investigated experimentally.
  6. The Phase II dataset filtering is not fully described, and the final class distribution is not reported.

- **Assessment against Nature-style criteria**
  - **Originality** Moderate. The combination of adversarial autoencoders with multi-task learning for genomic sequence generation is not entirely novel, but the specific focus on jointly preserving biophysical properties and functional class identity is a useful contribution. The TRTS/RTSR bidirectional evaluation is a positive methodological addition.
  - **Scientific importance** Moderate. The problem is relevant, but the demonstrated impact is limited by the small, synthetic Phase I dataset and the species-specific failure mode. The potential for data augmentation in genomics is real, but the evidence does not yet show that the generated sequences are useful in downstream biological applications.
  - **Interdisciplinary readership** The work sits at the intersection of deep learning and genomics. It would appeal to computational biologists and machine learning researchers, but the lack of biological validation (e.g., reporter assays, ChIP-seq) limits its appeal to a broader biological audience.
  - **Technical soundness** The architecture is reasonable, but the validation is incomplete. The lack of statistical tests, the fragile ablation results, and the unfair baseline comparison are significant technical weaknesses.
  - **Readability for nonspecialists** The manuscript is generally well-written and the concepts are explained clearly. However, the heavy reliance on domain-specific metrics (TRTS, RTSR, k-mer JSD) without sufficient intuitive explanation may hinder nonspecialist readers. The mathematical notation is appropriate but could be better integrated with the narrative.

- **Recommendation posture** Currently not established from the provided evidence. The manuscript addresses a relevant problem and has a sensible methodological core, but the central claims of improved functional fidelity, robustness, and interpretability are not adequately supported. The authors should be encouraged to revise and resubmit after addressing the major concerns, particularly the statistical validation, baseline fairness, and a deeper analysis of the ablation and cross-species results.

## Risk / unsupported claims
- The claim that the MT-AAE "alleviates mode collapse and posterior divergence" is not directly tested. The generation ratio analysis is indirect evidence and does not measure mode collapse in the latent space.
- The claim of "interpretable latent space" is unsupported. No analysis of latent dimensions or their biological meaning is provided.
- The claim that the model "generates variable-length genomic elements" is misleading, as the architecture operates on fixed-length (363 bp) sequences with a normalization strategy, not native variable-length generation.
- The reported TRTS accuracy of 74.7% is presented as a single point estimate without variance or significance testing, making it impossible to assess reliability.
- The cross-species generalization failure is reported, but the claim that this is "expected" is not supported by any comparative analysis with other models or species.
- The statement that the model "preserves biophysical properties" is based on GC-content and k-mer JSD, which are necessary but not sufficient indicators of biophysical plausibility. No thermodynamic or structural validation is provided.