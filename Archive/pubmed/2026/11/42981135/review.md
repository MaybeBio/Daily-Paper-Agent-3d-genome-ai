## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and conclusions as presented in the abstract; no methods, figures, tables, or supplementary material were available for evaluation
- **Shared manuscript claim summary** The authors combine pan-cancer histone mutation profiling with 31.5 microseconds of all-atom molecular dynamics simulations of complete nucleosomes to study recurrent mutations in H2A, H2B, H3, and H4 tails. They report mutation-specific redistribution of tail-DNA contacts, changes in MM/GBSA-derived relative interaction-energy estimates, and Markov state modeling results showing altered metastable tail-DNA contact states. They conclude that cancer-associated histone-tail mutations reshape conformational and interaction-state landscapes in nucleosomes.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or supplementary data provided
- **Missing materials affecting confidence** Full manuscript, methods description, simulation parameters, force field details, convergence criteria, statistical analyses, Markov state model validation, MM/GBSA calculation details, and all figures and tables

## Reviewer
- **Overall assessment** The abstract presents a potentially interesting computational study addressing an important gap in understanding how noncanonical histone-tail mutations affect nucleosome dynamics. The scale of simulation (31.5 microseconds total) is substantial and the combination of pan-cancer profiling with MD simulations is a reasonable strategy. However, the abstract alone provides insufficient detail to evaluate the technical soundness of the simulations, the statistical robustness of the conclusions, or the biological significance of the reported effects. Several claims are made without quantitative support, and the relationship between the identified mutations and cancer biology is not established beyond their occurrence in cancer datasets.
- **Who would be interested in the results, and why** Researchers in chromatin biology, epigenetics, and computational biophysics would be interested. Those studying oncohistones and cancer-associated chromatin dysregulation would value a broader view of tail mutations beyond canonical H3 sites. Computational biologists using MD simulations to study nucleosome dynamics would also find the methodological approach relevant.
- **Major strengths** The study addresses an understudied area by extending beyond canonical H3 oncohistones to include H2A, H2B, and H4 tail mutations. The simulation scale is substantial and appropriate for studying conformational ensembles. The combination of pan-cancer profiling with MD simulations provides a clinically motivated framework. The use of Markov state modeling to resolve metastable states adds methodological depth.
- **Major Concerns**  
  - R1-M1  
  - R1-M2  
  - R1-M3  
  - R1-M4
- **Minor Comments**  
  - R1-m1  
  - R1-m2  
  - R1-m3  
  - R1-m4
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3
- **Assessment against Nature-style criteria**  
  Originality: The focus on noncanonical tail mutations is a useful extension of existing oncohistone work, though the conceptual framework is not entirely novel.  
  Scientific importance: Potentially significant for understanding chromatin dysregulation in cancer, but the biological impact is not quantified in the abstract.  
  Interdisciplinary readership: The work bridges cancer genomics and biophysics, which could appeal to a broad audience if the findings are presented accessibly.  
  Technical soundness: Cannot be assessed from the abstract alone; simulation quality, convergence, and statistical rigor are not documented.  
  Readability for nonspecialists: The abstract is reasonably clear but uses specialized terminology without sufficient context for a general scientific audience.

- **Recommendation posture** Currently not established from the provided evidence. The abstract describes a plausible and potentially valuable study, but the technical and quantitative basis for the central claims cannot be evaluated without the full manuscript. Supportive if technical concerns are resolved.

### Major Concerns

- **Concern ID** R1-M1  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Technical soundness  
- **Claim pointer** The simulations reveal mutation-specific redistribution of tail-DNA contacts across the nucleosomal DNA surface, accompanied by changes in MM/GBSA-derived relative interaction-energy estimates.  
- **Evidence pointer** Location not provided  
- **Concern** The abstract reports qualitative outcomes from 31.5 microseconds of simulation but provides no information on simulation setup, force field selection, equilibration protocols, replica strategy, or convergence assessment. Without these details, the reliability of the conformational ensembles and contact redistributions cannot be judged.  
- **Why it matters** Molecular dynamics results are highly sensitive to force field parameters and sampling adequacy. Claims about mutation-induced changes in contact patterns and interaction energies require demonstrated convergence and appropriate error estimation to be credible.  
- **Resolution test** Provide full methods including force field version, water model, salt concentration, temperature coupling, simulation length per system, number of replicas, and convergence metrics such as block averaging or overlap of conformational distributions between independent runs.

- **Concern ID** R1-M2  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Statistical robustness  
- **Claim pointer** Markov state modeling further resolves metastable tail-DNA contact states and shows that mutations alter their structural characteristics and population distributions.  
- **Evidence pointer** Location not provided  
- **Concern** No information is given on how the Markov state models were constructed, validated, or used to compare populations across systems. The number of states, lag time selection, implied timescale tests, and uncertainty quantification are absent.  
- **Why it matters** Markov state models can produce artifacts if poorly constructed or overfitted. Claims about altered population distributions between mutant and wild-type systems require statistical comparison with confidence intervals, not just qualitative statements.  
- **Resolution test** Provide details on state definition, lag time selection, Chapman-Kolmogorov validation, and bootstrap or other uncertainty estimates for population differences between systems.

- **Concern ID** R1-M3  
- **Severity** Major  
- **Blocking** Yes  
- **Axis** Biological significance  
- **Claim pointer** We identify recurrent and understudied mutation sites beyond canonical H3 oncohistones and characterize how selected substitutions perturb histone-tail conformational ensembles and DNA contacts in their nucleosomal context.  
- **Evidence pointer** Location not provided  
- **Concern** The abstract does not specify which mutations were selected for simulation, how many systems were studied, or what criteria were used to select substitutions from the pan-cancer profiling. The relationship between the simulated mutations and cancer relevance is asserted but not demonstrated.  
- **Why it matters** Without a clear selection rationale and a defined set of mutations, the scope of the study is unclear. The claim that these mutations are cancer-associated requires evidence of recurrence frequency and functional relevance beyond their presence in tumor datasets.  
- **Resolution test** List the specific mutations simulated, their recurrence statistics in the pan-cancer data, and the criteria for selection. Provide evidence that the selected mutations are functionally implicated in cancer, such as association with patient outcomes or known chromatin phenotypes.

- **Concern ID** R1-M4  
- **Severity** Major  
- **Blocking** No  
- **Axis** Quantitative support  
- **Claim pointer** These perturbations are not confined to the substituted residues but extend to neighboring interaction networks.  
- **Evidence pointer** Location not provided  
- **Concern** The claim of extended perturbations to neighboring interaction networks is presented without quantitative measures. No metrics such as contact maps, correlation analyses, or energy decomposition are described to support this assertion.  
- **Why it matters** This claim is central to the physical picture the authors present, but without defined metrics and statistical comparisons, it remains an interpretation rather than a demonstrated result.  
- **Resolution test** Provide quantitative evidence such as residue-resolved contact difference maps, interaction energy decomposition per residue, or network analyses with statistical significance testing between mutant and wild-type systems.

### Minor Comments

- **Concern ID** R1-m1  
- **Severity** Minor  
- **Axis** Clarity  
- **Affected element** Abstract wording  
- **Evidence pointer** Location not provided  
- **Issue** The phrase "noncanonical mutations in intrinsically disordered histone tails" is used without defining what makes a mutation noncanonical in this context.  
- **Required correction** Clarify the definition of noncanonical mutations, for example by contrasting with well-studied H3K27M or H3G34R/V oncohistones.

- **Concern ID** R1-m2  
- **Severity** Minor  
- **Axis** Reproducibility  
- **Affected element** Simulation reporting  
- **Evidence pointer** Location not provided  
- **Issue** The abstract states 31.5 microseconds of total simulation but does not indicate how this is distributed across systems or whether this includes equilibration.  
- **Required correction** Specify the number of systems, simulation length per system, and whether the reported time refers to production runs only.

- **Concern ID** R1-m3  
- **Severity** Minor  
- **Axis** Terminology  
- **Affected element** MM/GBSA usage  
- **Evidence pointer** Location not provided  
- **Issue** The abstract refers to "MM/GBSA-derived relative interaction-energy estimates" but does not specify the reference state or whether these are per-residue or per-contact values.  
- **Required correction** Define the energy decomposition scheme and the reference state used for relative estimates.

- **Concern ID** R1-m4  
- **Severity** Minor  
- **Axis** Scope  
- **Affected element** Generalizability  
- **Evidence pointer** Location not provided  
- **Issue** The abstract does not state how many mutations were simulated or whether the findings are expected to generalize to other tail mutations not studied.  
- **Required correction** State the number of mutations simulated and discuss the expected generalizability or limitations of the selected set.

## Risk / unsupported claims
- The claim that identified mutations are "cancer-associated" is unsupported without recurrence statistics and functional evidence from the pan-cancer profiling.
- The claim that mutations "reshape conformational and interaction-state landscapes" is not quantitatively supported in the abstract.
- The claim that perturbations extend to neighboring interaction networks is asserted without defined metrics or statistical evidence.
- The biological significance of the observed changes in tail-DNA contacts and interaction energies is not established; no link to chromatin function or gene regulation is provided.
- The reliability of the simulation results cannot be assessed without methods details, making all simulation-based claims currently unevaluable.