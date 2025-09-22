# Automated Pathway Reconstruction using Attention Guided Graph Neural Networks (AG-GNN)
# Overview

This project builds a graph-based machine learning pipeline for predicting protein functions.
Proteins are represented in a protein–protein interaction (PPI) network, encoded with a Graph Neural Network (GNN), and clustered into functional groups.
We then use KEGG pathway enrichment analysis to map clusters to biological pathways.

To improve reliability, we introduce uncertainty-aware confidence scoring using Monte Carlo Dropout. This ensures that proteins are not only classified, but also assigned with a confidence estimate, reducing false assignments and improving trust in the results.

# Methodology
1. Data Preparation

Source: STRING database (protein–protein interactions, metadata, embeddings).

Graph Construction:

Nodes = proteins.

Edges = interactions (weighted by confidence score).

Node features = STRING embeddings + annotations.

2. Graph Neural Network (GNN)

Encoder: Graph Attention Network (GAT).

Task: Link prediction (train embeddings by predicting if an edge exists).

Output: protein embeddings that capture biological relationships.

3. Clustering

Embeddings → KMeans (primary method).

Alternative clustering tested: Spectral, DBSCAN.

Output: clusters of proteins with similar embeddings.

4. Pathway Enrichment

For each cluster, run Hypergeometric test against KEGG pathways.

Assign cluster → most enriched pathway.

This maps proteins → biological processes.

5. Uncertainty-Aware Confidence Scoring (Novelty)

Cluster confidence: distance to cluster center.

Pathway confidence: enrichment strength (scaled from –log10 p-value).

Stability (uncertainty): via Monte Carlo Dropout – check how stable cluster assignments are across multiple stochastic GNN runs.



Pathway Confidence
Final=α⋅Cluster Confidence+(1−α)⋅Pathway Confidence

multiplied by stability score.

Proteins below threshold → labeled “Uncertain”.

Proteins above threshold → assigned pathway (e.g., hsa00562 → Inositol phosphate metabolism).

# Key Features

Graph Neural Network (GNN) to embed proteins.
Multi-step clustering for functional grouping.
KEGG pathway enrichment to link clusters → biological processes.
Uncertainty-aware scoring (Novel contribution):

Monte Carlo Dropout to estimate stability.

Weighted confidence combining cluster, pathway, and uncertainty.

Reduces false “Uncertain” labels.

Flags proteins with unreliable assignments.

# Authors
PRATYUSH LENKA 23BAI1470

AAYUSH P MENON 23BAI1467

P.S THERE ARE SOME DATASETS WHICH ARE TOO BIG TO BE UPLOADED WILL BE UPLOADED LATER
