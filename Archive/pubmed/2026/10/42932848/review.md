## Review setup
- **Input scope** Full manuscript text (abstract, introduction, methods, results, discussion, conclusion, supplementary references)
- **Assessment boundary** Scientific content, methodological validity, evidence quality, and claims as presented in the provided text. No code, data, or supplementary files were available for inspection.
- **Shared manuscript claim summary** The authors present EpiInsula, a dilated convolutional regression framework that predicts the continuous Hi-C insulation score from six cell-type-specific epigenomic tracks over a ±700-kb window. They claim superior held-out correlation and boundary F1 against seven task-matched comparison methods and three retrained contact-map predictors, calibrated conditional-mean predictions, and utility for identifying cell-type-specific boundaries.
- **Visible evidence base** Abstract, full methods descriptions, results narrative with quantitative values, figure references (Figs 1–7), supplementary table references (Tables S1–S15), and GitHub repository URL.
- **Missing materials affecting confidence** Actual data files, code, trained model weights, supplementary tables and figures, detailed architecture diagrams, hyperparameter search results, and the full set of per-cell-line/per-fold results. These are referenced but not provided in the submitted text.

## Reviewer

- **Overall assessment** This manuscript addresses a meaningful gap in computational chromatin biology by reframing insulation prediction as calibrated regression rather than boundary classification. The evaluation design, particularly the chromosome-disjoint partitioning and the matched-protocol comparison across eight methods, is rigorous and addresses common pitfalls in this literature. The results are internally consistent and the claims are generally well-scoped. However, the manuscript's reliance on supplementary materials for critical details (architecture specifics, hyperparameter values, per-fold results) limits full verification from the submitted text alone. The descriptive nature of the interpretability analyses is appropriately acknowledged. The work is technically sound in its stated scope, though the novelty is primarily in problem formulation and evaluation rather than architectural innovation, which the authors explicitly acknowledge.

- **Who would be interested in the results, and why** Computational biologists and bioinformaticians working on 3D genome organization prediction, particularly those developing or benchmarking methods for chromatin architecture inference from epigenomic data. Researchers studying cell-type-specific genome folding and its relationship to gene regulation would find the cross-cell-type transfer and boundary-contrast analyses relevant. The calibrated regression framing and the matched-protocol evaluation methodology would also interest method developers seeking robust benchmarking practices in this domain.

- **Major strengths**
  1. The problem formulation as calibrated regression on a continuous insulation score is a well-motivated departure from binary boundary classification, with clear biological rationale.
  2. The chromosome-disjoint evaluation design with per-chromosome held-out scoring is methodologically strong and addresses a common leakage concern.
  3. The matched-protocol comparison across eight methods under identical inputs, windows, folds, and seeds is exemplary for fair benchmarking.
  4. The calibration assessment via regression slope and intercept, with explicit distinction from uncertainty calibration, is precise and appropriate.
  5. The cell-type-specific boundary endpoint, defined from measured data alone, provides a meaningful and stringent test of the model's utility.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence completeness
- **Claim pointer** The manuscript claims EpiInsula achieves held-out correlations of 0.791, 0.780, 0.860, and 0.774 across four cell lines, and that these are the highest among eight methods under a matched contract.
- **Evidence pointer** Results section, Fig 2A, Fig 3A, Supplementary Table S9
- **Concern** The primary quantitative claims rest on results presented in figures and supplementary tables that are not included in the submitted text. The reader cannot verify the correlation values, the comparison margins, the bootstrap intervals, or the per-fold consistency from the provided material. The methods section describes the evaluation protocol in detail, but the actual numbers are only summarized in the text.
- **Why it matters** The central claims of the paper are empirical. Without access to the underlying data tables, figures, and per-fold results, the claims cannot be independently assessed. This is particularly important for the comparison claims, where the margins over comparison methods are stated but not shown in a verifiable format.
- **Resolution test** Provide the full set of per-cell-line, per-fold, per-seed results in a supplementary table, along with the complete figures showing correlation scatter plots, calibration curves, and boundary F1 distributions. The bootstrap interval calculations should be reproducible from the provided data.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Methodological transparency
- **Claim pointer** The manuscript states the network is "a dilated residual convolution with a centre-plus-global read-out" with 583,681 trainable parameters, and that the half-width was selected on a development partition.
- **Evidence pointer** Methods section, "Network architecture and receptive field" and "Input representation and signal normalisation"; Supplementary Table S4
- **Concern** The architecture description is too brief to be reproducible. Key details are missing: the number of residual blocks is stated (eight), but the channel dimensions at each stage, the dilation schedule, the exact read-out mechanism, the dropout rate, the GELU activation placement, and the weight initialization are not specified in the main text. The receptive-field calculation is referenced to Supplementary Table S4 but not shown. The half-width selection criterion ("within 0.001 of the highest average") is stated, but the actual correlation values across the seven tested half-widths are not reported.
- **Why it matters** Reproducibility is a core requirement for computational methods papers. The architecture and hyperparameter details are essential for others to reimplement and build upon the method. The current description is at the level of a summary rather than a specification.
- **Resolution test** Provide a complete architecture specification in the main text or supplementary, including a table of layer types, output dimensions, kernel sizes, dilations, and activation functions. Report the half-width selection results (correlation vs. half-width) and the final hyperparameter values for all training settings.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Claim strength vs. evidence
- **Claim pointer** The manuscript states "On boundaries that differ between IMR-90 and K562 it recovers 0.383 of the contrasts against 0.024–0.264 for all seven comparison methods" and that EpiInsula "ranks first at every point of a 25-point threshold grid and in all six cell-line pairs."
- **Evidence pointer** Results section, "Predicted profiles recover boundaries differing between IMR-90 and K562"; Fig 7E; Supplementary Fig S6; Supplementary Tables S14–S15
- **Concern** The cell-type-specific boundary endpoint is described as "descriptive" and "not treated as independent validation," which is appropriately cautious. However, the strength of the claim ("ranks first at every point") is presented with high confidence, while the endpoint definition involves manually specified thresholds and the analysis is acknowledged as descriptive. The robustness analysis on a threshold grid is described, but the actual grid results are not shown in the text.
- **Why it matters** The claim of consistent first-place ranking across all grid points and cell-line pairs is strong and would be a notable result. However, the descriptive nature of the endpoint and the manual threshold specification introduce subjectivity. The reader needs to see the full grid results to assess whether the ranking is robust or driven by specific threshold choices.
- **Resolution test** Show the full 25-point grid results for all six cell-line pairs, including the recovered fractions for all eight methods. Provide a sensitivity analysis with alternative threshold definitions to demonstrate that the ranking is not an artifact of the specific thresholds chosen.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Comparison fairness
- **Claim pointer** The manuscript states "three published contact-map predictors retrained on the same data give lower correlation on the derived insulation score" and describes modifications to the training procedures of these methods.
- **Evidence pointer** Methods section, "Comparison with contact-map prediction methods"; Supplementary Table S6; Supplementary Fig S2
- **Concern** The comparison with Epiphany, C.Origami, and ChromNet involves retraining these methods with modifications to their training loops (e.g., "the chromosome split, the scoring of the full validation set each epoch, the retention of the validation-optimal checkpoint, the seed handling, and the data-loading paths were changed"). These modifications are described as necessary for the evaluation contract, but they may affect the performance of these methods in ways that are not fully characterized. The comparison is also conducted on a single fold (fold 1) with a single seed, which limits the statistical power of the comparison.
- **Why it matters** Fair comparison is essential for the claim that EpiInsula outperforms existing methods. If the modifications to the comparison methods inadvertently disadvantage them, the comparison would be biased. The single-fold, single-seed comparison also raises questions about the stability of the reported differences.
- **Resolution test** Provide a detailed analysis of how the modifications affect the performance of each comparison method, ideally by comparing modified vs. unmodified versions on a common benchmark. Report results across all five folds and three seeds for the contact-map predictors, not just fold 1.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract
- **Evidence pointer** Abstract, first sentence
- **Issue** The phrase "calibrated regression" is used in the title and abstract, and the authors define it in the methods as conditional-mean calibration. However, the abstract does not define this term, and readers may initially interpret "calibrated" in the uncertainty-calibration sense, which the authors explicitly disclaim.
- **Required correction** Add a brief parenthetical definition in the abstract, e.g., "calibrated regression (meaning the mean measured value among loci with a given prediction equals that prediction)".

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** Results, "Held-out prediction accuracy and calibration across cell lines"
- **Evidence pointer** Results section, first paragraph; Supplementary Table S9
- **Issue** The text reports correlation values and regression slopes but does not report confidence intervals for these quantities. The seedwise standard deviations are mentioned (at most 0.004), but the bootstrap intervals are only referenced for the comparison analyses.
- **Required correction** Report 95% confidence intervals for the correlation and slope estimates, either in the text or in Supplementary Table S9.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Terminology
- **Affected element** Methods, "Comparison with contact-map prediction methods"
- **Evidence pointer** Methods section, "Comparison with contact-map prediction methods"
- **Issue** The term "native inputs" is used to describe the inputs of the comparison methods, but it is not defined. It appears to mean the inputs specified in the original publications, but this should be stated explicitly.
- **Required correction** Define "native inputs" as the inputs specified in each method's original publication.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Data availability
- **Evidence pointer** Data availability section
- **Issue** The data availability statement lists the GitHub repository and the public data sources, but it does not state whether the trained model weights, the exact train/validation/test splits, or the preprocessing scripts are included in the repository.
- **Required correction** Specify in the data availability statement whether model weights, splits, and preprocessing scripts are included in the repository, or state that they are available upon request.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Interpretability
- **Affected element** Results, "Input ablation reveals cell-type-specific dependence and graded perturbation response"
- **Evidence pointer** Results section, "Input ablation reveals cell-type-specific dependence and graded perturbation response"; Fig 4
- **Issue** The ablation results are described in terms of which removals produce the largest changes, but the text does not report the actual correlation values for each ablation condition. The reader cannot assess the magnitude of the effects.
- **Required correction** Report the ablation correlation values (or the change from the full model) for each cell line and condition, either in the text or in a supplementary table.

- **Concern ID** R1-m6
- **Severity** Minor
- **Axis** Scope
- **Affected element** Discussion, limitations
- **Evidence pointer** Discussion, "Three limitations define the scope of the study"
- **Issue** The three stated limitations are reasonable, but the discussion does not address the potential impact of the fixed 10-kb resolution on the model's utility for finer-scale insulation features, nor does it discuss how the model might perform on non-human genomes or on data from different Hi-C processing pipelines.
- **Required correction** Add a sentence or two addressing these additional scope considerations, or explicitly state why they are outside the current study's scope.

## Risk / unsupported claims
- The specific correlation values (0.791, 0.780, 0.860, 0.774) and regression slopes (0.90–0.95) are stated in the text but cannot be verified without the underlying data tables and figures.
- The claim that EpiInsula "ranks first at every point" of the threshold grid across all six cell-type pairs is not verifiable from the provided text, as the full grid results are in supplementary materials.
- The comparison with Epiphany, C.Origami, and ChromNet is based on a single fold and single seed, and the modifications to these methods' training procedures may affect their performance in uncharacterized ways.
- The ablation results are described qualitatively ("largest changes involve...") without reporting the actual correlation values for each condition.
- The claim that "the lead is retained on the fine-scale component" is supported by text but the actual fine-scale correlation values are not provided in the main text.
- The statement that "three published contact-map predictors retrained on the same data give lower correlation" is presented without showing the derived insulation score correlations for these methods in the main text.
- The manuscript's statement that "EpiInsula provides a framework for predicting chromatin organisation on a continuous scale from routinely available epigenomic assays" is a reasonable summary, but the generalizability to cell types without matched Hi-C data for validation is not directly demonstrated.