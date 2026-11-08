## Review setup
- **Input scope** Full manuscript text (abstract, main text, references cited within text)
- **Assessment boundary** Scientific content, methodological framing, evidence quality, and internal consistency of the review as presented; no external literature verification performed
- **Shared manuscript claim summary** The manuscript is a narrative mini-review of AI and computational methods for reconstructing cell-state-specific gene regulatory networks from single-cell transcriptome and chromatin accessibility data in cancer. It proposes a taxonomy of four method families, an evidence hierarchy from statistical association to experimentally supported causal regulation, and a decision framework for method selection. It surveys applications in EMT, treatment resistance, lineage plasticity, and tumor subtyping, and discusses benchmarking, limitations, and translational prospects.
- **Visible evidence base** Full text of the manuscript including abstract, introduction, methods sections, applications sections, validation discussion, and conclusion. No figures, tables, or supplementary materials were provided.
- **Missing materials affecting confidence** Figures 1 and 2, Table 1, and all cited references were not provided. The absence of Table 1, which is referenced as the comparative summary of methods, limits verification of the claimed taxonomy and method categorization. The absence of figures limits assessment of the decision framework and workflow diagrams.

## Reviewer
- **Overall assessment** This is a well-structured and clearly written narrative review that addresses a timely and important topic. The authors propose a useful conceptual framework distinguishing four method families and an explicit evidence hierarchy, which helps clarify the often-conflated claims in this literature. The cancer applications section is informative and appropriately caveated. However, the review is limited by the absence of the comparative table and figures, which are central to the claimed contributions. The evidence hierarchy is well articulated but its application to the surveyed methods is not systematically demonstrated. The benchmarking discussion is thoughtful but lacks concrete recommendations or a critical comparison of existing benchmarks. The review would be strengthened by a more explicit mapping of each method to the evidence hierarchy and by a clearer articulation of what distinguishes this review from prior ones beyond scope.

- **Who would be interested in the results, and why** Computational biologists and bioinformaticians developing or applying single-cell multi-omics integration methods, particularly those focused on gene regulatory network inference. Cancer biologists studying tumor heterogeneity, cell-state transitions, treatment resistance, and lineage plasticity would find the applications section useful. Methodologists interested in benchmarking and validation standards for network inference would also benefit. The review provides a practical entry point for researchers new to this area who need guidance on method selection based on data availability and research question.

- **Major strengths**
  - Clear and explicit taxonomy of four method families based on inference objective and input requirement
  - Well-articulated evidence hierarchy distinguishing statistical association, directional prediction, in silico perturbation, and experimentally supported causal regulation
  - Practical decision framework for method selection based on data type and research question
  - Appropriate caveats about the limitations of virtual perturbation and attention-based interpretability
  - Honest acknowledgment of the review's own limitations as a narrative synthesis
  - Cancer applications are well chosen and illustrate the range of possible uses

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence completeness
- **Claim pointer** The manuscript claims to provide a comparative analysis of representative methods organized by data type, modeling strategy, cell-state resolution, and validation approach, as stated in the section on AI frameworks for GRN inference.
- **Evidence pointer** Table 1, referenced in the text but not provided
- **Concern** Table 1, which is described as comparing representative methods by data type, modeling strategy, cell-state resolution, and validation approach, was not included in the provided materials. This table appears central to the review's comparative contribution and to the claimed taxonomy.
- **Why it matters** Without the table, the reader cannot verify the categorization of methods into the four families, cannot compare methods across the stated dimensions, and cannot assess whether the taxonomy is consistently applied. The review's practical value as a method selection guide depends substantially on this comparative resource.
- **Resolution test** Provide Table 1 and confirm that all methods discussed in the text are included, that the categorization is consistent with the text, and that the comparison dimensions are applied uniformly.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** No
- **Axis** Methodological rigor
- **Claim pointer** The manuscript states that benchmarking and limitations are examined, and that benchmarks should state what they can and cannot establish, report label coverage and observable metric ceilings, and test incremental value over simple baselines.
- **Evidence pointer** Section "AI frameworks for GRN inference", subsection on evaluating GRN methods
- **Concern** The benchmarking discussion is prescriptive but does not provide a concrete assessment of existing benchmarks. The authors do not identify which benchmarks are most useful for cell-state-specific GRN inference, what their specific limitations are, or how the proposed standards would change current practice. The discussion of label completeness and metric ceilings is valuable but remains at the level of general principle.
- **Why it matters** A review that identifies benchmarking as a central challenge should provide more specific guidance. Without a critical evaluation of existing benchmarks, the reader is left with principles but no sense of which tools to use or what to expect from them. This weakens the practical utility of the review.
- **Resolution test** Add a subsection that critically evaluates 2-3 existing benchmarks for single-cell GRN inference, identifies their specific limitations for cell-state-specific reconstruction, and provides concrete recommendations for benchmark design in this setting.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Evidence hierarchy application
- **Claim pointer** The manuscript proposes an evidence hierarchy from statistical association to directional prediction, in silico perturbation, and experimentally supported causal regulation, and states that keeping these levels distinct clarifies what each method can claim.
- **Evidence pointer** Section "AI frameworks for GRN inference", final paragraph; Section "Applications of cell-state-specific GRNs in cancer"
- **Concern** The evidence hierarchy is clearly defined but is not systematically applied to the surveyed methods. The applications section discusses studies with varying levels of evidence, but the hierarchy is not used to classify or compare the strength of evidence across the presented examples. The reader is told which level each study reaches in some cases, but a systematic mapping is absent.
- **Why it matters** The evidence hierarchy is one of the review's main conceptual contributions. If it is not applied consistently to the surveyed literature, its utility as an organizing framework is diminished. A systematic application would help readers understand which methods and applications have the strongest evidentiary support and where the gaps are.
- **Resolution test** Add a summary table or figure that maps each discussed application or method to its position in the evidence hierarchy, or restructure the applications section to explicitly classify each study by evidence level.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Novelty and differentiation
- **Claim pointer** The manuscript states that existing reviews mostly organize methods by category or cover broad cancer applications, and that none centers on cell-state-specific GRN reconstruction from paired scRNA-seq and scATAC-seq data.
- **Evidence pointer** Section "Introduction", third paragraph
- **Concern** The claim of novelty is plausible but is not supported by a specific comparison with prior reviews. The authors do not name the prior reviews they are differentiating from, nor do they specify how their treatment of paired, unpaired, and imputed data differs from what has been done before. The statement that "none centers on cell-state-specific GRN reconstruction" is a strong claim that requires more support.
- **Why it matters** For a review to justify its existence, it must clearly articulate its contribution relative to prior work. Without a specific comparison, the reader cannot assess whether this review fills a genuine gap or is a re-organisation of existing material.
- **Resolution test** Add a paragraph that names 3-5 prior reviews, states their scope and limitations, and explicitly articulates how the present review differs in scope, organization, or treatment of the evidence hierarchy.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Section "Paired single-cell multi-omics data: technical foundations and challenges", paragraph on data types
- **Evidence pointer** Section "Paired single-cell multi-omics data: technical foundations and challenges", fourth paragraph
- **Issue** The distinction between "matched-but-unpaired" and "imputed or transferred" designs is stated but not illustrated with concrete examples. The reader may struggle to understand when each design is appropriate and what specific artifacts each introduces.
- **Required correction** Add one concrete example of each design type, ideally from the cancer literature, and briefly state the specific artifact or assumption each introduces.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Section "AI frameworks for GRN inference", method families
- **Evidence pointer** Section "AI frameworks for GRN inference", first paragraph
- **Issue** The four method families are described but the number of methods in each family is not stated, and the coverage is not claimed to be exhaustive. The reader cannot tell whether the review covers most available methods or a selected subset.
- **Required correction** State explicitly whether the method coverage is intended to be representative or comprehensive, and if representative, state the selection criteria.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Precision
- **Affected element** Section "Applications of cell-state-specific GRNs in cancer", paragraph on resistance
- **Evidence pointer** Section "Applications of cell-state-specific GRNs in cancer", second paragraph
- **Issue** The statement that "network topology determines whether resistant or sensitive cells move through distinct intermediate states" is presented without explaining what aspect of topology is meant. This is a strong claim that needs more specificity.
- **Required correction** Briefly explain what topological property (e.g., centrality, module structure, feedback loops) was implicated in the cited study.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Consistency
- **Affected element** Section "Controversies, challenges, limitations, and future directions", paragraph on evaluation standards
- **Evidence pointer** Section "Controversies, challenges, limitations, and future directions", first paragraph
- **Issue** The review cites three works by "Kendiukhov" (2026a, 2026b, 2026c) that are used to make strong claims about the limitations of attention-based interpretability and evaluation metrics. These are cited as if they are established findings, but no details are given about the methods or scope of these studies.
- **Required correction** Provide one sentence of context for each Kendiukhov citation, stating what was done and in what setting, so the reader can assess the relevance and strength of the evidence.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Readability
- **Affected element** Section "AI frameworks for GRN inference", final paragraph
- **Evidence pointer** Section "AI frameworks for GRN inference", final paragraph
- **Issue** The decision logic summarized in Figure 2 is described in text but the figure is not provided. The text alone is dense and the decision criteria are not fully specified.
- **Required correction** Either provide the figure or expand the text to state the decision criteria explicitly in prose.

- **Technical failings that need to be addressed before the case is established**
  - Table 1 is missing, which is central to the comparative claims
  - Figures 1 and 2 are missing, which are referenced as summarizing the workflow and decision logic
  - The evidence hierarchy is not systematically applied to the surveyed methods
  - The claim of novelty relative to prior reviews is not supported by specific comparison
  - The benchmarking discussion is prescriptive but not evaluative of existing benchmarks

- **Assessment against Nature-style criteria**
  - **Originality** The conceptual framework of four method families and the explicit evidence hierarchy are useful organizing principles, but the individual methods and applications surveyed are all previously published. The originality lies in the synthesis and framing rather than in new data or methods. This is adequate for a review but not high originality.
  - **Scientific importance** The topic is of high importance. Cell-state-specific gene regulatory networks are central to understanding tumor heterogeneity, treatment resistance, and plasticity. The review addresses a genuine need for practical guidance in a rapidly evolving field. The importance is well justified.
  - **Interdisciplinary readership** The review bridges computational method development and cancer biology applications. It is likely to interest both computational biologists and cancer researchers. However, the level of technical detail in the methods section may be challenging for cancer biologists without computational background, and the cancer applications section may be too brief for computational readers seeking biological depth.
  - **Technical soundness** The technical content appears sound based on the text provided, but the missing table and figures prevent full verification. The descriptions of methods are accurate at the level of general mechanism, but the lack of a comparative table limits the ability to assess whether the categorizations are correct and consistent.
  - **Readability for nonspecialists** The writing is clear and well organized. The evidence hierarchy is explained in accessible terms. However, the density of method names and the lack of a glossary or summary table will make this challenging for nonspecialists. The abstract is accessible and accurately represents the content.

- **Recommendation posture** Supportive if technical concerns are resolved. The review addresses an important topic with a useful conceptual framework and honest caveats. The main blocking issue is the missing Table 1, which is central to the comparative claims. The other concerns, while not blocking, would substantially strengthen the review. The evidence hierarchy should be applied systematically, the novelty claim should be supported by specific comparison with prior reviews, and the benchmarking discussion should be more concrete.