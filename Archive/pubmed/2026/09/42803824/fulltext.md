# CTCF-FXN regulatory axis plays critical roles in clinical assessments and disease progression of primary open-angle glaucoma


## Supplementary Information
  The online version contains supplementary material available at https://doi.org/10.1007/s00109-026-02717-2.


## Introduction
  Glaucoma is the leading cause of irreversible blindness and visual impairment worldwide [1]. As a complex neurological degenerative disease, primary open-angle glaucoma (POAG) is the most prevalent subtype of glaucoma, accounting for 69.3% of the total glaucoma patients. POAG is a heterogeneous group of progressive optic neuropathies characterized by degeneration of the optic nerve, loss of retinal ganglion cells and corresponding visual field loss [2]. So far, the main treatment of POAG is control pathologically high IOP through medications and surgery [3]. However successful reduction of IOP does not entirely delay or prevent progressive apoptosis of RGCs. Thus, finding and controlling potential pathogenic factors are essential to improve glaucoma prognosis.

  Oxidative stress refers to the disequilibrium of redox homeostasis, which ultimately leads to reactive oxygen species (ROS) outcompeting antioxidation defensive process. It is well established that oxidative stress and excessive ROS play critical roles in the pathogenesis of ophthalmologic diseases, especially for the optic nerve degeneration diseases well represented by glaucoma [4]. The action mechanisms of oxidative stress in glaucoma are multifaceted and complex. On one hand, the excess of ROS leads to direct cytotoxic stimulus to RGCs, thereby inducing programmed cell death (PCD), such as apoptosis, autophagy and ferroptosis [5]. On the other hand, ROS is able to increase the neuronal susceptibility to damage as a second messenger [6]. Moreover, the involvements of ROS in DNA damage, the accumulation of advanced glycation end products (AREs), and the disordered autoimmune response together govern the progression of glaucoma [7]. Evidently, digging deep into the molecule mechanisms of oxidative stress in glaucoma is promising to conquer this visual loss disease and bring gospel to patients.

  With the development of high throughput sequencing technology, efficient identification of core regulators in glaucoma has emerged as an available access [8]. Among numerous oxidative stress molecules, Frataxin (FXN) finally acted as the protagonists of our research. FXN belongs to the FRATAXIN family that is responsible for regulating mitochondrial iron transport and respiration [9]. Despite its dominant status in the regulation of oxidative stress, no previous studies have clarified its biofunctions in glaucoma. Herein, FXN was proved to be a biomarker of clinical and immune status in POAG. Meanwhile, it suppressed POAG progression through CTCF-mediated transcriptional regulation. Our findings will contribute to understanding glaucoma biology and provides new insights into glaucoma treatments.


## Materials and methods

### Data source
  Five datasets from the GEO database providing transcriptomic and clinical information were included in this study, and their detailed characteristics and sample information are summarized in Supplementary Table 1. GSE9963 (n = 81), derived from human optic nerve head astrocytes, was selected as the primary discovery cohort due to its relatively large sample size. All oxidative stress-related gene screening, WGCNA, and machine learning analyses were performed based on GSE9963. The remaining GEO datasets were used as independent validation cohorts. All transcriptome data was standardized by log2 (FPKM + 1) transformation.


### Oxidative stress related (OSR) gene set
  GeneCards (https://www.genecards.org/) and MSigDB databases (https://www.gsea-msigdb.org/gsea/msigdb) were applied to establish an OS gene set (n = 885) [10, 11]. Selected genes from GeneCards database fulfilled the condition that their correlation coefficients with oxidative stress process > = 10. Three gene sets from MSigDB database were also involved in the constructing process of OS gene set. The detailed information of these gene sets was shown in Supplementary Table 2. The biofunction of OS gene set was tested via MetaScape database (http://metascape.org/) [12].


### Weighted gene co-expression network analysis (WGCNA)
  Multiple R packages were employed to conduct WGCNA, including ‘WGCNA’, ‘MatrixStats’, ‘Hmisc’, ‘Foreach’, ‘DoParallel’, ‘Fastcluster’ and ‘dynamicTreeCut’. Similar modules were merged at the cut height of 0.15. The optimal power value was determined by both model fit threshold and connectivity. The former set as 0.8, the latter was as high as possible.


### Machine learning algorithms
  Lasso regression analysis and support vector machine recursive feature elimination (SVM-RFE) were performed for essential gene screening using ‘glmnet’ and ‘KeBABS’ R packages [13]. These approaches were both based on the 10-fold cross-validation scheme.


### Bioinformatic analyses of FXN
  Biological enrichment analyses of FXN-related genes were conducted via DAVID tool [14], including biological process (BP), molecular function (MF) and cellular component (CC). FXN-related genes referred to the genes with the expressive Pearson coefficients > = 0.8. The subcellular location and protein structure of FXN were explored using Hum-mPLoc 3.0 online tool [15] and AlphaFold database (https://alphafold.ebi.ac.uk/) [16], respectively.

  Diagnostic accuracy was assessed via receiver operating characteristic curve (ROC). Immune effects of FXN were investigated through CIBERSORT and ssGSEA methods [17, 18], including the infiltration levels of 21 immune cells and the activities of five glaucoma-related immune signaling pathways.


### Diagnostic meta-analysis
  The accuracy of FXN for diagnosing glaucoma across four GEO datasets (GSE9963, GSE27276, GSE2378, GSE101727 and GSE45570) was evaluated using Review Manager 5.2 software (The Cochrane Collaboration, Oxford, UK). This meta-analysis was based on Mantel-Haenszel method and fixed effect model. The heterogeneity was assessed by I2 value and the overall effectiveness was tested by Z-test. The funnel plots were used to detect the bias risk.


### Gene set enrichment analysis (GSEA)
  GSEA was utilized to investigate the metabolic effects of FXN in glaucoma. Metabolic gene sets were obtained from MSigDB database. Their detailed descriptions were shown in Supplementary Table 3. Phenotype labels were set as high-FXN expression samples versus low-FXN expression samples. Number of permutations was set as 1000. There was no collapse in gene symbols.


### Prediction of transcriptional regulatory mechanisms
  Potential transcription factors (TFs) for regulating FXN were predicted using hTFtarget (http://bioinfo.life.hust.edu.cn/hTFtarget#!/) [19], the “GeneHance” module in GeneCards database [20], and KnockTF database (https://bio.liclab.net/KnockTF/) [21]. The motif sequences of TFs and the predictive binding sites were obtained from JASPAR database (https://jaspar.genereg.net/) [22].


### Cells and in vitro model
  Mouse retinal ganglion cells (RGCs) were applied to conduct further biological experiments. These cells were purchased from the Procell Company (CP-M122, Wuhan, China) and were incubated in a specialized medium (Procell, CM-M122) containing 10% fetal bovine serum (FBS), 1% penicillin-streptomycin (P/S) and cell growth additives. FXN amplified vector (OE-FXN) and specific short hairpin RNA for knocking down FXN (sh-FXN) were designed and synthesized by GenePharma (Shanghai, China). The corresponding specific sequences were presented in Supplementary Table 4.

  A widely utilized cell model focusing on oxidative stress injury was employed to simulate the initiation of glaucoma, which has been applied successfully in numerous glaucoma research [23–27]. The modeling procedure closely resembled the previous strategy [23–27], wherein RCGs were treated by a 12-hour incubation with 200 µM H2O2.


### RT-PCR
  The total RNA was extracted using TRIzol Reagent (TakaRa, Japan), and its purity was assessed via an A260/A280 ratio (Nanodrop 2000 spectrophotometer). PrimeScript RT Reagent Kit (TaKaRa, Japan) was used for reverse transcription. RT-qPCR reaction was monitored using SYBR-Green PCR Reagent (Takara, Japan) and performed on the ABI Prism 7900 sequence detection system. GAPDH was used as an internal reference. The relative gene expression was calculated based on the 2-ΔΔCT method. The primer sequences were shown in Supplementary Table 5.


### Western blot
  Western blot assays were performed as previous research [28]. Briefly, transfected cells were lysed on ice by RIPA buffer (Beyotime, China). The protein concentration was measured using a BCA kit (Beyotime, China). Extracted proteins were separated by 10% SDS-PAGE (Applygen, China) and transferred to PVDF membranes (Absin, China) through electrophoresis. The membranes were sealed by 5% skim milk and were washed by TBST buffer (Absin, China). After incubation with primary and secondary antibodies in turn, protein blots were detected using BeyoECL plus solution (Beyotime, China). All antibodies were purchased from Abcam scientific (Shanghai, China). The primary antibodies were as follows: mouse monoclonal anti-FXN (1:1000, ab113691), anti-CTCF (1:1000, ab37477) and anti-GAPDH antibodies (1:2500, ab9485). The secondary antibody was goat-anti mouse IgG-HRP secondary antibody (1:2000, ab205719).


### EdU assay
  EdU assay was conducted for assessing the viability of RGCs. The cells were spread in 96-well plates at a density of 1 × 103 cells per well. An EdU working regent was prepared by diluting EdU regent (Beyotime, China) with cell culture medium (1:500). Cells were incubated with EdU working regent and equal volumes of serum-free medium for 2 h. Then, cells were fixed in 4% paraformaldehyde for 15 min and were incubated with Click Additive Solution (Beyotime, China) for 30 min in darkness. Nuclei were labeled using DAPI solution. EdU-positive cells were observed under a fluorescence microscope.


### CCK8 assay
  The viability of RGCs was also evaluated by CCK8 assay. Cells were added in 96-well plates at a density of 4 × 104 cells each well. Cells were further incubated with CCK-8 reagent for 1 h. Cell viability was measured according to the absorbance value of each well at 450 nm using a microplate reader.


### Intracellular ROS detection
  Cells were seeded in 12-well plates with a density of 2 × 105 per well. In each experimental group, cells were incubated with BODIPY-C11(581/591) (ABclonal Biotech company, Wuhan, China) for 1 h at 37 °C. A 300 µL cell suspension was prepared using PBS and 5% FBS. The proportion of cells whose fluorescence emission peak shifted from 590 nm to 510 nm was measured via flow cytometry detection, which enabled the comparison of ROS levels between groups.


### TUNEL assay
  The TUNEL procedure was similar as described previously [29]. Briefly, cells were suspended with PBS and were fixed with 4% paraformaldehyde at 4 °C for 25 min. Then, cells were incubated with Proteinase K for 5 min. Cells were moved into 4-well chamber slide and were incubated with TUNEL reaction mixture (Absin, China) in dark for 1 h. Nucleus was stained with DAPI solution (Beyotime, China) at 37 °C for 5 min. The results were observed by fluorescence microscopy.


### Apoptosis detection
  Cells were collected using trypsin and were resuspended with PBS. The cell suspension was centrifuged at 1000 g for 5 min. Then, cells were resuspended with Annexin binding buffer (Beyotime, China), and were incubated with Annexin V-PE and Annexin V–FITC (Beyotime, China) in dark for 20 min. Flow cytometric assays were performed to detect above samples.


### Chromatin immunoprecipitation (ChIP)
  Cells were lysed by ultrasonication and were crosslinked with BeyoChIP™ ChIP Assay Kit (Beyotime, China). DNA was further broken into 100–500-bp fragments using ultrasound. DNA immune complex was pull down by antibody targeting CTCF. Following two washes with elution buffer, eluted DNA was de-crosslinked using proteinase K in high salt conditions. Purified DNA was amplified by PCR. Electrophoresis on agarose gels was used to identify target DNA bands.


### Statistical analysis
  All statistical analyses were performed using GraphPad Prism (Version 8.0). Continuous variables were compared across different experimental groups using the unpaired T test. Three independent cell experiments were conducted. Statistical significance was defined as a P-value less than 0.05.


## Results

### FXN is identified as the critical oxidative stress gene in the pathogenesis of POAG
  The flowchart of this study was shown in supplementary Fig. 1. Relying on GeneCards (n = 567) and MSigDB databases (n = 485), a comprehensive OS gene set (n = 885) was constructed (Fig. 1A). The PPI network of above OS genes was depicted in Fig. 1B. Functional enrichment analysis showed that the constructed OS gene set was significantly enriched in oxidative stress-related biological processes and pathways (Fig. 1C). Considering the scale independence and mean connectivity, the optimal power was selected as 6 (Fig. 1DE). WGCNA analysis revealed that most modules were related to glaucoma sample type (Fig. 1FG). Among that, red and turquoise modules were screened out in virtue of their higher clinical correlations (Fig. 1G). 14.1% (125/885) OS genes differentially expressed between POAG and normal samples (Fig. 1H). Interestingly, up-regulated and down-regulated OS genes exhibited similar functional enrichments (Fig. 1IJ). Though Lasso regression and SVM-RFE algorithms, some potential critical genes in POAG onset and progression were screened out based on 125 OS DEGs (Fig. 1KL). Finally, the intersection of three bioinformatic methods was determined, FXN and CYP1B1 were hypothesized to exert pivotal functions in POAG development (Fig. 1M).

  Fig. 1Identification of the critical oxidative stress related genes in the pathogenesis of POAG. (A) Construction of OS gene set based on GeneCards and MSigDB database (n = 885). (B) PPI network of OS genes. (C) Function enrichment analysis of the OS gene set using Metascape database. (D) Selection of the optimal power value in WGCNA analysis based on their model fits. (E) Selection of the optimal power value in WGCNA analysis based on their mean connectivity. (F) The process of similar modules merging (Cut height = 0.15). (G) The correlations between different modules and clinical features of POAG based on WGCNA analysis. (H) DEGs between normal and POAG samples in GSE9963 dataset (The absolute value of Log2FC ≥ 0.5). (I) GO enrichment analysis of up-regulated DEGs. (J) GO enrichment analysis of down-regulated DEGs. (K) The result of Lasso regression analysis. (L) The result of SVM-RFE analysis. (M) Intersection part between WGCNA, Lasso regression and SVM-RFE analyses. PPI, protein‑protein interaction


### FXN exhibits potential diagnostic value in POAG
  Although FXN and CYP1B1 were both upregulated in glaucoma samples compared to normal samples (Fig. 2AB), FXN showed a higher ability to discriminate POAG samples from normal controls than CYP1B1 based on ROC analysis (Fig. 2CD, AUC = 0.700 vs. 0.945). Therefore, FXN was selected for further investigation. Functional enrichment analysis of FXN-associated genes revealed significant enrichment in multiple biological processes and signaling pathways, including the PI3K-AKT signaling pathway, regulation of cell development, and DNA-binding transcription activator activity (Fig. 2EF). FXN expression levels were associated with sample type, but not with race, gender, and age of POAG patients (Fig. 2G). The main subcellular localization of FXN was cytosol and mitochondrion via the bioinformatic prediction (Fig. 2HI). Moreover, for assisting medicine synthesis, the three-dimensional protein structure of FXN was obtained from AlphaFold database (Fig. 2J).

  In the four independent validation datasets, FXN expression was consistently elevated in POAG samples and showed potential diagnostic value, with AUC values ranging from 0.708 to 0.946 (Fig. 2K-S). A diagnostic meta-analysis further demonstrated that elevated FXN expression was significantly associated with POAG status, with an overall odds ratio of 6.35 (Fig. 2T).

  Fig. 2Expression pattern and diagnostic value of FXN in POAG. (A-B) Expressive differences of two OS candidate genes between normal and POAG samples in GSE9963 dataset (CYP1B1 and FXN). (C-D) Diagnostic accuracy of two OS candidate genes in GSE9963 dataset. (E) KEGG enrichment analyses of FXN-related genes. (F) GO enrichment analyses of FXN-related genes. (G) Clinical heatmap of FXN in GSE9963 dataset. (H-I) Subcellular localization of FXN. (J) Protein structure of FXN based on AlphaFold database. (K-N) Expressive differences of FXN between normal and POAG samples in four independent validation datasets (GSE2378, GSE27276, GSE45570, and GSE101727 datasets). (O-R) Diagnostic accuracy of FXN in four validation datasets. (S) AUC values of FXN in all five GEO datasets. (T) Diagnostic meta-analysis evaluating the association between FXN expression and POAG status across five GEO datasets. AUC, area under curve; *P<0.05; **P<0.01; ***P<0.001; NS, not significant


### Association between FXN expression and immune-related features in POAG
  The abnormality of immunological processes has adequately confirmed to mediate glaucoma progression [30]. Herein, CIBERSORT analyses suggested that the POAG samples with different FXN expressive levels exhibited differences in estimated immune cell abundance (Fig. 3A-E). Take GE9963 for instance, the infiltration levels of two macrophage subtypes (M1 and M2) were significantly decreased when high FXN expression appeared in POAG samples (Fig. 3A). The potential roles of these immune cell populations in POAG pathogenesis have been summarized in Supplementary Table 6, providing possible explanations for the association between FXN expression and immune-related features [31–33].

  Through ssGSEA analyses, several immune-related signatures were enriched in POAG samples with high FXN expression in GSE9963 dataset, such as ‘APC function’, ‘CCR interaction’, and ‘Inflammation-promoting’ (Fig. 3F). Nonetheless, above tendency was rarely observed in other datasets (Fig. 3G-J). Collectively, FXN expression was correlated with immune-related signatures in POAG, although further experimental validation is required to determine its impact on the immune microenvironment.

  Fig. 3Immune-related characteristics associated with FXN expression in POAG. (A-E) Differences in estimated immune cell abundance between high- and low-FXN expression groups. (F-J) Differences in immune-related pathway scores between high- and low-FXN expression groups. APC, antigen presentation cell; CCR, chemokine and chemokine receptor; *P<0.05; **P<0.01; ***P<0.001; NS, not significant


### FXN is associated with metabolic signatures related to glycolysis and pyruvate metabolism
  Given that the onset of glaucoma is often accompanied by the metabolic reprogramming, the potential linkages between FXN and multiple metabolic processes were also investigated. GSEA analyses revealed that several metabolic gene sets related to pyruvate metabolism, glycolysis, and cholesterol metabolism were significantly enriched in the samples with high FXN expressions (Fig. 4A-D). Nevertheless, only one glutamine dataset was significantly enriched in GSE45570 cohort (Fig. 4D). According to previous research (Supplementary Table 6), the enrichment of glycolysis- and pyruvate metabolism-related gene sets observed in samples with high FXN expression may indicate a potential association between FXN and metabolic alterations in POAG.

  Fig. 4Association between FXN expression and multiple metabolic pathways. GSEA analyses showing the enrichment of pyruvate (A), glycolysis (B), cholesterol (C), and glutamine (D) metabolism-related gene sets according to FXN expression in five GEO datasets. Pie charts showed the proportion of the metabolic gene sets with statistical significance. NES, normalized enrichment score; Sig, statistically significant; NS, not significant


### FXN protects R28 cells from H2O2-induced oxidative stress injury
  A H2O2-induced model was applied to simulate the disease process of POAG in vitro. Interestingly, although FXN was upregulated in POAG sample through previous bioinformatic analyses (Fig. 2B), H2O2 intervention significantly decreased FXN expression in R28 cells (Fig. 5AB). Therefore, it was speculated that FXN contributed to RGCs protection. Prior to further investigation, OE-FXN and sh-FXN vector tools were determined to effectively manipulate FXN expressions via PCR and Western blot tests (Fig. 5CD). CCK8 assays manifested that H2O2 intervention significantly inhibited RGCs survival, and FXN overexpression could reduce this degradation of cell viability, whereas FXN deletion aggravated this process (Fig. 5E). EdU assay further supported above results (Fig. 5FG). Clearly, FXN favored maintaining the RGCs survival in glaucoma occurrence. Furthermore, to investigate whether FXN regulates endogenous antioxidant defense mechanisms, the expression levels of NRF2, HO-1, and SOD1 were examined by western blot assays. Compared with the corresponding control groups, FXN knockdown significantly decreased the expression of NRF2, HO-1, and SOD1, whereas FXN overexpression markedly increased their expression levels (Fig. 5H). These findings suggested that FXN may contribute to cellular protection by enhancing antioxidant defense responses under oxidative stress conditions.

  Fig. 5FXN protects R28 cells against H2O2-induced oxidative stress injury. (A-B) The alterations of FXN expressions in H2O2 model. (C-D) Transfection efficiency of multiple FXN vectors. (E) The effects of FXN on the viability of RGCs (R18 cells) based on CCK8 assays. (F) The effects of FXN on the viability of RGCs (R18 cells) based on EdU assays. (G) The quantitative analyses of EdU assays. (H) The effects of FXN overexpression and knockdown on the expression levels of antioxidant-related proteins, including NRF2, HO-1, and SOD1, determined by western blot assays. H2O2 group means the POAG in vitro model; OE-FXN, FXN overexpression; sh-FXN, short hairpin targeting FXN; *P<0.05; **P<0.01; ***P<0.001; NS, not significant


### Overexpression of FXN impedes ROS accumulation and apoptosis of RGCs
  Oxidative stress injury (OSI) is the core link for driving glaucoma. In view of this context, the alterations of ROS levels on different FXN expressions were determined via flow cytometry. Compared to control group, H2O2 treatment markedly exacerbated ROS accumulation (Fig. 6A). Meanwhile, overexpression of FXN led a significantly relief on ROS increment caused by H2O2, whereas FXN deletion moderately accelerated ROS accumulation (Fig. 6A). Flow apoptotic detection revealed that H2O2 modeling could induce RGCs apoptosis especially cell later apoptosis (Fig. 6BC). Overexpression of FXN defended against this H2O2-induced apoptosis, inversely, silencing FXN further accelerated cell apoptosis (Fig. 6BC). TUNEL assays were also in accord with above tendency. The rate of TUNEL positive cells in H2O2 group was significantly higher than that in control group, but that in FXN-overexpression group obviously decreased compared to H2O2 group (Fig. 6DE). Collectively, FXN was able to protect RGCs from oxidative damage and cell apoptosis.

  Fig. 6FXN overexpression protects RGCs from oxidative damage and apoptosis. (A) The effects of FXN on intracellular ROS levels. (B) The effects of FXN on cell apoptosis based on flow cytometric detection. (C) The quantitative analyses of flow cytometric detection. (D) The effects of FXN on cell apoptosis based on TUNEL assays. (E) The quantitative analyses of TUNEL assays. **P<0.01; ***P<0.001


### CTCF is the potential transcriptional factor of FXN
  Mechanistically, the transcriptional regulatory mode of FXN was in-depth explored. The potential transcriptional factors (TFs) of FXN were predicted by GeneCards and hTFtarget databases, respectively. Their intersection was obtained using a Venn diagram, four candidates were identified including MAX, YY1, RAD21 and CTCF (Fig. 7A). All candidates differentially expressed in glaucoma samples (Fig. 7B). The sequencing data from KnockTF database revealed that only knockdown of MAX, YY1 and CTCF elicited an obvious reduction in FXN expressions (Fig. 7C). Moreover, CTCF and MAX appeared positive correlations with FXN, but a negative expressive association was observed in YY1 (Fig. 7D-F). PCR tests determined that only silencing CTCF could downregulate FXN expression in R28 cells whereas other two candidates failed (Fig. 7G). As the final potential TF of FXN, its motif feature was obtained from JASPAR database, which contained multiple CG bases (Fig. 7H). It was also informed that the coding strand of FXN was located on the forward strand of chromosome 9th through NCBI database (Fig. 7I).

  Fig. 7CTCF is the potential transcription factor of FXN. (A) Four candidate TFs are predicted using GeneCards and hTFtarget public databases. (B) The expressive differences of four candidate TFs between normal and POAG samples in GSE9963 dataset. (C) The expressive alterations of FXN upon silencing each candidate TF based on the public sequencing data from KnockTF database. (D-F) The expressive correlations between FXN and candidate TFs in GSE9963 dataset. (G) The expressive alterations of FXN when silencing three candidate TFs based on PCR assays. (H) The sequence feature of CTCF motif based on JASPAR database. (I) FXN is located on the sense strand of chromosome 9 (NCBI Gene database). ***P<0.001


### CTCF regulates FXN under oxidative stress
  OE-CTCF and sh-CTCF could positively manipulated FXN expressions in R28 cells, as determined by western blot assays (Fig. 8A). Consistent with FXN expressive alterations (Fig. 7B), CTCF expressions were also significantly decreased in H2O2 model compared to control group (Fig. 8BC). Furthermore, the binding sites between CTCF and the promoter region of FXN were predicted using JASPAR database, the binding sites with top 4 predicted score were selected for further validation (Fig. 8D). ChIP assays revealed that the immune complex pulled down by magnetic beads contained a plethora of the sequences of predicted site 3, but not that of other predicted sites (Fig. 8E). This strongly argued that CTCF could bind to the promoter region of FXN which was localized on the 1797th base to 1815th base upstream of FXN transcription start site (TSS).

  EdU assays indicated that overexpression of CTCF maintained the viability of R28 cells upon H2O2 treatment, which was similar to FXN functions (Fig. 8F). More importantly, FXN deletion weakened the protective effects of CTCF on R28 cells (Fig. 8F). The rate of EdU positive cell in co-transfected group (OE-CTCF + sh-FXN) were significantly lower than that in mono-transfected group (OE-CTCF) (Fig. 8G). Analogously, overexpression of CTCF also alleviated ROS accumulation and cell apoptosis brought by H2O2 intervention, however, simultaneously silencing FXN reversed above effects to some extent (Fig. 8HI and Supplementary Fig. 2). Therefore, these findings demonstrated that CTCF protected R28 cells against H2O2-induced injury, at least in part, through transcriptional activation of FXN. Considering that CTCF is a global transcription factor, we further explored whether CTCF may regulate additional oxidative stress-related genes in POAG. By intersecting the 125 oxidative stress-related differentially expressed genes with predicted CTCF target genes obtained from the hTFtarget database, 79 overlapping genes were identified (Supplementary Fig. 3). These results suggested that CTCF may participate in a broader oxidative stress-related transcriptional regulatory network in POAG.

  Fig. 8CTCF transcriptionally activates FXN and protects R28 cells against H2O2-induced injury. (A) The effects of CTCF on FXN expressions based on Western blot assays. (B-C) The alterations of CTCF expressions in H2O2 model. (D) The binding sites with top 4 predicted scores based on JASPAR database. (E) The results of ChIP assays combination with agarose electrophoresis. (F) FXN deletion could reverse the effects of CTCF overexpression on cell survival (EdU assay). (G) The quantitative analyses of EdU rescue assays. (H) FXN deletion could reverse the effects of CTCF overexpression on intracellular ROS levels. (I) FXN deletion could reverse the effects of CTCF overexpression on cell apoptosis (TUNEL assay). *P<0.05; **P<0.01; ***P<0.001


## Disscusion
  Globally, glaucoma is the leading cause of irreversible blindness, with over 11.1 million people affected world-wide [1]. Due to the damage of optic nerve and retinal nerve fiber layer, glaucoma commonly presented chronic visual loss [2]. Oxidative stress injury and the aberrant inflammation and autoimmune have been regarded as the culprit of above visual degeneration [4]. As the predominant type of glaucoma, POAG treatment highly relies on IOP control, such as medication well represented by beta adrenergic receptor blockers [34]. Nevertheless, existing therapeutic approaches could not completely reverse the course of this disease. Therefore, in-depth exploring the molecular mechanisms of POAG, especially OS related mechanisms will be promising to solve this clinical dilemma.

  Oxidant and antioxidant imbalance is a critical pathomechanism found in many ocular neurodegenerative diseases including glaucoma [4]. As the core effector of OS, ROS mediates POAG progression through multiple mechanisms. On one hand, ROS is able to attack polyunsaturated fatty acids on cell membranes, thus disrupting the integrity of cell membranes [35]. On the other hand, ROS can lead chromosomal and DNA lesions through targeting the nitrogenous bases and sugar-phosphate backbones in DNA [36]. Additionally, ROS triggers several programmed cell death (PCD), such as apoptosis, autophagy, and ferroptosis [35]. Herein, it was determined that overexpression of FXN obviously reduced ROS level in RGCs and inhibit cell apoptosis. This highlighted the pivotal effects of FXN in cellular redox homeostasis. In fact, Friedreich’s Ataxia (FRDA), a neurodegenerative disorder disease closely associated with ROS surge, is caused by FXN mutation, which impedes FXN transcription and inhibits its expression [37]. This evidence also witnessed the bridge between FXN and oxidation regulation.

  There have been some studies developing biomarkers for assessing disease status of POAG. Through a series of bioinformatic analyses, FXN exhibited excellent diagnostic performance and assisted us to acquire a better appreciation of clinical situations. In our view, FXN possessed some non-negligible preponderance over other biomarkers. For instance, Feng J et al. have identified LCN2, MAOA, HBB, PAX6, FN1 and CREB1 as the hub genes responsible for mediating glaucoma [38]. However, their diagnostic accuracy and clinical value were not investigated in detail. Huang X et al. have attempted to uncover new POAG-related genes using sequencing data [39]. Regrettably, their findings were not validated by experimentations which was well addressed in our study. In the present study, a comprehensive omics analysis focusing FXN was performed including expression pattern, diagnostic performance, immune-related features, and metabolism-related signatures. Meanwhile, its biofunctions and transcriptional regulatory mechanisms were also determined. These findings provide further evidence supporting the potential clinical value of FXN in POAG.

  As a mitochondrial protein, FXN mediates the mitochondrial iron transport and respiration [40]. A typical disease originating from FXN disorder is Friedreich ataxia that is due to the GAA repeat homozygous expansion of FXN and finally leads to a neurodegeneration [41]. Some pieces of available evidence pointed the potential associations between FXN and oxidative stress, which led us to involuntarily speculated FXN functions in POAG. For instance, FXN deficiency can control endothelial senescence and activity through mediating the cellular response to hypoxia and DNA damage [42]. In FRDA model, the genetic loss of FXN disrupts mitochondrial respiration and aggravates ROS accumulation [43]. In the present study, FXN deletion was also proved to elevate the cellular ROS level, and the overexpression of FXN contributed to maintain the survival of RGCs under disease conditions. These findings highlighted the critical roles of FXN in antioxidant damage and cytoprotection. Similarly, Schultz R et al. found that high FXN expression protected RGCs after acute ischemia reperfusion [44]. Furthermore, our additional experiments revealed that FXN overexpression increased the expression of antioxidant-related proteins, including NRF2, HO-1, and SOD1, whereas FXN knockdown resulted in their decreased expression. These findings suggest that FXN may enhance endogenous antioxidant defense mechanisms and contribute to cellular protection under oxidative stress conditions. However, whether FXN directly regulates mitochondrial ROS production or improves mitochondrial physiological functions requires further investigation. These findings suggest that FXN may serve as a potential therapeutic target for POAG.

  Naturally, several insufficiencies were required to be further improved. There was a lack of animal model to confirming the biofunctions and regulatory mode of FXN in POAG. Sufficient clinical data was necessary to validate expressive trend and diagnostic value of FXN. The metabolic and immune effects of FXN were needed further investigations though a series of experiments. Moreover, although oxidative stress was selected as the primary focus of this study due to its well-established role in POAG, other potential biological pathways involved in POAG pathogenesis were not investigated and require further exploration. In addition, the H2O2-induced R28 cell model represents an acute oxidative stress condition and may not fully mimic the chronic oxidative stress environment of POAG. Further studies using chronic oxidative stress models and animal models are needed to better clarify the neuroprotective effects and mitochondrial mechanisms of FXN. Although the CTCF-FXN regulatory relationship was supported by our current findings, additional experiments such as promoter activity assays with mutated binding sites and in vivo validation are required to further confirm this transcriptional regulatory mechanism. Furthermore, considering that CTCF is a global transcription factor, other potential CTCF downstream targets involved in oxidative stress regulation require further investigation. Therefore, there is still plenty of work that should be done for clarifying the oxidative stress related mechanisms of POAG.


## Conclusion
  POAG is a multifactorial disease, leading to the degenerative optic neuropathy. Oxidative stress is a critical pathogenic factor of POAG, whose action mechanisms are still ill-defined. Herein, we identified FXN as a pivotal eigengene for characterizing POAG. On a H2O2 in vitro model, CTCF-FXN transcription regulatory axis was proved to exert protect functions for RGCs viability through relieving ROS accumulation and retard cell apoptosis. In conclusions, our findings demonstrated a very attractive potential therapeutic clue in POAG, termed CTCF-FXN axis.


## Supplementary Information
  Below is the link to the electronic supplementary material.

  Supplementary Material 1(PNG 1.12 MB) High Resolution Image (TIF 16.5 MB)

  Supplementary Material 2(PNG 250 KB) High Resolution Image (TIF 17.8 MB)

  Supplementary Material 3(PNG 698 KB) High Resolution Image (TIF 15.4 MB)

  Supplementary Material 4(PNG 984 KB) High Resolution Image (TIF 16.1 MB)

  Supplementary Material 5(PNG 220 KB) High Resolution Image (TIF 16.8 MB)

  Supplementary Material 6

  Supplementary Material 7

  Supplementary Material 8(PNG 744 KB) High Resolution Image (TIF 15.5 MB)

  Supplementary Material 9(PNG 1.08 MB) High Resolution Image (TIF 17.1 M)

  Supplementary Material 10(PNG 630 KB) High Resolution Image (TIF 15.1 MB )

  Supplementary Material 11

  Supplementary Material 12

  Supplementary Material 13