## Review setup
- **Input scope** Full manuscript text (Abstract, Introduction, Materials and Methods, Results, Discussion) as provided. Figures, tables, and supplementary materials referenced but not included.
- **Assessment boundary** Assessment is limited to the claims and evidence as presented in the provided text. Statistical details, figure contents, and supplementary data are referenced but not directly verifiable from the supplied material.
- **Shared manuscript claim summary** The manuscript proposes that high densities of genomic sites co-bound by HPL-2, LIN-61, and marked by H3K9me2 form "Varied Ensembles of Long-range ChROmatin interactions" (VELCROs), which drive A/B chromatin compartmentalization in C. elegans embryos. The authors support this with Hi-C, ChIP-seq, mutant analyses, and polymer simulations.
- **Visible evidence base** Text descriptions of Hi-C, ChIP-seq, RNA-seq, FRAP experiments, and polymer simulations. Specific quantitative results, statistical tests, and figure panels are referenced but not shown.
- **Missing materials affecting confidence** All figures, supplementary figures, tables, and detailed statistical outputs. Exact numerical values for effect sizes, confidence intervals, and P-values are not provided in the text. Details of simulation parameters and validation metrics are incomplete.

## Reviewer
- **Overall assessment** The manuscript addresses a fundamental question in chromatin biology: the molecular determinants of A/B compartmentalization. The authors present a compelling conceptual framework, introducing VELCROs as a distinct class of chromatin interactions. The combination of experimental genetics, genomics, and simulation is ambitious and potentially impactful. However, the current text does not provide sufficient quantitative evidence to fully evaluate the robustness of the claims. Key concerns include the reliance on density versus intensity of marks, the interpretation of the mutant phenotypes, and the generalizability of the simulation results. The work is potentially significant but requires substantial additional evidence and clarification to be fully convincing.
- **Who would be interested in the results, and why** Chromatin biologists, epigenetics researchers, and computational biologists studying 3D genome organization. The work is also relevant to those interested in heterochromatin formation, HP1 biology, and the physical principles underlying genome compartmentalization. The introduction of VELCROs as a concept will likely stimulate discussion and further research in the field.
- **Major strengths** 1. The study addresses a key open question in the field using a genetically tractable organism. 2. The combination of Hi-C, ChIP-seq, and polymer simulations provides a multi-pronged approach. 3. The identification of density (rather than intensity) of heterochromatic features as a key determinant is an interesting and potentially important distinction. 4. The concept of VELCROs as stochastic, combinatorial interaction ensembles is a novel and thought-provoking framework. 5. The use of multiple mutants, including a double mutant, to probe redundancy is a strength.
- **Major Concerns** The following concerns are detailed below.
- **Minor Comments** The following minor comments are detailed below.
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4, R1-M5, R1-M6.
- **Assessment against Nature-style criteria** **Originality:** High. The VELCRO concept is novel and provides a new framework for understanding compartmentalization. **Scientific importance:** High. Understanding the molecular drivers of A/B compartments is a central question in the field. **Interdisciplinary readership:** Moderate. The work will primarily appeal to specialists in chromatin and genome organization, though the biophysical concepts may have broader appeal. **Technical soundness:** Currently not fully established. The text lacks sufficient quantitative detail to assess the rigor of the analyses. The simulation model is simplified and its predictive power is not fully validated. **Readability for nonspecialists:** The abstract is clear, but the results section is dense and assumes significant prior knowledge of Hi-C analysis and polymer physics. The manuscript would benefit from clearer explanations of key concepts and analyses for a broader audience.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence strength
- **Claim pointer** The claim that "high densities of H3K9me2, HPL-2, LIN-61, and LEM-2 peaks may be linked to B compartmentalization" is a central premise of the paper.
- **Evidence pointer** Results section, Figure 1B and related text.
- **Concern** The manuscript states that the separation of repressive from active components is "solely observed when considering peak densities... but not when analysing the intensities of the same peaks." This is a critical distinction, but the text does not provide the quantitative data supporting this claim. No correlation coefficients, effect sizes, or statistical significance values are given. The reader cannot assess how strong this density effect is, how it compares to intensity, or whether the null result for intensity is due to lack of power or a genuine biological effect.
- **Why it matters** The entire VELCRO model is predicated on the idea that the density of binding sites, not the strength of individual binding events, is the key driver. If this distinction is not robustly demonstrated, the conceptual foundation of the paper is weakened.
- **Resolution test** Provide a clear quantitative comparison of density versus intensity, including correlation coefficients (e.g., Spearman's rho) with confidence intervals and P-values for the relationship between each metric and PC1/PC2 values. Show that the density effect is significantly stronger than the intensity effect, and that the intensity null result is not due to a lack of statistical power.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence strength
- **Claim pointer** The claim that "HPL-2 and the MBT-domain protein LIN-61 jointly contribute to chromatin compartmentalization" and that the double mutant shows "no detectable transition between compartments."
- **Evidence pointer** Results section, Figure 2B,C and Supplementary Figure S4B,C.
- **Concern** The text states that the lin-61; hpl-2 double mutant shows "no detectable transition between compartments," but no quantitative measure of this "detectability" is provided. What is the statistical test? What is the effect size? Is the transition truly absent, or is it reduced below the limit of detection? The text also mentions a "significant flattening" for the set-32; met-2 set-25 mutant, but again, the magnitude of this effect is not quantified. The comparison between the double mutant and the single mutants is crucial for the redundancy argument, but the text does not provide a statistical comparison between these conditions.
- **Why it matters** The redundancy of HPL-2 and LIN-61 is a key finding. Without a rigorous statistical demonstration that the double mutant is significantly more affected than either single mutant, the claim of redundancy is not fully supported.
- **Resolution test** Provide the amplitude of the PC1/PC2 transition for each genotype with measures of variance (e.g., SEM or 95% CI). Perform a statistical test comparing the double mutant to each single mutant and to wild-type. Show that the double mutant is significantly different from both single mutants and that the transition amplitude is not significantly different from zero.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The claim that polymer simulations show VELCROs "can drive a phase transition that segregates B from A chromatin compartments."
- **Evidence pointer** Results section, Figure 6 and Supplementary Figures S10, S11.
- **Concern** The simulation model is described as a "minimal model" with interactions scaling with the number of triple-positive sites and loop anchors. However, the text does not provide sufficient detail on the model parameters, the range of interaction strengths tested, or the criteria for determining a "phase transition." The claim of a first-order phase transition is based on "bimodal distributions" of relative spatial separation, but the text does not show these distributions or provide a quantitative analysis (e.g., bimodality index, free energy calculations). The robustness of the phase transition to model parameters is not discussed.
- **Why it matters** The simulation is used to support the physical plausibility of the VELCRO model. If the phase transition is not robustly demonstrated, the claim that VELCROs "drive" compartmentalization is weakened.
- **Resolution test** Provide a detailed description of the simulation parameters and the range over which the phase transition is observed. Show the bimodal distributions and provide a quantitative measure of bimodality. Demonstrate that the phase transition is robust to changes in model parameters (e.g., interaction strengths, polymer length). Ideally, map the phase diagram of the model.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Evidence strength
- **Claim pointer** The claim that "VELCROs are defined by high density of H3K9me2, HPL-2, and LIN-61 sites, but not by the intensity of their individual peaks."
- **Evidence pointer** Results section, Figure 5E and Supplementary Figure S9D.
- **Concern** The text states that "the PC1 value abruptly changed from A to B when genome bins were sorted according to the number of HPL-2 + LIN-61 + H3K9me2 but not HPL-2 + LIN-61 sites they contain." This is a key result, but the text does not provide the quantitative details. What is the magnitude of the PC1 change? How many bins were analyzed? What is the statistical significance of the difference between the two sorting methods? The "abrupt" change is not quantified.
- **Why it matters** This result is used to argue that the triple-positive sites are the specific drivers of compartmentalization. Without quantitative support, this claim is not fully established.
- **Resolution test** Provide a quantitative analysis of the relationship between the number of triple-positive sites per bin and PC1 value, including a statistical test for the difference between the triple-positive and double-positive sorting. Show the distribution of PC1 values for bins with different densities of triple-positive sites.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Evidence strength
- **Claim pointer** The claim that "mutants that display defective chromatin compartmentalization are impaired in VELCROs."
- **Evidence pointer** Results section, Figure 5B and Supplementary Figure S9A,B.
- **Concern** The text states that VELCROs are "absent in mutants showing impaired compartmentalization." However, the definition of "absent" is not clear. Is this a qualitative visual assessment of the APA plots, or is there a quantitative measure? The text does not provide a statistical comparison of APA signal strength between wild-type and mutant conditions.
- **Why it matters** This is a direct link between the proposed mechanism (VELCROs) and the phenotype (compartmentalization). A qualitative assessment is insufficient to establish this link.
- **Resolution test** Provide a quantitative measure of VELCRO strength (e.g., the ratio of diagonal to off-diagonal signal in the APA plot) for each genotype, with statistical tests comparing mutants to wild-type.

- **Concern ID** R1-M6
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The claim that the effects on compartmentalization are not due to changes in transcription, based on α-amanitin treatment and RNA-seq analysis.
- **Evidence pointer** Results section, Supplementary Figure S7.
- **Concern** The text states that α-amanitin treatment "did not cause a marked change in genome organization" and that there was no correlation between "changes in RNA expression and changes in compartmentalization." However, the text does not provide the details of the α-amanitin experiment. Was the treatment effective in inhibiting transcription? What was the magnitude of the change in gene expression? The lack of correlation is stated, but no correlation coefficient or statistical test is provided.
- **Why it matters** This is a negative control that is important for ruling out an alternative explanation. Without evidence that the treatment was effective and that the analysis was adequately powered, the conclusion is not fully supported.
- **Resolution test** Provide evidence that α-amanitin treatment effectively inhibited transcription (e.g., a significant reduction in total RNA levels or in the expression of housekeeping genes). Provide a quantitative analysis of the relationship between changes in gene expression and changes in compartmentalization, including a correlation coefficient and confidence interval.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract
- **Evidence pointer** Abstract, first sentence.
- **Issue** The phrase "The chromatin components that are involved in organizing eukaryotic genomes into active and inactive compartments remain unclear" is very broad. The study focuses on C. elegans, and the opening could be more specific to set expectations.
- **Required correction** Consider revising to "The chromatin components that organize C. elegans genomes into active and inactive compartments remain unclear" or similar.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Methods, Hi-C data analysis
- **Evidence pointer** Materials and Methods, "Analysis of Hi-C data".
- **Issue** The description of the Hi-C data analysis is brief. Key steps such as mapping, filtering, and normalization are mentioned, but the specific parameters and software versions are not fully detailed.
- **Required correction** Provide a more detailed description of the Hi-C data processing pipeline, including software versions, mapping parameters, and filtering criteria. Consider citing a more detailed protocol or providing a supplementary methods section.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Results, Figure 1B
- **Evidence pointer** Results section, "Different mutations impair long-range interactions of the C. elegans genome".
- **Issue** The text refers to "peak densities" and "intensities" but does not clearly define these terms in the context of the analysis. It is unclear if "density" refers to the number of peaks per bin or the fraction of the bin covered by peaks.
- **Required correction** Define "density" and "intensity" explicitly in the text or figure legend.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Interpretation
- **Affected element** Discussion
- **Evidence pointer** Discussion, "Chromatin compartments are linked to Varied Ensembles of Long-range ChROmatin interactions".
- **Issue** The discussion of the stochastic nature of VELCROs is interesting but speculative. The text acknowledges that "this interpretation requires further experiments," which is appropriate, but it could be more clearly separated from the more established findings.
- **Required correction** Consider clearly distinguishing between the data-supported findings and the more speculative interpretations in the discussion.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Methods, FRAP
- **Evidence pointer** Materials and Methods, "Live imaging and fluorescence recovery after photobleaching".
- **Issue** The FRAP analysis is described, but the number of biological replicates and the number of foci analyzed per condition are not stated.
- **Required correction** Provide the number of independent experiments and the number of foci analyzed for each condition.

- **Concern ID** R1-m6
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Results, Figure 3
- **Evidence pointer** Results section, "Organization and features of genomes with impaired B compartmentalization".
- **Issue** The text describes "a large reduction in long-range interactions" and "a steep initial decay" but does not provide the quantitative values for these observations.
- **Required correction** Provide the quantitative values for the scaling exponents or other metrics used to describe the contact decay curves.

## Risk / unsupported claims
- The claim that VELCROs are "defined by high density... but not by the intensity" is not quantitatively supported in the provided text.
- The claim that the lin-61; hpl-2 double mutant shows "no detectable transition between compartments" is not supported by statistical evidence.
- The claim that the polymer simulations demonstrate a "first-order phase transition" is not supported by the provided details.
- The claim that VELCROs are "absent" in mutants with impaired compartmentalization is not quantitatively supported.
- The claim that compartmentalization is not coupled to transcription is not fully supported due to lack of details on the α-amanitin experiment and the correlation analysis.
- The generalizability of the findings beyond C. elegans is not discussed, and the title's broad claim about "eukaryotic genomes" is not supported by the data presented.