## Review setup

- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract, with reference to the stated methodology and results
- **Shared manuscript claim summary** The authors claim to have systematically perturbed every position of the complete telomere-to-telomere human genome using Nucleotide Transformer v3 on an exascale compute cluster, generating nucleotide-resolution dependency maps that reveal a directed, weighted network of position-to-position genomic relationships. They report the discovery of recurrent, directional architectures termed "relons" spanning coding, non-coding, and unannotated regions, which they state reflect evolutionary and functional constraints and associate with human genetic variation and pathogenic variants. They conclude that these findings suggest a higher-order relational layer of genome organization.
- **Visible evidence base** Abstract text only. No figures, tables, methods section, supplementary materials, or data availability statements were provided for review.
- **Missing materials affecting confidence** Full manuscript text, all figures and tables, detailed methodology, validation procedures, statistical analyses, data availability information, and any supplementary materials. The absence of these materials substantially limits the ability to assess the validity and robustness of the claims.

## Reviewer

- **Overall assessment** The abstract presents an ambitious and potentially significant claim regarding a higher-order relational architecture of the human genome. The concept of systematically perturbing every position of a complete telomere-to-telomere genome to derive dependency maps is conceptually interesting and could represent a novel contribution. However, the abstract alone provides insufficient evidence to evaluate the technical soundness of the approach, the biological validity of the findings, or the strength of the associations claimed. The computational scale described is extraordinary and raises questions about feasibility and interpretability that cannot be resolved from the supplied material. The claim of discovering a new organizational layer of the genome is strong and would require extensive validation, none of which is visible in the abstract.
- **Who would be interested in the results, and why** Researchers in genomics, computational biology, and genome architecture would be the primary audience. Those studying regulatory genomics, evolutionary constraints, and the interpretation of genetic variation in disease contexts would also find relevance. The work could interest scientists working on deep learning applications in genomics and those exploring higher-order genome organization beyond linear sequence and 3D structure. Clinically oriented geneticists might be interested if the associations with pathogenic variants prove robust.
- **Major strengths** The conceptual framing of genome organization as a relational network derived from systematic perturbation is original and potentially transformative. The use of a complete telomere-to-telomere genome represents a comprehensive reference. The stated ambition to cover coding, non-coding, and unannotated regions suggests a genome-wide scope that could reveal previously unrecognized features. The explicit connection to human genetic variation and pathogenic variants indicates potential translational relevance.
- **Major Concerns** 
  - R1-M1
  - R1-M2
  - R1-M3
  - R1-M4
- **Minor Comments** 
  - R1-m1
  - R1-m2
  - R1-m3
- **Technical failings that need to be addressed before the case is established** The absence of any methodological detail prevents assessment of the perturbation strategy, the interpretation of model outputs as biological dependencies, and the statistical framework used. The lack of validation data means the biological reality of "relons" cannot be evaluated. The claimed associations with genetic variation and pathogenic variants are presented without any supporting evidence.
- **Assessment against Nature-style criteria** Originality is potentially high, as the concept of a genome-wide relational network derived from systematic in silico perturbation appears novel. Scientific importance could be substantial if the claims are validated, as it would propose a new layer of genome organization. Interdisciplinary readership is plausible, spanning genomics, computational biology, and molecular genetics. Technical soundness cannot be assessed from the abstract alone, and the extraordinary computational claims require scrutiny. Readability for nonspecialists is adequate in the abstract, though the concept of "relons" would require clearer explanation in the full manuscript.
- **Recommendation posture** Currently not established from the provided evidence. The abstract presents intriguing possibilities, but the evidence base is insufficient to support the strong claims made. A supportive posture would require access to the full manuscript and its validation data.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The authors claim to have systematically perturbed every position of the complete telomere-to-telomere human genome using Nucleotide Transformer v3 with an exascale compute cluster, generating nucleotide-resolution dependency maps.
- **Evidence pointer** Abstract, methodology description. Location not provided.
- **Concern** The abstract provides no details on the perturbation strategy, the nature of the model outputs, or how these outputs were interpreted as position-to-position dependencies. The computational scale described is unprecedented, and no information is given on how computational feasibility was achieved, how artifacts were controlled, or how the model's predictions were validated against known biology.
- **Why it matters** Without methodological transparency, the core technical claim cannot be evaluated. The interpretation of deep learning model outputs as biological dependencies is non-trivial and requires careful benchmarking. The extraordinary computational claim raises questions about reproducibility and accessibility that are central to the work's credibility.
- **Resolution test** The full manuscript must provide a detailed methods section describing the perturbation protocol, the model architecture and training, the computational infrastructure, and validation against known regulatory elements, RNA structures, and other established genomic features.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence quality
- **Claim pointer** The authors claim the network recapitulates known biological features and uncovers recurrent, directional architectures termed "relons" spanning coding, non-coding, and unannotated regions.
- **Evidence pointer** Abstract, results description. Location not provided.
- **Concern** No data are presented to demonstrate that the network recapitulates known biological features. The existence and properties of "relons" are asserted without any supporting evidence, such as examples, statistical significance measures, or comparisons to known genomic features. The claim that these span unannotated regions is particularly strong and requires careful demonstration that such regions are not simply artifacts.
- **Why it matters** The central discovery claim of the paper rests on the existence and biological relevance of "relons." Without evidence, this remains an unsupported assertion. The recapitulation of known features is a critical sanity check that must be demonstrated explicitly.
- **Resolution test** The full manuscript must show clear examples of known features being correctly identified, provide statistical evidence for the existence of "relons" beyond what would be expected by chance, and demonstrate their presence across different genomic contexts with appropriate controls.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Claim support
- **Claim pointer** The authors claim these relational modules reflect evolutionary and functional constraints and associate with human genetic variation and pathogenic variants.
- **Evidence pointer** Abstract, results description. Location not provided.
- **Concern** The associations with evolutionary constraints, genetic variation, and pathogenic variants are stated without any quantitative support. No effect sizes, statistical significance values, or comparison to appropriate null models are provided. The direction and strength of these associations are entirely unspecified.
- **Why it matters** These associations are what give the work translational relevance and connect it to existing genomic knowledge. Without quantitative evidence, the claims are unfalsifiable from the abstract and cannot be distinguished from coincidental overlap.
- **Resolution test** The full manuscript must provide statistical analyses demonstrating that "relons" are enriched in conserved regions, depleted or enriched in variant-dense regions as appropriate, and significantly associated with pathogenic variants relative to appropriate controls.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Interpretability
- **Claim pointer** The authors suggest a higher-order relational layer of genome organization, providing a framework to interpret DNA as a complex system of dependencies beyond linear and 3D structure.
- **Evidence pointer** Abstract, conclusion. Location not provided.
- **Concern** The conceptual leap from computational dependency maps to a proposed biological organizational layer is substantial. The abstract does not explain what "relons" represent biologically, how they relate to known mechanisms of gene regulation, chromatin organization, or other established genome features, or what physical or molecular basis might underlie them.
- **Why it matters** For the work to have lasting impact, the biological interpretation must be grounded in testable hypotheses and mechanistic plausibility. A purely computational construct without biological anchoring would be of limited value to the field.
- **Resolution test** The full manuscript should provide biological interpretation of representative "relons," ideally with experimental validation or at least strong correlative evidence linking them to known molecular mechanisms.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Terminology
- **Evidence pointer** Abstract, term "relons". Location not provided.
- **Issue** The term "relons" is introduced without definition or etymological explanation. Readers cannot infer its meaning or significance from the abstract alone.
- **Required correction** Provide a clear definition of "relons" in the abstract or indicate that a formal definition appears in the full manuscript.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Resource availability
- **Evidence pointer** Footnotes, URL https://relome.org/. Location not provided.
- **Issue** A website is referenced but no description of its contents, availability status, or relationship to the manuscript is provided.
- **Required correction** Clarify what the website contains, whether it hosts data, code, or visualization tools, and how it relates to the manuscript's findings.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Author list
- **Evidence pointer** Footnotes, "Chance of author list in the online version". Location not provided.
- **Issue** The footnote appears to contain a typographical error, likely "Change" rather than "Chance," and suggests an inconsistency in the author list.
- **Required correction** Correct the typographical error and ensure the author list is consistent between the manuscript and the online version.

## Risk / unsupported claims

- The existence and biological reality of "relons" as defined recurrent architectural features is unsupported by the abstract alone.
- The claim that the network recapitulates known biological features is unverifiable without presented evidence.
- The associations with evolutionary constraints, human genetic variation, and pathogenic variants are stated without quantitative support.
- The claim of a higher-order relational layer of genome organization beyond linear and 3D structure is an interpretation that cannot be evaluated from the supplied material.
- The computational feasibility of the described exascale perturbation study cannot be assessed without methodological details.
- The generalizability of findings from a single telomere-to-telomere genome to human genetic diversity is not addressed.