## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence presented in the abstract
- **Shared manuscript claim summary** The authors propose that cell type families across distantly related animals (flatworms and vertebrates) are defined by evolutionarily stable sets of sequence motifs ("vocabularies"), while cell type-specific regulatory syntax evolves rapidly through combinatorial recombination of these motifs.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or supplementary materials provided
- **Missing materials affecting confidence** Full manuscript, including methods, figures, tables, supplementary data, and detailed results; no access to the deep learning model architecture, training data, or validation procedures

## Reviewer
- **Overall assessment** The abstract presents a conceptually interesting and potentially important model for the evolution of cell type regulatory programs. The central idea—that motif vocabularies are conserved at the family level while their combinatorial syntax evolves rapidly—is novel and could have broad implications for evolutionary developmental biology and regulatory genomics. However, the abstract alone provides insufficient evidence to evaluate the robustness of the key claims. Critical details about the experimental design, computational methods, statistical validation, and the nature of the "collective maintenance" model are absent. The claims are intriguing but currently not established from the provided evidence.

- **Who would be interested in the results, and why** Evolutionary biologists, developmental biologists, and computational genomicists interested in the evolution of gene regulation, cell type identity, and the mechanisms underlying phenotypic diversity. The proposed "collective maintenance" model offers a potential framework for understanding how cell type families are conserved across deep evolutionary time, which is a fundamental question in evolutionary biology.

- **Major strengths** 
  1. The central hypothesis—that motif vocabularies are conserved at the family level while syntax evolves rapidly—is conceptually elegant and addresses a long-standing question in evolutionary regulatory biology.
  2. The use of cross-species deep learning predictions to distinguish between family-level and cell type-level regulatory conservation is a clever and potentially powerful approach.
  3. The analogy to developmental homology and network-level conservation provides a compelling theoretical framework that connects the findings to broader biological principles.

- **Major Concerns**
  - **Concern ID** R1-M1
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Evidence sufficiency
  - **Claim pointer** "hundreds of accessibility-dictating sequence motifs partition into distinct yet conserved sets, or 'vocabularies', each associated with a specific cell type family"
  - **Evidence pointer** Abstract; location not provided
  - **Concern** The abstract states that motifs partition into conserved vocabularies associated with cell type families, but provides no quantitative evidence for this claim. It is unclear how the vocabularies were defined, how conservation was assessed across flatworms and vertebrates, and what statistical criteria were used to establish the association with cell type families. Without details on the number of species, the number of cell types, the method for motif discovery and clustering, and the conservation metrics, this central claim cannot be evaluated.
  - **Why it matters** The existence of conserved motif vocabularies is the foundational claim of the paper. If this claim is not robustly supported, the entire "collective maintenance" model collapses.
  - **Resolution test** Provide a clear description of the method used to define motif vocabularies, including the number of motifs, the clustering algorithm, the conservation metric (e.g., sequence identity, position weight matrix similarity), and the statistical test for association with cell type families. Show that the vocabularies are significantly enriched in specific cell type families across multiple species.

  - **Concern ID** R1-M2
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Evidence sufficiency
  - **Claim pointer** "Deep-learning models trained on one species accurately predict family-level chromatin accessibility in distantly related species, albeit frequently rely on different motifs from shared vocabularies to reach convergent predictions."
  - **Evidence pointer** Abstract; location not provided
  - **Concern** The abstract claims that deep learning models achieve accurate cross-species predictions, but provides no quantitative performance metrics (e.g., AUC, correlation coefficients, precision-recall). The phrase "frequently rely on different motifs" is vague and lacks a formal definition or statistical test. It is also unclear how the models' reliance on specific motifs was determined (e.g., via attribution methods like saliency maps or SHAP values) and how "convergent predictions" were defined.
  - **Why it matters** The cross-species predictive power of the models is the key experimental evidence for the conservation of motif vocabularies. Without quantitative metrics and a rigorous analysis of motif usage, the claim is unsubstantiated.
  - **Resolution test** Report the prediction accuracy (e.g., area under the ROC curve) for cross-species predictions, along with appropriate baselines (e.g., shuffled controls, models trained on random data). Describe the method used to identify motifs that drive predictions (e.g., in silico mutagenesis, integrated gradients) and provide a statistical test for the claim that different motifs from the same vocabulary are used.

  - **Concern ID** R1-M3
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Evidence sufficiency
  - **Claim pointer** "models trained on individual cell types within a family lose cross-species predictive power, indicating that the regulatory syntax governing cell type-level identity evolves rapidly."
  - **Evidence pointer** Abstract; location not provided
  - **Concern** The abstract contrasts family-level and cell type-level model performance, but does not specify how "individual cell types within a family" were defined or how the models were trained. It is unclear whether the loss of predictive power is due to rapid evolution of syntax, or to other factors such as reduced training data, overfitting, or differences in cell type homology across species. The claim that syntax evolves rapidly is an inference that requires direct evidence of motif combinatorial changes.
  - **Why it matters** This contrast is central to the paper's main conclusion that syntax evolves rapidly while vocabularies are stable. If the loss of predictive power has alternative explanations, the conclusion is weakened.
  - **Resolution test** Show that the loss of predictive power is not due to technical artifacts (e.g., by controlling for training set size, cell type purity, and species-specific biases). Provide direct evidence of motif combinatorial changes (e.g., changes in motif spacing, orientation, or co-occurrence patterns) between homologous cell types in different species.

- **Minor Comments**
  - **Concern ID** R1-m1
  - **Severity** Minor
  - **Axis** Clarity
  - **Affected element** Terminology
  - **Evidence pointer** Abstract
  - **Issue** The term "vocabularies" is used to describe conserved motif sets, but the abstract does not define what constitutes a "vocabulary" (e.g., a set of motifs that co-occur in a cell type family, or a set of motifs that are bound by a common set of transcription factors). This ambiguity could lead to confusion.
  - **Required correction** Provide a clear operational definition of "motif vocabulary" in the abstract or main text, including the criteria for membership and the method for delineating vocabularies.

  - **Concern ID** R1-m2
  - **Severity** Minor
  - **Axis** Completeness
  - **Affected element** Model description
  - **Evidence pointer** Abstract
  - **Issue** The abstract mentions "deep learning" but does not specify the model architecture (e.g., convolutional neural network, transformer) or the input features (e.g., DNA sequence, chromatin accessibility peaks). This lack of detail makes it difficult to assess the appropriateness of the method.
  - **Required correction** Briefly describe the model architecture and input features in the abstract or main text.

  - **Concern ID** R1-m3
  - **Severity** Minor
  - **Axis** Scope
  - **Affected element** Generalizability
  - **Evidence pointer** Abstract
  - **Issue** The study compares flatworms and vertebrates, which are vastly divergent, but it is unclear whether the findings are generalizable to other animal groups (e.g., arthropods, mollusks). The abstract does not discuss the potential limitations of the two-group comparison.
  - **Required correction** Acknowledge the limited taxonomic scope and discuss the potential for broader generalizability in the main text.

- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3. The core claims of conserved motif vocabularies, accurate cross-species predictions, and rapid syntax evolution are all unsupported by the abstract alone. Quantitative evidence, methodological details, and rigorous statistical tests are required.

- **Assessment against Nature-style criteria**
  - **Originality**: High. The "collective maintenance" model is a novel conceptual framework that integrates motif conservation with combinatorial syntax evolution.
  - **Scientific importance**: Potentially high. If validated, the model could provide a unifying principle for understanding cell type evolution and regulatory conservation across deep time.
  - **Interdisciplinary readership**: Moderate to high. The topic bridges evolutionary biology, genomics, and computational biology, and the conceptual model is accessible to a broad audience.
  - **Technical soundness**: Cannot be assessed from the abstract alone. The claims rely on complex computational analyses that require rigorous validation.
  - **Readability for nonspecialists**: The abstract is well-written and the central analogy to developmental homology is helpful. However, terms like "motif vocabularies" and "regulatory syntax" could be better defined for a general audience.

- **Recommendation posture** Currently not established from the provided evidence. The abstract presents a compelling hypothesis, but the key claims are unsupported by quantitative data or methodological details. A full manuscript with rigorous evidence is required to evaluate the validity of the model. The recommendation is supportive if the technical concerns are resolved in the full manuscript.

## Risk / unsupported claims
- The existence of conserved motif vocabularies associated with cell type families (R1-M1).
- The claim that deep learning models trained on one species accurately predict family-level chromatin accessibility in distantly related species (R1-M2).
- The claim that models trained on individual cell types lose cross-species predictive power due to rapid evolution of regulatory syntax (R1-M3).
- The "collective maintenance" model as a whole, as it is an inference from the above unsupported claims.