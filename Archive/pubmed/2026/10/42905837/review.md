## Review setup
- **Input scope** Full manuscript text including abstract, introduction, results, discussion, methods, and supplementary materials description
- **Assessment boundary** Scientific claims, methodological soundness, evidence quality, and internal consistency based solely on the provided manuscript text
- **Shared manuscript claim summary** The authors propose that multiple CCAN units assemble into a spherical shell-like structure in interphase DT20 kinetochores, with CENP-T and CENP-N localizing to the shell and the CENP-C cupin domain clustering at the center. They use coarse-grained molecular dynamics simulations, biochemical assays, and expansion microscopy to support this model, and show that CENP-C DNA binding via a basic stretch is critical for this organization.
- **Visible evidence base** Abstract, Introduction, Results sections (7 subsections), Discussion, Methods (partial), figure legends referenced but figures not visible, supplementary figure references
- **Missing materials affecting confidence** Figures and supplementary figures not provided; supplementary tables S1-S3 not provided; detailed simulation parameters and analysis code not fully described; raw imaging data not available; statistical details for imaging quantifications incomplete

## Reviewer
- **Overall assessment** This manuscript addresses a significant and timely question in chromosome biology: how multiple CCAN complexes organize spatially within the kinetochore. The combination of computational modeling, biochemistry, and super-resolution imaging is ambitious and potentially impactful. However, the evidence as presented has several critical gaps. The key claims regarding the spherical shell-like structure and the role of CENP-C DNA binding in organizing this structure are supported by indirect evidence, and the manuscript does not provide sufficient quantitative rigor or controls to fully establish the model. The imaging data, which are central to the main claim, cannot be evaluated without the figures. The simulation results are suggestive but rely on simplified models with limited validation. The functional significance of the proposed structure remains speculative. The manuscript is well-written and the logic is generally clear, but the evidence does not yet fully support the strong conclusions drawn.
- **Who would be interested in the results, and why** Researchers in chromosome biology, kinetochore structure and function, centromere biology, and cell division. The work is also relevant to those interested in applying integrative structural biology approaches combining simulation and imaging to study macromolecular assemblies in cells. The proposed model of CCAN organization could influence thinking about how kinetochores are assembled and how they transition from interphase to mitosis.
- **Major strengths** 1. The question is important and addresses a gap between high-resolution structures of individual CCAN complexes and the cellular context. 2. The multi-pronged approach combining MD simulations, biochemistry, and imaging is appropriate and potentially powerful. 3. The use of expansion microscopy to visualize kinetochore substructure is technically advanced. 4. The authors include important control experiments, such as testing antibody specificity and ruling out tagging artifacts. 5. The discussion of limitations, particularly regarding the oligomerization-deficient mutants, is honest and balanced.
- **Major Concerns** 
- **Minor Comments** 
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4, R1-M5
- **Assessment against Nature-style criteria** **Originality**: The question of how multiple CCAN units organize in cells is novel and the proposed spherical shell model is a new concept. However, the originality is somewhat tempered by the fact that the model is largely derived from simulations and the imaging evidence, while supportive, does not provide a definitive structural determination. **Scientific importance**: If the model is correct, it would be an important advance in understanding kinetochore architecture. The work addresses a fundamental question in cell biology. **Interdisciplinary readership**: The work bridges structural biology, computational biology, and cell biology, and would be of interest to a broad audience. **Technical soundness**: The technical approaches are generally sound, but there are concerns about the validation of the simulation models, the quantitative rigor of the imaging analysis, and the lack of direct evidence for the proposed molecular interactions. **Readability for nonspecialists**: The manuscript is clearly written and the logic is easy to follow, although some of the simulation details may be challenging for non-experts. The abstract and introduction effectively frame the problem.
- **Recommendation posture** Supportive if technical concerns are resolved

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence quality
- **Claim pointer** The central claim that "multiple CCAN units form a spherical shell-like structure in interphase DT40 kinetochores" is based primarily on expansion microscopy images.
- **Evidence pointer** Results section "The spherical shell-like structure is observed in DT40 kinetochores"; Figure 4; Figure 5
- **Concern** The manuscript's central claim rests on the interpretation of expansion microscopy images. However, the figures are not provided, making it impossible to assess the quality of the imaging data, the resolution achieved, or the validity of the image analysis. The description of the image quantification is insufficient. The authors state that they performed "rotational averaging followed by intensity profiling," but do not provide details on how many kinetochores were analyzed, how the rotational averaging was performed, what the variability was between kinetochores, or how the "shell-like" phenotype was defined and distinguished from other possible distributions. The claim that the structure is "spherical" requires 3D reconstruction or at least analysis of multiple z-slices, which is not described in sufficient detail. Without seeing the actual images and the quantitative analysis, the central claim cannot be evaluated.
- **Why it matters** The entire paper is built around the observation of a spherical shell-like structure. If this observation is not robust and rigorously quantified, the main conclusion of the paper is not supported.
- **Resolution test** The authors must provide the actual images and a detailed, quantitative description of the image analysis. This should include: the number of kinetochores analyzed, the method for determining the shell-like phenotype, a statistical comparison of the distribution of CENP-T and CENP-C signals, and a demonstration that the observed structure is not an artifact of the imaging or analysis method. Ideally, they would also provide a 3D reconstruction or orthogonal views to support the "spherical" claim.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Model validation
- **Claim pointer** The claim that "CENP-C–DNA interactions constrain the orientation of CCAN units, supporting a spherical shell-like organization via CENP-C oligomerization" is derived from coarse-grained molecular dynamics simulations.
- **Evidence pointer** Results section "CENP-C contributes to the organized orientation of CCAN units in the presence of DNA"; Results section "CG-MD simulations suggest a shell-like organization of multiple CCAN units around a central CENP-C core"; Figure 1; Figure 2; Figure 3
- **Concern** The coarse-grained MD simulations are a central pillar of the paper, but the validation of these models is insufficient. The authors use AlphaFold3 predictions to build their models, but the accuracy of these predictions for large, multi-subunit complexes with disordered regions is not established. The simulations are performed on a simplified system (two CCAN units or eight CCAN units) and the timescales are short (1 μs). The authors do not provide any evidence that the simulations have converged or that the results are independent of the initial conditions beyond testing six configurations. Most importantly, the simulations are used to make a specific prediction about the orientation of CCAN units, but this prediction is not directly tested experimentally. The link between the simulation results and the observed cellular structure is largely correlative.
- **Why it matters** The simulations are used to provide a mechanistic explanation for the observed structure. If the simulations are not reliable, the proposed mechanism is not supported.
- **Resolution test** The authors should provide a more thorough validation of their simulation models. This could include: comparing the simulation results to experimental data on CCAN dynamics or interactions, showing that the results are robust to changes in simulation parameters, or performing longer simulations to ensure convergence. Most importantly, they should design an experiment that directly tests a prediction of the simulation, such as the effect of specific mutations on CCAN orientation.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Causal evidence
- **Claim pointer** The claim that "CENP-C knockout or expression of a CENP-C DNA binding deficient mutant abolishes the structure" is used to establish a causal role for CENP-C DNA binding in shell formation.
- **Evidence pointer** Results section "CENP-C–DNA interaction is critical for kinetochore function"; Results section "CENP-C–DNA interaction is required for proper formation of the spherical shell-like structure in interphase DT40 cells"; Figure 7
- **Concern** The experiments with the CENP-C knockout and the DNA binding deficient mutant are critical for establishing causality. However, the manuscript does not provide sufficient detail on these experiments. For example, it is not clear how the "shell-like structure" was quantified in these experiments, or whether the observed effect is specific to the loss of DNA binding or a consequence of general CENP-C dysfunction. The authors note that the oligomerization-deficient mutants showed reduced kinetochore localization, which complicates the interpretation. The manuscript would be strengthened by a more detailed analysis of the phenotypes, including the localization of other kinetochore proteins and the integrity of the centromere.
- **Why it matters** The causal claim is essential to the paper's conclusion. If the loss of the shell structure is an indirect consequence of CENP-C dysfunction, the specific role of DNA binding in organizing the shell is not established.
- **Resolution test** The authors should provide a more detailed characterization of the CENP-C knockout and mutant phenotypes. This should include a quantitative analysis of the shell structure, an assessment of centromere integrity, and an analysis of whether other CCAN components are properly localized. They should also consider using a more targeted approach, such as a mutation that specifically disrupts DNA binding without affecting other CENP-C functions.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Quantitative rigor
- **Claim pointer** The claim that the shell structure is "most pronounced during S to G2 phases" is based on cell cycle analysis.
- **Evidence pointer** Results section "The spherical shell-like structure is most pronounced during S to G2 phases"; Figure 6
- **Concern** The cell cycle analysis is presented qualitatively. The authors state that the shell structure "gradually emerged at the mid S phase and was most pronounced at the G2 phase," but do not provide quantitative data on the frequency or size of the shell structure at different cell cycle stages. The use of CDK1-as for synchronization is a good approach, but the efficiency of synchronization and the potential for cell cycle arrest artifacts should be discussed.
- **Why it matters** The cell cycle dependence of the structure is an important aspect of the model. Without quantitative data, it is difficult to assess the strength of this claim.
- **Resolution test** The authors should provide quantitative data on the percentage of cells with a clear shell structure at each cell cycle stage, along with statistical analysis. They should also confirm the cell cycle stage using multiple markers.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Alternative explanations
- **Claim pointer** The claim that the spherical shell-like structure is a "genuine feature of the interphase kinetochore" is supported by a series of control experiments.
- **Evidence pointer** Results section "The spherical shell-like structure is a genuine feature of the interphase kinetochore"; Figure S5
- **Concern** While the authors have performed several important control experiments, they have not ruled out all potential artifacts. For example, the effect of the fixation and expansion protocol on the 3D organization of the kinetochore is not fully addressed. The authors mention that they used two different expansion methods (ExM and U-ExM), which is good, but they do not directly compare the results from these methods. Additionally, the possibility that the shell structure is a result of the specific antibody clone used, despite the Western blot analysis, cannot be completely excluded without testing multiple antibodies.
- **Why it matters** The claim that the structure is genuine is important, as it suggests the observation is not an artifact. If alternative explanations are not fully ruled out, the conclusion is weakened.
- **Resolution test** The authors should provide a more direct comparison of the results from different expansion methods and ideally use a different, well-characterized antibody against CENP-T to confirm the observation. They could also consider using a correlative light and electron microscopy approach to validate the structure at higher resolution.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Methods section "MD simulations"
- **Evidence pointer** Methods section "MD simulations"
- **Issue** The description of the MD simulation methods is not sufficiently detailed to be reproduced. The authors mention using the Martini 2.2 model and GROMACS, but do not provide specific parameters, such as the version of the Martini force field parameters, the water model, the salt concentration, or the temperature coupling scheme.
- **Required correction** Provide a more detailed description of the simulation parameters, including the specific Martini parameters used, the simulation box size, the number of water molecules and ions, and the equilibration and production run settings. It would also be helpful to provide a link to any input files or a repository where the simulation parameters are available.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** Results section "CENP-C–DNA interaction is critical for kinetochore function"
- **Evidence pointer** Results section "CENP-C–DNA interaction is critical for kinetochore function"; Figure 3F
- **Issue** The mitotic index data are presented as a bar graph, but the number of cells counted and the statistical test used are not stated in the text.
- **Required correction** State the number of cells counted for each condition and the statistical test used to compare the mitotic indices. Also, indicate whether the data are presented as mean ± SD or SEM.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Results section "The spherical shell-like structure is observed in DT40 kinetochores"
- **Evidence pointer** Results section "The spherical shell-like structure is observed in DT40 kinetochores"; Figure 4
- **Issue** The authors state that the shell structure has a size of "~200 nm" but do not provide a measure of variability or the number of kinetochores measured.
- **Required correction** Provide the mean and standard deviation of the shell size, along with the number of kinetochores analyzed.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Interpretation
- **Affected element** Discussion section
- **Evidence pointer** Discussion section
- **Issue** The discussion of the relationship between the interphase shell structure and the mitotic kinetochore plate is brief. The authors suggest the shell may be a "preorganized state," but do not elaborate on how this transition might occur.
- **Required correction** Expand the discussion on the potential functional significance of the interphase shell structure and how it might relate to the assembly of the mitotic kinetochore. This would strengthen the impact of the findings.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract
- **Evidence pointer** Abstract
- **Issue** The abstract states that "CENP-T and CENP-N localize to the CCAN shell, whereas the CENP-C cupin domain clusters at the center." This is a key finding, but the abstract does not mention the size of the structure or the cell cycle dependence, which are also important.
- **Required correction** Consider adding a brief mention of the size and cell cycle dependence of the structure to the abstract to provide a more complete summary of the findings.

## Risk / unsupported claims
- The claim that the spherical shell-like structure is a "genuine feature" of interphase kinetochores is not fully supported without the actual images and a more comprehensive set of controls.
- The claim that CENP-C DNA binding "constrains the orientation of CCAN units" is based on simulations that are not fully validated and is not directly tested experimentally.
- The claim that the shell structure is "most pronounced during S to G2 phases" is not supported by quantitative data.
- The functional significance of the interphase shell structure, and its relationship to mitotic kinetochore function, is speculative and not directly tested.
- The claim that the CENP-C basic stretch is "conserved across species" is made but the sequence alignment is not shown.
- The claim that the "predicted chicken CCAN model closely resembled the cryo-EM structure of the human CCAN core complex" is made but the comparison is not shown quantitatively.