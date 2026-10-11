## Review setup
- **Input scope** Full manuscript text including abstract, introduction, results, methods, and figure legends
- **Assessment boundary** Scientific validity, methodological rigor, claims versus evidence, and alignment with Nature-style criteria
- **Shared manuscript claim summary** The authors present OpenCGChromatin, a GPU-accelerated coarse-grained chromatin model with residue-level protein and nucleotide-level DNA resolution. They claim it enables near-atomistic simulations of chromatin systems an order of magnitude larger than previously possible, independently predicts linker-length-dependent chromatin structures observed by cryo-ET, resolves histone-tail dynamics inaccessible experimentally, and identifies H4K16 and H3K9 acetylation as the most energetically disruptive modifications for chromatin compaction. They further propose a mechanistic framework positioning chromatin as a semi-flexible stickers-and-spacers polymer whose phase behavior is governed by linker-DNA-imposed nucleosome orientation.
- **Visible evidence base** Main text figures 1-8, methods section, and references to supplementary figures 3-17 and tables
- **Missing materials affecting confidence** Supplementary Information (model Hamiltonian, parameterization details, validation protocols, full analysis definitions), Source Data files, and Reporting Summary were not provided for review

## Reviewer
- **Overall assessment** This manuscript presents a technically impressive computational advance with the potential to significantly impact the chromatin biology and biomolecular condensate fields. The OpenCGChromatin model addresses a genuine gap: the inability of existing near-atomistic models to access biologically relevant length and time scales. The validation against experimental sedimentation data and cryo-ET structures is a strength, and the mechanistic insights regarding linker-length-dependent phase behavior are conceptually novel. However, several concerns temper my enthusiasm. The central mechanistic claims regarding histone tail accessibility and the energetic dominance of specific acetylation sites rest on analyses whose definitions are only partially visible in the main text. The comparison between 25 bp and 30 bp systems, while informative, conflates linker length with nucleosome repeat length, and the attribution of phase behavior differences to "frustration" versus other physicochemical factors requires more rigorous support. The single-trajectory-per-condition design for the phase separation simulations, acknowledged by the authors, limits statistical confidence in the reported differences. The acetylation study, while suggestive, uses an extreme 50% random acetylation level that may not reflect physiological conditions, and the claim that H4K16 and H3K9 emerge as "most disruptive" requires careful interpretation given the pooling strategy across systems with different acetylation patterns. Overall, the model itself appears to be a valuable community resource, but the biological conclusions, particularly those extending beyond the validated compaction regime, need additional support or more cautious framing.

- **Who would be interested in the results, and why** Chromatin biologists studying higher-order genome organization, particularly those interested in the biophysical basis of chromatin phase separation and the role of linker DNA in shaping nuclear architecture. Computational biophysicists developing coarse-grained models of protein-DNA systems will find the methodological advances and GPU implementation of direct interest. Researchers studying histone post-translational modifications, especially acetylation, and their effects on chromatin structure will be interested in the predictive framework for identifying energetically important modification sites. The broader phase separation community, including those studying other nucleic acid-protein systems, may find the stickers-and-spacers framework with explicit spacer mechanics conceptually transferable.

- **Major strengths** The model represents a genuine methodological advance, achieving an order-of-magnitude improvement in accessible system size while maintaining near-atomistic resolution. The validation strategy is appropriate: reproducing experimental sedimentation coefficients across linker lengths provides a stringent test, and the agreement with cryo-ET structural features adds confidence. The phase separation predictions are bold and testable, and the connection between single-fiber conformational properties and collective phase behavior is conceptually elegant. The identification of H4K16 and H3K9 as energetically critical acetylation sites from unbiased simulations is a striking result with potential biological significance. The manuscript is generally well-written and the figures are informative.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Statistical rigor and reproducibility
- **Claim pointer** The authors claim that 25 bp chromatin phase-separates while 30 bp chromatin shows only weak phase separation, and that 25 bp arrays expand upon phase separation while 30 bp arrays do not.
- **Evidence pointer** Figure 4a-d, Figure 5b, Methods section "Phase separation"
- **Concern** The phase separation simulations consist of a single trajectory per condition (81 tetranucleosome arrays per simulation, one simulation for 25 bp and one for 30 bp). The authors acknowledge this in the Methods, noting that error bars represent temporal block-to-block variability rather than variation across independent replicates. This design fundamentally limits the statistical confidence in the reported differences between 25 bp and 30 bp systems. The differences in density profiles, largest connected component size, and conformational distributions could reflect initial condition sensitivity or stochastic variation rather than robust thermodynamic differences. The claim that 25 bp chromatin "phase-separates" while 30 bp does not is a strong binary statement resting on n=1 per condition.
- **Why it matters** The central mechanistic conclusion of the paper, that linker length controls phase behavior through conformational frustration, depends critically on the reliability of the difference between the 25 bp and 30 bp phase separation simulations. If this difference is not robust across independent simulations, the primary biological claim is undermined. The field of biomolecular condensates is already grappling with reproducibility challenges, and a claim of this significance requires demonstration of robustness.
- **Resolution test** The authors should provide at minimum 3 independent simulations per condition (ideally 5 or more) with different random seeds and, if feasible, different initial configurations. The reported differences in density profiles, cluster sizes, and conformational distributions should be shown to be consistent across replicates. Statistical comparison of the 25 bp and 30 bp conditions should be performed using appropriate tests that account for the hierarchical structure of the data (e.g., mixed-effects models or bootstrapping across replicates).

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Claim-evidence alignment
- **Claim pointer** The authors claim that "OpenCGChromatin resolves histone-tail dynamics and interaction networks that remain inaccessible experimentally, explaining how linker-DNA length controls histone tail accessibility and the resulting multiscale structure of chromatin condensates."
- **Evidence pointer** Figure 6, Methods section "Analysis methods"
- **Concern** The energy-weighted contact analysis presented in Figure 6 is central to the mechanistic claim that 30 bp linkers bury H4 and H2A N-terminal tails in intra-array contacts while 25 bp linkers expose all tails for inter-array interactions. However, the definition of the energy-weighted score is only partially described in the main text. The Methods state that contacts are weighted by pairwise interaction energy evaluated at instantaneous separation, but the specific functional form, the treatment of different interaction types (electrostatic vs. Lennard-Jones), and the normalization scheme are not fully specified. The claim that this analysis "resolves" tail dynamics implies a level of detail that may not be supported by the coarse-grained representation. Furthermore, the comparison between intra-array and inter-array contacts in Figure 6a vs 6b is presented as the key mechanistic distinction, but the absolute magnitudes and the statistical significance of the differences between 25 bp and 30 bp conditions are not reported.
- **Why it matters** The mechanistic explanation for why linker length controls phase behavior rests on this contact analysis. If the energy-weighted scoring is not rigorously defined and validated, or if the differences between conditions are not statistically robust, the proposed mechanism is not established. The claim of resolving "interaction networks that remain inaccessible experimentally" is strong and requires that the computational analysis be held to a high standard of rigor.
- **Resolution test** The authors should provide a complete mathematical definition of the energy-weighted contact score in the main text or clearly reference the Supplementary Information section where it is defined. They should report the statistical significance of the differences between 25 bp and 30 bp conditions for the key contact types (H4, H2A N) in both intra-array and inter-array categories. Ideally, they should also validate the energy-weighted approach against simpler contact frequency analyses to demonstrate that the weighting scheme does not introduce artifacts.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Interpretational overreach
- **Claim pointer** The authors state that "the simulations suggest that linker-induced frustration in the 25 bp fibers enables conformational expansion upon phase separation that exposes additional interaction sites, allowing fibers to reorganize and diversify their interaction modes" and that this "provides a direct coupling between single-fiber frustration, histone-tail accessibility, and network connectivity that defines how chromatin's geometry and chemical makeup jointly control its phase behavior."
- **Evidence pointer** Figure 5, Figure 6, Discussion
- **Concern** The causal chain proposed, from linker length to frustration to expansion to tail exposure to enhanced inter-array connectivity to phase separation, is presented as a coherent mechanism. However, the evidence for each causal link is correlational. The authors show that 25 bp arrays are more expanded in dilute conditions and expand further in the condensed phase, and that tail contacts differ between conditions. But they do not demonstrate that the expansion is caused by frustration rather than by, for example, differences in net charge, hydration, or excluded volume effects. The term "frustration" is used descriptively but is not quantified or directly measured. The claim of a "direct coupling" implies a mechanistic understanding that may exceed what the simulations can establish.
- **Why it matters** The conceptual framework presented in the Discussion, positioning chromatin as a semi-flexible stickers-and-spacers polymer where spacer mechanics control phase behavior, is potentially important and generative. However, if the causal claims are overstated relative to the evidence, the framework may be prematurely solidified and could misdirect future research. The distinction between correlation and causation is particularly important in computational studies where the modeler has full access to all variables.
- **Resolution test** The authors should either (a) provide additional analyses that directly test the proposed causal chain, such as perturbing specific interactions (e.g., neutralizing specific tail charges, modifying DNA flexibility) and showing the predicted effects on phase behavior, or (b) soften the causal language and present the mechanism as a hypothesis consistent with the simulations rather than a demonstrated principle. Quantifying "frustration" through a measurable order parameter would also strengthen the claim.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Generalizability of acetylation findings
- **Claim pointer** The authors claim that "extending simulations to 108-nucleosome fibers shows that acetylation disrupts chromatin compaction in a pattern-specific manner by weakening key tail-mediated interactions, with H4K16 and H3K9 emerging as the most energetically disruptive modifications."
- **Evidence pointer** Figure 7, Figure 8, Methods section "Long fiber dynamics"
- **Concern** The acetylation simulations use a 50% random acetylation level across all lysines in acetylated regions. This is acknowledged as an upper bound, but the interpretation of the results as identifying "the most energetically disruptive modifications" may be sensitive to this choice. The comparison between H4K16 and H3K9 as "most disruptive" is based on a ranking of energy-weighted contact scores, but the statistical significance of this ranking is not established. Furthermore, the simulations use only three acetylation patterns (0 Ac, 5x12 Ac, 54 Ac), and the 5x12 pattern creates alternating blocks of acetylated and unacetylated nucleosomes that may not represent any physiological arrangement. The claim that the findings reveal "pattern-specific" effects is based on a very limited exploration of the pattern space.
- **Why it matters** The acetylation results are presented as a key application of the model with potential biological significance. If the conclusions are sensitive to the specific simulation choices (acetylation level, pattern, and the specific lysines modified), the generalizability of the findings is limited. The claim that specific modification sites are "most disruptive" could be misinterpreted as a prediction about which acetylation marks are most biologically important, when the simulations only address which are most disruptive under a specific, extreme acetylation condition.
- **Resolution test** The authors should either (a) perform additional simulations with different acetylation levels (e.g., 10%, 25%) and patterns to test the robustness of the ranking, or (b) temper the claims to state that under the specific conditions simulated, H4K16 and H3K9 show the largest energetic effects, without generalizing to biological importance. Reporting confidence intervals or bootstrap estimates for the energy-weighted scores would also help establish the robustness of the ranking.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity of model validation
- **Affected element** Figure 2a and Supplementary Figure 4
- **Evidence pointer** Figure 2a, Supplementary Figure 4
- **Issue** The validation against experimental sedimentation coefficients is presented as a key strength, but the figure only shows simulated values with experimental values overlaid. It is unclear how the experimental values were obtained and whether the comparison is apples-to-apples (e.g., same salt conditions, same temperature, same buffer composition).
- **Required correction** Please clarify in the figure legend or main text the source of the experimental sedimentation coefficients and any adjustments made to ensure comparability with simulation conditions. If the experimental values are from different buffer conditions, this should be stated and the potential impact on the comparison discussed.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Completeness of benchmarking
- **Affected element** Figure 1b
- **Evidence pointer** Figure 1b
- **Issue** The benchmarking data in Figure 1b are described as single measurements (n=1) with no uncertainty or inferential comparison claimed. While this is appropriate for a hardware benchmark, the claim of "over an order-of-magnitude acceleration" would be more convincing with at least a few repeated measurements to demonstrate stability.
- **Required correction** Please provide at least 3 repeated benchmark measurements per condition and report the mean and range, or state clearly that the benchmarks are representative single measurements and the performance gain is approximate.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** Figure 2b-c, Figure 3a-b, Figure 6, Figure 7d, Figure 8b
- **Evidence pointer** Multiple figures
- **Issue** The Methods state that error bars represent standard deviations across five temporal blocks from a single trajectory. This is appropriate for describing temporal variability, but the figures do not consistently indicate whether any differences between conditions are statistically significant. For example, in Figure 3a-b, the differences between 10N and 10N+5 contact frequencies appear visually clear, but no statistical test is reported.
- **Required correction** Please add statistical comparisons (e.g., t-tests or Mann-Whitney U tests on block means) for the key comparisons between conditions, or state explicitly that the reported differences are descriptive and not statistically tested. If the latter, the language in the text should be adjusted to avoid implying statistical significance.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Parameter sensitivity
- **Affected element** Contact definitions
- **Evidence pointer** Methods section "Analysis methods"
- **Issue** The contact cutoff for residue-residue contacts is defined as rc = 0.5(sigma_i + sigma_j) + 0.25 nm, and the nucleosome-nucleosome contact cutoff is 13 nm. The sensitivity of the results to these choices is not discussed. Given that the central mechanistic claims depend on contact analyses, it would be valuable to know whether the conclusions are robust to reasonable variations in these cutoffs.
- **Required correction** Please add a sensitivity analysis in the Supplementary Information showing that the key conclusions (e.g., the ranking of tail contact frequencies, the difference between 25 bp and 30 bp systems) are robust to variations in the contact cutoffs (e.g., +/- 20%).

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Terminology precision
- **Affected element** Abstract and Introduction
- **Evidence pointer** Abstract, Introduction
- **Issue** The term "near-atomistic" is used throughout, but its precise meaning is not defined. The model represents each amino acid as one bead and each nucleotide as one bead, which is a coarse-grained representation, not "near-atomistic" in the sense of retaining atomic detail. The term could be misleading to readers unfamiliar with the field.
- **Required correction** Please define "near-atomistic" in the Introduction, clarifying that it refers to residue-level and nucleotide-level resolution, and consider whether a more precise term such as "residue-resolution" or "united-atom" would be more appropriate.

- **Concern ID** R1-m6
- **Severity** Minor
- **Axis** Discussion of limitations
- **Affected element** Discussion
- **Evidence pointer** Discussion
- **Issue** The Discussion does not adequately address the limitations of the implicit solvent treatment. The Debye-Hückel model is acknowledged in the Methods, but the potential impact of neglecting specific ion effects, hydration forces, and hydrophobic effects on the phase behavior predictions is not discussed.
- **Required correction** Please add a paragraph in the Discussion addressing the limitations of the implicit solvent model and how these might affect the quantitative predictions of phase behavior, particularly at the salt concentrations studied.

## Risk / unsupported claims
- The claim that OpenCGChromatin "independently predicts" experimental observations is partially supported for sedimentation coefficients but is not established for the phase separation behavior, as the experimental comparison relies on qualitative agreement with prior work from the same group.
- The claim that H4K16 and H3K9 are "the most energetically disruptive modifications" is not statistically supported and is based on a single simulation per acetylation pattern with an extreme 50% acetylation level.
- The claim that the model "resolves histone-tail dynamics and interaction networks that remain inaccessible experimentally" is overstated; the model provides predictions that are not directly validated against experimental measurements of tail dynamics.
- The mechanistic claim of "direct coupling between single-fiber frustration, histone-tail accessibility, and network connectivity" is presented as established but is a hypothesis consistent with the simulations, not a demonstrated causal chain.
- The claim of "over an order-of-magnitude acceleration" is based on single benchmark measurements and should be treated as approximate.
- The generalizability of the phase behavior findings to longer, heterogeneous chromatin fibers is acknowledged as limited by the authors, but the Discussion could more prominently caveat this limitation.