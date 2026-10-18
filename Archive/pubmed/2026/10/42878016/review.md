## Review setup
- **Input scope** Full manuscript text including abstract, main text, and references cited within the text.
- **Assessment boundary** Scientific content, technical soundness, and clarity of the review article. Editorial and formatting aspects are not assessed.
- **Shared manuscript claim summary** The manuscript reviews recent advances in coarse-grained (CG) simulations of nucleic acid condensation, arguing that base-mediated interactions are dominant drivers in homotypic nucleic acid condensation and that simulation resolution fundamentally determines which physical phenomena are accessible. It surveys models across resolutions, highlights applications to complex nucleic acid systems, and identifies gaps and future directions.
- **Visible evidence base** Full text of the manuscript, including abstract, introduction, sections on atomistic insights, CG models (SIS/TIS, iConRNA), emerging applications (G-quadruplex, nanostars), heterotypic systems, and concluding outlook. Figures and tables are referenced but not provided.
- **Missing materials affecting confidence** Figures (Figure 1, 2, 3) and Table 1 are referenced but not included. Specific numerical data, simulation parameters, and quantitative comparisons are not fully detailed in the text. Reference list is not provided in full.

## Reviewer
- **Overall assessment** This is a well-structured and timely review that addresses an important and rapidly evolving area at the interface of computational biophysics and cell biology. The manuscript provides a clear organizational framework based on model resolution, which is useful for readers. The central thesis, that base-mediated interactions dominate homotypic nucleic acid condensation and that resolution determines accessible physics, is coherent and supported by the examples discussed. However, the review would benefit from a more critical and quantitative comparison of model performance, a clearer articulation of validation standards, and a more balanced discussion of limitations. The absence of figures and Table 1 in the provided material limits full assessment of the presented evidence.

- **Who would be interested in the results, and why** Computational biophysicists and physical chemists developing or applying CG models for nucleic acids; experimental biologists studying biomolecular condensates, particularly those involving RNA; researchers in the fields of phase separation, gene regulation, and neurodegeneration where nucleic acid condensation is implicated; and synthetic biologists interested in programmable nucleic acid nanostructures.

- **Major strengths** The review fills a niche by focusing specifically on CG simulations of nucleic acid condensation, a topic that is often treated as a subsection within broader reviews of biomolecular condensates. The organization by model resolution is logical and helps readers navigate a complex field. The discussion of SIS and iConRNA in detail provides concrete examples of how different modeling choices affect outcomes. The identification of key gaps, such as the need for better protein–nucleic acid interaction parameters and the challenge of capturing temperature-dependent effects in implicit-solvent models, is valuable and forward-looking.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The manuscript states that "base-mediated interactions emerge as dominant drivers in homotypic nucleic acid condensation" and that this is a key theme across the reviewed models.
- **Evidence pointer** Sections "CG models for nucleic acid phase separation", "Single-site and triple-site interaction models (SIS/TIS)", "Intermediate resolution model for condensates of RNAs (iConRNA)"
- **Concern** The claim that base-mediated interactions are the dominant driver is primarily supported by two models (SIS and iConRNA). The SIS model does not include electrostatics at all, and iConRNA uses a scaling factor for Mg2+ interactions that is calibrated to experimental data. The review does not critically discuss whether this dominance is an artifact of model construction or a genuine physical feature. For example, in SIS, the absence of electrostatics means base pairing is the only attractive interaction, which could bias the conclusion. The review would be strengthened by a more nuanced discussion of how model construction choices might influence the apparent dominance of base-mediated interactions.
- **Why it matters** The central thesis of the review rests on this claim. If the dominance of base-mediated interactions is partly a consequence of model design rather than a universal physical principle, the review's main message could be misleading for readers who are not experts in CG modeling.
- **Resolution test** The authors should either (a) provide a more critical analysis of how the absence or simplification of electrostatic interactions in different models affects the conclusion, or (b) present evidence from models that include both electrostatics and base interactions at comparable resolution to show that base interactions still dominate. A comparative table of model features and their predicted dominant interactions would be helpful.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** No
- **Axis** Scientific importance
- **Claim pointer** The manuscript states that "simulation resolution fundamentally determines which physical phenomena are accessible and observable."
- **Evidence pointer** Sections "CG models for nucleic acid phase separation", "Emerging application of CG models to phase separation of complex nucleic acids"
- **Concern** While this statement is broadly true, the review does not systematically analyze how resolution choices map to specific physical phenomena. For example, the discussion of one-bead models notes their limitation in capturing base stacking, but the review does not provide a clear framework for readers to understand which phenomena require which resolution. A more explicit mapping, perhaps in a table or figure, would strengthen the review's utility.
- **Why it matters** The review aims to guide readers in choosing appropriate models. Without a clear articulation of the resolution–phenomenon relationship, readers may struggle to apply the insights to their own systems.
- **Resolution test** The authors should provide a more explicit and systematic discussion of the relationship between model resolution and accessible physical phenomena, potentially in the form of a summary table or figure that maps resolution levels to specific observable properties (e.g., phase boundaries, internal structure, dynamics, ion effects).

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The manuscript states that iConRNA "accurately recapitulate[s] the nontrivial dependence of CAG repeat phase separation on sequence length, ionic strength, temperature, Mg2+, and RNA concentrations" and that this "is a major achievement that has not been demonstrated by other CG or atomistic models to date."
- **Evidence pointer** Section "Intermediate resolution model for condensates of RNAs (iConRNA)"
- **Concern** This is a strong claim that would benefit from more detailed evidence. The text does not provide quantitative comparisons between iConRNA predictions and experimental data. Without figures or tables showing the agreement, the claim is difficult to evaluate. Additionally, the statement "not been demonstrated by other CG or atomistic models to date" is a strong negative claim that would require a comprehensive literature search to support.
- **Why it matters** The review's credibility depends on the accuracy of its claims about model performance. Overstating the achievements of a particular model could mislead readers.
- **Resolution test** The authors should provide quantitative comparisons (e.g., phase boundary coordinates, critical concentrations) between iConRNA predictions and experimental measurements, and temper the claim about uniqueness unless a thorough literature comparison is provided.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Interdisciplinary readership
- **Claim pointer** The manuscript aims to be accessible to a broad audience, including experimentalists, as implied by the abstract and introduction.
- **Evidence pointer** Throughout the manuscript, particularly in sections describing model details
- **Concern** The manuscript uses technical jargon without sufficient explanation for non-specialists. Terms such as "Debye–Hückel approximation," "reference interaction site model (RISM)," "stickers-and-spacers," and "Wang–Frenkel nonbonded interactions" are introduced without adequate context. While the intended audience may include computational biophysicists, the review's stated scope includes experimental biologists who study condensates. The manuscript would benefit from a glossary or more careful introduction of technical terms.
- **Why it matters** The review aims to bridge computational and experimental communities. If experimentalists cannot fully understand the model descriptions, the review's impact will be limited.
- **Resolution test** The authors should either add a glossary of technical terms or expand the explanations of key concepts to make the manuscript more accessible to non-specialists.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract
- **Evidence pointer** Abstract, first sentence
- **Issue** The abstract begins with a general statement about biomolecular condensates that is not specific to nucleic acids. This is acceptable, but the abstract could more quickly focus on the nucleic acid-specific aspects that are the subject of the review.
- **Required correction** Consider revising the first sentence to more directly introduce the nucleic acid focus, e.g., "Nucleic acid condensation, a key driver of biomolecular condensate formation and function, is increasingly studied using coarse-grained simulations..."

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Section "CG models for protein–nucleic acid heterotypic phase transitions"
- **Evidence pointer** Section "CG models for protein–nucleic acid heterotypic phase transitions", subsection "Minimal models and patchy particles"
- **Issue** The discussion of minimal models is brief and does not mention specific recent studies beyond general statements. Given the breadth of this area, a few more specific examples would strengthen the review.
- **Required correction** Add 1-2 specific examples of recent minimal-model studies of protein–nucleic acid systems, with brief descriptions of their key findings.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Section "Emerging application of CG models to phase separation of complex nucleic acids", subsection "G-quadruplex"
- **Evidence pointer** Section "G-quadruplex"
- **Issue** The text states that the Martini 3 model "can capture the spontaneous quadruplex folding without relying on an elastic network." This is an important technical achievement, but the text does not provide details on how this was validated or what the limitations are.
- **Required correction** Add a sentence or two describing the validation approach and any known limitations of the Martini 3 model for G-quadruplex simulations.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Section "Concluding discussion and outlook"
- **Evidence pointer** Section "Concluding discussion and outlook", first paragraph
- **Issue** The concluding paragraph lists several future directions but does not prioritize them or provide a clear sense of which are most urgent or feasible.
- **Required correction** Consider adding a sentence that prioritizes the most pressing challenges or opportunities, e.g., "Among these, the development of transferable protein–nucleic acid interaction parameters is arguably the most urgent need."

- **Technical failings that need to be addressed before the case is established** No fundamental technical failings identified. The main issues are the lack of quantitative evidence for some strong claims (R1-M3) and the need for a more critical analysis of the central thesis (R1-M1). These are matters of presentation and depth rather than technical errors.

- **Assessment against Nature-style criteria**
  - **Originality** The review addresses a specific and timely topic that is not covered in depth by existing reviews. The focus on CG simulations of nucleic acid condensation, as opposed to protein condensation or nucleic acid structure prediction, provides a distinct angle. The organization by model resolution is a useful framework. However, the review does not introduce fundamentally new concepts or perspectives; it synthesizes existing work.
  - **Scientific importance** The topic is of high importance given the growing recognition of nucleic acid condensation in gene regulation, stress response, and disease. The review identifies key gaps and future directions, which is valuable for the field. However, the impact would be enhanced by a more critical and quantitative assessment of model capabilities.
  - **Interdisciplinary readership** The review has the potential to appeal to both computational and experimental researchers. However, the technical detail may be challenging for experimentalists without a computational background. The review would benefit from improved accessibility.
  - **Technical soundness** The technical content appears sound based on the text provided. The descriptions of the models are accurate, and the discussion of limitations is generally appropriate. However, the lack of figures and Table 1 limits full verification. The strong claims about iConRNA's performance (R1-M3) require more evidence.
  - **Readability for nonspecialists** The manuscript is generally well-written and logically organized. However, the use of technical jargon without adequate explanation (R1-M4) reduces readability for non-specialists. The abstract and introduction are accessible, but the main text becomes more technical.

- **Recommendation posture** Supportive if technical concerns are resolved. The review addresses an important topic and provides a useful synthesis of recent work. The main issues are the need for more quantitative evidence for key claims, a more critical analysis of the central thesis, and improved accessibility for non-specialists. These are addressable through revision.

## Risk / unsupported claims
- The claim that iConRNA "accurately recapitulate[s] the nontrivial dependence of CAG repeat phase separation on sequence length, ionic strength, temperature, Mg2+, and RNA concentrations" is not supported by quantitative data in the provided text. Figures or tables showing the comparison are needed.
- The statement that iConRNA's achievement "has not been demonstrated by other CG or atomistic models to date" is a strong negative claim that is not supported by a comprehensive literature comparison in the provided text.
- The claim that "base-mediated interactions emerge as dominant drivers in homotypic nucleic acid condensation" is supported by the discussed models but may be influenced by model construction choices (e.g., SIS lacks electrostatics). A more critical discussion is needed.
- The statement that "simulation resolution fundamentally determines which physical phenomena are accessible and observable" is presented as a general principle but is not systematically analyzed across the reviewed models.
- The discussion of the Martini 3 model's ability to capture spontaneous quadruplex folding is not accompanied by validation details or limitations.