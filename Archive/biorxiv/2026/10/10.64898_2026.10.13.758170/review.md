## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the supplied abstract; no figures, tables, methods, or supplementary materials were provided
- **Shared manuscript claim summary** The authors present DeepD, a phylogeny-informed sparse mixture-of-experts genome foundation model operating at single-nucleotide resolution over a 1-million-token context. The model is pretrained on unselected whole-genome sequences across all domains of life, supports sequence-to-function prediction across species, demonstrates performance in human protein fitness and disease variant effect prediction, shows particular strength in regulatory regions, routes experts to capture exon-intron boundaries, transposable elements, and distal cis-regulatory elements, generates experimentally validated core promoters with specified transcriptional strengths, and enables generation of complete yeast chromosome sequences and megabase-scale Arabidopsis segments via a Context-Anchor-Body strategy.
- **Visible evidence base** Abstract text only. No quantitative results, benchmark comparisons, experimental validation details, model architecture specifications, or data descriptions are provided.
- **Missing materials affecting confidence** Full manuscript, all figures and tables, methods section, supplementary information, benchmark definitions, experimental validation protocols, and model implementation details. The absence of these materials severely limits the ability to assess the validity of the claims.

## Reviewer
- **Overall assessment** The abstract presents an ambitious and potentially impactful genome foundation model with a broad scope spanning prediction and generation across domains of life. The conceptual contributions, particularly the phylogeny-informed sparse mixture-of-experts design and the Context-Anchor-Body generation strategy, are interesting and could appeal to a wide audience. However, the abstract provides almost no quantitative evidence, no clear benchmark comparisons, and no methodological detail. The claims are broad and strong, but the visible evidence base is insufficient to establish them. The manuscript may have merit, but the case is not established from the supplied material.
- **Who would be interested in the results, and why** Computational biologists and bioinformaticians working on genome foundation models, sequence-to-function prediction, and generative models for genomics would be the primary audience. Researchers studying regulatory genomics, variant effect prediction, and synthetic genomics would also find the results relevant. The cross-domain scope and the generation capabilities could attract researchers interested in genome design and synthetic biology.
- **Major strengths** The conceptual framing is strong, combining phylogeny-informed architecture with sparse mixture-of-experts and single-nucleotide resolution over a long context. The breadth of applications, from variant effect prediction to genome-scale generation, is ambitious and potentially valuable. The Context-Anchor-Body strategy for controllable generation is a novel contribution that could address a real gap in the field.
- **Major Concerns** The abstract lacks quantitative results, benchmark comparisons, and methodological detail. The claims are broad and strong, but the evidence base is essentially absent. The relationship between the model's design choices and the claimed performance is not explained. The experimental validation of generated promoters is mentioned but not described. The scope of the evaluation across domains of life is not specified.
- **Minor Comments** The abstract is dense and could benefit from clearer organization. Some terms, such as "phylogeny-informed" and "Context-Anchor-Body strategy," are introduced without explanation. The claim of "efficient" is not supported by any computational cost comparison.
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4, R1-M5
- **Assessment against Nature-style criteria** Originality: The combination of phylogeny-informed sparse mixture-of-experts with single-nucleotide resolution and long-context generation appears novel, but the abstract does not clearly differentiate DeepD from existing genome foundation models. Scientific importance: The potential to unify prediction and generation across domains of life is scientifically important, but the evidence provided is insufficient to assess whether this potential is realized. Interdisciplinary readership: The work could appeal to computational and experimental biologists, but the abstract assumes significant background knowledge and does not make the case accessible to nonspecialists. Technical soundness: Cannot be assessed from the abstract alone; no quantitative results or methodological details are provided. Readability for nonspecialists: The abstract is technical and dense, with several terms and concepts introduced without sufficient context for a general scientific audience.
- **Recommendation posture** Currently not established from the provided evidence. The conceptual contributions are interesting, but the abstract does not provide sufficient quantitative or methodological support for the claims. A full manuscript with detailed results, benchmarks, and methods would be required to assess the validity of the claims.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "DeepD performs well in human protein fitness and disease variants effect prediction, such as BRCA1 and BRCA2, with particular strength in regulatory regions, such as promoter and transcription-factor binding sites."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim of strong performance in variant effect prediction is made without any quantitative results, benchmark comparisons, or baseline references. No metrics, datasets, or evaluation protocols are described.
- **Why it matters** Variant effect prediction is a crowded field with established benchmarks and baselines. Without quantitative comparisons, the claim of strong performance cannot be evaluated or contextualized.
- **Resolution test** Provide performance metrics on established benchmarks, such as ClinVar or DeepSEA, with comparisons to existing models and statistical significance tests.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "Expert routing captures exon-intron boundaries, transposable elements, and distal cis-regulatory elements."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim that expert routing captures specific genomic features is made without any supporting analysis. No visualization, quantification, or comparison to alternative architectures is provided.
- **Why it matters** This claim is central to the model's interpretability and to the value of the sparse mixture-of-experts design. Without evidence, it is unclear whether the routing behavior is meaningful or coincidental.
- **Resolution test** Provide analyses showing that specific experts consistently activate at these genomic features, with quantitative measures of specificity and comparison to random or alternative routing.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "DeepD also generates experimentally validated core promoters with specified transcriptional strengths."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim of experimental validation is made without any description of the experimental system, the number of promoters tested, the success rate, or the quantitative agreement between predicted and measured transcriptional strengths.
- **Why it matters** Experimental validation is a strong claim that requires detailed evidence. Without specifics, the validity and generalizability of the result cannot be assessed.
- **Resolution Test** Provide details of the experimental setup, the number of promoters tested, the correlation between predicted and measured strengths, and appropriate controls.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "The Context-Anchor-Body strategy enables generation of complete yeast chromosome sequences and megabase-scale Arabidopsis segments, preserving gene structure and order while introducing variations within natural ranges."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim of generating complete chromosome sequences and megabase-scale segments is made without any description of the evaluation criteria, the accuracy of gene structure preservation, the nature of the introduced variations, or comparisons to existing generation methods.
- **Why it matters** Genome-scale generation is a challenging task, and the claims are strong. Without detailed evaluation, it is unclear whether the generated sequences are biologically meaningful or merely statistically plausible.
- **Resolution test** Provide quantitative evaluations of generated sequences, including gene structure accuracy, sequence similarity to natural genomes, and comparisons to existing generative models.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** "Pretrained on unselected whole-genome sequences across all domains of life, DeepD learns genic and intergenic sequence features and supports broad sequence-to-function prediction across species."
- **Evidence pointer** Abstract only; location not provided
- **Concern** The claim of broad cross-species prediction is made without any description of the species covered, the prediction tasks evaluated, or the performance achieved. The scope of "all domains of life" is not specified.
- **Why it matters** Cross-species generalization is a key claim for a foundation model. Without details on the evaluation, it is unclear whether the model generalizes or simply memorizes training data.
- **Resolution test** Provide details on the species and tasks used for evaluation, with performance metrics and comparisons to species-specific models.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract terminology
- **Evidence pointer** Abstract; location not provided
- **Issue** The term "phylogeny-informed" is used without explanation of how phylogeny informs the model architecture or training.
- **Required correction** Clarify the role of phylogeny in the model design, or remove the term if it is not central.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract terminology
- **Evidence pointer** Abstract; location not provided
- **Issue** The "Context-Anchor-Body strategy" is introduced without any description of what the three components represent or how they function.
- **Required correction** Provide a brief explanation of the strategy in the abstract, or refer to a figure or methods section.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Quantitative support
- **Affected element** Efficiency claim
- **Evidence pointer** Abstract; location not provided
- **Issue** The claim of "reducing active computation" is made without any quantitative comparison to other models or baselines.
- **Required correction** Provide a quantitative measure of computational efficiency, such as FLOPs or inference time, compared to relevant baselines.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Scope clarity
- **Affected element** Evaluation scope
- **Evidence pointer** Abstract; location not provided
- **Issue** The abstract mentions "broad sequence-to-function prediction across species" but does not specify which species or tasks are included.
- **Required correction** List the species and tasks evaluated, or refer to a table or figure.

## Risk / unsupported claims
- The claim of strong performance in variant effect prediction is unsupported by any quantitative evidence.
- The claim that expert routing captures specific genomic features is unsupported by any analysis.
- The claim of experimentally validated promoter generation is unsupported by any experimental details.
- The claim of generating complete yeast chromosomes and megabase-scale Arabidopsis segments is unsupported by any evaluation criteria or results.
- The claim of broad cross-species prediction is unsupported by any species or task descriptions.
- The claim of computational efficiency is unsupported by any quantitative comparison.
- The overall claim that DeepD "unifies accurate sequence-to-function prediction with controllable genome-scale generation" is not assessable from the abstract alone.