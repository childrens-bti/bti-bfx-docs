---
icon: material/cloud-upload-outline
---

# Data Deposition

The BTI Bioinformatics Core can help deposit sequencing data to public repositories ahead of publication.
See [Services](pi-services.md) for the repositories we support, or [contact the Core](pi-working-with-core.md) to get started.

---

## SRA (Non-Human Data)

The NCBI [Sequence Read Archive (SRA)](https://www.ncbi.nlm.nih.gov/sra/docs/submit/){target="_blank" rel="noopener"} is the right place for raw, publicly shareable (non-controlled access) sequencing data such as mouse BAMs, CRAMs, and FASTQs.
It is not appropriate for human data that requires controlled access, methylation array data (IDATs), or processed data.

The PI owns the submission in the NCBI wizard, and the Core handles the data files:

1. **Core:** Fills out the SRA metadata template with the file names for your samples and sends it to you.
2. **PI:** Starts a new SRA submission, fills in the rest of the forms, and sends the Core the submission number (`SUBxxxxxxxx`).
3. **Core:** Uploads the data to the BTI SRA bucket and sends you the bucket name.
4. **PI:** Enters the bucket name in the wizard, reviews, and clicks **Submit**.

Step-by-step instructions with screenshots: [SRA Submission Instructions - Mouse](https://childrensnational.box.com/s/vat919yt8dua0nzlvf2tehho9bpowcyn){target="_blank" rel="noopener"}

SRA metadata templates: [BTI SRA Templates on Box](https://childrensnational.box.com/s/9yavr6rbga2pgnwho2d1ahwfw355ogeo){target="_blank" rel="noopener"}.

---

## GEO

The NCBI [Gene Expression Omnibus (GEO)](https://www.ncbi.nlm.nih.gov/geo/info/submission.html){target="_blank" rel="noopener"} is the right place for non-human functional genomics data, such as mouse RNA-seq and methylation arrays.
Unlike SRA, GEO requires both raw and processed data files, plus descriptive metadata.

The Core handles the data files and submission logistics; your lab supplies the study details and wet lab methods:

1. **Core:** Pre-fills the GEO submission spreadsheet with file metadata (file names, types, checksums) and sends it to you.
2. **PI:** Completes the remaining fields and returns the spreadsheet to the Core:
    - **Study information:** title, summary, overall design, and contributors.
    - **Wet lab methods:** e.g. DNA extraction through array scanning, or RNA-seq library prep and sequencing. If your paper's methods section is already written, share that.
    - **Per-sample information:** sample names (must match the processed data files), sex, preservation method (e.g. fresh frozen, FFPE), and which samples to include.
3. **Core:** Writes the data processing methods (if the Core ran the analysis) and gathers and uploads the raw files (IDATs, FASTQs) and processed matrices (beta values, signal intensities, raw counts).

For reference, see these example GEO submissions: [methylation](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE196902){target="_blank" rel="noopener"} and [RNA-seq](https://www.ncbi.nlm.nih.gov/geo/query/acc.cgi?acc=GSE232692){target="_blank" rel="noopener"}.

Full guide with field-by-field details: [GEO Submission Instructions - Mouse](https://docs.google.com/document/d/1pwVkZVikE7Z6rAJliD552ropgRTDvzK4kLLWmCsVqm0/edit){target="_blank" rel="noopener"}

---

## dbGaP

!!! note
    Instructions coming soon. In the meantime, [contact the Core](pi-working-with-core.md) for help with dbGaP submissions.
