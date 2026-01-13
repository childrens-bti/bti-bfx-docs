# Background and Literature

Here, we have compiled some important literature related to pediatric CNS brain tumors and computational workflows our group utilizes.
Please review. 

## Consortia

### The Children's Brain Tumor Network (CBTN)

The [CBTN](https://cbtn.org/) is a multi-institutional international clinical research consortium which was created to advance therapeutic development for children with central nervous system tumors through the collection and rapid distribution of biospecimens and data.
In 2018, the CBTN released WGS and RNA-Seq for ~1,000 tumors for researchers without embargo.
Read the CBTN manuscript [here](https://www.sciencedirect.com/science/article/pii/S1476558622000720).
The CBTN also has many cell line and organoid models available to researchers.
CBTN model descriptions, genomics, and characteristics can be viewed [here](https://d3b-rstudio-connect-public-prd.d3b.io/cbtn-preclinical-tumor-models/).

### The Pediatric Neuro-Oncology Consortium (PNOC)

The [PNOC](https://pnoc.us/) is an international consortium dedicated to advancing clinical paradigms and therapy for children and young adults with brain tumors.

### Clinical Proteomic Tumor Analysis Consortium (CPTAC) 
The CPTAC is an NCI effort "to accelerate the understanding of the molecular basis of cancer through the application of large-scale proteome and genome analysis, or proteogenomics".
For more information, see [here](https://gdc.cancer.gov/about-gdc/contributed-genomic-data-cancer-research/clinical-proteomic-tumor-analysis-consortium-cptac). 

## Open Source Platforms and Tools

### Gabriella Miller Kids First Data Resource Center (GMKF DRC)

We utilize the DNA and RNA sequencing workflows benchmarked and created by the [Kids First DRC](https://kidsfirstdrc.org/), which operates at the Children's Hospital of Philadelphia. 
The code for the workflows can be found in the [Kids First GitHub repository](https://github.com/kids-first) with corresponding CWL applications are publicly available within CAVATICA.

### OpenPBTA and OpenPedCan

The Open Pediatric Brain Tumor Atlas (OpenPBTA) was a global open-source analysis effort to analyze those first 1,000 PBTA tumors released by the CBTN and the PNOC003 DIPG clinical trial.
The OpenPBTA was led and maintained by researchers at CHOP and the [Childhood Cancer Data Lab (CCDL)](https://www.ccdatalab.org/) at Alex's Lemonade Stand Foundation.
Read the OpenPBTA manuscript [here](https://www.cell.com/cell-genomics/fulltext/S2666-979X(23)00115-5) and visit the archived GitHub repository [here](https://github.com/AlexsLemonade/OpenPBTA-analysis).

The OpenPBTA was later expanded to include additional pediatric cancer genomic data as well as gene expression data from TCGA and GTEx cohorts through the Open Pediatric Cancer (OpenPedcan) Project.
Read the OpenPedCan manuscript [here](https://www.biorxiv.org/content/10.1101/2024.07.09.599086v2).

### OpenScPCA

ALSF supported data generation, deposition, and harmonization of multiple pediatric cancer single cell studies, which are now housed in the [Single-cell Pediatric Cancer Atlas Portal](https://scpca.alexslemonade.org/). 
The CCDL created the Open Single-cell Pediatric Cell Atlas (OpenScPCA) [analysis project](https://github.com/AlexsLemonade/OpenScPCA-analysis) to analyze these data.

### CPTAC Data Portals
CPTAC raw data files can be explored on the [Proteomic Data Commons (PDC)](https://proteomic.datacommons.cancer.gov/pdc/).
A manifest can be generated from the PDC and files may be imported to CAVATICA for easy access.
In support of the collaborative publication between CBTN and CPTAC, ["Integrated Proteogenomic Characterization across Major Histological Types of Pediatric Brain Cancer"](https://pubmed.ncbi.nlm.nih.gov/33242424/), a web portal was created for easy multi-omic visualization and data download.
The portal can be found [here](https://pbt.cptac-data-view.org/). 

## CNS Tumor Literature

### Pediatric CNS Tumor Classification

The World Health Organization (WHO) introduced "integrated diagnoses" for CNS tumors in [2016](https://pubmed.ncbi.nlm.nih.gov/27157931/), followed by a significant update in [2021](https://pmc.ncbi.nlm.nih.gov/articles/PMC8328013/).
Today, there are still new entities and predispositions being discovered.

Most of these tumors can be classified by running methylation arrays through either the [DKFZ classifier](https://pmc.ncbi.nlm.nih.gov/articles/PMC6093218/) or the [NCI classifier](https://methylscape.ccr.cancer.gov/).

### Cancer-specific marker publications

This section is under construction.


