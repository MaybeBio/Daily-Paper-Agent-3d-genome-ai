## Review setup
- **Input scope** Full manuscript (Perspective/Review article)
- **Assessment boundary** Conceptual framework, logical coherence, evidence synthesis, and claims as presented in the manuscript
- **Shared manuscript claim summary** The authors propose "geometric mechanogenomics" as a conceptual framework in which geometric boundary conditions (confinement, curvature, anisotropy, multicellular architecture) act as upstream spatial regulators that organize conserved mechanotransductive machinery, transmit forces through a boundary-to-nucleus axis, and ultimately regulate chromatin organization, epigenetic remodeling, and transcriptional programs to enable deterministic cell fate control.
- **Visible evidence base** Literature citations (approximately 40 references), conceptual figures (Figure 1 referenced but not provided), Table 1 (comparing geometry vs. matrix stiffness), and textual argumentation
- **Missing materials affecting confidence** Figure 1 (conceptual framework illustration) is not provided; no original experimental data; no quantitative model or computational framework; no systematic literature search methodology described

## Reviewer
- **Overall assessment** This manuscript presents a conceptually ambitious and well-written perspective that attempts to integrate geometric boundary conditions, mechanotransduction, and genome regulation into a unified framework termed "geometric mechanogenomics." The authors make a clear distinction between geometric cues and bulk matrix mechanics, and they articulate a hierarchical boundary-to-nucleus axis. However, the manuscript is almost entirely conceptual and synthetic, lacking original data, quantitative models, or testable predictions. The framework, while plausible, remains largely descriptive and does not establish causal relationships or provide a roadmap for falsification. The claims about "deterministic" control and "predictive engineering" are not supported by the evidence presented, which consists of cited literature rather than demonstrated principles. The manuscript would benefit from a more critical discussion of limitations, alternative interpretations, and specific experimental or computational approaches to validate the framework.

- **Who would be interested in the results, and why** Researchers in mechanobiology, bioengineering, regenerative medicine, and developmental biology would find this framework of interest because it proposes a hierarchical integration of geometric cues with nuclear and genomic regulation, potentially offering new design principles for tissue engineering and organoid systems. The conceptual distinction between geometry and matrix stiffness may also interest the broader mechanotransduction community.

- **Major strengths**
  1. Clear conceptual distinction between geometric boundary conditions and bulk matrix mechanics (Table 1), which addresses a common conflation in the literature.
  2. Well-articulated hierarchical framework (boundary-to-nucleus axis) that connects tissue-scale geometry to nuclear mechanoregulation through conserved mechanotransductive machinery.
  3. Integration of literature from bioengineering, mechanobiology, and genome regulation into a coherent narrative, with appropriate citations to key studies.
  4. Recognition of the gap between engineered geometric platforms and genome-scale readouts, and identification of the need for multi-scale integrated approaches.

- **Major Concerns**
  - **Concern ID** R1-M1
  - **Severity** Major
  - **Blocking** Yes
  - **Axis** Claim-evidence mismatch
  - **Claim pointer** "Geometric mechanogenomics provides a conceptual foundation for the predictive engineering of cell fate through programmable physical boundary conditions" (Abstract, Introduction, Discussion)
  - **Evidence pointer** Entire manuscript
  - **Concern** The manuscript repeatedly claims that geometric boundary conditions enable "deterministic" and "predictive" control of cell fate, yet no quantitative, predictive model is presented, and no experimental data demonstrate that geometric inputs alone can deterministically specify cell fate. The cited literature shows correlations and improvements in reproducibility, not deterministic control. The framework remains descriptive and post-hoc.
  - **Why it matters** The central claim of the manuscript—that geometry can serve as a programmable, predictive regulator of genome function and cell fate—is not substantiated. Without a quantitative framework or causal evidence, the term "deterministic" is misleading and overstates the current state of the field.
  - **Resolution test** Provide a quantitative model (e.g., computational or mathematical) that predicts genome-scale outputs (e.g., chromatin accessibility, gene expression) from defined geometric parameters, or clearly delineate the current limitations and reframe claims as aspirational rather than established.

  - **Concern ID** R1-M2
  - **Severity** Major
  - **Blocking** No
  - **Axis** Falsifiability and testability
  - **Claim pointer** "Geometric mechanogenomics... establishes a conceptual foundation for the predictive engineering of cell fate" (Introduction, Discussion)
  - **Evidence pointer** Entire manuscript
  - **Concern** The framework, as presented, lacks specific, testable hypotheses or predictions that would allow it to be falsified or validated. The authors describe a hierarchical cascade (geometry → adhesion → cytoskeleton → nucleus → genome) but do not specify which geometric parameters (e.g., curvature radius, confinement aspect ratio, adhesive pattern) are predicted to produce which specific mechanogenomic outcomes. The framework is therefore difficult to distinguish from a general description of mechanotransduction.
  - **Why it matters** A conceptual framework in a Nature-style journal should generate testable predictions that advance the field. Without such predictions, the manuscript reads as a review rather than a novel framework.
  - **Resolution test** Articulate at least 2-3 specific, quantitative predictions (e.g., "Confinement with aspect ratio >3 will increase H3K9me3 at LADs by X% compared to isotropic confinement") that could be experimentally tested, and describe the experimental design to test them.

  - **Concern ID** R1-M3
  - **Severity** Major
  - **Blocking** No
  - **Axis** Novelty and differentiation
  - **Claim pointer** "We introduce geometric mechanogenomics, a conceptual framework that positions geometry as an upstream spatial regulator" (Abstract, Introduction)
  - **Evidence pointer** Introduction, Section "Geometric mechanogenomics: genome reconfiguration through boundary constraints"
  - **Concern** The concept that geometry influences cell fate through mechanotransduction and nuclear regulation is not new. Seminal studies (McBeath et al., 2004; Théry et al., 2006; Dupont et al., 2011; Jain et al., 2013; Swift et al., 2013) have already established that cell shape, adhesive geometry, and confinement regulate YAP/TAZ, nuclear deformation, and chromatin organization. The authors acknowledge these studies but do not clearly articulate what "geometric mechanogenomics" adds beyond a re-labeling of existing knowledge. The claim that geometry "spatially organizes conserved mechanotransductive machinery" is a restatement of known principles.
  - **Why it matters** For a new framework to be impactful, it must offer conceptual or predictive advances beyond existing paradigms. The manuscript does not convincingly demonstrate that "geometric mechanogenomics" provides new insights or enables new capabilities not already implicit in the mechanobiology literature.
  - **Resolution test** Explicitly state what specific predictions, experimental approaches, or engineering capabilities are uniquely enabled by the geometric mechanogenomics framework that are not already possible with existing mechanobiology concepts. Provide a comparison table or figure contrasting the framework with existing paradigms.

  - **Concern ID** R1-M4
  - **Severity** Major
  - **Blocking** No
  - **Axis** Evidence for causal chain
  - **Claim pointer** "Geometric boundary conditions... reorganize nuclear architecture, chromatin accessibility, epigenetic states, and transcriptional programs" (Abstract, Section "Geometric mechanogenomics")
  - **Evidence pointer** Section "Geometric mechanogenomics: genome reconfiguration through boundary constraints"
  - **Concern** The manuscript asserts a causal chain from geometry to genome regulation, but the cited evidence primarily demonstrates correlations or effects of mechanical force on nuclear organization, not direct causal links from specific geometric parameters to specific genomic changes. For example, studies on nuclear deformation (Lomakin et al., 2020; Nava et al., 2020) use confinement or stretching, but the geometric parameters are not systematically varied to establish geometry-specific effects. The claim that geometry "reorganizes" chromatin is supported by limited evidence, and the mechanistic steps (e.g., how curvature specifically alters LADs) are not established.
  - **Why it matters** The core premise of the framework—that geometry is a causal, upstream regulator of genome function—requires direct evidence of geometry-to-genome causality, not just force-to-genome correlations. Without this, the framework remains speculative.
  - **Resolution test** Provide a systematic review of studies that directly manipulate geometric parameters (e.g., curvature, confinement aspect ratio) and measure genome-scale outputs (e.g., Hi-C, ATAC-seq, RNA-seq) in a controlled manner, or acknowledge the current lack of such evidence and reframe the framework as a hypothesis to be tested.

- **Minor Comments**
  - **Concern ID** R1-m1
  - **Severity** Minor
  - **Axis** Clarity and precision
  - **Affected element** Terminology
  - **Evidence pointer** Abstract, Introduction
  - **Issue** The term "mechanogenomics" is used without clear definition. The authors state that mechanogenomics has "revealed that mechanical forces regulate... chromatin organization" but do not define the term or distinguish it from "mechanotransduction" or "mechanoepigenetics." The new term "geometric mechanogenomics" is then introduced without a clear operational definition.
  - **Required correction** Define "mechanogenomics" explicitly (e.g., "the study of how mechanical forces regulate genome structure and function") and then define "geometric mechanogenomics" as a subfield or specific framework. Ensure the terms are used consistently throughout.

  - **Concern ID** R1-m2
  - **Severity** Minor
  - **Axis** Overstatement
  - **Affected element** Claims about "deterministic" control
  - **Evidence pointer** Abstract, Discussion
  - **Issue** The manuscript uses "deterministic" to describe cell fate control through geometry, but the cited studies show improved reproducibility, not determinism. Stochasticity is inherent in biological systems, and no evidence is presented that geometry eliminates it.
  - **Required correction** Replace "deterministic" with "more reproducible" or "biased toward specific outcomes" throughout the manuscript, or provide a clear definition of what "deterministic" means in this context (e.g., "predictable with >90% efficiency").

  - **Concern ID** R1-m3
  - **Severity** Minor
  - **Axis** Missing critical discussion
  - **Affected element** Limitations and alternative interpretations
  - **Evidence pointer** Discussion
  - **Issue** The manuscript does not discuss alternative interpretations of the cited studies. For example, geometric effects on cell fate could be mediated by differential diffusion of soluble factors, cell-cell signaling, or metabolic changes, not solely by mechanotransduction. The framework assumes a purely mechanical interpretation without considering non-mechanical consequences of geometry.
  - **Required correction** Add a paragraph discussing non-mechanical mechanisms by which geometry could influence cell fate (e.g., diffusion constraints, paracrine signaling, metabolic gradients) and explain how the geometric mechanogenomics framework can be distinguished from these alternatives.

  - **Concern ID** R1-m4
  - **Severity** Minor
  - **Axis** Readability for nonspecialists
  - **Affected element** Introduction and framework description
  - **Evidence pointer** Section "Geometric control of cell fate: a multi-scale framework"
  - **Issue** The manuscript uses specialized terminology (e.g., "LINC complex," "lamina-associated domains," "mechanogenomic layer") without sufficient explanation for readers outside mechanobiology. The hierarchical framework is described in prose but would benefit from a clear schematic or table summarizing the levels and key components.
  - **Required correction** Provide a glossary or brief explanations of key terms upon first use. Consider adding a summary table or figure (beyond Figure 1) that lists each level of the boundary-to-nucleus axis, the key molecular players, and the predicted outcomes.

  - **Concern ID** R1-m5
  - **Severity** Minor
  - **Axis** Missing methodology
  - **Affected element** Literature review approach
  - **Evidence pointer** Entire manuscript
  - **Issue** The manuscript is presented as a perspective but does not describe the methodology for literature selection (e.g., search terms, databases, inclusion/exclusion criteria). This makes it difficult to assess whether the evidence base is comprehensive or biased.
  - **Required correction** Add a brief statement in the Methods or a footnote describing how the literature was selected, or explicitly state that this is a conceptual perspective rather than a systematic review.

- **Technical failings that need to be addressed before the case is established** R1-M1 (lack of predictive model or causal evidence for deterministic control), R1-M2 (lack of testable hypotheses), R1-M4 (lack of direct geometry-to-genome causal evidence)

- **Assessment against Nature-style criteria**
  - **Originality**: Moderate. The framework re-labels and integrates existing concepts (geometry → mechanotransduction → nuclear regulation) but does not introduce fundamentally new mechanisms or principles. The term "geometric mechanogenomics" is new, but the underlying ideas are largely derivative of established mechanobiology literature.
  - **Scientific importance**: Moderate to high. If validated, the framework could provide design principles for tissue engineering and organoid systems. However, the current manuscript does not provide the evidence or predictive power needed to establish its importance.
  - **Interdisciplinary readership**: High. The manuscript bridges bioengineering, mechanobiology, developmental biology, and genomics, and is written in a style accessible to researchers across these fields (with minor clarifications needed).
  - **Technical soundness**: Low to moderate. The manuscript is conceptually coherent but lacks original data, quantitative models, or testable predictions. The claims are not supported by the evidence presented, which consists of cited literature rather than demonstrated principles.
  - **Readability for nonspecialists**: Moderate. The prose is clear, but specialized terminology is used without sufficient explanation. A glossary or summary table would improve accessibility.

- **Recommendation posture** Currently not established from the provided evidence. The manuscript presents a plausible conceptual framework but does not provide the predictive models, testable hypotheses, or causal evidence required to support its central claims of deterministic and predictive cell fate control. Major revisions are needed to reframe the claims as aspirational, articulate testable predictions, and address the novelty and evidence gaps. The manuscript may be more suitable for a review or perspective journal rather than a primary research journal.