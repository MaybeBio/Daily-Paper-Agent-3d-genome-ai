## Review setup
- **Input scope** Full manuscript text (abstract, introduction, results, discussion, methods) without figures or supplementary tables
- **Assessment boundary** Technical and conceptual evaluation of the described methods, results, and claims as presented in the text
- **Shared manuscript claim summary** The authors present two droplet-based long-read single-cell epigenome sequencing methods (dscNanoATAC and dscNanoCUT) that achieve ~5000 cells per experiment, demonstrate allele-specific epigenetics, neighboring co-accessibility, and regulatory element detection in low-mappability regions, and introduce AS-C.Origami for predicting allele-specific 3D genome structures at 10 kb resolution. Applications in mouse brain reveal allele-specific regulation of Ube3a and transposon-associated regulatory elements.
- **Visible evidence base** Text descriptions of results, figure legends, methods, and supplementary table titles
- **Missing materials affecting confidence** All figures and supplementary figures, all supplementary tables, sequencing data availability, code availability, and detailed quality metrics

## Reviewer
- **Overall assessment** This manuscript describes a technically ambitious and potentially valuable advance in single-cell epigenomics by adapting droplet-based microfluidics to long-read Nanopore sequencing. The core methods, dscNanoATAC and dscNanoCUT, address a genuine need for higher-throughput long-read single-cell epigenome profiling. The biological applications, particularly the allele-specific analysis of the Pradet-Willi/Angelman syndrome region and transposon element profiling, are of interest. However, the manuscript as provided has several critical gaps that prevent full evaluation. The absence of all figures and supplementary data makes it impossible to assess data quality, reproducibility, and the validity of key claims. The AS-C.Origami section, while conceptually interesting, lacks sufficient detail on training, validation, and the biological significance of the predictions. The comparison with existing methods is incomplete, and several claims about performance and utility are not fully supported by the evidence presented in the text alone. The manuscript would benefit from a more critical discussion of limitations and a clearer demonstration of the advantages over existing approaches.

- **Who would be interested in the results, and why** Researchers in single-cell genomics, epigenomics, and long-read sequencing technologies would be the primary audience. Those studying allele-specific regulation, genomic imprinting, and the regulatory role of transposable elements would find the applications relevant. The methods could also be of interest to those developing high-throughput single-cell assays and computational tools for epigenome analysis. The potential for clinical translation in understanding disorders like Pradet-Willi and Angelman syndrome may attract a broader biomedical audience.

- **Major strengths**
  1. The development of droplet-based long-read single-cell epigenome methods addresses a clear technological gap, potentially making long-read single-cell profiling more accessible and scalable.
  2. The demonstration of allele-specific epigenetics and neighboring co-accessibility using long reads is a significant advantage over short-read methods.
  3. The application to complex tissues (mouse brain) and the identification of cell type-specific regulatory elements, including those in low-mappability regions, showcases the biological utility of the approach.
  4. The integration of a deep-learning model (AS-C.Origami) to predict allele-specific 3D genome structures from the generated data is a novel and forward-looking contribution.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence
- **Claim pointer** The claim that dscNanoATAC and dscNanoCUT achieve a throughput of ~5000 cells in a single experiment with high data quality.
- **Evidence pointer** Results section "Technology workflow and data quality"; Figure 1; Supplementary Figures S1-S4; Supplementary Table S1
- **Concern** The manuscript text describes the throughput and quality metrics, but the actual data supporting these claims are not visible. The figures and supplementary tables that would show cell counts, quality distributions, reproducibility, and comparisons with existing methods are not provided. Without these, the core performance claims cannot be verified.
- **Why it matters** The primary contribution of this work is the method itself. If the throughput, data quality, and reproducibility are not convincingly demonstrated with data, the central claims of the manuscript are unsupported.
- **Resolution test** Provide all figures and supplementary tables. Show clear evidence of cell capture rates, library complexity, signal-to-noise ratios, and reproducibility across replicates. Include direct comparisons with existing methods (e.g., scNanoATAC-seq, 10x scATAC-seq) using the same cell types and metrics.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Technical Soundness
- **Claim pointer** The claim that the AS-C.Origami model can predict allele-specific 3D genome structures at high resolution (10 kb) from dscNanoATAC data.
- **Evidence pointer** Results section "Allele-specific-C.Origami enables the prediction of high-resolution cell type- and allele-specific 3D chromatin architectures"; Figure 3; Supplementary Figures S9-S11
- **Concern** The description of the AS-C.Origami workflow is insufficient. The text mentions training a model based on a previous study, but does not provide details on the training data, model architecture, hyperparameters, or validation strategy. The benchmarking against Pote-C and Hi-C data is described, but the actual correlation values and their significance are not presented in the text. The claim of "high resolution" is not substantiated without a clear comparison to the resolution of the input data and existing methods.
- **Why it matters** The AS-C.Origami section is a major part of the manuscript's novelty. If the model's development and validation are not rigorously described and demonstrated, the claim of predicting allele-specific 3D structures is not credible.
- **Resolution test** Provide a detailed description of the model architecture, training procedure, and validation datasets. Show the actual correlation plots and statistics for the benchmarking against Pote-C and Hi-C data. Demonstrate that the model's predictions are accurate and specific, and that the 10 kb resolution claim is justified.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence
- **Claim pointer** The claim that dscNanoATAC and dscNanoCUT can identify allele-specific regulatory elements and transposon-associated regulatory elements in the mouse brain.
- **Evidence pointer** Results sections "dscNanoATAC revealed allele-specific regulatory elements in the mouse brain" and "dscNanoCUT captured allele-specific histone modifications in the mouse brain"; Figures 4-6; Supplementary Figures S12-S19; Supplementary Tables S5-S11
- **Concern** The biological findings, such as the allele-specific regulation of Ube3a and the identification of transposon-associated regulatory elements, are described in the text, but the supporting data are not visible. The figures that would show the genomic tracks, co-accessibility maps, and cell type-specific patterns are not provided. The statistical significance of these findings is not reported in the text.
- **Why it matters** The biological applications are important for demonstrating the utility of the methods. Without the actual data, the significance and validity of these findings cannot be assessed.
- **Resolution test** Provide all figures and supplementary tables. Show clear genomic tracks and statistical analyses for the allele-specific peaks and co-accessibility events. Include validation of the Ube3a findings and the transposon-associated regulatory elements.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Reproducibility
- **Claim pointer** The claim that the methods are scalable and cost-effective compared with previous techniques.
- **Evidence pointer** Results section "Technology workflow and data quality"; Supplementary Figure S3
- **Concern** The cost and time comparisons are mentioned in the text, but the details of the cost analysis are not provided. The comparison with plate-based methods is described, but the specific cost breakdown and time savings are not quantified in the text.
- **Why it matters** The scalability and cost-effectiveness are key selling points of the methods. Without a clear and detailed cost analysis, these claims are not substantiated.
- **Resolution test** Provide a detailed cost analysis table comparing dscNanoATAC and dscNanoCUT with existing methods, including reagent costs, sequencing costs, and hands-on time.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Abstract
- **Evidence pointer** Abstract
- **Issue** The abstract is dense and uses technical jargon without sufficient context for a general reader. The phrase "multidimensional regulatory elements" is vague.
- **Required correction** Clarify the abstract by briefly explaining what "multidimensional" means in this context and consider simplifying the language to improve accessibility.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Completeness
- **Affected element** Methods section
- **Evidence pointer** Materials and methods
- **Issue** The methods section for the computational pipeline is described in the results but not fully detailed in the methods. The specific parameters for the "local minima-based strategy" and the "stringent filtration step" are not fully described.
- **Required correction** Provide a more detailed description of the computational pipeline, including all parameters and thresholds used.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Statistical Rigor
- **Affected element** Results section
- **Evidence pointer** Results sections on allele-specific peaks and co-accessibility
- **Issue** The statistical methods for identifying allele-specific peaks and co-accessibility events are not described in the text. The thresholds for significance are not stated.
- **Required correction** Clearly describe the statistical tests and thresholds used for identifying allele-specific peaks and co-accessibility events.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Methods section
- **Evidence pointer** Materials and methods
- **Issue** The methods for the mouse brain experiments are described, but the number of biological replicates and the details of the reference datasets used for label transfer are not specified.
- **Required correction** Specify the number of replicates and provide details on the reference datasets used for cell type annotation.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Clarity
- **Affected element** Discussion
- **Evidence pointer** Discussion
- **Issue** The discussion of the AS-C.Origami model's advantages over existing methods is brief and does not fully address potential limitations or alternative approaches.
- **Required correction** Expand the discussion to include a more critical comparison with existing methods and a more detailed consideration of the model's limitations.

- **Technical failings that need to be addressed before the case is established**
  - R1-M1: Lack of visible data to support throughput and quality claims.
  - R1-M2: Insufficient detail on AS-C.Origami model development and validation.
  - R1-M3: Lack of visible data to support biological findings.
  - R1-M4: Incomplete cost and time analysis.

- **Assessment against Nature-style criteria**
  - **Originality** The work is original in its combination of droplet-based microfluidics with long-read sequencing for single-cell epigenomics. The AS-C.Origami approach is also novel. However, the originality is somewhat tempered by the fact that the underlying methods (scNanoATAC-seq, scNanoCUT) have been previously described, and the novelty lies in the droplet-based adaptation.
  - **Scientific importance** The methods have the potential to be important for the field by making long-read single-cell epigenomics more accessible and scalable. The biological findings, particularly in the Pradet-Willi/Angelman syndrome region, could be of significant interest.
  - **Interdisciplinary readership** The work is likely to appeal to a specialized audience in genomics and epigenomics. The technical nature of the methods and the focus on specific biological applications may limit its appeal to a broader interdisciplinary readership.
  - **Technical soundness** The technical soundness cannot be fully assessed due to the lack of visible data and methodological details. The described methods are plausible, but the evidence is insufficient to confirm their validity.
  - **Readability for nonspecialists** The manuscript is written for a specialist audience and uses technical jargon without sufficient explanation. The abstract and introduction are particularly dense and may be challenging for nonspecialists.

- **Recommendation posture** Currently not established from the provided evidence. The manuscript describes a potentially valuable technical advance, but the lack of visible data and methodological details prevents a full evaluation of the claims. The authors should be encouraged to resubmit a revised version with all figures, supplementary data, and a more detailed methods section. If the data support the claims, the work could be of significant interest to the field.

## Risk / unsupported claims
- The claim of achieving ~5000 cells per experiment is unsupported without visible data.
- The claim of high data quality and reproducibility is unsupported without visible quality metrics.
- The claim that AS-C.Origami predicts allele-specific 3D structures at 10 kb resolution is unsupported without model details and validation data.
- The claim of identifying allele-specific regulatory elements in the mouse brain is unsupported without visible genomic data.
- The claim of cost-effectiveness is unsupported without a detailed cost analysis.
- The claim that the methods can be easily applied to other droplet-based platforms is plausible but not demonstrated.