Comparative Analysis of GO-Enriched Communities in Bacterial STRING Networks

Overview
This project performs network-based analysis of protein-protein interaction (PPI) data from STRING. The goal is to identify functional modules, annotate them using GO enrichment, and detect conserved modules across and within bacterial species.

Objectives

Part 1:
- Construct PPI networks from STRING data
- Detect modules (communities) in each bacterium
- Perform GO enrichment analysis
- Interpret biological meaning

Part 2:
- Represent modules using enriched GO terms
- Compare modules using similarity metrics
- Identify conserved and unique modules

Datasets

B5  - Salmonella virulence network
B6  - Vibrio cholerae virulence network
B21 - Bacillus subtilis resistance network
B22 - Erwinia resistance network

Each dataset includes:
- string_interactions_X.tsv
- string_functional_annotations_X.tsv

Pipeline

1. Network Construction
Nodes represent proteins, edges represent interactions with confidence scores.
Edges are filtered using a threshold.

2. Module Detection
Main method: Louvain community detection
Additional methods tested:
- Greedy modularity
- Label propagation
- Spectral clustering
- KMeans (on adjacency matrix)

3. Functional Enrichment
- Hypergeometric test for each GO term
- Benjamini-Hochberg FDR correction
- Significant terms: adjusted p-value < 0.05

4. Module Comparison
Modules are compared using enriched GO terms.
Similarity metric:
- Overlap coefficient (main)
- Jaccard (secondary)

Parameters

RANDOM_SEED = 42
EDGE_SCORE_THRESHOLD = 0.7
MIN_MODULE_SIZE = 2
FDR_ALPHA = 0.05
TOP_TERMS_PER_MODULE = 10

Part 2 settings:

(B21, B22):
- similarity_metric = overlap_coefficient
- threshold = 0.30

(B5, B6):
- similarity_metric = overlap_coefficient
- threshold = 0.05

Main Findings

B5/B6 (Virulence):
- Protein secretion systems
- Biofilm formation
- Motility (flagella)
- Host interaction and toxins

B21/B22 (Resistance):
- Cell wall / peptidoglycan
- Transport systems
- Gene regulation
- Antibiotic response

Conserved Modules

Strong conservation:
- Secretion system: B5_M1 ↔ B6_M2
- Cell wall / peptidoglycan: B21_M7 ↔ B22_M6

Additional partial conservation:
- Transport
- Localization
- Antibiotic response

Biological Insight

Modules represent functional biological units rather than random clusters.
Functional conservation exists even without identical protein composition.
Different bacteria preserve core biological mechanisms:
- Virulence → secretion and interaction
- Resistance → cell wall and transport

Creative Extension

A directory-based screening pipeline was implemented:
- Runs full analysis on a target bacterium
- Scans external datasets
- Compares modules against the target
- Marks modules as conserved if supported by multiple datasets

This improves robustness and biological confidence.

Project Structure

project/
├── notebook.ipynb
├── README.txt

How to Run

1. Place all input files in the working directory
2. Run the notebook or script
3. Outputs are saved automatically in the current directory

Final Note

The pipeline is reproducible, data-driven, and aligned with project requirements.
