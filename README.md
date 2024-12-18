# PrecisionMed
Precision Medicine Project code: High-Throughput Single Cell RNA Sequencing of Arabidopsis Root.

# Project Overview
This project focuses on analyzing single-cell RNA sequencing (scRNA-seq) data from Arabidopsis root cells. The analysis identifies distinct cell populations, marker genes, and biological pathways contributing to stress adaptation mechanisms. Tools such as Seurat, clusterProfiler, and visualization libraries were employed for clustering, differential gene expression analysis, and Gene Ontology (GO) enrichment.

# Requirements
Before running the code, ensure the following packages are installed:

# R Libraries:
Seurat
ggplot2
ComplexHeatmap
pheatmap
dplyr
clusterProfiler
org.At.tair.db
BiocManager

# Steps in the Analysis
1. Data Preprocessing
Trimming and Quality Control:
Raw data is loaded into a Seurat object.
Normalization of gene expression is performed using LogNormalize.
Quality control plots visualize RNA features, counts, and mitochondrial percentages.
seurat_obj <- NormalizeData(seurat_obj, normalization.method = "LogNormalize", scale.factor = 10000)

2. Clustering and Visualization
Principal Component Analysis (PCA), UMAP, and t-SNE are used to identify clusters of root cells.
Clustering Parameters:
Dimensions: 1:10 (adjusted using ElbowPlot).
Resolution: 0.5 for optimal cluster granularity.

seurat_obj <- FindClusters(seurat_obj, resolution = 0.5)
seurat_obj <- RunUMAP(seurat_obj, dims = 1:10)
DimPlot(seurat_obj, reduction = "umap", label = TRUE)

3. Marker Gene Identification
Cluster-specific marker genes are identified using differential gene expression analysis.
Results are saved to Cluster_Markers.csv.

4. Differential Expression Analysis
Differentially expressed genes between clusters are identified, filtered by adjusted p-value and log-fold change.

5. Gene Ontology (GO) Enrichment Analysis
GO enrichment analysis (Biological Process) is performed using clusterProfiler.
Outputs include bar plots, dot plots, and network plots for enriched pathways.
go_bp <- enrichGO(gene = gene_list, OrgDb = org.At.tair.db, ont = "BP", pvalueCutoff = 0.05)
barplot(go_bp, showCategory = 10)

6. Visualization
UMAP/t-SNE Plots: Visualize annotated clusters.
Volcano Plots: Highlight significant differentially expressed genes.
Heatmaps: Show expression of top marker genes across clusters.

# Outputs
Cluster_Markers.csv: Marker genes for each cluster.
Differentially_Expressed_Genes.csv: Filtered differentially expressed genes.
GO_Enrichment_BP.csv: GO enrichment results for biological processes.
Visualizations:
UMAP plots
Volcano plots
Heatmaps

# How to Run
Clone this repository:
git clone https://github.com/YourUsername/YourRepoName.git
cd YourRepoName

Open the R script in RStudio or any R environment.
Replace file paths with your data locations.
Run the script step by step or as a whole.
