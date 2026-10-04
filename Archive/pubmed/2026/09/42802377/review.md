## Review setup
- **Input scope** Full manuscript text, including abstract, results, discussion, methods, and supplementary figure references.
- **Assessment boundary** Scientific validity, methodological rigor, reproducibility, and interpretation of the presented findings. No assessment of editorial fit or publication venue suitability.
- **Shared manuscript claim summary** The authors present ChromAgeNet, a convolutional neural network trained on 3D DAPI-stained confocal images of murine hematopoietic stem cell (HSC) nuclei, to classify young versus aged cells. They report an AUROC of 0.77 ± 0.03 at the nucleus level, outperforming classical machine learning models trained on handcrafted chromatin features. They apply explainable AI techniques to identify chromatin entropy, peripheral heterochromatin, and chromatin condensates as predictive markers. As a proof of concept, they evaluate the model's ability to detect rejuvenation in aged HSCs treated with epigenetic drugs.
- **Visible evidence base** Abstract, full results narrative, discussion, methods, and references to supplementary figures and tables. No actual figures, tables, or supplementary materials were provided for direct inspection.
- **Missing materials affecting confidence** All figures, tables, and supplementary materials referenced in the text are absent. This includes Figure 1–5, Figure S1–S11, Table 1–2, Table S1–S9, and the associated data. Without these, quantitative claims cannot be independently verified.

## Reviewer
- **Overall assessment** The manuscript addresses a relevant and timely question: whether 3D chromatin architecture imaged with a simple DNA stain can serve as a predictive biomarker of hematopoietic stem cell aging. The authors combine a well-established imaging modality (DAPI) with modern deep learning and explainability methods, which is a sensible and potentially impactful approach. The reported performance (AUROC 0.77) is modest but plausible for a biological classification task with inherent heterogeneity. However, the manuscript as presented has several critical gaps. The absence of all figures and tables makes it impossible to assess data quality, model behavior, or the validity of the interpretability analyses. The comparison with classical machine learning models is described but not shown. The drug treatment proof-of-concept is intriguing but lacks detail on experimental design, sample sizes, and statistical rigor. The discussion is thoughtful and appropriately cautious, but several claims go beyond what the visible evidence supports. The technical approach is sound in principle, but the manuscript requires substantial revision and the inclusion of all supporting materials before the case can be considered established.

- **Who would be interested in the results, and why** Researchers in stem cell biology, aging research, and computational biology would find this work of interest. The idea that a simple, inexpensive stain combined with deep learning can extract age-related information from chromatin structure is attractive for translational applications, particularly in drug screening for rejuvenation therapies. The methodological framework, including the use of explainable AI, may also appeal to those developing image-based biomarkers in other cell types or tissues.

- **Major strengths**
  1. The research question is clinically and biologically relevant, addressing a gap in quantitative, image-based aging biomarkers.
  2. The use of 3D chromatin architecture as a predictive feature is conceptually novel and underexplored.
  3. The inclusion of explainable AI techniques is commendable and aligns with current best practices for interpretable deep learning in biology.
  4. The authors acknowledge limitations, including batch effects and the need for external validation, which reflects scientific maturity.
  5. The release of the dataset and code is a significant strength for reproducibility and community use.

- **Major Concerns**

- **Concern ID** R1-M1
- **Severity** Major
- **Blocking** Yes
- **Axis** Evidence completeness
- **Claim pointer** The manuscript claims that ChromAgeNet achieves an AUROC of 0.77 ± 0.03 at the nucleus level and outperforms classical machine learning models.
- **Evidence pointer** Results section, Figure 2, Figure 3, Table S1, Table S2, Table S3, Table S4, Table S5
- **Concern** All figures and tables are missing from the provided material. The central quantitative claims of the paper, including the AUROC values, the comparison with classical models, and the calibration metrics, cannot be verified. The text describes these results but provides no visual or tabular evidence. This is a fundamental issue that prevents any meaningful assessment of the model's performance or the validity of the comparison.
- **Why it matters** The core contribution of the paper is a quantitative claim about model performance. Without the actual data, figures, and tables, the reader cannot assess whether the reported AUROC is robust, whether the comparison with classical models is fair, or whether the calibration is adequate. This is a blocking issue for the scientific case.
- **Resolution test** Provide all figures and tables with clear captions. Include error bars, confidence intervals, and statistical tests for all performance comparisons. Show representative images of young and aged nuclei, example attention maps, and the distribution of scores.

- **Concern ID** R1-M2
- **Severity** Major
- **Blocking** Yes
- **Axis** Experimental design and confounding
- **Claim pointer** The manuscript claims that ChromAgeNet captures biological aging signals rather than technical artifacts, supported by the absence of significant associations with technical parameters.
- **Evidence pointer** Results section, Figure S8, Figure S11, Table S9
- **Concern** The dataset comprises images acquired using two different microscopes and three independent operators. The authors state that they verified the absence of significant associations between model predictions and technical parameters, but the details are not provided. The supplementary figures and tables that would support this claim are missing. Moreover, the text does not describe how the potential confounding by acquisition batch was addressed during model training, beyond data augmentation. If batch effects are not explicitly modeled or controlled, the model may be learning technical rather than biological differences.
- **Why it matters** Image-based deep learning models are highly susceptible to learning batch effects, especially when the number of biological replicates is limited. If the model is not robust to technical variation, its utility as a biological biomarker is severely compromised. The claim that the model captures biological aging requires rigorous demonstration that technical factors do not drive predictions.
- **Resolution test** Provide a detailed analysis of model performance stratified by acquisition batch, microscope, and operator. Show that the model generalizes across these technical variables. Consider including batch as a covariate in the analysis or demonstrating that the model's performance is consistent when trained and tested on data from different batches.

- **Concern ID** R1-M3
- **Severity** Major
- **Blocking** Yes
- **Axis** Validation and generalizability
- **Claim pointer** The manuscript claims that ChromAgeNet can serve as a phenotypic screening tool for rejuvenation therapies, based on the drug treatment proof-of-concept.
- **Evidence pointer** Results section, Figure 5, Table S6
- **Concern** The drug treatment experiment is described as a proof of concept, but the details are sparse. The number of cells, number of biological replicates, drug concentrations, treatment duration, and statistical comparisons are not provided. The claim that UNC0646 and IOX1 restore youthful scores to levels matching young HSCs is striking but cannot be evaluated without the underlying data. Moreover, the manuscript does not discuss whether the observed shifts in youthful scores are specific to the drugs' effects on chromatin or could reflect general cytotoxicity or other nonspecific effects.
- **Why it matters** The translational potential of ChromAgeNet as a drug screening tool is a major selling point of the paper. If the proof-of-concept is not rigorously designed and analyzed, the claim is not supported. The specificity of the response to chromatin-modifying drugs needs to be demonstrated with appropriate controls and statistical rigor.
- **Resolution test** Provide full experimental details for the drug treatment experiments, including sample sizes, concentrations, and statistical methods. Show dose-response relationships if available. Include appropriate controls, such as a drug with no known chromatin effects, to demonstrate specificity.

- **Concern ID** R1-M4
- **Severity** Major
- **Blocking** No
- **Axis** Interpretability and biological validity
- **Claim pointer** The manuscript claims that explainable AI techniques identify chromatin entropy, peripheral heterochromatin, and chromatin condensates as predictive markers of aging.
- **Evidence pointer** Results section, Figure 4, Figure S6, Table S8
- **Concern** The interpretability analysis is described qualitatively. The text mentions that attention maps highlight the nuclear envelope in young cells and large DAPI blobs in aged cells, but no quantitative validation is provided. The claim that these features are "predictive markers" requires a more rigorous analysis, such as correlating attention values with measured chromatin features or demonstrating that these features are necessary and sufficient for the model's predictions. The choice of occlusion sensitivity over other methods is justified by fidelity scores, but the details of this comparison are not shown.
- **Why it matters** The biological interpretability of the model is a key contribution. If the identified features are not robustly validated, the claim that the model learns biologically meaningful patterns is weakened. The field is increasingly demanding rigorous validation of explainability results, not just qualitative visual inspection.
- **Resolution test** Provide quantitative analysis of attention maps, such as the distribution of attention values across nuclear compartments, and correlate them with independent measurements of chromatin features. Validate the identified markers by perturbing them in the images and showing that model predictions change accordingly.

- **Concern ID** R1-M5
- **Severity** Major
- **Blocking** No
- **Axis** Statistical rigor and reporting
- **Claim pointer** The manuscript reports performance metrics with standard deviations and confidence intervals across cross-validation folds.
- **Evidence pointer** Results section, Tables S1, S2, S5
- **Concern** The text reports mean ± standard deviation for several metrics, but the number of folds, the variance between folds, and the statistical significance of differences between models are not reported. The comparison between ChromAgeNet and classical models is described as "outperforming," but no statistical test is mentioned. The manuscript would benefit from a more rigorous statistical framework, including confidence intervals for the AUROC and tests for the significance of the difference between models.
- **Why it matters** The claim that deep learning outperforms classical machine learning is a central finding. Without statistical tests, the reader cannot determine whether the observed difference is meaningful or within the range of random variation. This is particularly important given the modest absolute performance (AUROC 0.77).
- **Resolution test** Report the full distribution of performance metrics across folds. Use appropriate statistical tests (e.g., paired tests across folds) to compare models. Report confidence intervals for all key metrics.

- **Minor Comments**

- **Concern ID** R1-m1
- **Severity** Minor
- **Axis** Clarity of methods
- **Affected element** Image preprocessing and resampling
- **Evidence pointer** Methods, Image Preprocessing and Segmentation
- **Issue** The text states that images were resized to 0.05 μm resolution in all dimensions, but the original acquisition resolution is not specified. The interpolation method used for Z-axis resampling is not described.
- **Required correction** Specify the original acquisition voxel size and the interpolation algorithm used. Justify the choice of 0.05 μm as the target resolution.

- **Concern ID** R1-m2
- **Severity** Minor
- **Axis** Data description
- **Affected element** Dataset composition
- **Evidence pointer** Results, Table 1, Table 2
- **Issue** The text mentions 1,229 3D images, but later states 1,848 images after quality control. The relationship between these numbers is unclear. The number of mice per age group and the sex distribution are mentioned but not fully detailed.
- **Required correction** Clarify the number of images at each stage of the pipeline. Provide a complete breakdown of the dataset by age group, sex, and experimental batch.

- **Concern ID** R1-m3
- **Severity** Minor
- **Axis** Terminology
- **Affected element** "Youthful score"
- **Evidence pointer** Results, Figure 2
- **Issue** The term "youthful score" is used throughout, but its exact definition and range are not explicitly stated. It is implied to be a calibrated probability, but this should be stated clearly.
- **Required correction** Define the youthful score explicitly as a calibrated probability and state its range.

- **Concern ID** R1-m4
- **Severity** Minor
- **Axis** Discussion of limitations
- **Affected element** Generalizability to human cells
- **Evidence pointer** Discussion
- **Issue** The discussion mentions that translation to human samples will require model adaptation, but this point is not elaborated. Given the potential clinical relevance, a more detailed discussion of the challenges and possible strategies for human translation would be valuable.
- **Required correction** Expand the discussion on human translation, including anticipated differences in chromatin organization and imaging characteristics.

- **Concern ID** R1-m5
- **Severity** Minor
- **Axis** Reproducibility
- **Affected element** Code and data availability
- **Evidence pointer** Data Availability Statement
- **Issue** The code repository and data are mentioned, but the manuscript does not specify the software environment, dependencies, or instructions for reproducing the results.
- **Required correction** Provide a detailed description of the software environment, including package versions, and clear instructions for running the code.

- **Technical failings that need to be addressed before the case is established**
  1. Missing all figures and tables, which are essential for verifying the central claims.
  2. Insufficient detail on the drug treatment experiment, including sample sizes and statistical analysis.
  3. Lack of explicit control for batch effects in the model training and evaluation.
  4. No statistical tests for the comparison between ChromNet and classical models.
  5. The interpretability analysis lacks quantitative validation.

- **Assessment against Nature-style criteria**
  - **Originality**: The application of deep learning to 3D chromatin images for aging prediction is a novel contribution. While image-based deep learning is not new, the specific focus on HSC aging and the use of a simple DNA stain is a fresh angle. The work is original in its specific combination of methods and biological question.
  - **Scientific importance**: The question of quantifying biological aging is of high importance. If validated, this approach could provide a cost-effective and scalable biomarker for aging and rejuvenation studies. The potential for drug screening adds translational significance. However, the modest performance and lack of external validation temper the immediate impact.
  - **Interdisciplinary readership**: The work bridges stem cell biology, aging research, and computational biology. It would appeal to a broad audience interested in biomarkers, deep learning applications in biology, and the biology of aging. The use of explainable AI adds an element that could interest method developers.
  - **Technical soundness**: The technical approach is generally sound in principle. The use of cross-validation, calibration, and explainability methods is appropriate. However, the lack of visible data and the potential for batch effects are significant concerns. The statistical rigor needs improvement.
  - **Readability for nonspecialists**: The manuscript is generally well-written and accessible. The abstract and introduction are clear. The methods section is technical but appropriate for the target audience. The discussion is readable and provides context. However, the absence of figures makes it difficult for any reader to follow the results.

- **Recommendation posture** Supportive if technical concerns are resolved. The core idea is promising and the methodological framework is appropriate. However, the manuscript in its current form does not provide sufficient evidence to support the central claims. The missing figures and tables, the lack of statistical rigor, and the potential for batch effects are blocking issues. With substantial revision, including the full presentation of data, a more rigorous experimental design for the drug treatment study, and a thorough analysis of potential confounders, this work could make a valuable contribution.

## Risk / unsupported claims
- The claim that ChromAgeNet outperforms classical machine learning models is unsupported without the actual comparison data and statistical tests.
- The claim that the model captures biological aging rather than technical artifacts is not fully supported without a detailed analysis of batch effects.
- The claim that chromatin entropy, peripheral heterochromatin, and chromatin condensates are predictive markers is not quantitatively validated.
- The claim that the drug treatment proof-of-concept demonstrates the model's utility for rejuvenation screening is not supported without full experimental details and controls.
- The claim that the model is "interpretable" is only partially supported; the interpretability analysis is qualitative and lacks rigorous validation.
- The generalizability of the model to other datasets, laboratories, or species is not demonstrated and remains an open question.