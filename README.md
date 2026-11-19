# Bioinformatics-Final-Project
# Gene Expression Patterns and Developmental Trajectories of Hematopoiesis in Early Mouse Embryos

## Project Information

- **Course:** BIOL 3340 / 5340 – Bioinformatics
- **Instructor:** Dr. Jeffery Demuth
- **Team Members:** Kelly Nguyen and Victoria Phan
- **Semester:** Fall 2026
- **Project Status:** Draft report completed; additional analyses in progress.

## Project Overview

This project investigates gene-expression patterns and developmental transitions during early mouse embryonic hematopoiesis using single-cell quantitative reverse transcription polymerase chain reaction (qRT-PCR) data. Computational methods, including dimensionality reduction, diffusion pseudotime, and clustering, are used to examine relationships among experimentally defined cell populations.

### Research Question

How do gene-expression patterns change across early mouse embryonic hematopoietic development, and can computational methods identify developmental transitions between experimentally defined cell populations?

## Dataset

The dataset is publicly available through the Scanpy Python library using `sc.datasets.moignard15()`. It originates from Supplementary Table 7 of Moignard et al. (2015).

- **Data type:** Normalized single-cell qRT-PCR dCt measurements
- **Number of cells:** 3,934
- **Number of genes:** 42
- **Data format:** AnnData object
- **Missing values:** None detected following numeric conversion

| Experimental Group | Description | Number of Cells |
|---|---|---:|
| PS | Primitive streak | 624 |
| NP | Neural plate | 552 |
| HF | Head fold | 1,005 |
| 4SG | Four-somite blood/GFP-positive | 983 |
| 4SFG | Four-somite endothelial/GFP-negative | 770 |
| **Total** | | **3,934** |

The dataset contains normalized dCt measurements rather than RNA-seq counts. Therefore, count-depth normalization and log1p transformation were not applied.

## Repository Contents

| File | Description |
|---|---|
| `README.md` | Project overview, repository contents, and instructions for reproducing the analysis. |
| `Bioinformatics_Project_Reviewed_and_Completed.ipynb` | Jupyter notebook containing preprocessing, computational analyses, visualizations, and evaluation metrics. |
| `ai_usage.md` | Documentation of AI assistance and verification procedures. |

## Computational Workflow

1. Load the Moignard et al. dataset using Scanpy.
2. Inspect dataset dimensions, experimental group counts, and missing values.
3. Convert the expression matrix to numeric values.
4. Preserve original normalized dCt measurements.
5. Standardize gene features for multivariate analysis.
6. Perform principal component analysis (PCA).
7. Construct a 15-nearest-neighbor graph.
8. Generate UMAP visualizations.
9. Compare selected gene measurements across experimental groups.
10. Perform diffusion map and diffusion pseudotime (DPT) analyses.
11. Evaluate pseudotime sensitivity using alternative root cells.
12. Perform optional Leiden clustering.
13. Evaluate experimental group separation using silhouette scores and adjusted Rand index (ARI).

## Software and Dependencies

The analysis was performed using Python and Jupyter Notebook.

| Software or Package | Version |
|---|---|
| Python | 3.13.18 |
| Scanpy | 1.12 |
| anndata | 0.12.19 |
| NumPy | 2.4.6 |
| pandas | 2.2.3 |
| scikit-learn | 1.6.1 |
| matplotlib | 3.10.0 |
| seaborn | 0.13.2 |
| leidenalg | 0.12.0 |

## How to Reproduce the Analysis

### Step 1: Clone the repository

    git clone https://github.com/KellyVNguyen/Bioinformatics-Final-Project.git
    cd Bioinformatics-Final-Project

### Step 2: Install the required packages

    pip install scanpy anndata numpy pandas scikit-learn matplotlib seaborn leidenalg igraph jupyter

Refer to the software and dependencies table for the versions used in the original analysis.

### Step 3: Open Jupyter Notebook

    jupyter notebook

### Step 4: Run the analysis

Open `Bioinformatics_Project_Reviewed_and_Completed.ipynb` and execute all cells sequentially from top to bottom.

The dataset is retrieved directly through Scanpy, so a separate manual dataset download is not required. An internet connection may be necessary when loading the dataset for the first time.

A random seed of 42 was used where specified to support reproducibility.

## Preliminary Results

- Successfully loaded and processed 3,934 cells and 42 genes without introducing missing values.
- PCA and UMAP revealed experimental group-specific patterns alongside considerable overlap.
- The 4SG blood population exhibited relatively distinct separation.
- HbbbH1, Cdh5, Kdr, and Lyl1 exhibited the largest differences in median normalized dCt measurements across experimental groups.
- Diffusion pseudotime demonstrated sensitivity to the selection of the starting cell.
- Optional Leiden clustering identified 13 computationally defined clusters.

### Quantitative Evaluation

| Evaluation Metric | Result |
|---|---:|
| PCA silhouette score | 0.133 |
| UMAP silhouette score | 0.121 |
| Diffusion map silhouette score | −0.113 |
| Leiden adjusted Rand index | 0.202 |
| Spearman correlation between two pseudotime roots | 0.488 |
| Number of Leiden clusters | 13 |

These preliminary findings suggest that computational methods capture meaningful structure associated with experimental populations. However, they do not establish direct developmental lineage relationships.

## Limitations

- The dataset contains only 42 targeted genes.
- Experimental groups have unequal cell counts.
- The direction of the normalized dCt scale requires confirmation.
- Diffusion pseudotime is sensitive to root selection.
- Gene rankings are exploratory and do not establish statistically significant differential expression.
- Computationally inferred developmental ordering does not establish cell ancestry.

## Project Progress and Next Steps

### Completed

- [x] Dataset loading and preprocessing
- [x] Data quality assessment
- [x] PCA and UMAP visualization
- [x] Experimental group comparisons
- [x] Selected gene-expression measurement comparisons
- [x] Diffusion pseudotime analysis
- [x] Initial two-root sensitivity comparison
- [x] Optional Leiden clustering
- [x] Quantitative evaluation
- [x] Draft report

### Remaining

- [ ] Verify the normalized dCt direction and interpretation of the −14 measurement floor.
- [ ] Evaluate additional plausible pseudotime root cells.
- [ ] Generate selected gene-measurement trends along pseudotime.
- [ ] Evaluate the robustness and biological interpretation of the inferred trajectories.
- [ ] Finalize repository documentation.
- [ ] Complete the final report and presentation.

## Team Contributions

**Kelly Nguyen:** PCA, UMAP, experimental group comparisons, silhouette score evaluation, and selected gene-expression measurement analysis.

**Victoria Phan:** Diffusion pseudotime analysis, experimental group pseudotime comparisons, Leiden clustering, and adjusted Rand index evaluation.

## AI Use and Reproducibility

ChatGPT was used to assist in planning the computational workflow, drafting and troubleshooting Python code, and organizing the project report.

AI-assisted outputs were verified through notebook execution, confirmation of dataset dimensions, missing-value checks, inspection of analytical results, and consultation of lecture materials and Scanpy documentation.

Additional information regarding AI assistance and verification procedures is provided in `ai_usage.md`.

The dataset is publicly available and contains no personal human data.

## References and Resources

- Moignard et al. (2015). Decoding the regulatory network of early blood development from single-cell gene expression measurements. *Nature Biotechnology, 33*, 269–276. https://doi.org/10.1038/nbt.3154
- Wolf, F. A., Angerer, P., & Theis, F. J. (2018). SCANPY: Large-scale single-cell gene expression data analysis. *Genome Biology, 19*, 15. https://doi.org/10.1186/s13059-017-1382-0
- Haghverdi, L., Büttner, M., Wolf, F. A., Buettner, F., & Theis, F. J. (2016). Diffusion pseudotime robustly reconstructs lineage branching. *Nature Methods, 13*, 845–848. https://doi.org/10.1038/nmeth.3971
- Scanpy dataset documentation: https://scanpy.scverse.org/en/stable/generated/scanpy.datasets.moignard15.html

## Acknowledgments

We thank Dr. Jeffery Demuth for his guidance and feedback throughout this bioinformatics project. We also acknowledge Moignard et al. for providing the original dataset and the Scanpy development team for providing computational analysis tools.
