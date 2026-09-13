## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no full text, figures, tables, or supplementary materials were provided
- **Shared manuscript claim summary** The authors present DNABERT-Enhancer, a fine-tuned DNABERT model for predicting enhancers in the human genome. They report benchmark performance (88.05% accuracy, 76% Matthews correlation coefficient), genome-wide predictions (1,684,595 enhancer regions covering 26.65% of the genome), and integrative variant effect analyses identifying 2,681 loss-of-function and 1,917 gain-of-function enhancer variants, plus 4,057 candidate de novo enhancers. Resources are made available via GitHub, a web application, and Zenodo.
- **Visible evidence base** Abstract text only; no methods, figures, tables, or supplementary data were provided
- **Missing materials affecting confidence** Full methods, benchmark dataset construction details, model architecture and hyperparameters, independent dataset composition, variant effect analysis methodology, statistical thresholds, validation strategies, and all quantitative results beyond those stated in the abstract

## Reviewer
- **Overall assessment** The abstract describes a potentially useful application of a pre-trained genomic language model to enhancer prediction, with substantial genome-wide outputs and a public resource. However, the abstract alone does not provide sufficient methodological detail to assess the validity of the performance claims, the rigor of the variant effect analyses, or the biological meaning of the genome-wide predictions. The core claims are plausible but currently not verifiable from the supplied material.
- **Who would be interested in the results, and why** Researchers in regulatory genomics, genome interpretation, and clinical variant annotation would be interested. The predicted enhancer annotations and candidate functional variants could serve as resources for studying gene regulation and interpreting non-coding variants in disease contexts. The application of a language model approach to enhancer prediction may also interest computational biologists working on sequence-based regulatory prediction.
- **Major strengths** The work addresses a relevant problem in regulatory genomics. The use of a pre-trained genomic language model is a current and reasonable approach. The authors provide public access to the model, predictions, and archived fine-tuned models, which supports reproducibility and community use. The scale of genome-wide predictions and the integration with transcription factor models suggest a substantial computational effort.
- **Major Concerns** 
  - R1-M1
  - R1-M2
  - R1-M3
  - R1-M4
- **Minor Comments** 
  - R1-m1
  - R1-m2
  - R1-m3
- **Technical failings that need to be addressed before the case is established** R1-M1 (benchmark validity), R1-M2 (variant effect methodology), R1-M3 (genome-wide prediction interpretation), R1-M4 (de novo enhancer claim)
- **Assessment against Nature-style criteria** Originality: moderate, as language model applications to regulatory genomics are emerging but not yet saturated. Scientific importance: potentially high if the predictions are validated, but the abstract does not demonstrate biological validation. Interdisciplinary readership: the topic bridges computational biology and genomics, but the abstract is written for a specialist audience. Technical soundness: cannot be assessed from the abstract alone; key methodological details are missing. Readability for nonspecialists: the abstract is dense and assumes familiarity with ENCODE, cCREs, and language model terminology, which limits accessibility.
- **Recommendation posture** Currently not established from the provided evidence. The claims are interesting and the resource is potentially valuable, but the abstract does not provide enough methodological detail to support the performance and variant effect conclusions. A full manuscript with methods, validation, and biological interpretation would be required to assess the case.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The best fine-tuned model achieved 88.05% accuracy and a Matthews correlation coefficient of 76% on an independent dataset.
- **Evidence pointer** Abstract, Results section; location not provided
- **Concern** The abstract reports performance metrics but does not describe the composition of the independent dataset, how it was selected, whether it overlaps with training data, or what baseline models were compared against. Without this information, the reported accuracy and MCC cannot be interpreted as evidence of generalizable performance.
- **Why it matters** Performance claims are central to the paper's contribution. If the independent dataset is not truly independent or is imbalanced, the metrics could be misleading. The absence of baseline comparisons prevents assessment of whether DNABERT-Enhancer improves upon existing methods.
- **Resolution test** Provide a detailed description of the independent dataset, including source, filtering criteria, and class balance. Report performance against at least one established enhancer prediction method. State whether any sequence similarity filtering was applied to avoid training-test leakage.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** By performing integrative analyses with DNABERT-based transcription factor models, we identify 2,681 statistically significant loss-of-function and 1,917 gain-of-function enhancer variants, which respectively alter the function of 1,623 and 1,247 ENCODE-cCRE enhancers.
- **Evidence pointer** Abstract, Results section; location not provided
- **Concern** The abstract does not describe the variant effect prediction methodology, the statistical test used, the multiple testing correction applied, or the threshold for significance. It is unclear how "loss-of-function" and "gain-of-function" are defined and whether these predictions were validated experimentally or against known variant effect databases.
- **Why it matters** Variant effect predictions are a major claimed contribution. Without methodological detail and validation, these numbers cannot be interpreted as reliable. The distinction between loss- and gain-of-function has clinical implications, so unsupported claims could mislead downstream users.
- **Resolution test** Describe the variant effect scoring method, the statistical framework, the significance threshold, and the multiple testing correction. Provide validation against known functional variants or experimental data. Clarify the definition of loss- and gain-of-function in this context.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Scientific importance
- **Claim pointer** Genome-wide application identified 1,684,595 enhancer regions covering 26.65% of the human genome.
- **Evidence pointer** Abstract, Results section; location not provided
- **Concern** The abstract reports a very large number of predicted enhancer regions covering more than a quarter of the genome. This is a striking claim that raises questions about the specificity of the model. The abstract does not provide any assessment of the precision of these predictions, such as overlap with known regulatory elements, chromatin state data, or functional validation.
- **Why it matters** If the model predicts enhancers across 26.65% of the genome, this may indicate low specificity and could undermine the utility of the resource. The biological plausibility of such a large fraction of the genome being enhancers needs to be addressed.
- **Resolution test** Provide precision estimates against independent enhancer annotations or experimental data. Report the distribution of predicted enhancer scores and justify the threshold used. Discuss the biological interpretation of the predicted genomic coverage.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** Similarly, we identify 4,057 candidate de novo enhancers, created by 5,464 gain-of-function variants.
- **Evidence pointer** Abstract, Results section; location not provided
- **Concern** The concept of "de novo enhancers" created by variants is not defined in the abstract. It is unclear how a variant can create an enhancer de novo, what evidence supports this, and how these predictions differ from the gain-of-function variants mentioned earlier. The distinction between the two categories is ambiguous.
- **Why it matters** This is a novel and potentially important claim, but without a clear definition and supporting evidence, it cannot be evaluated. If the claim is not well-supported, it could be seen as overinterpretation of model outputs.
- **Resolution test** Define what constitutes a de novo enhancer in this context. Provide examples with supporting evidence, such as chromatin state changes or experimental validation. Clarify the relationship between gain-of-function variants and de novo enhancer creation.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Benchmark dataset construction
- **Evidence pointer** Abstract, Methods section; location not provided
- **Issue** The abstract states that a benchmark dataset was curated from ENCODE cCREs, with 21,926 enhancers of 201 bp and 46,159 enhancers of 350 bp, but does not describe how negative examples were selected or whether the dataset is balanced.
- **Required correction** Provide details on negative set construction, class balance, and any filtering steps in the full manuscript.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Terminology
- **Evidence pointer** Abstract, Results section; location not provided
- **Issue** The terms "loss-of-function" and "gain-of-function" are used for enhancer variants, but it is not clear whether these refer to predicted changes in enhancer activity, transcription factor binding, or downstream gene expression.
- **Required correction** Define these terms explicitly in the manuscript and state the biological level at which the functional effect is predicted.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Accessibility
- **Affected element** Resource description
- **Evidence pointer** Abstract, Availability section; location not provided
- **Issue** The abstract mentions a web application and GitHub repository but does not describe the format of the predictions, how users can query the data, or whether the model can be run locally.
- **Required correction** Include a brief description of the resource interface and data format in the full manuscript.

## Risk / unsupported claims
- The reported accuracy and MCC values are unsupported without details on the independent dataset and baseline comparisons.
- The numbers of loss-of-function and gain-of-function variants are unsupported without methodological description and validation.
- The claim of 1,684,595 enhancer regions covering 26.65% of the genome is unsupported without precision estimates or biological validation.
- The identification of 4,057 candidate de novo enhancers is unsupported without a clear definition and evidence.
- The statement that these resources are "valuable for genome interpretation in functional and clinical genomics studies" is an assertion that cannot be evaluated from the abstract alone.