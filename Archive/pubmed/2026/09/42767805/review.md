## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence presented in the abstract; no methods, figures, tables, or supplementary materials were provided
- **Shared manuscript claim summary** The authors propose DeepAllele, a deep learning sequence-to-function model with paired allele-specific input, to predict cis-regulatory differences between alleles. The model is intended for datasets with unambiguous phasing, such as F1 hybrids, controlled crosses, or long-read sequencing (e.g., Fiber-seq). Applied to allele-specific immune cell data from F1 hybrid mice, the model reportedly learns cis-regulatory grammar aligned with known biological mechanisms across more genomic regions than baseline models.
- **Visible evidence base** Abstract text only; no quantitative results, model architecture details, dataset descriptions, or comparison metrics are provided
- **Missing materials affecting confidence** Full manuscript, methods section, figures, tables, supplementary data, baseline model specifications, and any statistical or performance metrics

## Reviewer
- **Overall assessment** The abstract presents a conceptually interesting idea, namely using paired allele-specific sequences as input to a deep learning model to learn cis-regulatory determinants of allelic imbalance. This is a plausible extension of existing sequence-to-function models and could be of value to the genomics community. However, the abstract provides no quantitative evidence, no clear description of model architecture or training strategy, and no explicit comparison to existing methods beyond a vague statement about "baseline models." The central claims of biological alignment and improved discovery are therefore not assessable from the supplied material. The work may have merit, but the case is not established from the abstract alone.
- **Who would be interested in the results, and why** Researchers in regulatory genomics, computational biology, and functional genetics would be interested, particularly those working on allele-specific expression, cis-regulatory element discovery, and deep learning applications to genomic sequence. The approach could also appeal to groups studying F1 hybrids or using long-read sequencing for phased genomes.
- **Major strengths** The idea of using paired allele-specific input is a conceptually novel twist on standard sequence-to-function models. The stated focus on unambiguously phased datasets is a sensible design choice that avoids phasing errors. The potential to learn regulatory grammar from natural genetic variation is scientifically appealing.
- **Major Concerns**  
  - R1-M1  
  - R1-M2  
  - R1-M3
- **Minor Comments**  
  - R1-m1  
  - R1-m2  
  - R1-m3
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3
- **Assessment against Nature-style criteria**  
  - Originality: The paired allele-specific input design appears original, but the abstract does not clarify how this differs functionally from existing approaches beyond input formatting.  
  - Scientific importance: Potentially high, if the model truly improves regulatory motif discovery, but this is not demonstrated.  
  - Interdisciplinary readership: The topic bridges machine learning and genomics, which could attract a broad audience, but the abstract is too thin to engage nonspecialists.  
  - Technical soundness: Not assessable from the abstract; no architecture, training, or validation details are given.  
  - Readability for nonspecialists: The abstract is understandable at a high level, but key terms such as "paired allele-specific input" and "cis-regulatory grammar" are not explained sufficiently for a general reader.
- **Recommendation posture** Currently not established from the provided evidence. The idea is promising, but the abstract alone does not support the claims made. A full manuscript with quantitative results and methodological detail is required for a fair assessment.

### Major Concerns

- **Concern ID** R1-M1  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Evidence sufficiency  
- **Claim pointer** The model "learns cis-regulatory grammar aligned with known biological mechanisms across a significantly larger number of genomic regions compared to baseline models."  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** No quantitative results are presented. The claim of "significantly larger number" is unsupported by any numbers, statistical tests, or effect sizes.  
- **Why it matters** Without quantitative evidence, the central performance claim cannot be evaluated or reproduced.  
- **Resolution test** Provide specific metrics, such as number of regions identified, enrichment scores, or precision-recall comparisons, with confidence intervals and statistical significance.

- **Concern ID** R1-M2  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Methodological clarity  
- **Claim pointer** "DeepAllele, a novel deep learning sequence-to-function model using paired allele-specific input."  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The abstract does not describe the model architecture, input representation, training data, or how "paired allele-specific input" is encoded.  
- **Why it matters** Reproducibility and assessment of novelty require a clear description of the method.  
- **Resolution test** Include a methods section or supplementary material detailing the architecture, training procedure, and input encoding.

- **Concern ID** R1-M3  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Comparison validity  
- **Claim pointer** "Compared to baseline models."  
- **Evidence pointer** Abstract only; location not provided  
- **Concern** The baseline models are not named or described, and the comparison criteria are unclear.  
- **Why it matters** Without a defined baseline, the claimed improvement is meaningless.  
- **Resolution test** Specify the baseline models, their configurations, and the evaluation protocol used for comparison.

### Minor Comments

- **Concern ID** R1-m1  
- **Severity** Minor  
- **Axis** Clarity  
- **Affected element** Terminology  
- **Evidence pointer** Abstract; location not provided  
- **Issue** The term "cis-regulatory grammar" is used without definition.  
- **Required correction** Define what is meant by "grammar" in this context, such as specific motif combinations or positional constraints.

- **Concern ID** R1-m2  
- **Severity** Minor  
- **Axis** Scope justification  
- **Affected element** Applicability statement  
- **Evidence pointer** Abstract; location not provided  
- **Issue** The abstract states the approach is suited for F1 hybrids and Fiber-seq but does not explain why it would not apply to other phased datasets.  
- **Required correction** Clarify the limitations or assumptions that restrict applicability.

- **Concern ID** R1-m3  
- **Severity** Minor  
- **Axis** Readability  
- **Affected element** Abstract structure  
- **Evidence pointer** Abstract; location not provided  
- **Issue** The abstract jumps from method description to application without a clear statement of the biological question or hypothesis.  
- **Required correction** Add a sentence framing the biological problem the model addresses.

## Risk / unsupported claims
- The claim of "significantly larger number of genomic regions" is unsupported by any data.
- The novelty of the model relative to existing deep learning approaches is not established.
- The alignment of learned features with "known biological mechanisms" is asserted without evidence.
- The generalizability of the approach beyond the specific F1 hybrid mouse dataset is not assessable.