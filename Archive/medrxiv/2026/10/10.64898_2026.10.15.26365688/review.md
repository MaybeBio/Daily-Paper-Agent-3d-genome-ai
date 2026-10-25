## Review setup
- **Input scope** Full manuscript text (abstract, introduction, methods, results, discussion, limitations, conclusions, data availability, contributions, acknowledgements) as provided in the submission.
- **Assessment boundary** The review is based solely on the text supplied. No figures, tables, supplementary materials, or referenced datasets were provided for direct inspection. Claims referring to these items are assessed on the basis of textual description only.
- **Shared manuscript claim summary** The authors propose that the 9p21.3 CVD risk locus regulates the lncRNA MIR31HG through long-range enhancer-promoter interactions in endothelial cells, and that MIR31HG depletion promotes an endothelial activation transcriptional program, implicating MIR31HG as an effector transcript in ECs.
- **Visible evidence base** Textual descriptions of promoter capture Hi-C in ECs (n=16) and SMCs (n=6), eQTL analysis in 136 vascular biopsies, in vitro flow experiments, siRNA knockdown with RNA-seq, CRISPRa validation, AlphaGenome predictions, and motif activity response analysis (MARA). No raw data, figures, or tables were available for verification.
- **Missing materials affecting confidence** All figures (Figure 1-3), tables (Table 1, S1-S8), supplementary methods, and the underlying sequencing datasets. Without these, quantitative claims, statistical details, and the validity of the interaction calls, eQTL associations, and CRISPRa effects cannot be independently assessed.

## Reviewer
- **Overall assessment** The manuscript addresses a long-standing and important question in cardiovascular genetics: how the 9p21.3 risk locus exerts its effects. The authors present a coherent hypothesis and a multi-pronged approach that moves beyond the nearest-gene paradigm. The identification of MIR31HG as a candidate distal effector in endothelial cells is novel and potentially significant. However, the strength of the conclusions is limited by the reliance on descriptive and correlative evidence, the small sample sizes, and the absence of direct mechanistic validation (e.g., endogenous perturbation of the enhancer or allele-specific assays). The manuscript is well-written and logically structured, but several technical and interpretive gaps need to be addressed before the case is fully established.
- **Who would be interested in the results, and why** Cardiovascular geneticists, vascular biologists, and researchers studying the functional interpretation of non-coding GWAS variants. The work is also relevant to those interested in long-range chromatin regulation and the role of lncRNAs in endothelial biology. The use of AlphaGenome as a predictive tool may interest computational biologists developing and applying deep learning models to variant prioritization.
- **Major strengths** 1. The study addresses a critical gap in the field by exploring non-nearest-gene targets of a well-known risk locus. 2. The integration of multiple complementary approaches (chromatin conformation, eQTL, functional perturbation, and predictive modeling) is a methodological strength. 3. The focus on endothelial cells, which are understudied in the context of 9p21.3, is a valuable contribution. 4. The manuscript is clearly written and the logical flow from hypothesis to evidence is easy to follow.
- **Major Concerns** See detailed items below.
- **Minor Comments** See detailed items below.
- **Technical failings that need to be addressed before the case is established** R1-M1 (sample size and interaction validation), R1-M2 (eQTL statistical power), R1-M3 (CRISPRa specificity and physiological relevance), R1-M4 (causal variant evidence).
- **Assessment against Nature-style criteria** **Originality:** High. The proposal of MIR31HG as an effector transcript in ECs for the 9p21.3 locus is a novel contribution that challenges the prevailing ANRIL-centric view. **Scientific importance:** High. The 9p21.3 locus is a major CVD risk locus, and understanding its mechanism is of significant clinical and biological importance. **Interdisciplinary readership:** Moderate to high. The work bridges human genetics, chromatin biology, and vascular cell biology, which should appeal to a broad audience. **Technical soundness:** Currently moderate. The study is technically ambitious, but the evidence base is weakened by small sample sizes, lack of direct validation of key findings, and reliance on predictive models without experimental confirmation. **Readability for nonspecialists:** Good. The manuscript is well-structured and explains complex concepts clearly, though some sections (e.g., AlphaGenome methodology) may be dense for a general reader.
- **Recommendation posture** Supportive if technical concerns are resolved. The core hypothesis is interesting and the data are suggestive, but the current evidence does not fully establish MIR31HG as a causal effector. The authors need to provide stronger validation of the key claims, particularly regarding the eQTL association, the specificity of the CRISPRa effect, and the causal role of the identified variant.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness / Statistical power
- **Claim pointer** The authors claim that promoter capture Hi-C identified MIR31HG as the most recurrent distal target of the 9p21.3 locus, based on data from 6 SMC and 16 EC samples.
- **Evidence pointer** Results section "Chromatin interaction mapping identifies MIR31HG as a target gene of the 9p21.3 locus", Figure 1A-F, Table 1.
- **Concern** The sample sizes for the Hi-C experiments are very small (n=6 for SMCs, n=16 for ECs). The authors do not report on the reproducibility of the interaction calls across biological replicates, nor do they provide any statistical measure of confidence for the interaction frequencies. The claim that MIR31HG is the "most recurrent" target is based on a qualitative assessment of interaction frequency, which may be highly variable given the small n. Furthermore, the authors do not validate the key long-range interaction (9p21.3-MIR31HG) by an independent method (e.g., 3C-qPCR or FISH) in the relevant cell types.
- **Why it matters** The entire premise of the paper rests on the identification of MIR31HG as a target of the 9p21.3 locus. If the interaction calls are not robust or are not reproducible, the subsequent eQTL, functional, and genetic analyses lose their foundation. The lack of validation and statistical rigor undermines the confidence in this central claim.
- **Resolution test** The authors should provide a statistical framework for identifying significant interactions (e.g., using a background model or comparing to a negative control set). They should also validate the 9p21.3-MIR31HG interaction in at least one of the primary cell types using an independent technique. Ideally, they would also show that the interaction is specific to ECs or SMCs and not a generic feature of all cell types.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Statistical power / Genetic evidence
- **Claim pointer** The authors state that eQTL analysis in 136 vascular biopsies showed the strongest association between MIR31HG expression and genetic variation at 9p21.3, specifically in the internal thoracic artery intima-media (MMed).
- **Evidence pointer** Results section "Chromatin interaction mapping identifies MIR31HG as a target gene of the 9p21.3 locus", Figure 1E, Table S1.
- **Concern** The eQTL analysis is based on a small number of samples (n=49 for AMed, n=43 for AAdv, n=44 for MMed). The authors report that only the MMed association passed multiple testing correction (FDR < 0.05), while other associations were suggestive (P < 0.05, FDR > 0.05). This is a weak genetic signal. The effect size (beta = 0.76) is reported, but the confidence intervals are not provided. The authors do not discuss the possibility of a false positive, nor do they attempt to replicate this finding in an independent cohort. The lack of a robust, replicated eQTL signal significantly weakens the claim that MIR31HG is genetically regulated by the 9p21.3 locus.
- **Why it matters** The eQTL analysis is the primary genetic evidence linking the 9p21.3 locus to MIR31HG expression. A weak, unreplicated signal is insufficient to establish this link, especially given the small sample size. Without a solid genetic association, the relevance of the subsequent functional experiments to human disease is uncertain.
- **Resolution test** The authors should provide effect sizes with confidence intervals and report the number of independent SNPs tested. They should attempt to replicate the eQTL association in an independent dataset (e.g., GTEx or STARNET). If replication is not possible, they should temper their conclusions and clearly state that the genetic association is suggestive and requires further validation.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Functional validation / Physiological relevance
- **Claim pointer** The authors claim that CRISPRa of a candidate enhancer located ~538 kb from the MIR31HG promoter significantly increased MIR31HG expression, confirming its capacity to regulate MIR31HG over a large genomic distance.
- **Evidence pointer** Results section "9p21.3 locus harbors a distal enhancer and putative regulatory SNPs of MIR31HG", Figure 3A.
- **Concern** The CRISPRa experiment was performed in hTERT-RPE1 cells, a non-vascular, non-endothelial cell line. The enhancer activity and the long-range interaction may be cell-type specific. The authors do not demonstrate that the same enhancer is active in primary ECs or that the CRISPRa effect is specific to the targeted region (e.g., no off-target controls or a negative control gRNA targeting a different region). The physiological relevance of an effect in an immortalized retinal pigment epithelial cell line for a cardiovascular phenotype is questionable.
- **Why it matters** The CRISPRa experiment is the only direct functional evidence that the identified enhancer can regulate MIR31HG. If this effect is not reproducible in a relevant cell type (e.g., primary ECs) or is not specific, the claim that this enhancer is a functional regulator of MIR31HG in the cardiovascular context is not supported.
- **Resolution test** The authors should repeat the CRISPRa experiment in primary human aortic endothelial cells. They should include a negative control (e.g., a non-targeting gRNA or a gRNA targeting a known inactive region) and demonstrate that the effect is specific to the MIR31HG locus. They should also consider using a more physiologically relevant readout, such as allelic expression analysis in cells heterozygous for the risk variant.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Causal variant identification
- **Claim pointer** The authors nominate rs1537373 as a candidate causal variant based on AlphaGenome predictions and concordance with eQTL data.
- **Evidence pointer** Results section "9p21.3 locus harbors a distal enhancer and putative regulatory SNPs of MIR31HG", Figure 3C, Table S8.
- **Concern** The evidence for rs1537373 as a causal variant is entirely computational. AlphaGenome is a predictive model, and its predictions are not validated by any experimental assay. The concordance with eQTL data is based on a single, unreplicated eQTL analysis. The authors do not perform any fine-mapping analysis (e.g., using a Bayesian approach like SuSiE or FINEMAP) to statistically prioritize causal variants. The claim that this is a "high-confidence" prioritization is overstated given the lack of experimental validation.
- **Why it matters** Identifying the causal variant is crucial for understanding the mechanism of the 9p21.3 association. If the nominated variant is not causal, the entire mechanistic model proposed in the paper may be incorrect. The current evidence is too weak to support a definitive claim.
- **Resolution test** The authors should perform a formal statistical fine-mapping analysis of the 9p21.3 locus using the eQTL data. They should validate the effect of rs1537373 on enhancer activity using a reporter assay (e.g., luciferase or MPRA) in ECs. They should also test whether the variant affects transcription factor binding (e.g., using an electrophoretic mobility shift assay or ChIP-qPCR).

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity / Data presentation
- **Affected element** Figure 1A-F
- **Evidence pointer** Results section "Chromatin interaction mapping identifies MIR31HG as a target gene of the 9p21.3 locus"
- **Issue** The description of the interaction network is complex, and the figure is not provided. It is unclear how the "19 putative regulatory elements" and "15 genes" are defined and how the network is visualized.
- **Required correction** Please provide a clear legend for Figure 1 that explains the criteria for defining regulatory elements and genes, and how the interaction frequencies are represented. Consider simplifying the figure to highlight the key interactions, particularly the 9p21.3-MIR31HG interaction.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** eQTL analysis
- **Evidence pointer** Results section "Chromatin interaction mapping identifies MIR31HG as a target gene of the 9p21.3 locus", Figure 1E
- **Issue** The effect size (beta = 0.76) is reported without a confidence interval or a measure of variance. The number of SNPs tested and the total number of tests performed are not stated.
- **Required correction** Please report the 95% confidence interval for the effect size and the total number of tests performed. This will allow the reader to assess the precision of the estimate and the stringency of the multiple testing correction.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Interpretation / Overstatement
- **Affected element** Discussion section
- **Evidence pointer** Discussion, paragraph 4
- **Issue** The statement "several layers of evidence suggest the high confidence of the prioritization strategy" is an overstatement. The evidence is largely correlative and computational, and the key functional validation (CRISPRa) was performed in a non-physiological cell type.
- **Required correction** Please temper this statement to reflect the suggestive nature of the evidence. For example, "these observations nominate rs1537373 as a candidate causal variant that warrants further investigation."

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Data availability
- **Affected element** Data Availability section
- **Evidence pointer** Data Availability section
- **Issue** The statement that "sensitive sequencing datasets are not publicly deposited" is a significant limitation for a study of this nature. The lack of public availability of the raw data prevents other researchers from replicating or extending the findings.
- **Required correction** Please consider depositing the de-identified, processed data (e.g., interaction matrices, eQTL summary statistics) in a public repository. At a minimum, please provide a detailed description of the data processing pipeline and the software used.

## Risk / unsupported claims
- The claim that MIR31HG is the "most recurrent" distal target of the 9p21.3 locus is unsupported without statistical analysis of the Hi-C data.
- The claim that the eQTL association in MIR31HG is "stable" is unsupported given the small sample size and lack of replication.
- The claim that the prioritized enhancer is "sufficient to upregulate MIR31HG" is based on a single CRISPRa experiment in a non-vascular cell line and is therefore not fully supported.
- The nomination of rs1537373 as a "candidate causal variant" is based on computational predictions and a single, unreplicated eQTL analysis; this is a hypothesis, not a validated finding.
- The statement that "several layers of evidence suggest the high confidence of the prioritization strategy" is an overstatement of the evidence presented.
- The claim that MIR31HG depletion promotes an "endothelial activation transcriptional program" is based on RNA-seq data, but the functional consequences of this program (e.g., effects on endothelial barrier function, leukocyte adhesion) are not directly demonstrated.