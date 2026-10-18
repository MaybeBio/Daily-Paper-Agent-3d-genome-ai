## Review setup
- **Input scope** Full manuscript text (abstract, results, discussion, methods) without supplementary figures, tables, or source data
- **Assessment boundary** Scientific claims, methodological soundness, and interpretive validity based solely on the provided text
- **Shared manuscript claim summary** The authors combine all-atom molecular dynamics simulations of tri-nucleosomes with varying linker lengths and cryo-ET maps of native human chromatin to develop a fitting framework that enables near-atomistic interpretation of cryo-ET density maps. They report that histone tails promote chromatin compaction through three interaction patterns: histone-DNA interactions, H2A-H4 tail-tail interactions, and H3-H4 tail-tail interactions. They further claim that simulated structural parameters (inter-nucleosomal distances and dihedral angles) reproduce experimental distributions from condensed chromatin arrays.
- **Visible evidence base** Main text figures referenced (Figs. 1-5), supplementary figures referenced (Figs. S1-S25), supplementary tables referenced (Tables 1-3), and methods text
- **Missing materials affecting confidence** Supplementary figures and tables, source data, reporting summary, and methodological details for cryo-ET map collection and processing are not provided in the submitted material

## Reviewer
- **Overall assessment** The manuscript presents a potentially valuable integrative approach that combines all-atom MD simulations with cryo-ET map fitting to interpret chromatin structure at near-atomistic resolution. The central concept of using tri-nucleosome conformations as fitting templates, rather than individual nucleosome cores, is a reasonable methodological advance that could address known limitations of mono-nucleosome fitting approaches. However, the manuscript as provided has several significant gaps that prevent full evaluation of the claims. The absence of quantitative validation metrics, limited description of the cryo-ET data processing pipeline, and the lack of direct comparison between simulated and experimental distributions with statistical rigor weaken the central claims. The mechanistic conclusions regarding histone tail interactions are based on simulation data without experimental validation, and the manuscript does not adequately address potential force field limitations or sampling convergence. The writing is generally clear, but the results section would benefit from more precise quantitative reporting.

- **Who would be interested in the results, and why** Researchers in chromatin biophysics, computational structural biology, and cryo-electron tomography methodology would find this work relevant. The approach of using MD-derived multi-nucleosome conformations for cryo-ET map interpretation could be of interest to the structural biology community working on flexible or heterogeneous macromolecular assemblies. The mechanistic insights into histone tail-mediated chromatin compaction would interest chromatin biologists studying gene regulation and epigenetic mechanisms. The methodological framework may also appeal to computational biologists developing integrative modeling approaches that combine simulation with experimental data.

- **Major strengths**
  1. The conceptual advance of using tri-nucleosome conformations from MD simulations as fitting templates for cryo-ET maps is a thoughtful approach that addresses known limitations of mono-nucleosome fitting, particularly in condensed chromatin regions where ambiguous fits are common.
  2. The systematic comparison of three linker lengths (22, 26, and 31 bp) provides a useful parameter sweep that allows assessment of how linker length affects nucleosome organization and compaction.
  3. The identification of specific histone tail interaction patterns (tail-tail and tail-DNA) at atomistic resolution provides mechanistic hypotheses that are testable and could guide future experimental work.
  4. The authors acknowledge limitations of their approach, including sampling constraints and force field accuracy, which demonstrates scientific rigor.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence sufficiency
- **Claim pointer** The authors claim that "the distributions of MD-generated structural parameters of tri-nucleosomes were found to be in strong agreement with those of experimental condensed chromatin arrays."
- **Evidence pointer** Figure 2 and associated text, location not provided
- **Concern** The claim of "strong agreement" between simulated and experimental distributions is not supported by quantitative statistical analysis in the provided text. The authors state that simulated distributions were "narrower than experimental ones, possibly pointing to some degree of conformational under-sampling," which contradicts the characterization of "strong agreement." No statistical tests comparing the distributions are reported, and the figure panels referenced do not include confidence intervals or quantitative comparison metrics.
- **Why it matters** The central validation of the MD approach rests on this comparison. If the agreement is only qualitative or if the distributions are systematically narrower, the claim that MD simulations capture the relevant conformational ensemble of native chromatin is not established. This directly affects whether the mechanistic conclusions about histone tail function can be generalized.
- **Resolution test** Provide quantitative statistical comparisons between simulated and experimental distributions (e.g., Kolmogorov-Smirnov tests, overlap coefficients, or Bayesian comparison metrics). Report effect sizes and confidence intervals. If distributions are systematically narrower in simulations, discuss the implications for the interpretation of the fitting results and mechanistic conclusions.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Methodological completeness
- **Claim pointer** The authors claim that their tri-nucleosome fitting approach "provides a practically superior strategy for building biologically meaningful chromatin models" compared to mono-nucleosome fitting.
- **Evidence pointer** Figure 1 and associated text, location not provided
- **Concern** The comparison between tri-nucleosome and mono-nucleosome fitting approaches is presented qualitatively. The authors state that mono-nucleosome fitting has limitations, but no quantitative comparison of fitting quality between the two approaches is provided. The claim of superiority requires a systematic comparison using the same cryo-ET maps, with quantitative metrics for both approaches. Additionally, the authors note that "inside-contour values could not be directly compared between tri-nucleosome and mono-nucleosome systems because this measure is very sensitive to the fitted system's size," which limits the comparability of the reported metrics.
- **Why it matters** The methodological contribution of this work depends on demonstrating that tri-nucleosome fitting provides meaningful advantages over existing approaches. Without a quantitative head-to-head comparison, the practical value of the method is not established, and readers cannot assess whether the additional computational cost is justified.
- **Resolution test** Perform a systematic comparison of fitting quality between mono-nucleosome and tri-nucleosome approaches on the same cryo-ET maps, reporting quantitative metrics (correlation coefficients, cross-validation scores, or similar) with appropriate statistical testing. Address the size-dependence issue of the inside-contour metric or use alternative comparison metrics that are size-independent.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Interpretive validity
- **Claim pointer** The authors claim that histone tails "promote chromatin compaction via three major patterns: through histone-DNA interactions, histone H2A-H4 and H3-H4 tail-tail interactions."
- **Evidence pointer** Figures 4-5 and associated text, location not provided
- **Concern** The mechanistic conclusions about histone tail interactions are derived exclusively from MD simulations. The authors do not provide experimental validation of these specific interaction patterns, nor do they compare their findings with available experimental data on histone tail interactions (e.g., cross-linking studies, NMR, or mutagenesis experiments). The claim that these are the "major patterns" of tail-mediated compaction requires either experimental support or a more careful caveat that these are simulation-derived predictions. Additionally, the authors do not report whether these interaction patterns are stable across the independent simulation runs or whether they represent transient states.
- **Why it matters** The mechanistic claims are the primary scientific contribution of the work. If these patterns are not validated or are presented without appropriate caveats, readers may overinterpret simulation results as established biological mechanisms. The transient nature of histone tail interactions, acknowledged elsewhere in the manuscript, complicates the identification of "major" interaction patterns.
- **Resolution test** Provide a more nuanced interpretation that clearly distinguishes simulation-derived predictions from experimentally established mechanisms. Report the persistence and reproducibility of the identified interaction patterns across independent runs. If possible, compare with available experimental data on histone tail interactions or clearly state the predictions that could be tested experimentally.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The authors state that "three independent simulation runs were performed for each system, 4 µs each" and that "the initial 200 ns of each simulation trajectory were discarded as equilibration."
- **Evidence pointer** Methods section, location not provided
- **Concern** The manuscript does not report convergence metrics for the MD simulations. For intrinsically disordered histone tails, which are expected to sample a broad conformational ensemble, 4 µs may not be sufficient to achieve converged sampling, particularly for the larger tri-nucleosome systems. The authors do not report whether the structural parameters (distances, angles) have converged within each trajectory or across the three independent runs. The choice of 200 ns for equilibration is not justified.
- **Why it matters** The reliability of all structural and mechanistic conclusions depends on adequate conformational sampling. If the simulations are not converged, the reported distributions and interaction patterns may not be representative of the equilibrium ensemble, and the comparison with experimental data would be compromised.
- **Resolution test** Report convergence metrics such as block averaging, autocorrelation times, or split-half analysis for the key structural parameters. Show that the three independent runs sample similar distributions. Justify the equilibration time and demonstrate that the results are robust to the choice of equilibration period.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Reproducibility
- **Claim pointer** The authors state that "the raw tilt series are available from the Dryad data repository" and that "a library of successfully fitted conformations" will be provided.
- **Evidence pointer** Methods section and Discussion, location not provided
- **Concern** The manuscript does not provide sufficient detail on the cryo-ET data processing pipeline, including the specific steps of tomographic reconstruction, denoising, and the criteria used to select regions for fitting. The deep learning-based denoising method is referenced but not described in sufficient detail. The criteria for determining a "successful" fit are not explicitly defined. The availability of the fitting library is mentioned but the format and access details are not provided.
- **Why it matters** Reproducibility is a core requirement for scientific publication. Without detailed methods for the cryo-ET processing and fitting pipeline, other researchers cannot replicate the approach or assess its robustness. The lack of clear criteria for successful fits undermines the objectivity of the reported results.
- **Resolution test** Provide a detailed description of the cryo-ET processing pipeline, including software versions, parameters, and validation steps. Define explicit criteria for successful fits. Provide clear access information for the fitting library and any code used in the analysis.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Figure 1 caption and text
- **Evidence pointer** Figure 1, location not provided
- **Issue** The text describing Figure 1 is incomplete and contains a grammatical error. The sentence "see Fig. S1 for strong contrast with a black background and volume rendering of cryo-ET density maps" appears to be missing a closing parenthesis and the description is unclear.
- **Required correction** Revise the figure caption and associated text to clearly describe what is shown in each panel of Figure 1 and the supplementary figures. Ensure the sentence structure is complete and grammatically correct.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Statistical reporting
- **Affected element** Figure 2 and associated text
- **Evidence pointer** Figure 2, location not provided
- **Issue** The manuscript reports median values for distances and angles but does not report measures of dispersion (e.g., interquartile ranges) or sample sizes for the experimental distributions. The number of nucleosome pairs analyzed in the experimental cryo-ET maps is not stated.
- **Required correction** Report the sample sizes and appropriate measures of dispersion for all experimental distributions. If the experimental data are from a previous study, clearly state the sample sizes from that study.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Terminology
- **Affected element** Abstract and Results
- **Evidence pointer** Abstract, location not provided
- **Issue** The term "near-atomistic interpretation" is used in the abstract and throughout the manuscript. This is imprecise, as the fitting approach uses all-atom models but the cryo-ET maps are at much lower resolution. The term could be misinterpreted as claiming atomic resolution for the cryo-ET maps.
- **Required correction** Clarify the terminology. For example, use "all-atom model fitting into cryo-ET maps" or "atomistic model-based interpretation" to avoid implying that the cryo-ET maps themselves achieve atomic resolution.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Methods section
- **Evidence pointer** Methods, location not provided
- **Issue** The methods section does not describe the force field parameters used for the histone tails specifically, nor does it describe how post-translational modifications (if any) were modeled. Given that the manuscript discusses H3K9 methylation in the Discussion, it is unclear whether modified histone states were included in the simulations.
- **Required correction** Clarify whether post-translational modifications were included in the simulations. If not, clearly state this limitation and adjust the Discussion accordingly.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Referencing
- **Affected element** Discussion
- **Evidence pointer** Discussion, location not provided
- **Issue** The Discussion references "recent super-resolution microscopy studies" and "previous studies" without providing specific citations in the text provided. While the reference list is not included in the submitted material, the in-text citations should be checked for completeness.
- **Required correction** Ensure all references cited in the text are included in the reference list and that the citation format is consistent throughout.

## Risk / unsupported claims
- The claim of "strong agreement" between simulated and experimental structural parameter distributions is not quantitatively supported in the provided text
- The claim that tri-nucleosome fitting is a "practically superior strategy" compared to mono-nucleosome fitting is not supported by a systematic quantitative comparison
- The identification of "three major patterns" of histone tail-mediated compaction is presented as a finding but is based solely on simulation data without experimental validation
- The statement that "histone tails were shown to promote chromatin compaction" implies experimental demonstration, but the evidence presented is from simulations
- The claim that the approach "may help to resolve ambiguities in cryo-ET maps" is speculative and not directly demonstrated
- The assertion that the tri-nucleosome models "specify the relative orientation of consecutive nucleosomes" in partially resolved maps is not validated with specific examples or quantitative assessments of fitting reliability
- The manuscript mentions "a library of successfully fitted conformations" but the criteria for "successful" fitting are not defined, making this claim unverifiable from the provided material