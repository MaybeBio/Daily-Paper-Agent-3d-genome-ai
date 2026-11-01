## Review setup
- **Input scope** Full manuscript text (abstract, introduction, methods, results, discussion, conclusions) without figures, tables, or supplementary materials
- **Assessment boundary** Scientific validity, methodological rigor, and interpretation of reported results based on the provided text only
- **Shared manuscript claim summary** The authors benchmark six deep learning models for eQTL prediction across nine xQTL classes, finding variable cross-task transferability, with foundation models (AlphaGenome, Borzoi) performing best, and apply these models to prioritize candidate caQTLs in coronary artery disease GWAS loci
- **Visible evidence base** Text descriptions of results, performance metrics mentioned in text (AUROC, AUPRC, F1, MCC, Brier scores), sensitivity analyses described, enrichment analyses described
- **Missing materials affecting confidence** All figures, tables, supplementary materials, and the GitHub repository contents were not provided; exact performance values for many comparisons are only described qualitatively in text

## Reviewer
- **Overall assessment** This manuscript addresses an important and timely question: whether deep learning models trained for eQTL prediction generalize across diverse molecular QTL types. The cross-task benchmarking framework is well conceived, and the inclusion of six models spanning annotation-based, local-sequence, and long-range genomic foundation models provides a useful comparative landscape. The finding that performance varies substantially across xQTL types, with chromatin-related QTLs being more predictable than looping or microRNA QTLs, is biologically plausible and of practical value. However, the manuscript as presented has several limitations that temper enthusiasm. The reliance on text descriptions without access to the actual figures and tables makes full verification impossible, but even from the text, several concerns emerge: the negative control construction may introduce biases not fully addressed, the comparison across models with different feature dimensionalities is acknowledged but not resolved, and the clinical application section, while interesting, would benefit from clearer demonstration that the predicted caQTLs add information beyond existing annotations. The sensitivity analyses described are commendable and suggest robustness, but the manuscript would be strengthened by more explicit reporting of confidence intervals or variability measures across the random seeds tested.

- **Who would be interested in the results, and why** Computational biologists and bioinformaticians developing or applying deep learning models for regulatory variant interpretation would find this benchmarking useful for model selection. Statistical geneticists working on fine-mapping and variant prioritization in GWAS follow-up studies would be interested in the practical application to CAD. Researchers studying the genetic architecture of gene regulation across molecular phenotypes would benefit from the cross-xQTL perspective. The finding that tree-based classifiers substantially outperform linear models on deep learning features is methodologically informative for the broader machine learning for genomics community.

- **Major strengths**
  1. The cross-xQTL benchmarking framework addresses a genuine gap in the field, as most evaluations focus on eQTLs alone
  2. The inclusion of six models spanning different architectural paradigms (annotation-based, local sequence, long-range foundation models) provides a comprehensive comparison
  3. The sensitivity analyses addressing negative control selection, random seed variability, and classification threshold are rigorous and strengthen confidence in the main findings
  4. The application to CAD GWAS loci demonstrates practical utility and provides biological validation through enrichment analyses and allele-specific DNase-seq signal differences
  5. The discussion of limitations, including feature dimensionality confounding and the exclusion of emerging DNA language models, is honest and balanced

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Experimental design and control selection
- **Claim pointer** The authors claim that negative controls were "randomly selected from the 1000 Genomes Project reference panel at a 1:10 ratio relative to the number of significant xQTLs" and that a "more stringently matched negative-control set" was constructed for sensitivity analysis
- **Evidence pointer** Materials and methods, Data collection and processing; Results, Cross-xQTL prediction performance
- **Concern** The primary negative control selection strategy of random sampling from 1000 Genomes without matching for genomic context, MAF, or LD structure may introduce substantial confounding. Randomly selected variants are likely to differ systematically from true xQTLs in allele frequency, local sequence composition, and proximity to genes or regulatory elements. While the authors describe a matched control set for sensitivity analysis, the primary results rely on the unmatched controls. The matched control set requires variants to be at least 500 kb from xQTLs and matched by MAF and regulatory annotation, but the text does not clarify whether this matched set was used for all nine xQTL types or only a subset, nor does it report the number of controls successfully matched. If matching substantially reduced the control pool, statistical power may be compromised.
- **Why it matters** The choice of negative controls is arguably the most consequential decision in any variant effect prediction benchmark. If controls are not matched on key confounders, the reported performance differences between models may reflect differences in how well each model captures these confounders rather than true biological signal. This directly affects the validity of the central claim that foundation models generalize better across xQTL types.
- **Resolution test** The authors should report the number of matched controls achieved for each xQTL type, demonstrate that the matched and unmatched control sets produce similar conclusions, and ideally include a third control set matched for LD structure or genomic position. If the matched control analysis is only reported in supplementary materials, it should be moved to the main text for the primary performance comparisons.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** No
- **Axis** Statistical rigor and uncertainty quantification
- **Claim pointer** The authors report performance differences between models (e.g., "AlphaGenome achieved the best overall performance (AUROC = 0.810, AUPRC = 0.389)") and state that "standard deviations ranging from 0.00012 to 0.00735 for AUROC" across random seeds
- **Evidence pointer** Results, Comparative evaluation of model prediction performance for eQTL identification; Results, Cross-xQTL prediction performance
- **Concern** The manuscript reports point estimates for performance metrics but does not describe any formal statistical testing for differences between models. The random seed variability is reported as standard deviations, but it is unclear whether these represent variability across three seeds only, which is a very small sample for estimating uncertainty. No confidence intervals are provided for the AUROC or AUPRC values, and no statistical test (e.g., DeLong test for correlated ROC curves, or bootstrap-based comparisons) is described to establish whether observed differences between models are statistically significant. The text frequently uses qualitative language such as "consistently outperformed" and "substantially reduced" without quantitative support.
- **Why it matters** The central claims of the paper are about relative model performance. Without formal statistical comparison, readers cannot assess whether the observed differences are meaningful or within the range of sampling variability. This is particularly important for the more nuanced claims, such as intermediate performance for apaQTLs, pQTLs, and sQTLs, where differences between models may be small.
- **Resolution test** The authors should provide confidence intervals for all reported performance metrics, perform formal statistical comparisons between models (e.g., DeLong tests for AUROC differences, or bootstrap-based tests for AUPRC), and report the number of bootstrap replicates or the specific test used. For the random seed analysis, they should clarify whether three seeds is the total and acknowledge the limitation of this approach for uncertainty estimation.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Clinical application and validation
- **Claim pointer** The authors claim that applying AlphaGenome and Borzoi to CAD GWAS loci "identifies 337 high-confidence candidate chromatin accessibility QTLs, including 11 previously reported and 326 candidates that display significantly larger allele-specific differences in predicted chromatin accessibility signals"
- **Evidence pointer** Results, Identification of novel CAD-associated caQTLs; Discussion
- **Concern** The clinical application section, while potentially valuable, raises several questions. First, the threshold for "high-confidence" is not defined in the text. Second, the validation is limited to allele-specific differences in predicted chromatin accessibility signals, which is somewhat circular since the models were trained to predict such signals. The enrichment analyses for cholesterol metabolism and atherosclerosis are supportive but do not establish causality. The authors acknowledge that "fine-mapping, colocalization, or orthogonal functional assays will be required to establish their causal roles," which is appropriate, but the current validation is relatively weak. Third, the overlap with previously reported caQTLs is only 11 out of 337, which raises the question of whether the remaining 326 are genuinely novel or false positives. Fourth, the text mentions that 9 CAD variants overlapped with positive caQTL training samples and 15 with negative controls, but the implications of this overlap for potential data leakage are not discussed.
- **Why it matters** The clinical application is presented as a demonstration of practical utility, but the validation is insufficient to establish that the predicted caQTLs are biologically meaningful. If the primary value of the paper is the benchmarking framework, the clinical application is secondary, but it should be presented with appropriate caveats and stronger validation or clearly framed as hypothesis-generating.
- **Resolution test** The authors should define the threshold for high-confidence predictions, provide a more detailed comparison of the 11 previously reported versus 326 novel caQTLs (e.g., effect sizes, genomic annotations), discuss the potential for data leakage given the overlap with training samples, and either strengthen the validation (e.g., with independent functional data) or explicitly frame the CAD application as hypothesis-generating rather than validated.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Feature comparability and confounding
- **Claim pointer** The authors state that "all benchmarking analyses were conducted using a unified preprocessing and evaluation pipeline" and that features were "retained as generated by the original models to preserve their intended regulatory information"
- **Evidence pointer** Materials and methods, Framework for cross-xQTL prediction; Discussion
- **Concern** The authors acknowledge that the six models generate features with different dimensionalities, which they note "may represent a potential confounding factor when comparing model performance." However, this issue is not addressed beyond acknowledgment. Models with higher-dimensional features may perform better simply because they provide more information to the downstream classifier, regardless of the quality of the underlying biological representation. Additionally, the text does not describe how features were normalized or standardized across models before being fed to the classifiers, which could affect performance. The comparison between annotation-based (GWAVA) and sequence-based models is particularly problematic, as these feature types are fundamentally different in nature.
- **Why it matters** The central benchmarking claim requires that performance differences reflect genuine differences in model quality rather than artifacts of feature dimensionality or preprocessing. Without addressing this, the ranking of models may be misleading.
- **Resolution test** The authors should either (a) perform a dimensionality-controlled comparison, such as using PCA or feature selection to match feature counts across models, (b) report performance as a function of feature dimensionality to demonstrate that the observed differences are not simply a consequence of more features, or (c) provide a more thorough discussion of why feature dimensionality is unlikely to explain the observed patterns, with supporting analysis.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Reporting clarity
- **Affected element** Performance metrics reporting
- **Evidence pointer** Results, Comparative evaluation of model prediction performance for eQTL identification
- **Issue** The text reports AUROC and AUPRC values for some models but not all, and the values for F1, MCC, and Brier scores are mentioned as being in Table 1 without specific numbers in the text. This makes it difficult to follow the comparative narrative without constantly referring to the table.
- **Required correction** Consider reporting all key metrics for the main comparisons in the text, or at least for the top-performing and bottom-performing models, to make the results section self-contained.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Terminology precision
- **Affected element** Use of "foundation models"
- **Evidence pointer** Abstract; Introduction; Results
- **Issue** The term "foundation models" is used to describe AlphaGenome and Borzoi, but the text also includes Enformer in this category in some places. The distinction between "foundation models" and "sequence-based models" is not consistently applied, which could confuse readers about which models belong to which category.
- **Required correction** Define the model categories explicitly and use them consistently throughout the manuscript.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Methodological detail
- **Affected element** Classifier training details
- **Evidence pointer** Materials and methods, Framework for cross-xQTL prediction
- **Issue** The text states that XGBoost classifiers were trained with hyperparameter optimization using 5-fold cross-validation, but does not describe the hyperparameter search space, the number of tuning iterations, or the criteria for selecting the final hyperparameters. Similarly, the Random Forest and linear models are mentioned but not described in detail.
- **Required correction** Provide additional details on the hyperparameter search procedure, including the parameter grids and the selection criteria, to enable reproducibility.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Data availability
- **Affected element** Source data for figures
- **Evidence pointer** Data availability
- **Issue** The data availability statement mentions a GitHub repository for code and candidate caQTLs, but does not mention whether the underlying xQTL datasets, processed features, or model predictions will be made available. This limits reproducibility.
- **Required correction** Consider depositing the processed feature matrices and model predictions in a public repository, or clearly state why these cannot be shared.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Discussion completeness
- **Affected element** Comparison with prior benchmarks
- **Evidence pointer** Discussion
- **Issue** The discussion does not compare the findings with prior benchmarking studies of regulatory variant prediction models, which would help contextualize the results and highlight what is newly learned.
- **Required correction** Add a brief comparison with relevant prior benchmarking efforts, noting where the current findings agree or disagree.

## Risk / unsupported claims
- The claim that "foundation models consistently outperform local-context and annotation-based models" across all xQTL types is not fully supported by the text, as specific performance values for all models across all nine xQTL types are not provided in the visible text
- The claim that "326 candidates that display significantly larger allele-specific differences in predicted chromatin accessibility signals" implies biological validation, but this is based on model predictions rather than independent experimental data
- The statement that "the concordance between AlphaGenome and Borzoi provides a consensus-based prioritization strategy" is reasonable but the clinical utility of this strategy is not demonstrated with external validation
- The claim that "tree-based ensemble methods provide a stable advantage in ranking causal variants" is based on the described analyses, but the text does not report whether this advantage was consistent across all xQTL types or only for specific ones
- The assertion that "the degree of tissue and cell-type correspondence between the model pretraining data and the xQTL datasets may influence model performance" is presented as a possible explanation but is not directly tested in the reported analyses