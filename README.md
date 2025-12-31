# Discovering Hidden Patterns in Protein Sequences

**Course**: CSCE 676 :: Data Mining and Analysis :: Texas A&M University :: Fall 2025  
**Team Name**: Motif Hunters  
**Team Members**: Uday Reddy (436000929), Aayush Yadav (535005643), Yash Phatak (136004827)

## 🧬 Project Overview

This project applies advanced data mining techniques to discover hidden patterns and functional motifs in protein sequences. Using the UniProt Swiss-Prot dataset containing over 573,000 manually curated protein sequences, we employ clustering algorithms and sequence analysis to automatically identify proteins with similar functions and extract recurring sequence patterns (motifs).

## 🎯 Motivation

Proteins are fundamental building blocks of life, composed of amino acid sequences that determine their function. While two proteins may appear completely different, they can share the same biological role through conserved sequence patterns called motifs. With hundreds of millions of discovered proteins, manual identification of these patterns is impossible.

**Research Question**: *"Given millions of protein sequences, how can we automatically find which ones are similar in function and what repeating sequence patterns (motifs) make them similar?"*

## 🌟 Impact & Applications

- **Drug Discovery**: Through motif matching, newly discovered proteins can be rapidly classified into existing protein families based on shared sequence patterns, accelerating drug development since proteins within the same family typically exhibit similar behaviors and target the same biological pathways
- **Functional Annotation**: Predicting functions of unknown proteins in newly sequenced organisms
- **Evolutionary Biology**: Understanding protein evolution and conservation patterns
- **Biotechnology**: Engineering proteins with desired properties based on functional motifs

## 📊 Dataset

**Source**: [UniProt Swiss-Prot (Reviewed)](https://www.uniprot.org/uniprotkb)
- **Size**: ~573,661 manually verified protein entries
- **Quality**: High-quality, manually curated sequences with accurate functional annotations
- **Content**: Each entry contains:
  - Protein amino acid sequence
  - Organism information (Bacteria, Virus, Eukaryote, Archaea)
  - Functional annotations and metadata
  - Structural information where available

## 🔬 Methodology

### 1. Data Preprocessing
- **Sampling**: Random selection of 100,000 sequences for computational efficiency
- **Feature Extraction**: 3-mer (tripeptide) analysis
  - Rationale: 3-mers capture biologically significant local patterns
  - Generated 9,138 unique 3-mer features across the dataset

### 2. Feature Engineering
- **TF-IDF Transformation**: Applied to 3-mer count vectors to emphasize discriminative patterns
- **Dimensionality Reduction**: PCA reduced features from 9,138 to 50 dimensions
  - Preserved ~6% of variance while maintaining clustering structure
  - Computational efficiency for large-scale clustering

### 3. Clustering Analysis
- **Algorithm**: HDBSCAN (Hierarchical Density-Based Spatial Clustering)
- **Parameters**: 
  - `min_cluster_size = 10`
  - `min_samples = 10`
  - `metric = euclidean`
- **Validation**: k-distance plots confirmed healthy clustering structure

### 4. Motif Discovery
- **Multiple Sequence Alignment (MSA)**: Applied MSA to each protein cluster to identify shared motifs
- **Consensus Patterns**: Extracted conserved sequence regions from aligned cluster members

### 5. Validation and Biological Interpretation
- **Functional Validation**: Cross-referenced discovered motifs with Pfam database annotations
- **Biological Interpretation**: Analyzed motif conservation patterns to understand functional significance

## 📈 Results

### Clustering Performance
- **Total Clusters**: 609 distinct protein clusters identified
- **Noise Points**: 83,700 sequences (~84%) classified as noise
- **Cluster Size Distribution**: Ranges from 10 to several hundred proteins per cluster

### Key Findings

#### Biologically Meaningful Clusters
1. **Cluster 0**: ATP synthase subunit beta proteins
   - Highly conserved energy metabolism proteins
   - Cross-species conservation (bacteria to eukaryotes)

2. **Cluster 6**: GroEL chaperonin proteins
   - Essential protein folding machinery
   - ~550 amino acids, structurally constrained

3. **Cluster 73**: Ribosomal proteins
   - Protein synthesis machinery
   - Conserved across bacteria and organellar ribosomes

4. **Cluster 108**: Cytochrome b proteins
   - Electron transport chain components
   - Mitochondrial respiratory complexes

#### Statistical Insights
- **High Noise Percentage**: 84% noise rate aligns with literature (70-95% typical)
- **Functional Coherence**: Clusters show strong biological coherence
- **Cross-Species Conservation**: Many clusters span multiple organisms
- **Size Distribution**: Power-law distribution typical of biological networks

## 🛠 Technical Implementation

### Dependencies

**Required Python Packages:**
- `numpy` - Numerical computing
- `pandas` - Data manipulation and analysis
- `matplotlib` & `seaborn` - Data visualization
- `biopython` - Bioinformatics tools for sequence analysis
- `scikit-learn` - Machine learning algorithms (PCA, vectorization)
- `hdbscan` - Density-based clustering algorithm
- `json` & `os` - Data processing utilities

### Key Functions
- `get_k_mers()`: Extract k-mer subsequences from protein sequences
- `extract_pfam_and_domain_hits()`: Parse Pfam domain annotation results
- `cluster_insights()`: Generate biological insights for protein clusters

## 📁 Repository Structure

```
├── motif_hunters.ipynb          # Main analysis notebook
├── clusters-pfam-data/          # Pfam domain analysis results
│   ├── cluster_0_pfam.json     # ATP synthase cluster annotations
│   ├── cluster_6_pfam.json     # GroEL chaperonin annotations
│   ├── cluster_31_pfam.json    # Ribosomal protein annotations
│   ├── cluster_239_pfam.json   # Additional cluster annotations
│   ├── cluster_402_pfam.json   # Tryptophan synthase annotations
│   └── cluster_608_pfam.json   # Mixed/unknown protein annotations
├── presentation.pdf             # Project presentation slides
└── README.md                   # This file
```

## 🚀 Getting Started

### Prerequisites
- Python 3.7+
- Jupyter Notebook
- Required packages: `biopython`, `hdbscan`, `scikit-learn`, `pandas`, `numpy`, `matplotlib`, `seaborn`

### Installation
```bash
pip install biopython hdbscan scikit-learn pandas numpy matplotlib seaborn
```

### Usage
1. **Download Dataset**: Obtain UniProt Swiss-Prot FASTA file
2. **Update Paths**: Modify file paths in the notebook to match your data location
3. **Run Analysis**: Execute `motif_hunters.ipynb` step by step
4. **Explore Results**: Examine clustering results and Pfam annotations

### Data Requirements
- UniProt Swiss-Prot FASTA file (`uniprot_sprot.fasta`)
- Pfam domain analysis results (JSON format)

## 🔍 Key Insights

### Biological Validation
- **ATP Synthase Cluster**: Perfect example of functional clustering
  - All proteins involved in cellular energy production
  - Conserved across all domains of life
  - Multiple Pfam domains confirm ATP synthase function

- **Chaperonin Cluster**: Protein folding machinery
  - GroEL family proteins essential for cell viability
  - Highly conserved structure and function
  - Critical for protein homeostasis

### Methodological Contributions
- **3-mer Features**: Effective for capturing local sequence patterns
- **HDBSCAN Performance**: Successfully identifies density-based protein families
- **High Noise Tolerance**: Algorithm handles sequence diversity appropriately
- **Scalable Pipeline**: Methodology applicable to larger datasets


## 📚 References

- UniProt Consortium. "UniProt: the universal protein knowledgebase." *Nucleic Acids Research* (2023)
- Pfam Database. "The Pfam protein families database." *Nucleic Acids Research* (2023)
- HDBSCAN Documentation and methodology papers
- Bioinformatics literature on protein sequence analysis

## 🤝 Contributing

This is a course project, but feedback and suggestions are welcome. Please feel free to:
- Report issues with the analysis
- Suggest improvements to the methodology
- Share insights about the biological findings

## 📄 License

This project is created for educational purposes as part of CSCE 676 coursework at Texas A&M University.

## 🙏 Acknowledgments

- **Course Instructor**: Prof. James Caverlee
- **Data Sources**: UniProt Consortium, Pfam Database
- **Tools**: Biopython, scikit-learn, HDBSCAN communities
- **Computational Resources**: Colab platform for analysis

---