## Review setup
- **Input scope** Full manuscript text (abstract, introduction, methods, results, discussion, conclusions) without supplementary figures/tables
- **Assessment boundary** Scientific claims, methodological soundness, evidence consistency, and alignment with stated conclusions
- **Shared manuscript claim summary** The authors use extensive classical MD simulations, NMR spectroscopy, and fluorescence polarization to propose that MBD2 binding to methylated CpG DNA involves a bistable equilibrium between a primary X-ray-like state and a secondary reduced-affinity state, with S189 acting as a key macro-switch controlling the equilibrium.
- **Visible evidence base** Main text figures referenced (Figs 1–5), supplementary figure/table references (Figs S1–S28, Tables S1–S4), methods descriptions, experimental protocols
- **Missing materials affecting confidence** Supplementary figures and tables not provided; full NMR spectral assignments not shown; force field parameter details for 5mC not fully specified; convergence metrics for umbrella sampling not shown; raw MD trajectory data not accessible

## Reviewer

### Overall assessment
This manuscript presents a substantial computational and experimental investigation into the conformational dynamics of MBD2 binding to methylated CpG DNA. The central claim of a bistable binding equilibrium, with S189 as a key structural switch, is interesting and potentially significant for understanding epigenetic recognition. The combination of unbiased MD simulations, mutagenesis, NMR, and fluorescence polarization provides a multi-pronged approach that is commendable. However, several technical concerns regarding simulation convergence, force field accuracy for 5mC, and the interpretation of the NMR data need to be addressed before the bistable equilibrium claim is fully established. The broader generalization to other protein-DNA complexes is intriguing but currently speculative.

### Who would be interested in the results, and why
Structural biologists and computational biophysicists studying protein-DNA recognition, epigenetic researchers focused on methyl-CpG binding proteins (MBD family), and researchers interested in conformational dynamics of biomolecular complexes. The proposed bistable equilibrium concept could inform studies on other DNA-binding proteins and may have implications for understanding how binding affinity and specificity are balanced in epigenetic regulation.

### Major Strengths
- The study addresses a significant and timely question about the molecular basis of MBD2 selectivity and binding dynamics
- The combination of long-timescale unbiased MD simulations with experimental validation (NMR, FP) is methodologically strong
- The identification of S189 as a potential macro-switch is a concrete, testable hypothesis
- The use of two different DNA sequences to validate the secondary state strengthens the generality of the finding
- The computational setup is described in sufficient detail to be reproducible

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The authors claim that the secondary state is a stable, distinct conformational state of the MBD2-mCpG complex that persists over microseconds.
- **Evidence pointer** Results section "The secondary state adopts a distinct complex conformation"; Fig 2C; Fig 3
- **Concern** The identification of the secondary state relies heavily on clustering of MD trajectories. The manuscript does not provide sufficient evidence that the secondary state represents a true thermodynamic minimum rather than a kinetically trapped intermediate. The clustering criteria, the choice of RMSD cutoffs, and the statistical significance of the separation between states are not fully described. Furthermore, the persistence of the secondary state over "multiple microseconds" in only 3 out of 7 replicas raises questions about its thermodynamic relevance. The authors should provide free energy profiles or at least demonstrate that the secondary state is visited reversibly within individual trajectories.
- **Why it matters** The central claim of the paper is the existence of a bistable equilibrium. If the secondary state is merely a kinetic artifact or a rarely visited intermediate, the bistability claim collapses. The distinction between a true equilibrium and a metastable state is fundamental to the paper's thesis.
- **Resolution test** Provide free energy calculations (e.g., well-tempered metadynamics or umbrella sampling along a suitable reaction coordinate) that demonstrate two distinct minima separated by a finite barrier. Alternatively, show that individual trajectories transition between primary and secondary states multiple times, demonstrating reversibility.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The authors claim that the S189A mutation shifts the equilibrium toward the secondary state, and that this is consistent with reduced binding affinity measured by FP.
- **Evidence pointer** Results section "S189A mutation shifts the MBD2-mCpG complex toward the secondary state conformation"; Fig 5A-B; Fig 5D-E
- **Concern** The link between the MD simulations of the S189A mutant and the experimental FP measurements is not quantitatively established. The authors report a 10-fold reduction in binding affinity for S189A, but do not demonstrate that this reduction is specifically due to a shift toward the secondary state. Other factors, such as changes in the on-rate or off-rate due to loss of a single hydrogen bond, could equally explain the affinity reduction. The MD simulations show that S189A adopts a secondary-state-like conformation, but this does not prove that the secondary state is the cause of reduced affinity. A more direct test would be to measure the binding affinity of a mutant that stabilizes the primary state or to perform free energy perturbation calculations.
- **Why it matters** The paper's conclusion that S189 acts as a "macro-switch" controlling the equilibrium between two states requires that the experimental affinity reduction be mechanistically linked to the conformational shift. Without this link, the functional significance of the bistable equilibrium remains speculative.
- **Resolution test** Perform free energy calculations (e.g., FEP or TI) to compute the binding free energy difference between WT and S189A and compare with the experimental value. Alternatively, design a mutant that stabilizes the primary state and show that it has higher affinity than WT.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Scientific importance
- **Claim pointer** The authors suggest that "such alternative bound-state equilibria may represent an inherent feature of specific protein-DNA complexes" (Abstract) and that bistable binding "may be a fundamental feature of sequence-specific protein-DNA recognition" (Conclusions).
- **Evidence pointer** Abstract; Conclusions
- **Concern** This generalization is based on a single example (MBD2) and one prior report (Liu et al. on WRKY). While the authors acknowledge this is speculative, the statement in the abstract and conclusions is presented with more confidence than the evidence warrants. The WRKY study involved a different type of DNA-binding domain and the connection to MBD2 is not mechanistically established. The authors should either provide additional evidence for the generality of bistable binding or temper these claims.
- **Why it matters** The broader significance of the work, and its appeal to a wide readership, depends on the generality of the bistable equilibrium concept. Overstating the generality could mislead readers and reduce the credibility of the specific MBD2 findings.
- **Resolution test** Either provide additional examples (e.g., from published MD studies of other DNA-binding proteins) or revise the language to clearly indicate that this is a hypothesis requiring further testing.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The authors use the S189A mutation to validate the role of S189 as a macro-switch, and state that NMR confirms the mutation does not alter mCpG selectivity.
- **Evidence pointer** Results section "S189A mutation retains MBD2 selectivity for mCpG but reduces binding affinity"; Fig 5C
- **Concern** The NMR experiment is described as a 15N HSQC experiment, but the manuscript does not provide details on how the chemical shift changes were quantified or how the conclusion of "unchanged selectivity" was reached. The three cross-peaks (G169, R166, A172) are described as reflecting mCpG-specific binding, but the manuscript does not show the actual spectra or provide quantitative chemical shift perturbation data. Without this information, the claim that S189A does not alter selectivity is not fully supported.
- **Why it matters** The NMR data is a key experimental validation of the computational predictions. If the NMR data are not presented in sufficient detail, the experimental support for the paper's central claims is weakened.
- **Resolution test** Provide the full HSQC spectra (or at least the relevant regions) in the supplementary material, along with quantitative chemical shift perturbation values for the key residues. Show a direct comparison between WT and S189A spectra.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Readability for nonspecialists
- **Affected element** Introduction, first paragraph
- **Evidence pointer** Introduction
- **Issue** The introduction assumes significant prior knowledge of the MBD family and epigenetic regulation. A brief explanation of why MBD2 is biologically important and how it differs from other MBD proteins would help nonspecialist readers.
- **Required correction** Add 2-3 sentences in the introduction providing context on the biological role of MBD2 and the significance of mCpG recognition.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Methods, MD simulation protocol
- **Evidence pointer** Materials and methods, "Molecular dynamics simulation"
- **Issue** The manuscript states that the AMBER14SB and AMBER parmbsc1 force fields were used, and that a "combined protocol suggested by Liebl et al." was used for 5mC. However, the specific parameters for 5mC are not described in detail. This is important because the accuracy of the 5mC parameters directly affects the validity of the simulations.
- **Required correction** Provide a more detailed description of the 5mC parameters, including the source of the partial charges and any modifications to the standard AMBER parameters. If the Liebl et al. protocol involves specific modifications, these should be clearly stated.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Methods, Umbrella sampling
- **Evidence pointer** Materials and methods, "Umbrella sampling"
- **Issue** The manuscript states that 35 umbrella sampling windows were used, each simulated for 80 ns, and that the first 30 ns were discarded as equilibration. However, the convergence of the free energy profiles is only shown in the supplementary material (Fig S28). The main text should provide at least a brief statement about convergence.
- **Required correction** Add a sentence in the Results or Methods section stating that the free energy profiles converged within the simulation time, referencing Fig S28.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Scientific importance
- **Affected element** Discussion, paragraph on bistable binding
- **Evidence pointer** Discussion
- **Issue** The discussion of the potential functional implications of bistable binding (e.g., exchange between mCpG sites, assembly of the NuRD complex) is interesting but somewhat speculative. The authors should more clearly distinguish between what is directly supported by their data and what is hypothesis.
- **Required correction** Add qualifying language such as "we speculate" or "it is plausible that" when discussing functional implications that go beyond the direct simulation and experimental results.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Readability for nonspecialists
- **Affected element** Results, "The secondary state adopts a distinct complex conformation"
- **Evidence pointer** Results section
- **Issue** The description of the structural differences between primary and secondary states is dense and may be difficult for nonspecialists to follow. A schematic figure or a more accessible description of the key conformational changes would be helpful.
- **Required correction** Consider adding a schematic figure (or simplifying the existing Fig 3) that clearly illustrates the key differences between the primary and secondary states, particularly the position of the head domain and the S189-mC interaction.

### Technical failings that need to be addressed before the case is established
- R1-M1: Lack of evidence for thermodynamic stability of the secondary state (reversibility, free energy profile)
- R1-M2: Lack of quantitative link between S189A-induced conformational shift and reduced binding affinity
- R1-M4: Insufficient detail in NMR data presentation to support the claim of unchanged selectivity

## Risk / unsupported claims
- The claim that bistable binding is "an inherent feature of specific protein-DNA complexes" is not supported by the data presented, which only covers MBD2 and references one prior study on WRKY.
- The claim that the secondary state "retains comparable selectivity for mCpG" is based on MD simulations and the NMR data, but the NMR data are not presented in sufficient detail to fully evaluate this claim.
- The statement that the S189A mutation "shifts the equilibrium toward the secondary state" is supported by MD simulations, but the equilibrium shift is not quantified (e.g., no free energy difference between states is provided).
- The functional implications discussed in the Discussion (e.g., role in NuRD complex assembly, exchange between mCpG sites) are speculative and not directly tested in this work.

## Assessment against Nature-style criteria
- **Originality**: The concept of a bistable binding equilibrium in MBD2-mCpG recognition is novel and not previously reported for this system. The identification of S189 as a macro-switch is a specific and testable hypothesis. However, the broader concept of conformational heterogeneity in protein-DNA complexes is well established, and the originality lies primarily in the specific application to MBD2.
- **Scientific importance**: The work has the potential to be important for understanding how MBD2 balances high-affinity binding with dynamic behavior, which is relevant to its biological function in epigenetic regulation. The findings could inform future studies on MBD2-related diseases and on other MBD family members. However, the importance is somewhat limited by the lack of direct experimental validation of the bistable equilibrium concept beyond the S189A mutation.
- **Interdisciplinary readership**: The topic is of interest to structural biologists, computational biophysicists, and epigenetic researchers. The combination of MD simulations and experimental validation makes it accessible to both computational and experimental audiences. However, the dense structural descriptions may limit accessibility for nonspecialists.
- **Technical soundness**: The MD simulation protocol is generally sound, with appropriate force fields and simulation lengths. The use of multiple replicas is commendable. However, the lack of free energy calculations to support the bistability claim is a significant technical gap. The umbrella sampling calculations are described but the results are not fully integrated into the main text. The NMR and FP experiments are appropriate but the NMR data presentation is insufficient.
- **Readability for nonspecialists**: The manuscript is well-written but assumes significant background knowledge in both MD simulations and MBD biology. The abstract is clear, but the results section is dense and may be challenging for readers outside the immediate field.

## Recommendation posture
**Supportive if technical concerns are resolved.** The core finding of a bistable binding equilibrium in MBD2-mCpG recognition is interesting and potentially significant. However, the current evidence does not fully establish the thermodynamic stability of the secondary state, and the link between the S189A-induced conformational shift and reduced binding affinity is not quantitatively demonstrated. If the authors can provide free energy calculations demonstrating two distinct minima, show reversibility of state transitions, and present the NMR data in sufficient detail, the case would be substantially strengthened. The broader generalization to other protein-DNA complexes should be tempered unless additional evidence is provided.