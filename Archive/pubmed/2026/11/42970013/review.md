## Review setup
- **Input scope** Full manuscript text (Abstract, Introduction, all sections, figure legends, tables) as provided by the user.
- **Assessment boundary** Scientific content, logical coherence, evidence quality, and adherence to review article standards. Not assessed: editorial quality of figures (not provided), reference list accuracy (not provided), or formatting.
- **Shared manuscript claim summary** The manuscript argues that super-enhancers (SEs) are operationally defined, context-dependent regulatory domains whose biological relevance requires functional validation. It reviews SE architecture, identification methods, regulatory mechanisms, physiological functions, disease associations, and therapeutic targeting, using breast cancer as a detailed case study. The authors emphasize distinguishing descriptive SE maps from functionally validated regulatory dependencies and critically evaluate translational barriers.
- **Visible evidence base** The manuscript cites numerous primary research articles and reviews (references 1-285, not individually verified). It includes two figures (schematic diagrams) and two tables (technology overview and therapeutic strategies). The text describes specific experimental findings from cited studies, including CRISPR perturbations, ChIP-seq analyses, and clinical trial data.
- **Missing materials affecting confidence** Reference list (full citations not provided), figure images (only legends), table contents (Table 2 partially described in text), and any supplementary materials. Without the reference list, verification of citation accuracy and completeness is impossible. The absence of figures limits assessment of schematic clarity and accuracy.

## Reviewer
- **Overall assessment** This is a comprehensive, well-structured, and thoughtfully written review of super-enhancer biology. The authors successfully navigate a complex and rapidly evolving field, consistently emphasizing the critical distinction between chromatin-based annotation and functional validation. The use of breast cancer as a recurring case study provides coherence and depth. The manuscript is balanced, acknowledging both the promise and the limitations of SE-directed therapies. The writing is clear and accessible to a broad scientific audience. The main weaknesses are the lack of a systematic methodology for the literature search, some redundancy across sections, and the absence of a critical discussion on the limitations of the H3K27ac-centric definition of SEs. The clinical translation section, while appropriately cautious, could benefit from a more structured framework for evaluating evidence quality.
- **Who would be interested in the results, and why** This review will be of significant interest to researchers in gene regulation, chromatin biology, epigenetics, cancer biology, and immunology. Clinicians and translational scientists working on targeted therapies, particularly in breast cancer and hematologic malignancies, will find the critical evaluation of therapeutic strategies valuable. The clear explanations of technical methods (e.g., ROSE, CUT&Tag, HiChIP) make it a useful resource for newcomers to the field. The emphasis on functional validation and the discussion of emerging technologies (single-cell, spatial, AI) will appeal to methodologists and computational biologists.
- **Major strengths**
    1.  **Consistent and rigorous conceptual framework:** The manuscript's central thesis—that SE annotation is operational and requires functional validation—is applied consistently throughout, preventing over-interpretation of descriptive data.
    2.  **Comprehensive and current scope:** The review covers a wide range of topics from basic mechanisms (phase separation, ncRNAs) to disease states and therapeutic strategies, incorporating recent advances like ecDNA biology and AI applications.
    3.  **Balanced and critical perspective:** The authors do not oversell the therapeutic potential of SE targeting. They explicitly discuss toxicity, selectivity, and the lack of clinical validation, providing a realistic assessment of the field.
    4.  **Effective use of a case study:** The deep dive into breast cancer subtypes (luminal, HER2+, TNBC) effectively illustrates the principles of subtype-specific and context-dependent SE regulation, making abstract concepts concrete.
    5.  **Excellent readability:** The prose is clear, direct, and logically organized. Technical jargon is explained, making the content accessible to nonspecialists.
- **Major Concerns**

    - **Concern ID** R1-M1
    - **Severity** Major
    - **Blocking** No
    - **Axis** Methodology / Reproducibility
    - **Claim pointer** The review claims to provide a comprehensive overview of SE research but does not describe the methodology used to select and synthesize the literature.
    - **Evidence pointer** Section "Introduction" and all subsequent sections; location not provided.
    - **Concern** The manuscript is presented as a comprehensive review, but there is no description of the search strategy, inclusion/exclusion criteria, or timeframe for the literature search. This makes it difficult to assess whether the review is systematic, balanced, or potentially biased towards certain studies or viewpoints.
    - **Why it matters** For a field as broad and rapidly expanding as SE biology, a narrative review without a defined methodology risks being incomplete or reflecting the authors' specific focus. A clear methodology enhances reproducibility and trust in the conclusions.
    - **Resolution test** The authors should add a short "Search strategy and selection criteria" section (common in Nature reviews) detailing the databases searched, keywords used, and the period covered. This would clarify the scope and enhance the review's credibility.

    - **Concern ID** R1-M2
    - **Severity** Major
    - **Blocking** No
    - **Axis** Scientific Rigor / Conceptual Clarity
    - **Claim pointer** The review consistently uses H3K27ac as the primary operational marker for SEs but does not critically discuss the limitations of this approach.
    - **Evidence pointer** Section "Structural, functional, and methodological framework of SEs", subsection "Structural organization and molecular features of SEs"; location not provided.
    - **Concern** The manuscript acknowledges that SE annotation is dependent on H3K27ac signal but does not deeply explore the biological and technical limitations of this marker. For instance, H3K27ac is not a universal mark of all active enhancers, its levels can be influenced by cell cycle or cellular stress, and its deposition is not always functionally required for enhancer activity. The review would be strengthened by a more nuanced discussion of alternative or complementary markers (e.g., H3K4me1, ATAC-seq, MED1 occupancy) and the potential for H3K27ac-based annotations to miss or misclassify functional regulatory elements.
    - **Why it matters** The entire SE field is built on the operational definition. If the primary marker is flawed or incomplete, the conclusions drawn from SE maps may be misleading. A critical discussion of this foundational issue is essential for a rigorous review.
    - **Resolution test** The authors should add a paragraph in the methodology section discussing the strengths and weaknesses of H3K27ac as a marker, referencing studies that compare different SE identification methods and their concordance. This would demonstrate a deeper, more critical understanding of the field's foundations.

    - **Concern ID** R1-M3
    - **Severity** Major
    - **Blocking** No
    - **Axis** Evidence Quality / Translational Relevance
    - **Claim pointer** The manuscript discusses therapeutic targeting of SE-associated machinery but does not provide a clear framework for evaluating the strength of evidence for specific dependencies.
    - **Evidence pointer** Section "Therapeutic targeting of SEs and resistance-associated reprogramming", subsections "Small-molecule inhibitors targeting SE-associated transcriptional machinery" and "CRISPR-based epigenetic editing of SE activity"; location not provided.
    - **Concern** The review lists various therapeutic strategies (BET inhibitors, CDK7/9 inhibitors, PROTACs, CRISPR editing) and mentions their limitations, but it does not systematically grade the evidence for SE-dependence in different contexts. For example, the evidence that a specific cancer type is "addicted" to a particular SE is often based on correlative data or cell-line studies. The review would be more useful if it proposed criteria for establishing a "functional SE dependency" (e.g., genetic perturbation of the SE, not just the target gene, is required; phenotypic rescue; in vivo validation) and then applied these criteria to the examples discussed.
    - **Why it matters** The clinical translation of SE biology depends on identifying true dependencies. Without a clear framework for evaluating evidence, the review risks conflating descriptive associations with causal, therapeutically actionable dependencies, which could mislead future research efforts.
    - **Resolution test** The authors should introduce a set of explicit criteria for defining a functional SE dependency and use these to critically evaluate the examples in the therapeutic section. This would provide a valuable and actionable framework for the field.

- **Minor Comments**

    - **Concern ID** R1-m1
    - **Severity** Minor
    - **Axis** Clarity / Readability
    - **Affected element** Section "Therapeutic targeting of SEs and resistance-associated reprogramming", subsection "SE-associated programs in chemotherapy resistance and cancer stemness"
    - **Evidence pointer** Location not provided.
    - **Issue** The section on chemotherapy resistance is dense and covers a lot of ground (topoisomerase poisons, platinum agents, doxorubicin, cancer stemness) in a short space. The connection between acute transcriptional effects of chemotherapy and the long-term, selected changes in enhancer landscapes could be made clearer.
    - **Required correction** Consider splitting this into two subsections or adding a summary sentence to explicitly distinguish between acute, non-specific effects of chemotherapy on transcription and the stable, adaptive enhancer reprogramming that emerges in resistant cells.

    - **Concern ID** R1-m2
    - **Severity** Minor
    - **Axis** Completeness / Balance
    - **Affected element** Section "SE dysregulation in neurological and neurodevelopmental disorders"
    - **Evidence pointer** Location not provided.
    - **Issue** The section on neurological disorders is shorter and less detailed than the sections on cancer and immune diseases. While the authors note that evidence is less comprehensive, the section could benefit from a more explicit discussion of the technical challenges in studying SEs in the brain (e.g., cell-type heterogeneity, post-mortem tissue quality) that might explain this gap.
    - **Required correction** Add a sentence or two acknowledging the specific technical challenges of studying enhancer biology in the CNS, which would help contextualize the relative lack of functional data.

    - **Concern ID** R1-m3
    - **Severity** Minor
    - **Axis** Clarity / Readability
    - **Affected element** Section "Challenges and future directions in SE research", subsection "Artificial intelligence and computational integration"
    - **Evidence pointer** Location not provided.
    - **Issue** The discussion of AI is somewhat general. It mentions deep learning and graph-based methods but does not provide specific examples of how these have been successfully applied to SE research or what the key challenges are (e.g., data scarcity, interpretability).
    - **Required correction** Provide one or two concrete examples of AI models applied to enhancer-promoter prediction or SE classification, and briefly mention the main limitations (e.g., lack of gold-standard training data, difficulty in validating predictions).

## Risk / unsupported claims
- The claim that "CDK7 and CDK9 inhibitors interfere with RNA polymerase II phosphorylation and transcriptional initiation or elongation, which can preferentially affect genes driven by high-density regulatory elements" is presented as a general statement. While plausible, the "preferential" effect on SE-driven genes is still debated and may be context-dependent. The review should be more cautious in asserting this as a general principle.
- The statement that "BET inhibitors... may attenuate BRD4-dependent SE transcription" is appropriately hedged with "may," but the subsequent discussion of clinical trials (e.g., pelabresib) could be misread as implying SE-specific efficacy. The text correctly notes that trial participation does not establish SE-specific efficacy, but this caveat should be more prominently placed.
- The section on "SE-associated programs in chemotherapy resistance and cancer stemness" makes a claim that "In breast cancer stem-like cell models, HDAC7 contributes to H3K27ac enrichment at SEs..." This is a specific finding from a cited study and is presented as such, which is acceptable. However, the generalization to "cancer stemness" as a broad phenomenon should be treated with caution.
- The claim that "SEs are frequently located within topologically associating domains (TADs)" is a general statement that is likely true but may oversimplify the complex relationship between SEs and TAD boundaries. The review should acknowledge that some SEs can also be located at TAD boundaries or participate in inter-TAD interactions.
- The overall assessment of therapeutic strategies is appropriately cautious, but the review does not explicitly state that no SE-targeted therapy has yet received regulatory approval. This is a key fact for readers and should be stated explicitly.