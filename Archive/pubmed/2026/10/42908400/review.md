## Review setup
- **Input scope** Full manuscript text including abstract, introduction, materials and methods, results, discussion, and supplementary figure legends
- **Assessment boundary** Scientific validity, methodological rigor, interpretation of results, and support of claims by the presented evidence
- **Shared manuscript claim summary** The authors present a polymer-based simulation framework for the E. coli chromosome that separates nonspecific polymer confinement effects from specific-folding interactions (SFIs), and use this framework to identify a small subset of SFIs that shape chromosome organization, including domain structure, nucleoid accessibility, and gene expression patterns
- **Visible evidence base** Main text figures 1-5, supplementary figures S1-S7, supplementary tables S1-S2, methods descriptions, and data availability statements
- **Missing materials affecting confidence** Supplementary figures and tables were referenced but not provided in the submitted material; specific numerical values for some statistical tests were not fully reported; details of the Markov Chain Monte Carlo implementation were not described

## Reviewer
- **Overall assessment** This manuscript presents a conceptually interesting approach to disentangling polymer physics from biologically encoded interactions in bacterial chromosome organization. The central idea, that a null polymer model can serve as a baseline against which to identify specific interactions, is sound and potentially valuable. However, the manuscript as presented has several technical concerns that need to be addressed before the conclusions can be fully accepted. The sensitivity analyses are thoughtful, but the lack of detail on the MCMC procedure and the incomplete reporting of some statistical results limit the current assessment. The biological conclusions, particularly regarding H-NS and MatP as determinants of SFIs, are plausible but would benefit from additional validation.

- **Who would be interested in the results, and why** Researchers studying bacterial chromosome organization, genome architecture, and the interplay between polymer physics and protein-mediated interactions. The methodological framework could also interest computational biologists developing polymer models for chromosome folding. The findings on SFI distribution and their correlation with gene expression and prophage localization would be relevant to those studying bacterial gene regulation and stress responses.

- **Major strengths**
  1. The conceptual separation of polymer confinement from specific interactions is a valuable contribution that addresses a known limitation in Hi-C analysis
  2. The null model approach is well motivated and the sensitivity analyses for parameter choices are thorough
  3. The integration of multiple data types (Hi-C, ChIP-seq, RNA-seq, supercoiling) provides a comprehensive view
  4. The validation against single-cell imaging data strengthens the biological relevance of the findings

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The authors claim that the specific-fold model reproduces chromosomal interaction domains and single-cell heterogeneity, and that the identified SFIs are the drivers of E. coli chromosome organization
- **Evidence pointer** Results section "Isolating specific-folding interactions", Figure 2
- **Concern** The Markov Chain Monte Carlo (MCMC) approach used to generate the specific-fold ensemble is not described in sufficient detail. The methods section mentions that MCMC was applied but does not specify the proposal distribution, acceptance criteria, convergence diagnostics, or the number of iterations. Without this information, it is impossible to assess whether the generated ensemble is properly sampled and whether the resulting SFI identification is reliable.
- **Why it matters** The entire framework depends on the statistical validity of the specific-fold ensemble. If the MCMC sampling is not well characterized, the identified SFIs and all subsequent analyses (including the correlations with protein binding and gene expression) could be artifacts of insufficient sampling or poor convergence.
- **Resolution test** Provide a detailed description of the MCMC procedure, including the proposal distribution, acceptance criteria, burn-in period, number of chains, and convergence diagnostics. Show that the ensemble is reproducible and that the SFI identification is stable across multiple independent MCMC runs.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical soundness
- **Claim pointer** The authors state that the null model recapitulates global chromosome organization with a correlation of rPearson = 0.83 and ρSpearman = 0.80 between simulated and experimental Hi-C maps
- **Evidence pointer** Results section "Simulated chromosome-fold null model reproduces experimentally determined global organization", Figure 1D
- **Concern** The correlation between the null model and experimental Hi-C maps is reported as a single global value. However, Hi-C maps contain distance-dependent signals that dominate the overall correlation. It is unclear whether the high correlation is driven primarily by the expected distance decay of contact frequency rather than by genuine structural recapitulation. The authors should report correlations stratified by genomic distance or use a metric that accounts for the expected distance dependence.
- **Why it matters** If the high correlation is largely due to the trivial distance-decay effect, the claim that the null model captures global organization is overstated. This would affect the interpretation of what the null model actually explains and what the SFIs contribute.
- **Resolution test** Report correlation coefficients separately for different genomic distance bins (e.g., 0-100 kb, 100-500 kb, 500 kb-1 Mb, >1 Mb) or use a distance-normalized comparison. Show that the null model captures features beyond the expected distance decay.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** No
- **Axis** Scientific importance
- **Claim pointer** The authors claim that H-NS and MatP emerged as major chromosome-wide and local determinants of SFIs, respectively
- **Evidence pointer** Results section "Protein binding underlies SFIs", Figure 4D-E
- **Concern** The cross-correlation analysis between SFI density and protein binding is descriptive and does not establish causality. The authors conclude that H-NS and MatP are determinants of SFIs, but the analysis only shows correlation. The manuscript would be strengthened by perturbation experiments or additional analyses that test whether removing or altering these proteins changes the SFI landscape.
- **Why it matters** The claim that specific proteins are determinants of SFIs has implications for understanding the molecular mechanisms of chromosome organization. Without causal evidence, the conclusion remains speculative and could be misleading for future research directions.
- **Resolution test** Include in silico perturbation experiments where H-NS or MatP binding is removed from the model and assess whether the SFI landscape changes accordingly. Alternatively, compare the SFI predictions with experimental data from strains lacking these proteins.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Technical soundness
- **Claim pointer** The authors state that SFIs are enriched in the ter region and depleted in the ori region, and that this correlates with reduced nucleoid accessibility
- **Evidence pointer** Results section "SFIs reduce nucleoid accessibility", Figure 3D-E
- **Concern** The alpha-shape analysis used to compute nucleoid accessibility depends on the choice of the alpha parameter. The authors state that they varied the alpha parameter for different probe sizes but do not report how the results depend on this choice. It is unclear whether the observed differences in accessibility between the null and specific-fold models are robust across a range of alpha values or are sensitive to this parameter.
- **Why it matters** The conclusion that SFIs reduce nucleoid accessibility is a key finding of the paper. If this result is sensitive to the alpha parameter choice, the conclusion may not be robust and could limit the generalizability of the findings.
- **Resolution test** Provide a sensitivity analysis showing how the accessibility differences between the null and specific-fold models vary across a range of alpha parameters. Demonstrate that the qualitative conclusions are stable across this range.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Readability for nonspecialists
- **Affected element** Introduction
- **Evidence pointer** Introduction, first paragraph
- **Issue** The introduction assumes familiarity with polymer physics concepts and Hi-C methodology. Terms such as "excluded-volume effects" and "ensemble-averaged contact maps" are used without brief definitions.
- **Required correction** Add brief explanations of key terms for readers who may not be specialists in polymer physics or Hi-C analysis.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Methods, Hi-C data processing
- **Evidence pointer** Materials and methods, "Hi-C data processing"
- **Issue** The authors state that they used the Hi-C dataset from Cockram et al. with accession PRJNA587586 and run SRR10394904. However, they do not specify the number of biological replicates or whether the data were pooled across replicates.
- **Required correction** Clarify whether the analysis was performed on a single Hi-C dataset or pooled across replicates, and discuss any potential batch effects.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Results, Cryptic prophage analysis
- **Evidence pointer** Results section "Cryptic prophages coincide with highly SFI regions", Supplementary Figure S6
- **Issue** The permutation test for prophage enrichment is described briefly. The authors state that 10,000 random perturbations were performed but do not specify how the null distribution was constructed or whether the test accounts for the non-uniform distribution of prophages along the genome.
- **Required correction** Provide more detail on the permutation test, including how random placements were generated and whether the test accounts for genomic features that might confound the analysis.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Interdisciplinary readership
- **Affected element** Discussion
- **Evidence pointer** Discussion, paragraph 3
- **Issue** The comparison with other modeling approaches is brief and does not clearly articulate the advantages of the presented framework over existing methods.
- **Required correction** Expand the comparison with other approaches, highlighting specific advantages and limitations of the presented framework in a way that is accessible to readers from different disciplines.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Technical soundness
- **Affected element** Methods, Polymer model setup
- **Evidence pointer** Materials and methods, "Polymer model setup"
- **Issue** The authors state that the bead diameter was estimated from reported DNA occupancy in the nucleoid volume but do not provide the specific calculation or reference for this estimate.
- **Required correction** Provide the calculation or a more specific reference for the bead diameter estimate to allow readers to assess the appropriateness of this parameter.

## Risk / unsupported claims
- The claim that the specific-fold model reproduces single-cell heterogeneity is based on comparison with a previous imaging study (seqFISH), but the details of this comparison are not fully described and the supplementary figure referenced was not provided
- The conclusion that high-SFI regions are associated with stress-resistant phenotypes is based on GO enrichment analysis, but the statistical thresholds and multiple testing corrections for the GO analysis were not fully reported
- The statement that the framework is "readily generalized to circular chromosomes of other bacterial species" is not supported by any demonstration or analysis in the current manuscript
- The claim that SFIs are "the drivers" of chromosome organization is stronger than what the correlative evidence supports; the analysis identifies associations but does not establish causal relationships