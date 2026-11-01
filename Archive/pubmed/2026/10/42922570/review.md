## Review setup
- **Input scope** Full manuscript text provided (Abstract, Introduction, Results, Discussion, Methods, Data/Code availability, Acknowledgments). Supplementary figures, tables, and methods referenced but not supplied.
- **Assessment boundary** Evaluation is restricted to the material supplied. Quantitative claims that depend on Supplementary Figures S1–S3, Supplementary Tables S1–S2, and Supplementary Methods cannot be independently verified and are treated as unverifiable rather than confirmed.
- **Shared manuscript claim summary** The authors present HiC-LEGO, a domain-aware hierarchical framework that combines ensemble TAD selection, graph neural network structural learning, and progressive chromosome assembly to reconstruct high-resolution 3D genome structures. They claim higher reconstruction concordance (dSCC) than FLAMINGO and Hierarchical3DGenome at 5-kb resolution across five human cell lines, better preservation of TAD boundaries and intra-domain organization, kilobase-resolution reconstruction of GM12878 chromosome 8 with recovery of a MYC enhancer–promoter proximity, capture of Micro-C/RCMC microcompartment interactions, preservation of breast cancer stage-associated and patient-specific organization, and enrichment of compact configurations for Pore-C multi-way contacts.
- **Visible evidence base** Main-text figures referenced as Fig. 1–Fig. 8, with quantitative values reported in the text. External datasets are enumerated in Data availability. No supplementary figures, tables, or supplementary methods are included in the supplied material.
- **Missing materials affecting confidence** Supplementary Figure S1 (Hypothesis 2 vs 3 per-chromosome dSCC), Supplementary Figure S2 (breast cancer sensitivity analyses), Supplementary Figure S3 (Pore-C per-chromosome), Supplementary Table S1 (FISH probe distances), Supplementary Table S2 (CTCF anchor statistics), and Supplementary Methods (null model construction, matched-control generation, lower-confidence classification). These are load-bearing for several central claims.

## Reviewer
- **Overall assessment** The manuscript describes a coherent and reasonably well-motivated method for high-resolution 3D genome reconstruction and reports a broad set of evaluations spanning contact-map concordance, domain preservation, regulatory proximity, Micro-C/RCMC features, disease-associated organization, and multi-way Pore-C contacts. The conceptual framing, namely that domain definition is a critical and under-addressed step in hierarchical reconstruction, is sensible and the ensemble-selection idea is a reasonable response to TAD-caller variability. However, the supplied material does not permit independent verification of several central quantitative claims because key statistics, null models, and per-chromosome results reside in supplementary items that were not provided. Several reported effects are modest in magnitude, and the manuscript itself acknowledges that a stricter null does not reproduce the Pore-C compaction advantage in mean distance. The evidence as presented is suggestive but not yet sufficient to establish the stronger claims in the title and abstract.
- **Who would be interested in the results, and why** Researchers in computational genomics and 3D genome biology interested in converting Hi-C/Micro-C/Pore-C contact maps into explicit spatial coordinates; groups studying TAD-caller disagreement and ensemble domain definitions; cancer genomics researchers interested in structural correlates of disease progression; and method developers benchmarking high-resolution reconstruction against FLAMINGO and Hierarchical3DGenome. The work would also interest scientists seeking structural frameworks for interpreting regulatory interactions such as enhancer–promoter proximity.
- **Major strengths** The problem framing is clear and identifies a genuine limitation of existing hierarchical methods, namely sensitivity to domain definition. The pipeline is described in sufficient methodological detail to be reimplemented in principle, with explicit equations for domain interaction aggregation, embedding, distance conversion, and assembly. The evaluation spans multiple cell lines, multiple resolutions, multiple data modalities (Hi-C, Micro-C, RCMC, Pore-C), and a disease progression dataset, which is broader than typical for a single reconstruction method. The authors report a negative or non-confirmatory result for the stricter Pore-C anchor-shuffle null, which is a point of scientific honesty. Runtime and GPU compatibility are reported, which is relevant for practical adoption.
- **Major Concerns**
  - **Concern ID** R1-M1
    **Severity** Major
    **Blocking** Yes
    **Axis** Benchmarking validity and baseline fairness
    **Claim pointer** HiC-LEGO achieves higher reconstruction concordance than evaluated state-of-the-art methods at 5-kb resolution across five cell lines, with the highest mean chromosome-level dSCC in all 23 chromosomes per cell line.
    **Evidence pointer** Results section "Benchmarking HiC-LEGO Against State-of-the-Art..."; Fig. 2a, 2b, 2i
    **Concern** The comparison rests on dSCC as the primary metric, but the manuscript does not establish that dSCC is comparably optimized or comparably defined across the three methods. FLAMINGO and H3DG may use different internal objectives, distance conversions, or output conventions, and dSCC computed on reconstructed coordinates can favor methods whose training objective is itself a distance-correlation-like criterion. The reported margins (for example 0.52 versus 0.44–0.45 and 0.40–0.41 in K562 and HMEC) are not accompanied by dispersion, confidence intervals, or paired tests across chromosomes, so it is not possible to judge whether the differences are statistically separable from chromosome-to-chromosome variability.
    **Why it matters** The central comparative claim of the paper depends on this benchmark. If the metric is not neutral across methods, or if the differences are within noise, the headline claim of superior concordance is not established.
    **Resolution test** Provide per-chromosome dSCC values with dispersion, paired statistical tests across the 115 chromosome-level reconstructions, and a demonstration that dSCC is computed identically and neutrally for all three methods. Ideally include at least one orthogonal accuracy metric that is not a distance-correlation measure.
  - **Concern ID** R1-M2
    **Severity** Major
    **Blocking** Yes
    **Axis** Statistical support for null-model comparisons
    **Claim pointer** The MYC enhancer–promoter pair is 4.01-fold closer than the control median with empirical p = 0.0050; the 249 RCMC interactions are 1.24-fold enriched with p = 4.87 × 10−10; Pore-C native contacts show a genome-wide 7.4% median reduction and 17.4% falling in the most compact 10% of controls.
    **Evidence pointer** Results sections on 1-kb MYC locus, Ppm1g RCMC, and Pore-C; Fig. 3c,d, Fig. 4d, Fig. 7b,c; Supplementary Methods referenced but not provided
    **Concern** The construction of genomic-distance-matched controls, the number of control draws, the treatment of multiple comparisons across loci and chromosomes, and the definition of the empirical p-value are all deferred to Supplementary Methods that were not supplied. The Pore-C analysis in particular reports a genome-wide median reduction of 7.4% and an enrichment of 17.4% versus a 10% null, which are modest effects whose interpretation depends entirely on how the null preserves genomic distance, anchor identity, and interaction complexity. The manuscript also reports that under the stricter anchor-shuffle null the mean maximum distance advantage disappears genome-wide, which weakens the robustness of the compaction claim.
    **Why it matters** These null-model comparisons carry several of the paper's biological validation claims. Without the null construction, the reported p-values and fold-enrichments cannot be assessed for correctness or for sensitivity to null design.
    **Resolution test** Supply the Supplementary Methods with the exact control-generation procedure, the number of matched controls per test, the multiple-testing correction, and a sensitivity analysis showing that the reported enrichments survive reasonable alternative null constructions, including the anchor-shuffle null for the RCMC and MYC analyses.
  - **Concern ID** R1-M3
    **Severity** Major
    **Blocking** No
    **Axis** Internal consistency of ensemble domain selection
    **Claim pointer** Hypothesis 2 consistently outperforms Hypothesis 3 across all autosomes and chromosome X, with mean chromosome-wide dSCC increasing from 0.399 to 0.477, supporting the use of Hypothesis 2 for subsequent reconstruction.
    **Evidence pointer** Results section "Ensemble-based TAD optimization..."; Supplementary Figure S1 (not provided)
    **Concern** The selection of Hypothesis 2 is based on downstream dSCC, which is the same metric used to benchmark against competing methods. This creates a risk that the ensemble strategy is tuned to the evaluation metric rather than to biological fidelity. In addition, Hypothesis 1 was excluded because it retained too few domains, which means the ensemble framework's most stringent consensus option was never quantitatively evaluated. The claim that Hypothesis 2 reduces dependence on individual domain definitions is therefore supported only relative to Hypothesis 3, not relative to the full space of domain-selection strategies.
    **Why it matters** The methodological novelty of the paper is the ensemble domain selection. If its selection is driven by the same metric used to claim superiority, the independence of the validation is reduced.
    **Resolution test** Report the per-chromosome comparison underlying Supplementary Figure S1 in the main text, and evaluate the selected domain set against at least one biological criterion that is not dSCC, for example boundary overlap with an independent annotation or recovery of CTCF-anchored loops.
  - **Concern ID** R1-M4
    **Severity** Major
    **Blocking** No
    **Axis** Generalizability of the 1-kb claim
    **Claim pointer** HiC-LEGO reconstructs complete GM12878 chromosome 8 at 1-kb resolution and recovers close spatial proximity between an epigenomically supported distal MYC enhancer and its promoter.
    **Evidence pointer** Results section "HiC-LEGO resolves regulatory chromatin proximity at 1 kb resolution"; Fig. 3a–e
    **Concern** The 1-kb evaluation is limited to a single chromosome in a single cell line, and the chromosome-wide dSCC of 0.34 is substantially lower than the 5-kb values. The enhancer–promoter result rests on one selected HiCCUPS loop with a single empirical p-value, and the manuscript does not report how many other candidate enhancer–promoter pairs were tested or whether the selected pair is representative. The authors state that the analysis was limited by computational cost, which is understandable, but the abstract and title foreground kilobase resolution as a general capability.
    **Why it matters** The kilobase-resolution claim is a headline element. A single-locus, single-chromosome demonstration does not establish that the method generally preserves regulatory proximity at this resolution.
    **Resolution test** Either extend the 1-kb analysis to additional chromosomes or cell lines, or report a systematic survey of multiple enhancer–promoter pairs with an explicit multiple-testing framework, and temper the generality of the kilobase claim accordingly.
  - **Concern ID** R1-M5
    **Severity** Major
    **Blocking** No
    **Axis** Interpretation of disease-associated findings
    **Claim pointer** HiC-LEGO reconstructs structures that maintain stable TAD organization across healthy breast, primary tumors, and liver metastases, while revealing greater inter-patient structural heterogeneity in malignant pleural effusion samples.
    **Evidence pointer** Results sections on breast cancer at 5-kb and 1-kb; Figs. 5 and 6; Supplementary Figs. S1 and S2 (not provided)
    **Concern** The breast cancer analyses are explicitly described as partially recovering reported patterns, with several metrics following the expected direction but not all, and with five of twenty chromosome 13 reconstructions (including three PE samples) classified as lower confidence. The leave-one-out centroid analysis and boundary-similarity comparisons depend on Supplementary Figures that were not supplied. The claim of "stable TAD organization" across HB, PB, and LM is therefore a partial reproduction of a prior study's finding rather than an independent discovery, and the manuscript does not clearly separate what is reproduced from what is newly contributed.
    **Why it matters** The disease-associated claims are presented as validation of biological relevance. If they largely restate prior findings and are only partially recovered, their weight as independent evidence is limited.
    **Resolution test** Clearly delineate reproduced versus novel observations, report the lower-confidence samples explicitly in the main text with their effect on the conclusions, and provide the sensitivity analyses currently in Supplementary Figs. S1 and S2.
- **Minor Comments**
  - **Concern ID** R1-m1
    **Severity** Minor
    **Axis** Numerical reporting
    **Affected element** Distance values in the 1-kb MYC analysis
    **Evidence pointer** Results section on 1-kb MYC locus; Fig. 3c,d
    **Issue** The reported 3D Euclidean distance of 50.17 and control median of 201.39 are given without units, and the Methods state that coordinates are in arbitrary model units not calibrated to physical nanometres. The reader cannot judge the physical plausibility of the proximity.
    **Required correction** State explicitly that these are model units, and where possible provide a conversion or a scale-free normalized measure to aid interpretation.
  - **Concern ID** R1-m2
    **Severity** Minor
    **Axis** Metric definition
    **Affected element** dSCC
    **Evidence pointer** Results sections throughout; Methods
    **Issue** dSCC is used as the primary metric but its exact definition, including how distances are derived from contact maps and how ties and zeros are handled, is not given in the supplied Methods.
    **Required correction** Provide the formal definition of dSCC and the preprocessing steps applied before its computation.
  - **Concern ID** R1-m3
    **Severity** Minor
    **Axis** Reproducibility of hyperparameters
    **Affected element** Grid search ranges and convergence criteria
    **Evidence pointer** Methods sections on graph-based reconstruction and hierarchical assembly
    **Issue** The exponent grid search ranges differ across stages (0.1–1.9 for domains, 0.1–2.0 for fine-resolution and chromosome-wide refinement), and the rationale for these differences is not explained.
    **Required correction** Justify the differing ranges or unify them, and report the distribution of selected exponents across chromosomes and domains.
  - **Concern ID** R1-m4
    **Severity** Minor
    **Axis** Terminology consistency
    **Affected element** "LEGO" regions and "megabase-indexed" assembly
    **Evidence pointer** Methods section on hierarchical assembly
    **Issue** The term LEGO is used throughout without a formal definition in the supplied text, and its relationship to the 1-Mb backbone and to TAD boundaries is described operationally but not conceptually.
    **Required correction** Add a concise definition of a LEGO region and clarify how it differs from a TAD and from a fixed 1-Mb window.
  - **Concern ID** R1-m5
    **Severity** Minor
    **Axis** Figure and table accessibility
    **Affected element** Supplementary Tables S1 and S2
    **Evidence pointer** Results sections on FISH validation and CTCF anchors
    **Issue** Key validation statistics are placed in Supplementary Tables that were not supplied, and the main text reports only summary statements.
    **Required correction** Move the essential statistics for the FISH probe ordering and CTCF anchor distance comparisons into the main text or main figures.
- **Technical failings that need to be addressed before the case is established** R1-M1 (benchmark neutrality and statistical separability), R1-M2 (null-model construction and multiple testing), R1-M4 (generality of the 1-kb claim). R1-M3 and R1-M5 affect the strength but not the basic viability of the case.
- **Assessment against Nature-style criteria** Originality is moderate. Ensemble TAD selection and hierarchical assembly are individually established ideas, and the contribution is their combination with graph-based structural learning; the novelty is incremental rather than conceptual. Scientific importance is potentially meaningful for the 3D genome reconstruction community, but the demonstrated gains over existing methods are modest and the biological validations are largely reproductions of prior findings. Interdisciplinary readership is limited; the work is primarily of interest to computational genomics and 3D genome biology, with only indirect relevance to broader biology or medicine. Technical soundness is the weakest axis in the supplied material, because several central quantitative claims depend on supplementary null models and per-chromosome statistics that were not provided, and the primary benchmark metric is not demonstrated to be neutral across methods. Readability for nonspecialists is adequate in the Introduction and Discussion, but the Results sections assume substantial familiarity with dSCC, TAD callers, and contact-map conventions, and the abstract overstates generality relative to the single-chromosome 1-kb demonstration.
- **Recommendation posture** Currently not established from the provided evidence. The work is potentially supportive if the technical concerns, in particular the benchmark neutrality, null-model construction, and generality of the kilobase claim, are resolved with the missing supplementary material and additional statistical reporting.

## Risk / unsupported claims
- The claim of higher reconstruction concordance than state-of-the-art methods is supported only by dSCC, whose neutrality across methods is not demonstrated, and without dispersion or paired tests (weakly supported).
- The claim that Hypothesis 2 reduces dependence on individual domain definitions is supported only relative to Hypothesis 3, with Hypothesis 1 excluded and Supplementary Figure S1 not provided (weakly supported).
- The MYC enhancer–promoter proximity claim rests on a single selected loop with an empirical p-value whose null construction is not provided (unverifiable from supplied material).
- The RCMC microcompartment compaction claim (1.24-fold, p = 4.87 × 10−10) depends on a matched-control procedure described only in Supplementary Methods (unverifiable from supplied material).
- The Pore-C multi-way compaction claim is weakened by the manuscript's own report that the stricter anchor-shuffle null does not show a genome-wide mean-distance advantage, and the genome-wide 7.4% median reduction and 17.4% versus 10% enrichment are modest (weakly supported).
- The breast cancer claims of stable early-stage TAD organization and increased pleural-effusion heterogeneity are partial reproductions of van den Brand et al., with five of twenty chromosome 13 reconstructions classified as lower confidence and sensitivity analyses deferred to Supplementary Figures (weakly supported).
- The generalizability of kilobase-resolution reconstruction is asserted in the title and abstract but demonstrated only for GM12878 chromosome 8 (unsupported as a general claim).
- The statement that HiC-LEGO "preserves regulatory interactions, disease-associated chromatin organization and higher-order spatial relationships beyond pairwise contact-map concordance" is broader than the supplied evidence, which is largely concordance-based with limited independent biological validation (overstated relative to evidence).