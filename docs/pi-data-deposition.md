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

---

## GEO (Non-Human Data)

The NCBI [Gene Expression Omnibus (GEO)](https://www.ncbi.nlm.nih.gov/geo/info/submission.html){target="_blank" rel="noopener"} is the right place for non-human functional genomics data, such as RNA-seq and methylation arrays.
See GEO's list of [data types it accepts](https://www.ncbi.nlm.nih.gov/geo/info/faq.html#kinds){target="_blank" rel="noopener"}.
It is not appropriate for human data that requires controlled access (see [dbGaP](#dbgap)).
If you're not sure whether your data belongs in GEO, [contact the Core](pi-working-with-core.md) before starting.

GEO requires both raw and processed data files, plus descriptive metadata.
The PI owns the GEO account, and the Core handles the data files and the submission:

1. **Core:** Pre-fills the GEO metadata spreadsheet with file information (file names, types, checksums) and sends it to you. If you're submitting more than one data type (e.g. RNA-seq and methylation), you'll get a separate spreadsheet for each.
2. **PI:** Completes the remaining fields and returns the spreadsheet(s) to the Core:
    - **Study information:** title, summary, overall design, and contributors.
    - **Wet lab methods:** e.g. DNA extraction through array scanning, or RNA-seq library prep and sequencing. If your paper's methods section is already written, share that.
    - **Per-sample information:** e.g. sex and preservation method (fresh frozen, FFPE).
    - **Externally processed files:** if processed data was generated outside the Core, add those files to the sheet. They must follow GEO's [processed data guidelines](https://www.ncbi.nlm.nih.gov/geo/info/seq.html#processed){target="_blank" rel="noopener"}.
3. **PI:** Creates a [GEO submitter account](https://www.ncbi.nlm.nih.gov/geo/submitter/){target="_blank" rel="noopener"} and adds Rehman Qureshi and Bailey Farrow as Submitters/Account Managers.
4. **PI:** Gets your personalized upload folder from the [GEO FTP upload page](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"} and sends the folder name to the Core.
5. **Core:** Transfers the data files and metadata spreadsheets to GEO and creates the submission.

GEO typically issues accession numbers within 5 business days of a complete submission, but plan for at least 2 months end to end (see [Data Deposition Timelines](pi-authorship-guidelines.md#data-deposition-timelines)).

Step-by-step instructions with screenshots: [GEO Submission Instructions](https://childrensnational.box.com/s/ixv13smr5jdegb9co1dmgkucexg3d5f0){target="_blank" rel="noopener"}

---

## dbGaP

!!! note
    Instructions coming soon. In the meantime, [contact the Core](pi-working-with-core.md) for help with dbGaP submissions.
