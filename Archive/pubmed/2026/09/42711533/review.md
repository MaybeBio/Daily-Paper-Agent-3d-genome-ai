## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and conclusions as stated in the abstract; no methods, figures, or supplementary materials were available for evaluation
- **Shared manuscript claim summary** The authors propose that cell type families across deeply divergent animals (flatworms and vertebrates) are defined by conserved sets of accessibility-dictating sequence motifs ("vocabularies"), while the combinatorial syntax among these motifs is largely species-specific. Deep-learning models trained on one species predict family-level chromatin accessibility across species but lose predictive power at the cell type level, supporting a "collective maintenance" model of regulatory evolution.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or statistical details provided
- **Missing materials affecting confidence** Methods, all figures and tables, model architecture and training details, dataset descriptions, species and cell type inventories, quantitative performance metrics, statistical analyses, and any validation or ablation experiments

## Reviewer
- **Overall assessment** This abstract presents a conceptually ambitious framework for understanding regulatory evolution at the cell type family level. The central claim, that conserved motif vocabularies maintain family identity while motif recombination drives cell type-specific divergence, is intellectually appealing and would be of broad interest if rigorously supported. However, the abstract alone provides insufficient evidence to evaluate the strength of the underlying analyses. The key claims regarding cross-species predictive accuracy, the partitioning of motifs into vocabularies, and the rapid evolution of regulatory syntax are stated without quantitative support. The conceptual framing is strong, but the evidentiary basis cannot be assessed from the supplied material.

- **Who would be interested in the results, and why** Evolutionary developmental biologists studying the deep conservation of regulatory programs; computational biologists working on cross-species regulatory genomics and deep learning; researchers interested in cell type evolution and the genotype-phenotype map. The proposed "collective maintenance" model offers a testable framework that could influence how the field thinks about homology at the regulatory level.

- **Major strengths** 
  1. The conceptual contribution is significant: distinguishing between conserved motif vocabularies and rapidly evolving combinatorial syntax provides a potentially powerful resolution to the apparent paradox of conserved cell type families despite extensive regulatory divergence.
  2. The cross-species deep-learning transfer approach is methodologically innovative and, if validated, would constitute a strong demonstration of conserved regulatory logic.
  3. The analogy to developmental homology and "character identity" is well placed and gives the work broader theoretical relevance beyond the specific datasets.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "hundreds of accessibility-dictating sequence motifs partition into distinct yet conserved sets, or 'vocabularies', each associated with a specific cell type family"
- **Evidence pointer** location not provided
- **Concern** The abstract states that motifs partition into conserved vocabularies associated with cell type families, but provides no quantitative information about how this partitioning was determined, how conservation was assessed across the two animal groups, or how robust the association with cell type families is.
- **Why it matters** This is the foundational claim upon which the entire "collective maintenance" model rests. Without evidence for the stability and distinctness of these vocabularies, the central thesis is unsupported.
- **Resolution test** Provide the number of motifs per vocabulary, the statistical significance of the partitioning, the conservation metrics across species, and the specificity of vocabulary-cell type family associations.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "Deep-learning models trained on one species accurately predict family-level chromatin accessibility in distantly related species"
- **Evidence pointer** location not provided
- **Concern** The abstract claims accurate cross-species prediction but provides no performance metrics, no comparison to baselines, and no specification of which species pairs were tested. The phrase "accurately predict" is undefined.
- **Why it matters** The cross-species transfer result is the key empirical pillar of the paper. Without quantitative evidence of predictive accuracy and appropriate controls, the claim cannot be evaluated.
- **Resolution test** Report AUPRC or AUROC values, correlation coefficients, or other relevant metrics for cross-species predictions, with comparisons to appropriate null models and species-matched controls.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "models trained on individual cell types within a family lose cross-species predictive power, indicating that the regulatory syntax governing cell type-level identity evolves rapidly"
- **Evidence pointer** location not provided
- **Concern** The contrast between family-level and cell type-level predictive power is central to the argument for rapid syntax evolution. However, no data are shown demonstrating this loss of predictive power, and the interpretation that this reflects syntax evolution rather than technical limitations (e.g., smaller training sets, cell type heterogeneity across species) is not addressed.
- **Why it matters** This claim distinguishes the authors' model from simpler alternatives. If the loss of cell type-level predictive power is due to technical factors, the conclusion about syntax evolution would be weakened.
- **Resolution test** Show the quantitative drop in performance from family-level to cell type-level models, and include analyses controlling for training set size, cell type annotation consistency, and technical batch effects.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Conceptual clarity
- **Claim pointer** "combinatorial relationships among these motifs preferred by individual cell types are largely species specific"
- **Evidence pointer** location not provided
- **Concern** The abstract states that motif combinations are species-specific but does not clarify what "largely" means quantitatively, nor how combinatorial relationships were defined and compared across species. The relationship between "preferred" combinations and functional regulatory syntax is not specified.
- **Why it matters** The distinction between conserved vocabularies and species-specific syntax is the core of the proposed model. Ambiguity in how syntax is defined and measured weakens the conceptual contribution.
- **Resolution test** Define the metric used to compare combinatorial relationships across species, report the distribution of conservation scores, and specify the threshold for "largely species specific."

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Terminology
- **Evidence pointer** Abstract, "vocabularies"
- **Issue** The term "vocabularies" is used metaphorically but not formally defined. It is unclear whether this refers to a specific computational clustering of motifs or a conceptual grouping.
- **Required correction** Provide an operational definition of "vocabulary" in the abstract or indicate where it is defined in the main text.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Scope
- **Affected element** Species coverage
- **Evidence pointer** Abstract, "two groups of vastly divergent animals including flatworms and vertebrates"
- **Issue** The abstract mentions "two groups" but does not specify how many species were analyzed within each group, nor the phylogenetic breadth of the sampling.
- **Required correction** State the number of species and the phylogenetic distance covered, or refer to the methods for this information.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Interpretation
- **Affected element** "collective maintenance" model
- **Evidence pointer** Abstract, final paragraph
- **Issue** The analogy to developmental homology is evocative but the mechanistic link between the observed data and the proposed "collective maintenance" model is not fully articulated. It is unclear what specific predictions this model makes that distinguish it from alternative explanations.
- **Required correction** Briefly state one or two testable predictions of the model that go beyond the observed data.

- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3. The core empirical claims regarding vocabulary conservation, cross-species predictive accuracy, and the loss of cell type-level predictive power are all stated without quantitative support. These are the pillars of the paper and must be substantiated with data.

- **Assessment against Nature-style criteria** 
  - Originality: High. The distinction between conserved motif vocabularies and rapidly evolving combinatorial syntax is a novel framing that could influence thinking about regulatory evolution.
  - Scientific importance: Potentially high. If the claims hold, the work would provide a mechanistic framework for understanding cell type family conservation across deep evolutionary time.
  - Interdisciplinary readership: The topic bridges evolutionary biology, genomics, and machine learning, and the conceptual framing would appeal to a broad audience.
  - Technical soundness: Cannot be assessed from the abstract. The deep-learning approach and multi-omic integration are plausible but unverifiable without methods and results.
  - Readability for nonspecialists: The abstract is well written and accessible, though terms like "accessibility-dictating sequence motifs" and "regulatory syntax" could benefit from brief clarification.

- **Recommendation posture** Currently not established from the provided evidence. The conceptual framework is promising and the work could be suitable for a high-impact venue, but the abstract alone does not provide sufficient evidence to evaluate the validity of the core claims. A full assessment requires the methods, figures, and quantitative results.

## Risk / unsupported claims
- The claim that motif vocabularies are "conserved" across flatworms and vertebrates is unsupported without conservation metrics.
- The claim of "accurate" cross-species prediction is unsupported without performance metrics or baselines.
- The claim that cell type-level models "lose cross-species predictive power" is unsupported without data and controls.
- The "collective maintenance" model is presented as a conclusion but is not derived from any visible evidence.
- The statement that regulatory syntax "evolves rapidly" is an interpretation that requires temporal calibration or comparative rate analysis not described in the abstract.