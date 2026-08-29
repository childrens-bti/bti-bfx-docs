---
icon: material/rocket-launch
---

# Services

The [BTI Bioinformatics Core](https://rokitalab.com/core/) offers a range of computational and analytical support for projects involving genomic, transcriptomic, and clinical data. 
See [Working with the Core](pi-working-with-core.md) for how to initiate a collaboration.

---

## Data Transfers & Management

- Data transfer from external or internal sites
- Data deposition to repositories (GEO, dbGaP, PRIDE)
- Data storage — creation and management of AWS buckets or L Drive shares
- Data Access Agreement support (dbGAP, EGA, CBTN, PNOC expertise)
- Globus/IT/ServiceNow general support (e.g. - AD group setup, L drive, Box, Slack)

## Data Ingest

- Manifest generation, bioassay ID and internal identifier generation, data file warehouse ingest
- Data merge across datasets/sources

## Sequencing Data Harmonization (Defaults listed below)

For additional customization of workflows, additional fees may apply.

**PDX preprocessing**

- Quality control assessment
- Xenome classification of human and mouse reads

**Normal DNA**

- Quality control assessment
- Sentieon alignment, single sample genotyping (GATK HaplotypeCaller) with gnomAD v3.1.1 and 4.1 annotation
- Normal CNV calls (CNVnator, MantaSV, SVaba) with AnnotSV annotation
- Normal SV calls (MantaSV, SVaba) with AnnotSV annotation
- Pathogenicity assessment (ClinVar, InterVar, AutoPVS1, AutoGVP)

**Tumor DNA (WGS, WXS, Panel from T/N pairs)**

- Quality control assessment
- Sentieon alignment, somatic SNV calls (Lancet, VarDict, Strelka2, Mutect2), and consensus SNV calls with VEP v105 annotation
- CNV (ControlFREEC, CNVkit) and SV (MantaSV) calls (WGS and WXS only) with AnnotSV annotation

**Tumor only DNA (WGS, WXS, Panel)**

- Quality control assessment
- Sentieon alignment, somatic SNV calls (Mutect2) using PON with VEP v105 annotation
- CNV (ControlFREEC, CNVkit) and SV (MantaSV) calls (WGS and WXS only) with AnnotSV annotation

**Quality control (sample identity/relatedness checks)**

- NGSCheckMate or 
- Somalier Relate 

**Short-read RNA (tumor or normal)**

- Quality control assessment (RNASeCQ, STAR)
- STAR two-pass alignment (GENCODE v39 annotation)
- Gene counts and TPM (RSEM)
- Isoform counts and TPM (RSEM)
- Isoform abundance (Kallisto)
- Fusion detection (STAR-Fusion, Arriba Fusion)
- Splice events (rMATS turbo)
- Flash-Seq supported

**miRNA-Seq**

- novel miRNA target prediction (miRanda, GENCODE v39)

**Long-read RNA (PacBio Kinnex)**

- Quality control assessment
- Alignment
- Gene and isoform expression

**Single cell or nucleus whole transcriptome**

- Quality control assessment
- Alignment and filtering (ALSF CCDL workflow, alevin-fry)
- Gene expression
- Cell type annotation

**10X Flex Gene Expression**

- Custom probe design
- Quality control assessment
- Alignment and filtering (STAR alignment with Cell Ranger)
- Gene expression
- Cell type annotation

**Methylation**

- CNS tumor classification via NIH Methylscape (CNS tumors only; subject to API limits)
- Preprocessing — m-values, beta values, CNVs
- Probe annotation

**Neoantigen Discovery (paired RNA-Seq and DDA proteomics)**

- Translation of DNA SNVs and/or RNA fusions/splice events into peptides
- Peptide identification with custom FASTA (FragPipe)
- Peptide ranking

**Kids First DNA long-read (PacBio, ONT)**

- Available on request

**LOH assessment**

- AlleleCouNT for paired germline/tumor samples

## Software Development / Engineering

- New workflow development (GitHub, local, EC2)
- New workflow development (CWL, EC2)

## Manuscript Contributions

- Poster review — collaborative, not charged
- Figure compilation — collaborative, not charged
- Manuscript writing and review — collaborative, not charged
- Public code releases — final run script, repo readiness, GitHub release, Zenodo DOI

## Bioinformatics Consultation

- Experimental design
- Grant review and cost estimation
- Grant writing
- Clinical trial readiness (typically a 6+ month engagement)

## Custom Projects

- Custom engineering (e.g. FreezerPro API extract, transform, and ingest to REDCap, Dashboard or App design and creation)
- Custom scientific analyses (e.g. understanding the effects of CAR-T treatment on the tumor microenvironment using paired miRNA-Seq and RNA-Seq across species)

## Administration & Infrastructure

- Scheduling, project management, and PI coordination
- Project meetings
- CAVATICA API support
- Data file warehouse
- Automations
- Bug fixes and upgrades

---

## Workflows in Development

The following workflows are newer or still under active development. 
Availability and turnaround may vary — check with the Core when scoping a project that needs one of these.

- Methylation CNV segmentation and annotation
- Visium spatial transcriptomics
- TIRTL-seq
- Ribo-seq + RNA-seq
- Kinnex long-read RNA-Seq
- IsoLaser for isoform-level analysis of long-read RNA-Seq
- VarRNA for RNA variant calling