## Review setup
- **Input scope** Abstract only
- **Assessment boundary** Claims and evidence presented in the abstract; no methods, figures, or supplementary material were provided
- **Shared manuscript claim summary** The authors present a simulation framework that uses region-capture micro-C contact maps to infer nucleosome-resolution conformational ensembles of megabase-scale chromatin regions. They report that euchromatin forms condensed domains with short active regions protruding from their surface, challenging the classical view of euchromatin as uniformly open.
- **Visible evidence base** Abstract text only; no figures, tables, methods, or supplementary information were provided
- **Missing materials affecting confidence** Full methods, all figures and tables, supplementary information, code availability, and any statistical details

## Reviewer
- **Overall assessment** The abstract presents a potentially interesting computational framework and a provocative biological claim that euchromatin is generally condensed with protruding active regions. However, the evidence base provided is insufficient to evaluate the technical soundness of the simulation framework, the validity of the micro-C balancing strategy, or the robustness of the structural inferences. The central claim departs from established views and would require substantial validation, none of which is visible in the supplied material.
- **Who would be interested in the results, and why** Researchers in chromatin structure, transcriptional regulation, and computational biology would be interested. The claim that euchromatin forms condensed domains with accessible protrusions could reshape models of enhancer-promoter communication and gene regulation. Methodologists developing integrative modeling approaches for chromosome conformation capture data would also find the framework relevant.
- **Major strengths** The abstract addresses a significant gap in the field, namely the nucleosome-resolution organization of regulatory elements. The integration of micro-C data with simulation to infer conformational ensembles is a sensible approach. The claim directly challenges a long-standing assumption and offers a testable structural model for enhancer-promoter communication.
- **Major Concerns** The abstract provides no quantitative evidence, no validation metrics, and no comparison with alternative models. The central claim is stated without supporting data. The relationship between the simulation framework and the imaging-based observations is asserted but not demonstrated. The biological implications are speculative in the absence of functional validation.
- **Minor Comments** The abstract would benefit from clarifying the scale and resolution of the inferred structures. The term "short active regions" is vague and should be defined. The relationship between the micro-C balancing strategy and the final structural inference is unclear from the abstract alone.
- **Technical failings that need to be addressed before the case is established** R1-M1, R1-M2, R1-M3, R1-M4
- **Assessment against Nature-style criteria** Originality is potentially high, as the claim of condensed euchromatin with protruding active regions departs from the classical view. Scientific importance is potentially substantial for the chromatin field. Interdisciplinary readership could be broad, spanning genomics, biophysics, and cell biology. Technical soundness cannot be assessed from the abstract alone. Readability for nonspecialists is adequate, though some terms require definition.
- **Recommendation posture** Currently not established from the provided evidence. The abstract presents an interesting hypothesis, but the evidence base is insufficient to support the central claims.

### Major Concerns

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The simulation framework leverages region-capture micro-C contact maps to infer conformational ensembles of megabase-scale regions at nucleosome resolution.
- **Evidence pointer** Abstract only; location not provided
- **Concern** The abstract provides no details on the simulation methodology, the model parameters, the validation of the inferred ensembles, or the uncertainty quantification. No convergence criteria, error estimates, or comparison with independent data are described.
- **Why it matters** Without evidence that the inferred ensembles are accurate and reproducible, the structural claims derived from them cannot be trusted. The field has seen multiple examples of chromatin structure inference methods producing artifacts due to insufficient validation.
- **Resolution test** Provide a detailed methods section with validation against independent experimental data, such as chromatin tracing or imaging, with quantitative agreement metrics. Show that the inferred ensembles are robust to parameter choices and initial conditions.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** A key component of this framework is a micro-C balancing strategy that identifies variation in contact density.
- **Evidence pointer** Abstract only; location not provided
- **Concern** The balancing strategy is described as a key component, but no details are given on how it works, what assumptions it makes, or how it affects the inferred structures. The term "identifies variation in contact density" is vague and could mean many different things.
- **Why it matters** If the balancing strategy introduces biases or artifacts, the resulting structures could be incorrect. The validity of the entire framework depends on this step being sound and well-justified.
- **Resolution test** Provide a full description of the balancing strategy, including mathematical formulation, assumptions, and sensitivity analyses. Demonstrate that the strategy does not introduce spurious structural features.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence strength
- **Claim pointer** The simulations reproduce pairwise distance distributions measured by chromatin tracing and contain packing domains and nucleosome clutches, as observed in imaging studies.
- **Evidence pointer** Abstract only; location not provided
- **Concern** The abstract claims agreement with chromatin tracing and imaging data, but no quantitative comparison is shown. No correlation coefficients, error bars, or statistical tests are reported. The claim of reproducing "packing domains and nucleosome clutches" is qualitative and could be subjective.
- **Why it matters** Agreement with independent experimental data is the primary validation for the simulation framework. Without quantitative evidence, the claim of reproducibility is unsubstantiated.
- **Resolution test** Provide quantitative comparisons with chromatin tracing data, including statistical measures of agreement. Show representative images or structural features that demonstrate the presence of packing domains and nucleosome clutches, with clear criteria for their identification.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence strength
- **Claim pointer** Euchromatin generally forms condensed domains with comparable densities but smaller sizes than heterochromatin domains. Kilobase-scale regions at promoters and enhancers often protrude from these condensed domains and become highly accessible.
- **Evidence pointer** Abstract only; location not provided
- **Concern** This is the central biological claim of the manuscript, yet no quantitative data are presented. No measurements of domain sizes, densities, or protrusion frequencies are shown. No statistical comparisons between euchromatin and heterochromatin are provided. The claim that active regions "often protrude" is vague and lacks a defined frequency or criterion.
- **Why it matters** This claim directly challenges the classical view of euchromatin as uniformly open. Such a departure requires strong quantitative evidence across multiple cell types and genomic regions. Without this evidence, the claim remains speculative.
- **Resolution test** Provide quantitative measurements of domain sizes and densities for euchromatin and heterochromatin, with statistical comparisons. Show the frequency and extent of protrusions at promoters and enhancers, with clear definitions and criteria. Ideally, demonstrate the generality of the finding across multiple cell types and genomic contexts.

### Minor Comments

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract terminology
- **Evidence pointer** Abstract; location not provided
- **Issue** The term "short active regions" is vague and could be interpreted in multiple ways. It is unclear whether "short" refers to genomic length, physical size, or temporal activity.
- **Required correction** Define the term explicitly, for example by specifying the genomic length range and the criteria for "active" (e.g., presence of active histone marks, transcription factor binding, or transcriptional activity).

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract terminology
- **Evidence pointer** Abstract; location not provided
- **Issue** The phrase "compartmentalizes regulatory elements from the surrounding chromatin" is ambiguous. It is unclear whether this refers to physical separation, biochemical insulation, or functional isolation.
- **Required correction** Clarify the intended meaning of "compartmentalizes" and provide a more precise description of the proposed mechanism.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Scope
- **Affected element** Abstract claims
- **Evidence pointer** Abstract; location not provided
- **Issue** The abstract claims that the arrangement "facilitates protein binding and enhancer-promoter communication," but no functional data are presented to support this claim.
- **Required correction** Either provide functional validation (e.g., perturbation experiments) or soften the claim to reflect that this is a proposed implication of the structural findings.

## Risk / unsupported claims
- The claim that euchromatin generally forms condensed domains with comparable densities but smaller sizes than heterochromatin domains is unsupported by the provided evidence.
- The claim that kilobase-scale regions at promoters and enhancers often protrude from condensed domains and become highly accessible is unsupported by the provided evidence.
- The claim that the arrangement facilitates protein binding and enhancer-promoter communication is speculative and unsupported by functional data.
- The claim that the simulations reproduce pairwise distance distributions measured by chromatin tracing is unverifiable without quantitative comparisons.
- The claim that the inferred structures contain packing domains and nucleosome clutches as observed in imaging studies is unverifiable without representative images or quantitative criteria.