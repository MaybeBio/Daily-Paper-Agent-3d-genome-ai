## Review setup
- **Input scope** Abstract / summary
- **Assessment boundary** Claims and evidence presented in the abstract only
- **Shared manuscript claim summary** Hi-cGAN is a conditional GAN that predicts Hi-C interaction matrices from chromatin factor occupancy alone (no DNA sequence), achieving matrix-level agreement slightly below Epiphany and well below sequence-based methods (C.Origami, Akita), with performance dependent on measure, resolution, and cell type.
- **Visible evidence base** Abstract text; no figures, tables, or supplementary materials provided
- **Missing materials affecting confidence** Full manuscript, figures, tables, supplementary data, code, and detailed methods

## Reviewer
- **Overall assessment** The abstract presents a potentially useful computational tool for predicting Hi-C maps from chromatin factor tracks, but the claims are poorly structured, internally inconsistent, and lack sufficient quantitative detail to evaluate the method’s novelty or utility. The key finding—that Hi-cGAN underperforms sequence-based methods—is stated without clear justification for why this approach is valuable. The conclusions appear to extend beyond the evidence presented, and several critical technical details are missing. The abstract reads more like a discussion than a concise summary of results.

- **Who would be interested in the results, and why** Researchers in computational genomics and 3D genome organization may be interested in a method that predicts Hi-C from chromatin factor occupancy, potentially enabling predictions in cell types where only ChIP-seq data are available. However, the abstract does not convincingly demonstrate that this approach offers advantages over existing sequence-based methods.

- **Major strengths** 
  - Addresses a relevant problem: reducing the experimental burden of Hi-C by computational prediction.
  - Evaluates multiple bin sizes (2–25 kb) and whole-genome prediction, which is more flexible than fixed-window methods.
  - Compares against three existing methods (Akita, C.Origami, Epiphany).

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Clarity and consistency of claims
- **Claim pointer** "Hi-cGAN predicts Hi-C interaction matrices with a conditional generative adversarial network from chromatin factor occupancy alone, without DNA sequence."
- **Evidence pointer** Abstract, Findings and Key points
- **Concern** The abstract states that Hi-cGAN uses "chromatin factor occupancy alone" as input, yet the Conclusions claim that "chromatin factor occupancy determines a substantial part of contact structure, and two tracks capture most of it." It is unclear whether the model uses all available factor tracks or only two. The number and identity of input tracks are not specified.
- **Why it matters** The input dimensionality is fundamental to understanding the model’s scope, generalizability, and comparison to sequence-based methods. Without this information, the reader cannot assess whether the comparison is fair or whether the model is practically useful.
- **Resolution test** Specify the exact number and identity of chromatin factor tracks used as input. Clarify whether the "two tracks" in the Conclusions refer to a subset of inputs or a different analysis.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Quantitative evidence and internal consistency
- **Claim pointer** "On held-out data Hi-cGAN reaches matrix-level agreement slightly below Epiphany’s... and well below C.Origami’s and Akita’s."
- **Evidence pointer** Abstract, Findings and Key points
- **Concern** The abstract provides only one quantitative comparison: "over Akita’s 411 held-out windows the mean correlation is 0.238 against 0.506." This is a single metric (Pearson correlation?) on a single test set. The claim that Hi-cGAN is "slightly below Epiphany" is not supported by any number. The claim that "which method is better depends on the measure used" is stated but no alternative measures or their values are given.
- **Why it matters** Without multiple quantitative comparisons across methods and metrics, the relative performance claims are unsubstantiated. The reader cannot evaluate whether Hi-cGAN is competitive or useful.
- **Resolution test** Provide correlation (or other metric) values for all methods on the same test sets. Specify which metric is used (e.g., Pearson, Spearman, HiCRep, SCC). Report performance for boundary and loop recovery with quantitative values.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Logical coherence of conclusions
- **Claim pointer** "Chromatin factor occupancy determines a substantial part of contact structure, and two tracks capture most of it."
- **Evidence pointer** Abstract, Conclusions
- **Concern** This conclusion appears to be a biological claim about the importance of specific factors, but the abstract provides no evidence that Hi-cGAN’s predictions are biologically interpretable or that the model’s performance is driven by specific tracks. The claim that "two tracks capture most of it" is not supported by any ablation analysis or feature importance measure.
- **Why it matters** The conclusion conflates model performance with biological insight. Without feature importance analysis, the statement is speculative and potentially misleading.
- **Resolution test** Provide ablation experiments or feature attribution analysis showing that removing specific tracks degrades performance. Clarify whether this conclusion is derived from the model or from prior knowledge.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Clarity of evaluation protocol
- **Claim pointer** "With the input chosen on a validation chromosome, agreement approaches Epiphany’s and stays below the sequence-based C.Origami and Akita."
- **Evidence pointer** Abstract, Findings
- **Concern** The phrase "input chosen on a validation chromosome" is ambiguous. Does this mean hyperparameters were tuned on a validation chromosome? Which chromosome? Were the test chromosomes completely held out from any tuning? The comparison to Akita uses "Akita’s 411 held-out windows"—are these the same test windows used for Hi-cGAN? The evaluation protocol is not described clearly enough to assess potential overfitting or data leakage.
- **Why it matters** Fair comparison requires identical or clearly described test sets. Ambiguity in the evaluation protocol undermines confidence in the reported performance.
- **Resolution test** Clearly describe the train/validation/test split. Specify which chromosome(s) were used for validation and which for testing. Confirm that test chromosomes were never used for model selection.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** Yes
- **Axis** Interpretation of baseline comparison
- **Claim pointer** "A ridge regression on the same single track reaches 0.691 against Hi-cGAN’s 0.715 on HiCRep, while its predicted matrix shows stripes but no domains, so that measure alone does not establish what the network contributes."
- **Evidence pointer** Abstract, Key points
- **Concern** This is a critical comparison that undermines the claimed contribution of the GAN architecture. If a simple ridge regression on a single track achieves nearly the same HiCRep score, the added complexity of a GAN may not be justified. The dismissal of this result ("so that measure alone does not establish what the network contributes") is a non-sequitur: the measure does establish that the GAN’s advantage is marginal on this metric. The abstract does not provide any metric where the GAN clearly outperforms the ridge regression.
- **Why it matters** The core claim of the paper is that a GAN is useful for this task. If a simple baseline performs similarly, the novelty and utility of the method are in question.
- **Resolution test** Provide metrics where Hi-cGAN significantly outperforms the ridge regression (e.g., boundary/loop recovery, visual quality, biological interpretability). Alternatively, acknowledge that the GAN’s advantage is limited to specific aspects.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Readability
- **Affected element** Abstract, Findings
- **Evidence pointer** "It predicts a whole genome as a cool file at bin sizes from 2 to 25 kb, where Akita, C.Origami and Epiphany emit fixed windows of 1 Mb, 2 Mb and 990 kb."
- **Issue** The sentence is grammatically awkward and the comparison is unclear. "Where" should be "whereas" or "while." The fixed window sizes are listed without context for why this matters.
- **Required correction** Rewrite for clarity: "Hi-cGAN predicts whole-genome contact maps as cool files at bin sizes from 2 to 25 kb, whereas Akita, C.Origami, and Epiphany emit fixed windows of 1 Mb, 2 Mb, and 990 kb, respectively."

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Precision
- **Affected element** Abstract, Key points
- **Evidence pointer** "The same architecture learns raw contact counts, genomic-distance z-scores and observed/expected normalized data."
- **Issue** It is unclear whether this means the model was trained separately on each data type, or whether it can handle all three simultaneously. The phrase "learns" is ambiguous.
- **Required correction** Specify: "The same architecture can be trained to predict raw contact counts, genomic-distance z-scores, or observed/expected normalized data."

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Abstract, Conclusions
- **Evidence pointer** "Transfer to an unseen cell type costs about 0.12 SCC"
- **Issue** The value "0.12 SCC" is given without context. Is this a drop in SCC? What is the baseline SCC in the source cell type? Is this a large or small drop?
- **Required correction** Provide the baseline SCC in the source cell type and the SCC after transfer. Clarify whether 0.12 is an absolute or relative change.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract, Conclusions
- **Evidence pointer** "which method leads depends on the measure"
- **Issue** This is vague. Which measures favor which method? Without examples, the statement is uninformative.
- **Required correction** Provide at least one example: "For example, on HiCRep, method X leads, while on SCC, method Y leads."

## Risk / unsupported claims
- "Chromatin factor occupancy determines a substantial part of contact structure" – unsupported by any evidence in the abstract; no causal or correlational analysis is presented.
- "Two tracks capture most of it" – unsupported; no ablation or feature importance analysis is described.
- "Transfer to an unseen cell type costs about 0.12 SCC" – unsupported without baseline values and context.
- "Which method is better depends on the measure used" – unsupported; no alternative measures or their values are provided.
- "Boundary and loop recovery does not follow the matrix-level scores" – unsupported; no quantitative values for boundary/loop recovery are given.