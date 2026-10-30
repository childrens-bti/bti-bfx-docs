---
icon: material/database-arrow-up-outline
---

# GEO Submission Instructions (Non-Human RNA-seq and Methylation Arrays)

How to submit non-human RNA-seq data (bulk or single-cell) and DNA methylation array data (Illumina Infinium) to the NCBI [Gene Expression Omnibus (GEO)](https://www.ncbi.nlm.nih.gov/geo/info/submission.html){target="_blank" rel="noopener"}.

!!! warning
    **Check GEO's current pages before each submission.** GEO changes its templates, FTP folder layout and submission steps from time to time. Steps marked **(check GEO)** are especially likely to change. The authoritative pages are [Submitting high-throughput sequence data](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"} (RNA-seq), [Submitting microarray data](https://www.ncbi.nlm.nih.gov/geo/info/spreadsheet.html){target="_blank" rel="noopener"} and [Illumina submission guidelines](https://www.ncbi.nlm.nih.gov/geo/info/geo_illu.html){target="_blank" rel="noopener"} (methylation arrays), and [Transferring files to GEO](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"} (all). See [References](#references).

---

## Overview

A GEO submission has three parts, and all three must agree exactly:

1. **Metadata spreadsheet:** GEO's Excel template describing the study, each sample, the protocols and every file. Sequencing and microarray data use **different templates**.
2. **Processed data:** e.g. count matrices (RNA-seq) or beta-value matrices (methylation arrays).
3. **Raw data:** FASTQs for sequencing, which GEO passes to SRA for you so you don't make a separate SRA submission. IDAT files for methylation arrays, which stay in GEO.

Every file name in the spreadsheet must match an uploaded file exactly, and every uploaded file must be listed in the spreadsheet with its MD5 checksum.

Rough split of work:

| Who | Does what |
|---|---|
| PI / lab | Study title, summary, design, contributors; wet-lab protocols; sample descriptions; final review |
| Core | Identifies the correct raw and processed files; data-processing protocol; file naming; checksums; upload from the HPC transfer node |

---

## File types

GEO's requirements for each kind of data are on [Submitting high-throughput sequence data](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"}. In short:

### Raw data (required)

| File | What it is | Notes |
|---|---|---|
| `*_R1_001.fastq.gz` / `*_R2_001.fastq.gz` | Read 1 and read 2 of each paired-end run | One pair per lane or run. Upload **all** lanes and runs, including top-off or re-sequencing runs that went into the counts. |
| `*_R1_001.fastq.gz` only | Single-end reads | Mark the sample as single-end in the spreadsheet. |
| `*_I1_001.fastq.gz` / `*_I2_001.fastq.gz` | Index reads (sample barcodes) | Mostly relevant for single-cell. If you upload them, list them in the paired-end section's file name 3/4 columns. |
| `*.bam` | Aligned reads | Only if FASTQs aren't available. SRA can accept BAM as raw data. Otherwise upload FASTQs. |

### Processed data, bulk RNA-seq (required)

| File | What it is | Notes |
|---|---|---|
| Raw counts matrix (`.txt`/`.tsv`/`.csv`, often gzipped) | Genes × samples integer counts from featureCounts, HTSeq, STAR `--quantMode`, RSEM or similar | GEO wants raw counts where possible. Use gene IDs (e.g. Ensembl) as the first column. |
| Normalized values (TPM, FPKM, CPM) | Genes × samples | Optional, in addition to raw counts. Say which normalization in the protocol. |
| Per-sample quantification files (e.g. Salmon `quant.sf`, RSEM `.genes.results`) | One file per sample | An alternative to a combined matrix. Rename each to include the sample name. |

A combined matrix covering all samples can usually be listed as a series-level supplementary file, or referenced from each sample row. Check [GEO's sequencing page](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"} for the current rule.

### Processed data, single-cell RNA-seq with Cell Ranger (required)

| File | What it is | Notes |
|---|---|---|
| `barcodes.tsv.gz`, `features.tsv.gz`, `matrix.mtx.gz` | The filtered feature-barcode matrix in Matrix Market format: cell barcodes, genes, sparse counts | The standard choice. From `outs/filtered_feature_bc_matrix/` (`cellranger count`) or `outs/per_sample_outs/<sample>/count/sample_filtered_feature_bc_matrix/` (`cellranger multi`). **Rename** to `<sample>_barcodes.tsv.gz` and so on. All three are needed for each sample. |
| `filtered_feature_bc_matrix.h5` (`sample_filtered_feature_bc_matrix.h5` in multi) | The same filtered matrix in one HDF5 file | Acceptable instead of, or as well as, the three MEX files. Rename with the sample name. |
| `raw_feature_bc_matrix/` or `.h5` | Unfiltered matrix with all barcodes, including empty droplets | Optional. Useful for reanalysis (e.g. ambient RNA correction). |
| `metrics_summary.csv`, `web_summary.html` | Run QC metrics | Optional supplementary files. Rename per sample if included. |
| `molecule_info.h5`, `*.cloupe`, `possorted_genome_bam.bam` | Per-molecule info, Loupe Browser file, aligned reads | Not usually submitted. The BAM is large and redundant with the FASTQs. |
| `config.csv` (`cellranger multi`) | Run configuration: reference, probe set, sample-to-barcode assignments | Optional supplementary file. It contains internal file-system paths, so many submitters give a small sample-to-barcode mapping file instead (see section 3). |
| Analysis objects (Seurat `.rds`, AnnData `.h5ad`) | Normalized, clustered and annotated data | Optional supplementary files. Large. Count matrices are still expected. |

### Methylation arrays (Illumina Infinium: EPIC v1/v2, 450K, mouse MM285)

GEO treats these as **microarray** submissions, not sequencing. They use the microarray metadata template and a GEO **platform** record (GPL) for the array, and nothing goes to SRA. See GEO's [Illumina submission guidelines](https://www.ncbi.nlm.nih.gov/geo/info/geo_illu.html){target="_blank" rel="noopener"} for the current required files **(check GEO)**.

| File | What it is | Notes |
|---|---|---|
| `<SentrixID>_<R0xC0x>_Grn.idat` and `..._Red.idat` | Raw green and red channel intensities from the scanner, two per sample | **Raw data, required.** Upload **both** channels for every sample. Keep the original names. They're already unique, and they record chip and position. |
| Processed matrix: beta values + detection p-values | Probes × samples. One beta-value column per sample, each followed by its detection p-value column | **Processed data, required.** Output of minfi, SeSAMe or similar, after your QC and normalization. Column headers must match the sample names in the spreadsheet. Usually one tab-delimited file for the whole series. |
| Signal matrix: methylated + unmethylated intensities | Probes × samples. Unmethylated and methylated signal columns per sample | Usually requested alongside the beta-value matrix for Illumina methylation **(check GEO)**. |
| M-values or other derived tables | Further-processed values | Optional supplementary files. |

Platform (GPL): look up the GPL that matches your array **and manifest version** (e.g. EPIC v1 vs v2, MM285) by searching [GEO platforms](https://www.ncbi.nlm.nih.gov/geo/browse/?view=platforms){target="_blank" rel="noopener"}. Enter that GPL in the spreadsheet. If none matches, GEO will ask for the manifest and create one.

---

## 1. Identify the correct data

Do this first. It's the easiest step to get wrong.

- **Use the processed data the paper's analysis used.** If the analysis downloads a versioned data release, or there have been several processing runs (e.g. before and after re-sequencing), confirm which one the analysis used and upload that. Compare MD5s against the release or analysis inputs:
  ```bash
  md5sum <candidate_file>                 # compare against the release's checksum list
  ```
- **Include every FASTQ that went into those counts,** including top-off or re-sequencing runs. Check the pipeline configuration (e.g. Cell Ranger's `--fastqs` or the `[libraries]` section of `config.csv`) and the FASTQ folder. The first line of each FASTQ shows its instrument and run ID, which tells separate runs apart:
  ```bash
  gzip -dc file.fastq.gz | head -1        # @<instrument>:<run number>:<flowcell>:<lane>:...
  ```
- **Don't rely on folder names alone.** Names like `topoff`, `combined` or `final` don't always describe what's inside. Check the contents (read counts in the run summary, checksums, dates).
- **Multiplexed libraries** (10x Flex, cell hashing, CellPlex, pooled bulk libraries demultiplexed after sequencing): the FASTQs contain every sample in the pool, including any that aren't in the study. Raw reads can't be split by sample, so upload the pooled FASTQs once (see section 3).

---

## 2. Create the submission and get upload credentials (check GEO)

1. Sign in to GEO with an NCBI account (the PI's, or whoever will own the submission).
2. Open GEO's file transfer page ([Transferring files to GEO](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"}). It shows:
   - the FTP host (`ftp-private.ncbi.nlm.nih.gov`), username (`geoftp`) and password
   - your **personal upload folder**, under `uploads/` and named after your account
3. Inside your personal folder, create **one subfolder for this submission** (e.g. `<lab>-<assay>-<year>`) and put every file for the submission in it.
4. Download the **current** metadata template. Templates change, so don't reuse an old copy:
   - RNA-seq: from [GEO's sequencing submission page](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"}
   - Methylation arrays: the microarray template from [Submitting microarray data](https://www.ncbi.nlm.nih.gov/geo/info/spreadsheet.html){target="_blank" rel="noopener"} (see also [Illumina guidelines](https://www.ncbi.nlm.nih.gov/geo/info/geo_illu.html){target="_blank" rel="noopener"})

!!! danger "Credentials"
    Keep the FTP password out of scripts, shared documents, Slack and AI tools. Type it in when prompted, or read it into an environment variable with `read -rs`.

---

## 3. Fill in the metadata spreadsheet

Work on a copy of the template. Read the EXAMPLE tabs (there are separate ones for RNA-seq and scRNA-seq), and hover over red-triangle cells for GEO's notes. GEO's field-by-field requirements are on [Submitting high-throughput sequence data](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"}.

### Study section
- **Title, summary, experimental design:** from the PI. The design should explain how samples relate to files, especially for pooled or multiplexed libraries.
- **Contributors:** one per row, `Firstname,Lastname`.
- **Supplementary files:** study-level files, such as a combined counts matrix or a sample-to-barcode mapping.

### Samples section (one row per GEO sample)
- **Library name:** unique. Use the names in the processed file prefixes and the analysis code. Avoid inconsistent internal IDs (e.g. pipeline sample IDs with typos).
- **Title:** unique and readable. Use GEO's convention for replicates, `<condition>, biol rep 1` / `<condition>, biol rep 2`. Name treatments and constructs consistently, the same way as in the manuscript.
- **Characteristics** (tissue, cell line, cell type, genotype, treatment, etc.): fill in at least one of tissue, cell line or cell type.
- **Processed data files:** one file per column. Each file name must be **unique across the whole submission**, so never use plain `matrix.mtx.gz` or `counts.txt`. Prefix each with the sample or library name.
- **Raw files:** if you need more columns than the template has, add them and fill in the header (`raw file`) for each new column. Otherwise GEO may ignore them.
- **Instrument model:** take it from GEO's list. The instrument ID in the FASTQ header helps (e.g. `LH…` is NovaSeq X, `A…` is NovaSeq 6000, `VH…` is NextSeq 2000).

**Multiplexed or pooled libraries:**
- One row per biological sample, with that sample's **processed files only**.
- One extra row for the physical pooled library, with the **raw FASTQs only**, listed once. Its description explains that it holds the shared reads and how samples were assigned.
- A supplementary mapping file (e.g. `sample_barcode_mapping.csv` with `library_name,barcode`) so readers can connect the pooled reads to samples.
- Optional: a sentence noting any pooled samples that aren't part of the study.

### Protocols section
- **Extraction and library construction:** from the lab.
- **Data processing:** from whoever ran the analysis. Include each tool and its version (e.g. aligner or Cell Ranger version), the reference genome and annotation version, any probe set or barcode whitelist, filtering and normalization, and how multiplexed samples were assigned.
- **Genome build** and a **description of the processed file format** are required.

### Paired-end section
- One row per read pair: R1 in `file name 1`, R2 in `file name 2`. Index reads (I1/I2) go in columns 3–4 if you upload them. Every file here must also appear in the Samples section.

### MD5 Checksums tab
- Raw files on the left, processed and supplementary files on the right. Every uploaded file needs a full 32-character MD5.
- Paste checksums straight from `md5sum` output rather than retyping them. A dropped character is easy to miss.

### Methylation array differences
The microarray template is laid out differently, but the same rules apply (unique sample names and titles, every file listed, full checksums). The main differences:
- **Platform:** each sample row gives the array's GPL accession instead of an instrument model.
- **Raw files:** each sample lists its own **two** IDATs (`_Grn.idat` and `_Red.idat`). There's no paired-end section.
- **Processed data:** the matrix files are usually listed once for the series, and each sample's **column headers** in the matrix must match its sample name or title exactly as GEO's template instructs **(check GEO)**.
- **Characteristics:** include tissue/cell type, sex, and preservation (e.g. fresh frozen vs FFPE). FFPE affects data quality and reviewers expect it.
- **Protocols:** extraction (DNA isolation), bisulfite conversion kit, hybridization and scanning (scanner model), and data processing: software and version (e.g. minfi, SeSAMe), normalization method, probe and sample filtering (detection p-value threshold, SNP or cross-reactive probes, sex chromosomes), and the manifest version.
- **Sample sheet:** keep the Illumina sample sheet (Sentrix ID and position per sample) to fill in the IDAT names and check them. A swapped position is the most common mistake.

---

## 4. Prepare files on the HPC transfer node

Run everything on the transfer node, not on a laptop over a network share. The share's path on the transfer node is usually different from its path on your computer (e.g. `/Volumes/...` on a Mac).

### Copy and rename processed files
- Put everything to upload in one folder, renamed to match the spreadsheet.
- Copy, don't move. Keep the original pipeline output untouched.
- After copying, check each copy's MD5 against the source (or the analysis release) to catch bad copies and sample mix-ups.
- For pipeline outputs organized by sample folder (e.g. Cell Ranger), a short script that maps `<pipeline_sample_id>` → `<geo_library_name>` and copies `<sample_dir>/<file>` → `<geo_library_name>_<file>` avoids manual mistakes. Check the mapping against the pipeline config before copying.

### Methylation arrays
- Copy the IDATs for the samples in the submission into one upload folder, keeping their original names. Check that each sample has both `_Grn` and `_Red`:
  ```bash
  ls *_Grn.idat | wc -l; ls *_Red.idat | wc -l      # should both equal the number of samples
  ```
- Export the processed matrices as tab-delimited text (gzipped if large). Make sure the column headers match the spreadsheet's sample names.
- IDATs are small (about 8–15 MB each), so even large array studies upload quickly. Option B (FileZilla) in section 5 is fine.

### Compute checksums
`md5sum` uses one CPU core per file, so run several files in parallel:
```bash
cd /path/to/FASTQ/dir                 # or the IDAT folder: use *.idat instead of *.fastq.gz
nohup sh -c 'ls *.fastq.gz | xargs -P 8 -n 1 md5sum | sort -k2 > /path/elsewhere/fastq_md5.txt' &
```
- Write checksum files **outside** the upload folders so they aren't uploaded.
- Rough timing: one core hashes about 500–800 MB/s, so in parallel the largest file sets the total time. A few hundred GB usually takes under an hour on a transfer node, but can take many hours over a network share from a laptop.

### Final check before uploading
- The upload folders contain **only** files listed in the spreadsheet. Remove checksum files, configs, logs and `.DS_Store`.
- Every file name in the spreadsheet exists in the folders, and every file in the folders is in the spreadsheet.
- The checksums in the spreadsheet match the files.

---

## 5. Upload the files

GEO's FTP instructions are on [Transferring files to GEO](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"}. That page gives the host, username, password and your personal upload folder (you need to be signed in), and it covers command-line FTP and graphical clients. There are two ways to upload:

| | Option A: `lftp` on the transfer node | Option B: FileZilla on your computer |
|---|---|---|
| Best for | Large raw data (FASTQs, tens to hundreds of GB) | Small submissions, or processed/supplementary files only |
| Data path | Storage → transfer node → GEO | Storage → your computer → GEO |
| Survives laptop sleep or disconnect | Yes (with `screen`/`tmux`) | No: the computer must stay awake and connected |
| Resume after failure | `mirror -R --continue` | Re-queue failed files (see below) |

For large FASTQ sets, use Option A. With FileZilla, every byte passes through your computer, often over a network share first, which is much slower and needs the computer to stay online for hours.

### Option A: lftp from the HPC transfer node

Use `lftp` rather than plain `ftp`. It can resume interrupted transfers and upload several files in parallel, which matters for large FASTQs.

```bash
screen -S geo                                   # or tmux, so the upload survives a disconnect
lftp -u geoftp ftp-private.ncbi.nlm.nih.gov     # enter the password when prompted
lftp> set ftp:ssl-allow no                      # only if you get TLS/certificate errors
lftp> cd uploads/<your_personal_folder>
lftp> mkdir <submission_folder>
lftp> cd <submission_folder>
lftp> mirror -R --dry-run /path/to/processed .  # preview: lists what would upload
lftp> mirror -R --parallel=4 /path/to/processed .
lftp> mirror -R --parallel=8 /path/to/fastqs .
lftp> ls -l                                     # check file count and sizes
```

- `mirror -R` uploads a local folder (local to remote). Without `-R` it downloads.
- Give the **local** folder as a full path. A bare `.` means lftp's local working directory (`lpwd`), probably your home directory.
- The trailing `.` uploads into the current remote folder rather than creating a subfolder.
- If the connection drops, reconnect, `cd` back, and rerun the same command with `--continue`.
- Local commands inside lftp: `lpwd`, `lcd /path`, or `!ls -l /path`.
- Speeds to GEO of tens of MB/s per transfer are typical. At about 70 MB/s, 100 GB takes about 25 minutes per transfer. With parallel transfers, the largest file sets the total time.

### Option B: FileZilla (graphical FTP client)

[FileZilla](https://filezilla-project.org/){target="_blank" rel="noopener"} is a free FTP program for macOS, Windows and Linux. GEO's [Transferring files to GEO](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"} page lists graphical FTP clients as an alternative to the command line. Follow that page if its settings differ from the ones below.

**Before you start**
- Get the files onto (or mounted on) the computer running FileZilla, already renamed and checked as in section 4.
- Take the FTP host, username, password and personal upload folder from GEO's transfer page. Don't save the password in FileZilla on a shared computer.
- Stop your computer from sleeping during the upload (macOS: System Settings → Battery/Energy, or run `caffeinate -i` in Terminal while it runs).

**1. Set up the connection** (File → Site Manager → New site)

| Setting | Value |
|---|---|
| Protocol | FTP - File Transfer Protocol |
| Host | `ftp-private.ncbi.nlm.nih.gov` (as given on GEO's transfer page) |
| Port | leave blank (21) |
| Encryption | *Use explicit FTP over TLS if available*. If connecting fails or file listings hang, change this to *Only use plain FTP (insecure)*, which is the same as `set ftp:ssl-allow no` in lftp. |
| Logon Type | *Ask for password* |
| User | `geoftp` |

Then, on the **Transfer Settings** tab, tick *Limit number of simultaneous connections* and set it to 2–4. Click **Connect** and enter the password from GEO's transfer page when asked.

**2. Change these settings once** (FileZilla → Settings on macOS, Edit → Settings on Windows)
- **Transfers → File Types:** set the default transfer type to **Binary**. In ASCII mode, `.gz`, `.h5` and other binary files get corrupted.
- **Connection → Timeout:** raise it (e.g. 120 seconds) or set it to 0 (no timeout). Large uploads can sit for a while at the end of a file while the server finishes writing it.
- **Transfers → File exists action:** for uploads, choose *Resume file transfer* (or *Ask*) so a retry continues partial files instead of starting again.

**3. Go to your upload folder**
- In the right-hand (**Remote site**) panel, type `/uploads/<your_personal_folder>` in the path box and press Return. Use the folder name exactly as shown on GEO's transfer page.
- Right-click → **Create directory and enter it**, and name it for this submission.

**4. Upload**
- In the left-hand (**Local site**) panel, open the folder of prepared files.
- Select all the files to upload (Cmd/Ctrl+A) and drag them into the remote panel. Drag the files, not their parent folder, unless you want a subfolder on GEO's side.
- Repeat for each folder (e.g. processed files, then FASTQs). Files are queued at the bottom of the window, and the **Queued files / Failed transfers / Successful transfers** tabs show progress.

**5. Handle failures**
- If anything appears under **Failed transfers**, select it, right-click → **Reset and requeue selected files**, then **Transfer → Process Queue**. With *Resume* set in step 2, partial files continue where they stopped.
- If FileZilla quits or the computer restarts, reconnect, drag the same files again and choose **Resume** for any that already exist.

**6. Verify**
- In the remote panel, switch to the detailed list view and compare the **file count** and **file sizes** with the local files. Sizes must match exactly. A smaller remote file means the upload was incomplete, so resume it.
- Ignore the date/time column. GEO's server shows upload times, not the original file dates.

Once everything is there, go on to section 6.

---

## 6. Submit the metadata and notify GEO (check GEO)

1. Once all files are uploaded and the remote listing shows the expected count and sizes, submit the completed metadata spreadsheet through GEO's submission web page (check GEO for the current method).
2. Tell GEO the upload is complete using their submission form, giving the upload subfolder name.
3. A GEO curator reviews it and may email questions (common ones: missing software versions, unclear sample relationships, file-name mismatches).
4. Once approved, GEO issues a GSE accession and a **reviewer token** for private access during peer review. Set the release date to publication. You can bring it forward later. See the [GEO FAQ](https://www.ncbi.nlm.nih.gov/geo/info/faq.html){target="_blank" rel="noopener"} for reviewer access and release dates.

---

## References

GEO's own documentation is the authority. Check it before each submission, because GEO changes templates, folder layout and submission steps from time to time.

| Topic | GEO page |
|---|---|
| Overview of what GEO accepts and how to submit | [Submitting data](https://www.ncbi.nlm.nih.gov/geo/info/submission.html){target="_blank" rel="noopener"} |
| High-throughput sequencing submissions: metadata template, raw and processed data requirements, single-cell guidance | [Submitting high-throughput sequence data](https://www.ncbi.nlm.nih.gov/geo/info/seq.html){target="_blank" rel="noopener"} |
| Microarray submissions, including methylation arrays: metadata template | [Submitting microarray data](https://www.ncbi.nlm.nih.gov/geo/info/spreadsheet.html){target="_blank" rel="noopener"} |
| Illumina arrays (incl. Infinium methylation): required raw IDATs and processed/signal matrices | [Illumina submission guidelines](https://www.ncbi.nlm.nih.gov/geo/info/geo_illu.html){target="_blank" rel="noopener"} |
| Finding the platform (GPL) for your array | [GEO platform browser](https://www.ncbi.nlm.nih.gov/geo/browse/?view=platforms){target="_blank" rel="noopener"} |
| FTP host, credentials, personal upload folder, command-line and graphical (e.g. FileZilla) clients | [Transferring files to GEO](https://www.ncbi.nlm.nih.gov/geo/info/submissionftp.html){target="_blank" rel="noopener"} |
| Reviewer access, release dates, updating records, common questions | [GEO FAQ](https://www.ncbi.nlm.nih.gov/geo/info/faq.html){target="_blank" rel="noopener"} |
| Recent GEO changes (new FTP folders, web metadata upload) | [NCBI Insights: GEO posts](https://ncbiinsights.ncbi.nlm.nih.gov/tag/geo/){target="_blank" rel="noopener"} |

Other references:
- Cell Ranger output files: [10x Genomics: Cell Ranger outputs](https://www.10xgenomics.com/support/software/cell-ranger/latest/analysis/outputs/cr-outputs-overview){target="_blank" rel="noopener"}
- FileZilla: [FileZilla Client tutorial](<https://wiki.filezilla-project.org/FileZilla_Client_Tutorial_(en)>){target="_blank" rel="noopener"} and [Using FileZilla](https://wiki.filezilla-project.org/Using){target="_blank" rel="noopener"}

!!! note
    GEO reorganizes its pages from time to time. If a link above is broken, start from GEO's [Submitting data](https://www.ncbi.nlm.nih.gov/geo/info/submission.html){target="_blank" rel="noopener"} page.

---

## Checklist

- [ ] Processed files are the ones the analysis used (MD5-checked)
- [ ] All FASTQs from all sequencing runs (including top-off or re-sequencing runs) included
- [ ] Library names and titles unique; replicates titled `biol rep N`
- [ ] Every processed file name unique and prefixed with its sample name
- [ ] Every raw/processed/supplementary file in the sheet matches an uploaded file exactly (case, lane numbers)
- [ ] Extra raw-file columns have headers
- [ ] Paired-end section lists every R1/R2 pair (plus I1/I2 if uploaded)
- [ ] Tool versions, reference genome and annotation in the data-processing steps
- [ ] Multiplexed pools: pooled row for FASTQs, sample rows for processed files, mapping file
- [ ] Full 32-character MD5 for every file
- [ ] Methylation arrays: microarray template used; correct GPL for array and manifest version; both `_Grn` and `_Red` IDATs per sample; beta-value (+ detection p-value) and signal matrices with headers matching sample names; bisulfite kit, scanner, normalization and filtering in protocols
- [ ] Upload folders contain only submission files
- [ ] Upload verified (file count and sizes); metadata submitted; GEO notified
