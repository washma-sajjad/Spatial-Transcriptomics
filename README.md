# 🔬 Spatial Transcriptomics Analysis

A collection of Jupyter notebooks for analyzing spatial transcriptomics data using three major platforms: **10x Genomics Visium (H&E)**, **Visium (Fluorescence)**, and **10x Genomics Xenium**. These notebooks cover the full analysis pipeline — from raw data loading to clustering, differential gene expression, and spatial visualization.

---

## 📁 Repository Structure

```
Spatial-Transcriptomics/
│
├── basic_analysis_spatial_transcriptomics.ipynb   # General intro pipeline for spatial data
├── Visium_H&E.ipynb                                # Visium analysis with H&E staining
├── Visium fluorescence.ipynb                       # Visium analysis with fluorescence imaging
├── Results                                          # Rsulting graphs
└── xenium_spatial_analysis.ipynb                   # Xenium single-cell spatial analysis
```

---

## 🧬 What is Spatial Transcriptomics?

Spatial transcriptomics is a cutting-edge genomics method that allows researchers to measure gene expression across tissue sections while **preserving spatial context** — meaning you can see *where* in the tissue each gene is being expressed, not just *whether* it is expressed.

This is important because:
- Different tissue regions (e.g., tumor core vs. tumor margin) express genes differently.
- Cell identity and function are tightly linked to position in tissues.
- Spatial data bridges the gap between histology (tissue imaging) and genomics.

---

## 📓 Notebook Descriptions

### 1. `basic_analysis_spatial_transcriptomics.ipynb`
**A general-purpose spatial transcriptomics analysis pipeline.**

This notebook serves as an introductory walkthrough for anyone new to spatial transcriptomics analysis using [Scanpy](https://scanpy.readthedocs.io/) and [Squidpy](https://squidpy.readthedocs.io/). It covers the fundamental steps that apply broadly across platforms.

**Key steps covered:**
- Loading spatial gene expression data into an `AnnData` object
- Quality control (QC): filtering spots/cells by gene count, mitochondrial gene percentage, etc.
- Normalization and log-transformation
- Highly variable gene (HVG) selection
- Dimensionality reduction via PCA and UMAP
- Neighborhood graph construction
- Leiden clustering to identify tissue regions/cell types
- Spatial scatter plots overlaid on tissue images

---

### 2. `Visium_H&E.ipynb`
**Spatial analysis of 10x Genomics Visium data with H&E stained tissue.**

10x Visium is a spot-based spatial transcriptomics platform where each spot captures RNA from a ~55 µm area of tissue. The H&E (Hematoxylin & Eosin) staining allows simultaneous histological and gene expression analysis.

**Key steps covered:**
- Loading Visium data using `sc.read_visium()` with the H&E image
- Visualizing the tissue with spatially-mapped gene expression (`sq.pl.spatial_scatter`)
- QC filtering (mitochondrial %, min genes per spot)
- Normalization and HVG selection
- PCA → UMAP → Leiden clustering
- Annotating clusters with known marker genes
- Spatial autocorrelation analysis (Moran's I) to identify spatially variable genes
- Visualizing cluster distributions overlaid on the H&E image

**Why H&E?** H&E staining is the gold standard in pathology. Combining it with gene expression data allows direct comparison between tissue morphology and molecular profiles, making it particularly useful for cancer, neuroscience, and developmental biology research.

---

### 3. `Visium fluorescence.ipynb`
**Spatial analysis of 10x Genomics Visium data with fluorescence microscopy images.**

Unlike H&E, fluorescence imaging highlights specific proteins or structures using labeled antibodies or dyes, giving additional layer of information about the tissue microenvironment.

**Key steps covered:**
- Loading Visium data paired with a fluorescence tissue image
- Preprocessing the fluorescence image for display
- Standard spatial analysis pipeline (QC → normalization → clustering → UMAP)
- Overlaying gene expression on fluorescence images
- Comparing cluster boundaries with fluorescence channel signals
- Spatially variable gene identification

**Why Fluorescence?** Fluorescence allows visualization of specific cell markers (e.g., DAPI for nuclei, specific antibodies for protein markers) simultaneously with transcriptomics, enabling multi-modal analysis.

---

### 4. `xenium_spatial_analysis.ipynb`
**Single-cell resolution spatial analysis using 10x Genomics Xenium.**

Xenium is a newer, higher-resolution platform compared to Visium. It uses *in situ* sequencing to profile individual cells (not spots), giving **subcellular and single-cell level spatial resolution**. This makes it more powerful for dissecting heterogeneous tissues.

**Key steps covered:**
- Loading Xenium output data (cell-by-gene matrix + cell centroid coordinates)
- QC filtering at the single-cell level
- Normalization and HVG selection
- PCA → UMAP → Leiden clustering
- Cell type annotation based on marker gene expression
- Spatial visualization of individual cells colored by cluster/cell type
- Neighborhood enrichment analysis — which cell types are spatially co-localized?
- Ligand-receptor interaction analysis (cell communication)

**Why Xenium over Visium?** Visium spots contain mixtures of cells (~1–10 cells per spot), while Xenium resolves single cells, allowing finer-grained analysis of cell heterogeneity within the same tissue region.

---

## 🛠️ Libraries & Tools Used

| Library | Purpose |
|---|---|
| [Scanpy](https://scanpy.readthedocs.io/) | Single-cell/spatial analysis framework |
| [Squidpy](https://squidpy.readthedocs.io/) | Spatial statistics and visualization |
| [AnnData](https://anndata.readthedocs.io/) | Data container for annotated matrices |
| [NumPy](https://numpy.org/) | Numerical computations |
| [Pandas](https://pandas.pydata.org/) | Data manipulation |
| [Matplotlib](https://matplotlib.org/) | Plotting |
| [Seaborn](https://seaborn.pydata.org/) | Statistical visualizations |

---

## ⚙️ Installation

It is recommended to use a conda environment.

```bash
conda create -n spatial_env python=3.10
conda activate spatial_env

pip install scanpy squidpy anndata matplotlib seaborn pandas numpy
```

For Xenium-specific analysis, you may also need:

```bash
pip install spatialdata spatialdata-io
```

---

## 🚀 Getting Started

1. Clone the repository:
   ```bash
   git clone https://github.com/washma-sajjad/Spatial-Transcriptomics.git
   cd Spatial-Transcriptomics
   ```

2. Launch Jupyter:
   ```bash
   jupyter notebook
   ```

3. Open a notebook based on your data type:
   - New to spatial transcriptomics? Start with `basic_analysis_spatial_transcriptomics.ipynb`
   - Have Visium H&E data? Use `Visium_H&E.ipynb`
   - Have Visium fluorescence data? Use `Visium fluorescence.ipynb`
   - Have Xenium data? Use `xenium_spatial_analysis.ipynb`

4. **Data:** These notebooks use publicly available datasets from 10x Genomics. Download the relevant datasets from the [10x Genomics datasets page](https://www.10xgenomics.com/datasets) and update the file paths in the notebooks accordingly.

---

## 📊 Results 

A  `results/` folder with the following outputs:

###  `Results/` folder structure:
```
results/
├── visium_HE/
│   ├── umap_clusters.png          # UMAP plot colored by Leiden clusters
│   ├── spatial_clusters.png       # Clusters overlaid on H&E tissue image
│   ├── spatially_variable_genes.png  # Top spatially variable genes heatmap
│   └── marker_genes_dotplot.png   # Dotplot of top marker genes per cluster
│
├── visium_fluorescence/
│   ├── umap_clusters.png
│   ├── spatial_fluorescence_overlay.png  # Gene expression over fluorescence image
│   └── cluster_comparison.png
│
└── xenium/
    ├── umap_celltypes.png         # UMAP colored by annotated cell types
    ├── spatial_celltypes.png      # Single-cell map of the tissue
    ├── neighborhood_enrichment.png  # Heatmap of cell-type co-localization
    └── ligrec_interactions.png    # Ligand-receptor interaction dotplot
```

---

## 📖 References & Resources

- [Scanpy Documentation](https://scanpy.readthedocs.io/)
- [Squidpy Documentation](https://squidpy.readthedocs.io/)
- [10x Genomics Visium](https://www.10xgenomics.com/products/spatial-gene-expression)
- [10x Genomics Xenium](https://www.10xgenomics.com/products/xenium-in-situ)
- Palla et al. (2022) *Squidpy: a scalable framework for spatial omics analysis*. Nature Methods.
- Wolf et al. (2018) *SCANPY: large-scale single-cell gene expression data analysis*. Genome Biology.

---

## 👩‍💻 Author

**Washma Sajjad**
GitHub: [@washma-sajjad](https://github.com/washma-sajjad)

---

## 📄 License

This project is open-source. Feel free to use, adapt, and build upon these notebooks for your own spatial transcriptomics analyses.
