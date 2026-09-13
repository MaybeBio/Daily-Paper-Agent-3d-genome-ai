## Review setup
- **Input scope** Full manuscript (Abstract, Introduction, Materials and Methods, Results, Discussion, References, Supplementary Material reference)
- **Assessment boundary** Scientific content, experimental design, data analysis, interpretation, and conclusions as presented in the manuscript
- **Shared manuscript claim summary** The manuscript claims that loss of SUMOylation in Drosophila wing imaginal discs transforms PRC1 condensates into large, gel-like structures with reduced dynamics, rewires 3D genome architecture (specifically inter-TAD contacts) independently of H3K27me3 changes, and that these topological shifts correlate with gene misregulation.
- **Visible evidence base** Abstract, Introduction, Materials and Methods, Results (including Figures 1-6 and Supplementary Figures S1-S8), Discussion, Data availability statement
- **Missing materials affecting confidence** Raw sequencing data (GSE320399) and processed data files (e.g., Hi-C contact matrices, CUT&RUN peak files) are not provided for independent verification. The Zenodo link (https://doi.org/10.5281/zenodo.21446525) is referenced but not accessible in this review. Supplementary figures are referenced but not provided. Code for the polymer model and Hi-C analysis is not provided.

## Reviewer
- **Overall assessment** This manuscript presents a compelling and well-integrated study combining in vivo imaging, biophysical modeling, and multi-omics (RNA-seq, CUT&RUN, Hi-C) to investigate the role of SUMOylation in regulating PRC1 condensate properties and 3D genome organization. The central finding that SUMO depletion drives aberrant PRC1 clustering and rewires inter-TAD contacts without major changes in H3K27me3 is novel and significant. The study is technically ambitious and the data generally support the main conclusions. However, several major concerns regarding the specificity of the SUMO depletion phenotype, the robustness of the biophysical model parameterization, and the causal link between contact rewiring and gene expression need to be addressed before the case is fully established.
- **Who would be interested in the results, and why** Researchers in chromatin biology, 3D genome organization, phase separation, Polycomb group biology, and post-translational modifications. The work provides a mechanistic link between a specific PTM (SUMOylation), the material state of a key chromatin regulator (PRC1), and higher-order genome architecture, which is of broad interest to the fields of gene regulation and nuclear organization.
- **Major strengths** 1. The combination of in vivo imaging (AiryScan, half-FRAP) with a biophysical polymer model to explain the observed changes in PRC1 condensate morphology is a powerful and elegant approach. 2. The demonstration that 3D genome rewiring (specifically PcG-PcG and PcG-Active TAD contact changes) occurs independently of global H3K27me3 changes is a significant and novel finding, challenging the view that histone marks are the sole drivers of Polycomb-mediated genome organization. 3. The quartile-based analysis of inter-TAD contacts (Figures 5, 6) is a sophisticated and informative way to dissect the bidirectional nature of contact rewiring, revealing that both strong and weak contacts are differentially affected.
- **Major Concerns**
    - **Concern ID** R1-M1
    - **Severity** Major
    - **Blocking** Yes
    - **Axis** Specificity of perturbation
    - **Claim pointer** The manuscript claims that the observed effects on PRC1 condensates and 3D genome organization are a direct consequence of reduced PRC1 SUMOylation.
    - **Evidence pointer** Results (Figures 1-6), Discussion (Limitations and future directions)
    - **Concern** The study uses global SUMO depletion (smt3 RNAi), which affects hundreds of SUMOylated proteins. The authors acknowledge this limitation and mention that a Pc-3KR mutant did not phenocopy the strong SUMO RNAi effects. This is a critical weakness. The observed changes in PRC1 clustering, 3D genome rewiring, and gene expression could be indirect consequences of SUMO depletion on other pathways (e.g., transcription factors, other chromatin regulators, stress responses) rather than a direct effect on PRC1 condensate properties. The claim that SUMOylation is a "critical regulator of PRC1 condensates" is not fully supported by the data, as the perturbation is not specific to PRC1.
    - **Why it matters** The central mechanistic model of the paper hinges on the idea that SUMOylation directly modulates PRC1 self-interactions. Without a PRC1-specific perturbation (e.g., a SUMOylation-deficient PRC1 mutant that phenocopies the key effects), the possibility of indirect effects cannot be ruled out, significantly weakening the core conclusion.
    - **Resolution test** The authors should either (a) provide evidence that a PRC1-specific SUMOylation mutant (e.g., a more comprehensive mutant targeting multiple SUMO sites on Pc, Ph, or Sce) recapitulates the key phenotypes (large foci, reduced dynamics, TAD rewiring, gene misregulation), or (b) perform a rescue experiment by expressing a SUMO-PRC1 fusion protein in the SUMO RNAi background. If this is not feasible, the claims must be substantially tempered to reflect that the study identifies a correlation between global SUMO loss and PRC1-related phenotypes, not a direct regulatory mechanism.

    - **Concern ID** R1-M2
    - **Severity** Major
    - **Blocking** Yes
    - **Axis** Causal link between contact rewiring and gene expression
    - **Claim pointer** The manuscript claims that the rewiring of PcG-PcG contacts "correlates with" and is "most directly tied to" gene misregulation, implying a causal or instructive role.
    - **Evidence pointer** Results (Figures 5, 6, Supplementary Figure S8)
    - **Concern** The correlation between PcG-PcG contact changes and gene expression changes is weak (Spearman ρ = -0.21, P = .003). While statistically significant, this correlation explains only a small fraction of the variance in gene expression. The analysis is also correlative and does not establish causality. The observed changes in gene expression could be a consequence of altered transcription factor activity, changes in other chromatin features (e.g., H3K27ac, which is also altered), or the direct effect of SUMO depletion on transcription machinery, rather than a direct result of the 3D contact rewiring. The claim that PcG-PcG contacts are the "structural feature most directly tied to PcG-mediated repression" is an overstatement based on the presented correlative evidence.
    - **Why it matters** The paper's narrative positions the 3D genome rewiring as a key mechanism for gene misregulation. If the link is merely correlative and weak, the functional significance of the observed topological changes is diminished. The paper would benefit from a more cautious interpretation.
    - **Resolution test** The authors should perform an experiment to test causality. For example, they could use an engineered system to force or disrupt specific PcG-PcG contacts (e.g., using dCas9-based tools or synthetic TAD boundaries) in the presence or absence of SUMO and measure the effect on gene expression. Alternatively, they could use a time-course experiment to see if contact changes precede or follow expression changes. A more conservative interpretation of the correlative data is also required.

    - **Concern ID** R1-M3
    - **Severity** Major
    - **Blocking** No
    - **Axis** Biophysical model parameterization and validation
    - **Claim pointer** The manuscript claims that the biophysical model shows that an increase in PRC1 self-attraction (EP-P) is sufficient to explain the SUMO RNAi phenotype, and that this provides "indirect evidence that chromatin-mediated phase-separation of PRC1 occurs in vivo."
    - **Evidence pointer** Results (Figure 2, Supplementary Figure S2), Materials and Methods (Polymer model, Monte Carlo simulation)
    - **Concern** The model is parameterized with a specific set of values (e.g., EP-P = 1 kBT for wild-type) that are described as "representative." The authors state that results are "not qualitatively dependent on this choice," but this is not rigorously demonstrated. The model explores a range of EP-P, EP-H, and RP/H values, but the parameter space is large and the choice of the "wild-type" set is somewhat arbitrary. Furthermore, the model's prediction that an increase in EP-P alone (and not a change in EP-H) explains the SUMO RNAi phenotype is based on a qualitative comparison of simulated and experimental foci properties (number, size, nucleoplasmic fraction). A more quantitative validation, such as directly fitting the model to the experimental data (e.g., foci size distributions, FRAP recovery curves), would significantly strengthen the claim. The model is also a coarse-grained representation and may not capture all relevant biophysical details.
    - **Why it matters** The model is a central piece of evidence supporting the claim that SUMOylation directly modulates PRC1 self-interactions. If the model's parameterization is not robustly justified or validated, the conclusions drawn from it are weakened. The claim of "indirect evidence" for phase separation is also a strong statement that requires more rigorous support.
    - **Resolution test** The authors should (a) perform a sensitivity analysis to show that the qualitative conclusions hold across a wider, biologically plausible range of parameters, (b) attempt to quantitatively fit the model to the experimental data (e.g., using Bayesian inference or approximate Bayesian computation), and (c) provide a more direct experimental test of the model's prediction, for example by measuring PRC1-PRC1 interaction strength (e.g., via FRET or crosslinking) in control and SUMO RNAi conditions.

    - **Concern ID** R1-M4
    - **Severity** Major
    - **Blocking** No
    - **Axis** Half-FRAP interpretation and controls
    - **Claim pointer** The manuscript claims that half-FRAP analysis reveals that PRC1 foci in SUMO RNAi are "gel-like or solid-like" with "restricted internal dynamics" and "absence of the surface tension that would be expected from a phase-separated liquid structure."
    - **Evidence pointer** Results (Figure 1e)
    - **Concern** The half-FRAP experiments were only performed on SUMO RNAi wing discs because control foci were too small. This is a significant limitation. The claim that the foci are "gel-like" is based on the absence of a characteristic dip in the unbleached half curve and a low mobile fraction (~30%). However, without a control (e.g., a known liquid-like condensate in the same tissue, or a control with smaller foci that can be bleached), it is difficult to interpret these results. The low mobile fraction could also be due to the large size of the foci, which might limit diffusion, or to the fact that the foci are chromatin-associated and thus inherently less dynamic. The observation that ~14% of foci show a small dip suggests heterogeneity, which is not fully explained.
    - **Why it matters** The material state of the condensates is a key part of the paper's narrative. The claim that they are "gel-like" is a strong biophysical statement that is not adequately supported by the data, given the lack of a proper control and the potential for alternative interpretations.
    - **Resolution test** The authors should (a) perform half-FRAP on a known liquid-like condensate in the same tissue (e.g., a nuclear speckle marker) as a positive control, (b) attempt to perform half-FRAP on the largest control foci, or use a different technique (e.g., FRAP on smaller regions within the large foci) to assess internal dynamics, and (c) discuss alternative interpretations for the observed FRAP behavior (e.g., size-dependent diffusion, chromatin tethering).

- **Minor Comments**
    - **Concern ID** R1-m1
    - **Severity** Minor
    - **Axis** Data presentation
    - **Affected element** Figure 1e
    - **Evidence pointer** Results (Figure 1e)
    - **Issue** The half-FRAP data is presented as a single representative curve and a pie chart. The number of foci analyzed (n) is not stated in the figure legend or main text. The variability between foci is not shown.
    - **Required correction** Provide the number of foci analyzed (n) and show the variability (e.g., individual traces or a shaded area representing the standard deviation/error) in the FRAP recovery curve.

    - **Concern ID** R1-m2
    - **Severity** Minor
    - **Axis** Statistical reporting
    - **Affected element** Results (Figures 3, 4, 5, 6)
    - **Evidence pointer** Results (Figures 3, 4, 5, 6)
    - **Issue** Many statistical comparisons are reported with P-values, but the specific statistical test used is not always stated in the figure legend or main text (e.g., for comparisons in Figures 4, 5, 6). The use of "P = .077" (Figure 4c) without specifying the test is insufficient.
    - **Required correction** Clearly state the statistical test used for each comparison (e.g., Wilcoxon rank-sum test, t-test, Kruskal-Wallis test) in the figure legends or methods.

    - **Concern ID** R1-m3
    - **Severity** Minor
    - **Axis** Data availability
    - **Affected element** Data availability statement
    - **Evidence pointer** Data availability
    - **Issue** The Zenodo link (https://doi.org/10.5281/zenodo.21446525) is provided for computational analysis descriptions, but the code for the polymer model and Hi-C analysis is not explicitly mentioned as being available.
    - **Required correction** Provide a clear statement about the availability of all custom code (e.g., for the polymer model, Hi-C analysis scripts) in a public repository (e.g., GitHub, Zenodo).

    - **Concern ID** R1-m4
    - **Severity** Minor
    - **Axis** Clarity
    - **Affected element** Results (Figure 4a)
    - **Evidence pointer** Results (Figure 4a)
    - **Issue** The Z-score differential map in Figure 4a is described as showing "some regions... that loose contacts in SUMO RNAi." The color scale and interpretation of positive/negative Z-scores are described in the methods, but it would be helpful to explicitly state in the figure legend what the positive and negative Z-scores represent (e.g., "Red: more contacts in SUMO RNAi; Blue: more contacts in Control").
    - **Required correction** Add a clear description of the Z-score color scale in the Figure 4a legend.

    - **Concern ID** R1-m5
    - **Severity** Minor
    - **Axis** Interpretation
    - **Affected element** Discussion
    - **Evidence pointer** Discussion
    - **Issue** The discussion states that the findings "reveal a broader paradigm in which reversible post-translational modifications fine-tune the material state and regulatory capacity of nuclear condensates." While this is a plausible and interesting idea, the study only examines one PTM (SUMOylation) on one condensate (PRC1). The claim of a "broader paradigm" is an overgeneralization.
    - **Required correction** Temper this claim to reflect that the study provides a specific example of this paradigm, and that future work is needed to test its generality.

- **Technical failings that need to be addressed before the case is established** R1-M1 (Specificity of perturbation), R1-M2 (Causal link between contact rewiring and gene expression)

- **Assessment against Nature-style criteria** 
    - **Originality**: High. The concept that a specific PTM (SUMOylation) can regulate the material state of a chromatin regulator (PRC1) and thereby control 3D genome architecture independently of histone marks is novel and not previously demonstrated.
    - **Scientific importance**: High. The findings have significant implications for understanding how post-translational modifications can dynamically control genome organization and gene expression, a fundamental question in cell and developmental biology.
    - **Interdisciplinary readership**: Broad. The work will be of interest to researchers in chromatin biology, 3D genomics, phase separation, epigenetics, and gene regulation.
    - **Technical soundness**: Moderate. The study uses a sophisticated and appropriate set of techniques. However, the major concerns regarding the specificity of the perturbation (R1-M1) and the causal link between contact rewiring and expression (R1-M2) are significant weaknesses that need to be addressed. The biophysical model, while elegant, requires more rigorous validation (R1-M3).
    - **Readability for nonspecialists**: Good. The manuscript is generally well-written and the narrative is clear. The figures are informative. Some of the more technical details (e.g., the polymer model Hamiltonian) are well-explained in the methods.

- **Recommendation posture** Supportive if technical concerns are resolved. The core findings are novel and potentially important, but the major concerns regarding the specificity of the perturbation and the causal link between contact rewiring and gene expression must be addressed. The authors should provide additional evidence (e.g., PRC1-specific mutants, causal experiments) or substantially temper their claims. The biophysical model also requires more rigorous validation.

## Risk / unsupported claims
- The claim that SUMOylation is a "critical regulator of PRC1 condensates" is not fully supported, as the perturbation is global (smt3 RNAi) and not specific to PRC1.
- The claim that PcG-PcG contact rewiring is "most directly tied to" gene misregulation is an overstatement based on a weak correlative analysis (Spearman ρ = -0.21).
- The claim that the half-FRAP data demonstrates a "gel-like" state is not adequately supported due to the lack of a proper control.
- The claim that the findings reveal a "broader paradigm" for PTM regulation of condensates is an overgeneralization.