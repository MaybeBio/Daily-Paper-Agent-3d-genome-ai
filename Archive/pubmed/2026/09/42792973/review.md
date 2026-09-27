## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no full text, figures, tables, or supplementary materials were provided
- **Shared manuscript claim summary** The authors report a pipeline integrating transcriptomic profiling, deep learning (ZEN-former), and in vivo reporter assays to identify compact cis-regulatory elements driving zebrafish habenular expression, with two ~1.2 kb constructs validated in transgenic lines showing high labeling completeness.
- **Visible evidence base** Abstract text only; no numerical data, statistical details, or methodological specifics beyond those summarized
- **Missing materials affecting confidence** Full manuscript, all figures and tables, supplementary data, model architecture details, training and validation metrics, ATAC-seq processing details, transgenic line characterization protocols, and quantitative imaging methods

## Reviewer
- **Overall assessment** The abstract presents a conceptually interesting cross-species transfer of deep learning predictions from mammalian chromatin accessibility to zebrafish regulatory element discovery. The reported outcomes, particularly the high labeling completeness values, are potentially valuable for the habenula research community. However, the abstract alone provides insufficient detail to evaluate the robustness of the computational pipeline, the rigor of the experimental validations, or the statistical support for the quantitative claims. Several key methodological steps are described only superficially, and the evidence base is too thin to establish the case as presented.
- **Who would be interested in the results, and why** Researchers studying zebrafish neurogenetics, habenular circuitry, and cis-regulatory element biology would find these tools and transgenic lines useful. Additionally, computational biologists working on cross-species transfer of deep learning models for genomics may be interested in the ZEN-former approach as a proof of concept.
- **Major strengths** The study addresses a real gap in genetic tools for the zebrafish habenula. The integration of multiple data types (transcriptomics, chromatin accessibility, repeat annotations, gene models) for candidate prioritization is methodologically sensible. The cross-species transfer of deep learning features is an innovative angle with potential broader applicability. The reported stable transgenic lines with high labeling completeness suggest practical utility.
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
  - R1-m5
- **Technical failings that need to be addressed before the case is established** R1-M1 (model validation), R1-M2 (candidate selection rationale), R1-M3 (transient versus stable data), R1-M4 (quantitative imaging methodology)
- **Assessment against Nature-style criteria** Originality is moderate to high given the cross-species deep learning application, though the concept of using mammalian data for zebrafish element discovery is not entirely unprecedented. Scientific importance is solid for the zebrafish and habenula communities but may be narrower for a general readership. Interdisciplinary readership is plausible given the intersection of genomics, deep learning, and neurobiology. Technical soundness cannot be adequately assessed from the abstract alone, particularly for the computational and quantitative imaging components. Readability for nonspecialists is acceptable, though some terms (e.g., ZEN-former, Tol2 transposon) are used without explanation.
- **Recommendation posture** Currently not established from the provided evidence. The abstract suggests a promising approach and useful resources, but the lack of methodological detail and quantitative support prevents a definitive assessment. A revised submission with full methodological transparency and robust validation data could change this posture.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** "The model demonstrated strong correlation between predicted and experimentally measured signals across held-out genomic regions."
- **Evidence pointer** Abstract, Results section (location not provided)
- **Concern** The abstract claims strong correlation but provides no correlation coefficients, no definition of "strong," no description of the held-out regions, and no comparison to baseline or alternative models. The training data are from adult mouse brain neuronal subclasses, yet the validation appears to be on genomic regions that are not clearly specified as mouse or zebrafish.
- **Why it matters** Without quantitative metrics and clear validation design, the predictive performance of ZEN-former cannot be evaluated. The cross-species transfer claim depends entirely on this validation being robust and appropriately designed.
- **Resolution test** Provide specific correlation values (e.g., Pearson or Spearman rho) with confidence intervals, describe the held-out region selection process, and clarify whether validation was performed on mouse or zebrafish data. Include comparison to a null model or existing tools.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Reproducibility and rigor
- **Claim pointer** "To prioritize regulatory candidates, we integrated ZEN-former predictions with available zebrafish ATAC-seq data, RepeatMasker annotations, and gene models, identifying two ~600 bp intervals at each gene locus."
- **Evidence pointer** Abstract, Methods section (location not provided)
- **Concern** The integration process is described in a single sentence. No criteria are given for how ZEN-former scores were weighted against ATAC-seq peaks, how repeat masking influenced interval selection, or why ~600 bp was chosen as the interval size. The selection of gng8 and ano2 from the in situ hybridization screen is also not justified beyond "highly reproducible expression."
- **Why it matters** The reproducibility of the candidate selection pipeline is central to the study's utility. If the integration rules are not specified, other researchers cannot apply or adapt the method, and the specificity of the chosen intervals cannot be assessed.
- **Resolution test** Provide a detailed step-by-step description of the prioritization algorithm, including thresholds, scoring functions, and decision rules. Justify the interval size and the choice of gng8 and ano2 relative to other candidates.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "In transiently injected larvae, both constructs successfully drove reporter expression in the habenular region. Furthermore, the resulting stable transgenic lines displayed highly specific and reproducible habenular expression."
- **Evidence pointer** Abstract, Results section (location not provided)
- **Concern** The abstract reports transient and stable transgenic outcomes but provides no images, no quantification of specificity (e.g., ectopic expression rates), and no reproducibility metrics across independent injection batches or generations. The transition from transient to stable lines is mentioned without describing how many lines were generated, how many were characterized, or how stability was confirmed.
- **Why it matters** The core claim of the study is that these constructs are functional and specific. Without visual or quantitative evidence of expression patterns, including off-target expression, the specificity claim is unsupported. Reproducibility across animals and generations is essential for a genetic tool.
- **Resolution test** Include representative images of reporter expression in transient and stable lines, quantify the proportion of larvae or fish showing the expected pattern, report ectopic expression rates, and describe the number of independent transgenic lines and generations examined.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** "Quantitative confocal analysis showed mean habenular labeling completeness values of 84.5% and 96.2% for the gng8- and ano2-derived lines, respectively."
- **Evidence pointer** Abstract, Results section (location not provided)
- **Concern** The labeling completeness metric is not defined. It is unclear whether this refers to the proportion of habenular neurons labeled, the proportion of the habenular volume covered, or another measure. No sample sizes, variance estimates, or statistical comparisons are provided. The method for defining the habenular region in the analysis is also not described.
- **Why it matters** These quantitative values are the primary quantitative outcome of the study. Without a clear definition and statistical context, the numbers cannot be interpreted or compared to other tools. The claim of "high" completeness depends on the metric and the reference standard.
- **Resolution test** Define labeling completeness precisely, state the number of animals and sections analyzed, provide standard deviations or confidence intervals, describe the segmentation method for the habenula, and include a statistical comparison between the two lines or against a reference marker.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Methods, transcriptomic profiling
- **Evidence pointer** Abstract, Methods section (location not provided)
- **Issue** The abstract states that GFP-positive cells were isolated and profiled via microarray, but the number of biological replicates, the sorting strategy, and the analysis pipeline are not described.
- **Required correction** Provide details on the number of larvae pooled, the FACS gating strategy, and the microarray analysis methods, including normalization and differential expression criteria.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Methods, in situ hybridization
- **Evidence pointer** Abstract, Methods section (location not provided)
- **Issue** The validation of candidate genes by whole-mount in situ hybridization is mentioned for two developmental stages, but the stages are not specified and the number of genes validated is not stated.
- **Required correction** Specify the developmental stages (e.g., hours post-fertilization) and the number of candidate genes tested, along with the criteria for "highly reproducible expression."

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Methods, ZEN-former architecture
- **Evidence pointer** Abstract, Methods section (location not provided)
- **Issue** The term "Enformer-based" is used without explaining what modifications were made for zebrafish or how the model handles sequence length differences between mouse and zebrafish.
- **Required correction** Describe the model architecture, input sequence length, training details, and any species-specific adaptations.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Results, stable transgenic lines
- **Evidence pointer** Abstract, Results section (location not provided)
- **Issue** The abstract does not state whether the stable lines are germline-transmitted or whether expression is maintained in adult fish.
- **Required correction** Clarify the generation of stable lines (F0 founders versus F1 or later generations) and report expression persistence in adults if assessed.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Accessibility
- **Affected element** Terminology
- **Evidence pointer** Abstract, throughout (location not provided)
- **Issue** Terms such as "ZEN-former," "Tol2 transposon mediated transgenesis," and "labeling completeness" are used without definition, which may hinder nonspecialist readers.
- **Required correction** Add brief definitions or explanatory phrases at first use in the full manuscript.

## Risk / unsupported claims
- The claim of "strong correlation" for ZEN-former validation is unsupported without quantitative metrics.
- The claim of "highly specific and reproducible" expression in stable lines is unsupported without images or quantitative specificity data.
- The labeling completeness values (84.5% and 96.2%) are uninterpretable without a defined metric and statistical context.
- The cross-species transfer conclusion ("sequence features learned from mammalian chromatin accessibility datasets can effectively guide the prioritization of functional regulatory elements across species") is a broad generalization from two loci and cannot be established from the abstract alone.
- The statement that the selected intervals are "compact" is not quantified relative to other known habenula enhancers or regulatory elements.