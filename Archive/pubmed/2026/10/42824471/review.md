## Review setup
- **Input scope** Full manuscript text (Mini Review, Frontiers in Plant Science)
- **Assessment boundary** Scientific content, technical soundness, clarity, and alignment with stated scope; no assessment of editorial fit or publication policy
- **Shared manuscript claim summary** The manuscript argues that sequence-to-function (seq2func) models in plant regulatory genomics, while improving in accuracy, are predominantly trained and evaluated on observational data from reference genomes, and therefore may not generalize to natural genetic, developmental, environmental, or species diversity. It proposes evaluation frameworks based on biologically meaningful distribution shifts and outlines a closed-loop experimental–computational system involving pan-genomes, multi-omics, genome editing, reporter assays, active learning, and continual learning.
- **Visible evidence base** Full text including abstract, introduction, sections on seq2func models, plant-specific challenges, causal inference, evaluation frameworks, and closed-loop systems; one figure referenced (Figure 1); one table referenced (Table 1); citations to prior work
- **Missing materials affecting confidence** Figure 1 and Table 1 are referenced but not provided; no data, code, or empirical results are included; no supplementary materials; no line numbers

## Reviewer
- **Overall assessment** This Mini Review provides a well-structured and timely synthesis of seq2func modelling in plant regulatory genomics, with a clear emphasis on generalization beyond reference genomes. The manuscript is conceptually coherent and identifies important gaps in current evaluation practices. However, several claims are made without direct evidence or detailed support, and the absence of Figure 1 and Table 1 limits full assessment. The review would benefit from more concrete examples, quantitative benchmarks, and a clearer distinction between established findings and proposed directions.
- **Who would be interested in the results, and why** Researchers in plant functional genomics, computational biology, and breeding, particularly those working on cis-regulatory element discovery, variant effect prediction, and integration of multi-omics data. The manuscript is also relevant to method developers in machine learning applied to genomics, and to those interested in causal inference and experimental design in plant systems.
- **Major strengths** The manuscript addresses a timely and important problem: the gap between reference-genome-based prediction and real-world genetic and environmental diversity in plants. The discussion of distribution shifts (covariate, label, concept) is a useful framework. The emphasis on combining observational and perturbation data, and on closed-loop systems, is forward-looking and practical. The writing is clear and accessible for a broad audience.
- **Major Concerns** Several claims are made without supporting data or detailed examples. The manuscript repeatedly states that models may not generalize, but does not provide quantitative evidence or case studies. The discussion of polyploidy and transposable elements is general and lacks specific examples of model failures. The proposed evaluation frameworks are described at a high level but not operationalized. The absence of Figure 1 and Table 1 prevents assessment of key illustrative content. Some statements are repeated verbatim (e.g., the sentence about interpretability methods), suggesting incomplete editing.
- **Minor Comments** The manuscript would benefit from a glossary of terms for nonspecialists. Some references are cited but not discussed in context. The section on closed-loop systems is speculative and could be strengthened by referencing existing examples in other fields. The conclusion is somewhat repetitive of earlier sections.
- **Technical failings that need to be addressed before the case is established** The manuscript does not provide empirical evidence or detailed case studies to support the central claim that seq2func models fail to generalize. The proposed evaluation frameworks are not tested or exemplified. The absence of Figure 1 and Table 1 means that key content cannot be evaluated. Some claims about model limitations are stated as fact without citation or data.
- **Assessment against Nature-style criteria** Originality: The manuscript offers a useful synthesis but does not present novel methods or data; the conceptual framework of distribution shifts is not new but is applied here to plant genomics in a coherent way. Scientific importance: The topic is important and timely, but the manuscript does not provide new evidence or a testable framework that would advance the field beyond current discussions. Interdisciplinary readership: The manuscript is accessible to a broad audience, but the lack of concrete examples and data may limit its impact. Technical soundness: The manuscript is technically sound in its descriptions but lacks empirical support for its central claims. Readability for nonspecialists: The writing is clear, but some sections assume familiarity with machine learning and genomics terminology.
- **Recommendation posture** Supportive if technical concerns are resolved, particularly the addition of concrete examples, quantitative benchmarks, and the inclusion of Figure 1 and Table 1. Currently, the manuscript is a reasonable review but does not establish a strong case for its central claims from the provided evidence.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** The manuscript claims that seq2func models trained on reference genomes may not generalize to natural haplotypes, structural variants, tissues, developmental stages, environments, or species.
- **Evidence pointer** Sections "Why plant genomes challenge seq2func prediction" and "Evaluating generalization in plant seq2func models"; location not provided
- **Concern** The central claim of limited generalization is stated repeatedly but is not supported by specific examples, quantitative data, or case studies. No empirical evidence is provided to demonstrate that models fail under the described distribution shifts. The manuscript would be strengthened by citing or summarizing specific studies that show performance degradation, or by presenting a small illustrative analysis.
- **Why it matters** Without evidence, the claim remains an assertion. The manuscript's value depends on convincing the reader that this is a real and important problem, not just a theoretical possibility.
- **Resolution test** Provide at least two concrete examples from the literature or from the authors' own work where seq2func models show degraded performance under covariate, label, or concept shift. Include quantitative metrics (e.g., accuracy, AUROC, calibration) comparing reference-genome and shifted settings.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Completeness of key content
- **Claim pointer** The manuscript references Figure 1 (closed-loop framework) and Table 1 (distribution shifts) as key illustrative content.
- **Evidence pointer** Figure 1 and Table 1 are referenced but not provided; location not provided
- **Concern** The manuscript relies on Figure 1 and Table 1 to convey important concepts, but these are not included in the provided material. Without them, the reader cannot fully understand the proposed framework or the taxonomy of distribution shifts.
- **Why it matters** The absence of these elements prevents a complete assessment of the manuscript's contribution and clarity. The framework and table are likely central to the authors' argument.
- **Resolution test** Include Figure 1 and Table 1 in the manuscript or provide a detailed textual description of their content. Ensure that all referenced elements are available for review.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Operationalization of proposed frameworks
- **Claim pointer** The manuscript proposes evaluation frameworks based on biologically meaningful distribution shifts and a closed-loop system involving active learning and continual learning.
- **Evidence pointer** Sections "Evaluating generalization in plant seq2func models" and "Toward closed-loop plant regulatory AI"; location not provided
- **Concern** The proposed frameworks are described at a high level but are not operationalized. No specific metrics, benchmarks, or protocols are given for implementing the distribution-shift tests. The closed-loop system is described conceptually but lacks details on how active learning or continual learning would be implemented in practice, especially given the practical barriers mentioned.
- **Why it matters** For the manuscript to be actionable, the frameworks need to be concrete enough for other researchers to adopt. Without operational details, the proposals remain aspirational.
- **Resolution test** Provide a specific example of a benchmark design, including data sources, split strategies, and evaluation metrics. For the closed-loop system, describe a concrete workflow with steps, data types, and decision criteria.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Repetition and editing
- **Claim pointer** The manuscript contains a duplicated sentence about interpretability methods.
- **Evidence pointer** Section "Evaluating generalization in plant seq2func models"; location not provided
- **Concern** The sentence "Interpretability methods, including attribution maps and in silico mutagenesis, should be treated as hypotheses rather than causal proof" appears twice in the same section. This suggests incomplete editing and detracts from the manuscript's professionalism.
- **Why it matters** Repetition undermines clarity and may indicate a lack of careful revision, which is important for a review article.
- **Resolution test** Remove the duplicate sentence and ensure the text is free of unintended repetition.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity for nonspecialists
- **Affected element** Introduction and Section "Sequence-to-function models and plant regulatory genomics"
- **Evidence pointer** Location not provided
- **Issue** Terms such as "one-hot-encoded DNA sequences," "attention-based, state-space, and other long-context architectures," and "TF-MoDISco-style motif clustering" are used without definition or explanation.
- **Required correction** Add brief definitions or a glossary for these terms to improve accessibility for readers outside computational biology.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Citation completeness
- **Affected element** Section "Why plant genomes challenge seq2func prediction"
- **Evidence pointer** Location not provided
- **Issue** Some statements about plant genome diversity and transposable elements are made without specific citations (e.g., "Maize provides a prominent example of extensive structural and transposable-element variation").
- **Required correction** Add citations to support these statements, or clarify that they are general knowledge.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Consistency of terminology
- **Affected element** Throughout
- **Evidence pointer** Location not provided
- **Issue** The term "seq2func" is defined in the abstract and introduction, but the manuscript also uses "sequence-to-function" and "sequence-to-function (seq2func)" interchangeably.
- **Required correction** Use "seq2func" consistently after first definition, or define the abbreviation once and use it throughout.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Structure and flow
- **Affected element** Section "From observational prediction to causal inference"
- **Evidence pointer** Location not provided
- **Issue** The subsection "Bridging seq2func predictions to organismal phenotypes in plants" is placed within the causal inference section but reads more like a separate topic. The transition is abrupt.
- **Required correction** Consider moving this subsection to a separate section or integrating it more smoothly with the preceding discussion.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Speculative content
- **Affected element** Section "Toward closed-loop plant regulatory AI"
- **Evidence pointer** Location not provided
- **Issue** The discussion of active learning and continual learning is speculative and does not reference any existing implementations in plant genomics.
- **Required correction** Either cite examples from other fields or clearly label this as a proposal for future work.

## Risk / unsupported claims
- The claim that seq2func models "may not translate" to natural diversity is unsupported by direct evidence in the manuscript.
- The claim that "aggregate scores can conceal poor performance" is plausible but not demonstrated with examples.
- The claim that "longer context alone does not guarantee mechanistic insight or generalization" is stated without supporting data.
- The proposed closed-loop framework is not supported by any empirical or simulation-based evidence.
- The statement that "interpretability methods... should be treated as hypotheses rather than causal proof" is a reasonable recommendation but is presented as a conclusion without discussion of counterarguments.
- The manuscript's assertion that "a practical near-term roadmap is to establish two or three well-characterized anchor loci" is a proposal, not a finding, and is not supported by feasibility analysis.