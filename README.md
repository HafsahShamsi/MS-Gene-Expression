# 🧬 Multiple Sclerosis — Gene Expression Analysis

![Python](https://img.shields.io/badge/Python-3.8+-blue?logo=python&logoColor=white)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-orange?logo=jupyter&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-green)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

> Analysing blood gene expression from MS patients vs healthy controls using public GEO data — identifying dysregulated genes, visualising immune patterns, and connecting findings to known MS biology.

**Author:** Hafsah Shamsi | Microbiology + Data Science | Mithibai College, Mumbai

---

## 📖 Overview

Multiple Sclerosis (MS) is a chronic autoimmune neurological disease in which the immune system attacks the myelin sheath — the protective coating around nerve fibres. It affects over **2.8 million people worldwide** and is the leading cause of non-traumatic neurological disability in young adults.

This project performs a full differential gene expression pipeline on a real, publicly available MS dataset from NCBI GEO, covering data retrieval through to biological interpretation.

---

## 📊 Dataset

| Field | Details |
|---|---|
| **Accession** | [GSE26927](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE26927) |
| **Source** | NCBI GEO (Gene Expression Omnibus) |
| **Tissue** | Peripheral whole blood |
| **Platform** | Affymetrix microarray |
| **Subjects** | Relapsing-remitting MS patients + healthy controls |
| **Publication** | Kemppinen et al. |

---

## 🔬 Analysis Pipeline

```
Raw GEO Data (GSE26927)
        │
        ▼
 Data Retrieval (GEOparse)
        │
        ▼
 Expression Matrix + Sample Labels
        │
        ▼
 Normalisation (log2) + Variance Filtering (top 25%)
        │
        ├──────────────────────┐
        ▼                      ▼
 PCA (unsupervised)    Differential Expression
 MS vs Healthy         Welch t-test + FDR (BH)
        │                      │
        ▼                      ▼
 PCA + Scree Plot      Volcano Plot + Heatmap
        │                      │
        └──────────┬───────────┘
                   ▼
         Biological Interpretation
```

---

## 📁 Project Structure

```
MS-Gene-Expression/
│
├── ms_gene_expression.ipynb    # Main analysis notebook
├── ms_deg_results.csv          # Full differential expression results
│
├── outputs/
│   ├── pca_ms.png              # PCA scatter + scree plot
│   ├── volcano_ms.png          # Volcano plot
│   └── heatmap_ms.png          # Clustered heatmap of top DEGs
│
└── README.md
```

---

## 📦 Requirements

```bash
pip install pandas numpy matplotlib seaborn scipy scikit-learn statsmodels GEOparse adjustText
```

Or install all at once:

```bash
pip install -r requirements.txt
```

**`requirements.txt`**
```
pandas>=2.0
numpy>=1.26
matplotlib>=3.7
seaborn>=0.13
scipy>=1.11
scikit-learn>=1.3
statsmodels>=0.14
GEOparse>=2.0
adjustText>=1.0
```

---

## 🚀 Usage

1. **Clone the repository**
   ```bash
   git clone https://github.com/HafsahShamsi/ms-gene-expression.git
   cd ms-gene-expression
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Run the notebook**
   ```bash
   jupyter notebook ms_gene_expression.ipynb
   ```

   > ⚠️ **First run** downloads ~50 MB from NCBI GEO. Subsequent runs use the local cache.

---

## 📈 Key Outputs

### PCA Plot
Principal component analysis showing separation between MS patients and healthy controls in gene expression space, alongside a scree plot of variance explained.

### Volcano Plot
Each dot represents a probe. The x-axis shows log₂ fold change (MS vs Healthy); the y-axis shows −log₁₀ adjusted p-value. Top significant probes are labelled.

* 🔴 **Red** — Upregulated in MS (FDR < 0.05, log₂FC > 0.5)
* 🔵 **Blue** — Downregulated in MS (FDR < 0.05, log₂FC < −0.5)
* ⚫ **Grey** — Not significant

### Heatmap
Z-score normalised expression of the top 40 differentially expressed probes, clustered by gene and ordered by group (Healthy → MS).

---

## 🧠 Biological Context

In MS, the immune system — particularly T cells and B cells — becomes activated against myelin antigens. Blood gene expression reflects this systemic immune dysregulation:

* **Upregulated in MS** → Interferon-stimulated genes (ISGs), innate immune activation, inflammatory cytokine pathways
* **Downregulated in MS** → Markers of regulatory T cell function, immune tolerance genes

Key gene families of interest: **HLA genes**, **interferon signalling**, **myelin-related pathways**

---

## 🔭 Next Steps

* [ ] Map probe IDs → gene symbols using the GPL annotation file
* [ ] Run pathway enrichment analysis (KEGG / GO) on significant DEGs
* [ ] Cross-cohort validation with a second MS GEO dataset
* [ ] Integrate with GWAS risk loci — do MS genetic risk genes show expression changes?
* [ ] Machine learning classifier (MS vs Healthy) using top DEGs

---

## 📚 References

* Kemppinen AK et al. (2011). *Genome-wide association study on multiple sclerosis.* 
* Barrett T et al. (2013). *NCBI GEO: archive for functional genomics data sets.* Nucleic Acids Research.
* GEOparse library: https://geoparse.readthedocs.io

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

*Built as part of a Microbiology + Data Science project at Mithibai College, Mumbai.*
