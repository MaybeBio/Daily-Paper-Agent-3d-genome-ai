## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence as presented in the abstract; no methods, figures, or supplementary materials were provided for verification
- **Shared manuscript claim summary** The authors present HiC-LEGO, a hierarchical domain-aware framework for 3D genome reconstruction from Hi-C data. They claim superior reconstruction concordance across five human cell lines at 5-kb resolution, successful 1-kb reconstruction of GM12878 chromosome 8 with recovery of a distal MYC enhancer-promoter interaction, compact 3D configurations for RCMC microcompartment interactions at the Ppm1g locus from Micro-C data, stable TAD organization across breast cancer samples with heterogeneity in malignant pleural effusion, and enrichment of multi-way Pore-C contacts in compact configurations across all 23 chromosomes.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or supplementary data provided
- **Missing materials affecting confidence** Full manuscript, all figures and tables, methods description, validation protocols, comparison details, statistical analyses, and code availability

## Reviewer
- **Overall assessment** The abstract presents an ambitious and potentially valuable contribution to the 3D genome reconstruction field. The hierarchical domain-aware approach is conceptually appealing and addresses a recognized limitation in reconciling local chromatin organization with chromosome-scale structure. However, the abstract alone provides insufficient methodological detail and quantitative evidence to evaluate the validity of the central claims. Several assertions regarding biological validation (enhancer-promoter proximity, microcompartment configurations, disease-associated organization) require careful scrutiny of the underlying computational and experimental validation approaches, none of which are visible in the provided material.
- **Who would be interested in the results, and why** Researchers in 3D genome organization, chromatin structure prediction, and computational genomics would be the primary audience. The work also holds relevance for investigators studying gene regulation through enhancer-promoter interactions, cancer genomics researchers interested in chromatin reorganization during metastasis, and method developers working on Hi-C and Micro-C analysis pipelines. The kilobase-resolution reconstruction capability, if validated, would be of broad interest to the chromosome conformation capture community.
- **Major strengths** The conceptual framing of a domain-aware hierarchical approach that reduces dependence on individual domain definitions is a thoughtful response to a known instability in TAD-based methods. The multi-scale validation strategy spanning 5-kb Hi-C, 1-kb reconstruction, Micro-C, cancer datasets, and Pore-C multi-way contacts demonstrates ambition and breadth. The inclusion of biological validation beyond pairwise concordance metrics, such as enhancer-promoter proximity and microcompartment configurations, represents a welcome shift toward functionally meaningful assessment.
- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** "HiC-LEGO achieves higher reconstruction concordance than evaluated state-of-the-art methods while better preserving domain organization" across five human cell lines at 5-kb resolution
- **Evidence pointer** Abstract only; no comparison details, metrics, or statistical significance provided
- **Concern** The abstract states superior concordance without specifying which methods were compared, which concordance metrics were used, the magnitude of improvement, or whether differences reached statistical significance. The phrase "evaluated state-of-the-art methods" is vague and does not indicate the comparison set.
- **Why it matters** Reconstruction concordance is the primary quantitative claim of the work. Without knowing the comparator methods, the metrics employed, and the effect sizes, the reader cannot assess whether the improvement is meaningful or marginal. The field has multiple established reconstruction tools, and the choice of comparators substantially influences the interpretation.
- **Resolution test** Provide a comparison table with named methods, multiple concordance metrics (e.g., Pearson/Spearman correlation of distance maps, genome structure similarity scoring), effect sizes, and significance testing across all five cell lines.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** "At 1-kb resolution, HiC-LEGO reconstructs complete GM12878 chromosome 8 and recovers close spatial proximity between an epigenomically supported distal MYC enhancer and its promoter"
- **Evidence pointer** Abstract only; no reconstruction quality metrics or proximity quantification provided
- **Concern** Reconstructing a complete chromosome at 1-kb resolution is computationally demanding and the abstract provides no information on how reconstruction quality was assessed at this resolution. The enhancer-promoter proximity claim requires quantitative distance measurements, comparison to expected distributions, and ideally orthogonal validation. The phrase "epigenomically supported" suggests external data was used, but the nature of this support is unspecified.
- **Why it matters** The 1-kb reconstruction is a headline capability claim. If the reconstruction quality at this resolution is not rigorously validated, the biological interpretation of enhancer-promoter proximity could be an artifact of the reconstruction algorithm rather than a reflection of true spatial organization. The MYC locus is among the most studied enhancer-promoter systems, so the claim invites close scrutiny.
- **Resolution test** Provide reconstruction quality metrics at 1-kb resolution (e.g., distance map correlation, reproducibility across replicates), quantitative enhancer-promoter distances with statistical comparison to a null distribution, and ideally validation with independent methods such as FISH or capture Hi-C.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** "Reconstructions from 5-kb Micro-C data show that 249 experimentally defined RCMC microcompartment interactions at the Ppm1g locus occupy compact 3D configurations"
- **Evidence pointer** Abstract only; no definition of "compact" or quantitative support provided
- **Concern** The term "compact 3D configurations" is not operationally defined. It is unclear what metric was used to assess compactness, how compactness was compared to a null expectation, and whether the 249 interactions were treated as a set or individually. The relationship between RCMC microcompartment definitions and the reconstruction output requires clarification.
- **Why it matters** Microcompartment interactions are a relatively recent and biologically important class of chromatin structures. The claim that they occupy compact configurations is potentially significant, but without a clear definition of compactness and statistical testing, the observation could reflect trivial properties of the reconstruction algorithm rather than biological organization.
- **Resolution test** Define the compactness metric explicitly, provide the distribution of distances or volumes for the 249 interactions compared to matched controls or randomized expectations, and report statistical significance.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Scientific importance
- **Claim pointer** "In the breast cancer dataset, HiC-LEGO reconstructs structures that maintain stable TAD organization across healthy breast, primary tumors, and liver metastases, while revealing greater inter-patient structural heterogeneity in malignant pleural effusion samples"
- **Evidence pointer** Abstract only; no quantitative measures of TAD stability or heterogeneity provided
- **Concern** The claim of stable TAD organization across conditions and greater heterogeneity in pleural effusion samples is presented without quantitative support. It is unclear how TAD stability was measured, whether the comparison was statistically tested, and what the magnitude of the heterogeneity difference was.
- **Why it matters** This is the primary disease-relevant claim of the work. If TAD organization is truly stable across healthy and metastatic samples, this has implications for understanding chromatin reorganization in cancer. However, the claim as stated could also reflect limitations in the reconstruction method that mask genuine differences.
- **Resolution test** Provide quantitative measures of TAD boundary conservation or insulation score stability across conditions, with statistical testing and effect sizes for the heterogeneity comparison.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** "Pore-C validation shows that experimentally observed multi-way contacts spanning 1–5 Mb are enriched in compact reconstructed configurations across all 23 chromosomes"
- **Evidence pointer** Abstract only; no enrichment statistics or compactness definition provided
- **Concern** The enrichment claim requires a clear definition of "compact reconstructed configurations" and a statistical framework for assessing enrichment. The abstract does not specify how multi-way contacts were mapped onto reconstructed structures, what null model was used, or the magnitude of enrichment.
- **Why it matters** Pore-C validation is a distinctive and potentially powerful aspect of the work, as it tests higher-order spatial relationships beyond pairwise contacts. However, the claim as stated cannot be evaluated without the enrichment statistics and the operational definition of compactness.
- **Resolution test** Provide enrichment scores with confidence intervals, the null model used, and a clear description of how multi-way contacts were mapped to reconstructed coordinates.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Method description
- **Evidence pointer** Abstract, first sentence
- **Issue** The phrase "domain-aware hierarchical framework integrating ensemble chromatin domains with graph-based structural learning and progressive chromosome assembly" is dense and does not convey the key innovation clearly to a nonspecialist reader.
- **Required correction** Consider a more accessible description of the method that distinguishes the key novelty from existing hierarchical reconstruction approaches.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Data availability
- **Evidence pointer** Abstract only
- **Issue** No mention of code availability, data accession numbers, or whether the five cell lines and cancer datasets are publicly available.
- **Required correction** Include data and code availability statements in the full manuscript.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Comparison scope
- **Evidence pointer** Abstract, concordance claim
- **Issue** The abstract does not specify which "state-of-the-art methods" were used for comparison, making it difficult to contextualize the claimed improvement.
- **Required correction** Name the comparison methods in the abstract or indicate that they are listed in the main text.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Interpretation
- **Affected element** Biological interpretation
- **Evidence pointer** Abstract, MYC enhancer claim
- **Issue** The phrase "epigenomically supported" is ambiguous. It is unclear whether this refers to histone marks, chromatin accessibility, or other epigenomic features, and how this support was integrated into the analysis.
- **Required correction** Clarify the nature of the epigenomic support and whether it was used as input to the reconstruction or as independent validation.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Terminology
- **Affected element** "Compact configurations"
- **Evidence pointer** Abstract, Micro-C and Pore-C claims
- **Issue** The term "compact" is used in multiple contexts without a consistent operational definition.
- **Required correction** Define compactness once, operationally, and apply the same definition throughout.

## Risk / unsupported claims
- The claim of superior reconstruction concordance across five cell lines at 5-kb resolution is unverifiable from the abstract alone; no metrics, comparators, or significance values are provided.
- The 1-kb reconstruction of GM12878 chromosome 8 and the MYC enhancer-promoter proximity claim lack quantitative support and validation details.
- The assertion that 249 RCMC microcompartment interactions occupy "compact 3D configurations" is not operationally defined or statistically supported.
- The breast cancer findings regarding TAD stability and inter-patient heterogeneity are presented without quantitative measures or statistical testing.
- The Pore-C enrichment claim across all 23 chromosomes lacks enrichment statistics and a defined null model.
- The overall claim that HiC-LEGO "preserves regulatory interactions, disease-associated chromatin organization and higher-order spatial relationships" extends beyond what can be assessed from the abstract.

## Assessment against Nature-style criteria
- **Originality** The hierarchical domain-aware approach with ensemble chromatin domain selection appears conceptually novel, though the abstract does not provide enough detail to fully distinguish it from existing hierarchical reconstruction methods. The integration of multiple validation modalities (Hi-C, Micro-C, cancer datasets, Pore-C) is commendable.
- **Scientific importance** If the claims are substantiated, the work addresses a recognized bottleneck in kilobase-resolution 3D genome reconstruction and could have broad impact on understanding gene regulation and disease-associated chromatin organization. The potential to recover biologically meaningful enhancer-promoter interactions and higher-order contacts would be a significant advance.
- **Interdisciplinary readership** The work bridges computational genomics, chromatin biology, and cancer research. The abstract is written in a way that is largely accessible to these communities, though some terminology is dense.
- **Technical soundness** Cannot be assessed from the abstract alone. The central claims require detailed methodological description, quantitative validation, and statistical rigor that are not visible in the provided material. The absence of any figures, tables, or methods text prevents evaluation of the technical implementation.
- **Readability for nonspecialists** The abstract is reasonably readable for a specialized audience but would benefit from clearer articulation of the methodological innovation and the significance of the biological validations. The density of claims without supporting numbers makes the abstract feel more like a summary of a larger work than a self-contained communication.

## Recommendation posture
Currently not established from the provided evidence. The abstract presents an ambitious and potentially important contribution, but the absence of methodological detail, quantitative results, and validation information means the central claims cannot be evaluated. A full review of the complete manuscript would be required to determine whether the technical concerns can be resolved. The work is promising enough to warrant full review, but the claims as stated in the abstract are not verifiable from the supplied material.