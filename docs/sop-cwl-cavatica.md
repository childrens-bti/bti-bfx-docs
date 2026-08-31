---
icon: material/sitemap-outline
---

# SOP: Quality Assurance & Best Practices for Running CWL Workflows on Cavatica
**Version:** 1.0  
**Date:** 2026-01-15  
**Team:** BTI-BFX-Engineering

---

## Purpose
This SOP defines standards and procedures for designing, validating, launching, and exporting data from **CWL workflows run on Cavatica**, focusing on reducing task deletions, reruns, and increasing workflow reliability.
See [CAVATICA Compute](cavatica.md) for account access, project naming, and general usage.

---

## Scope
This SOP applies to all CWL workflows executed on Cavatica.

---

## Guiding Principles
- Reproducibility  
- Validation before execution  
- Predictable outputs  
- Immutability  
- Traceability  

---

## Pre-Run Task Preparation (Cavatica-Specific)

### File Inputs
- Validate file types and metadata  
- Confirm file IDs  
- Verify references  

### CWL Workflow Validation (Before Depolying to Cavatica)
- Use `cwltool --validate`  
- Validate input schema  

### Versioning Requirements
- Document CWL version, Docker digest, reference bundle  

### CWL Runtime Settings
- Set resource requirements  
- Avoid hard-coded paths  

---

## Workflow Design Standards

### Required Validation Steps
- Input metadata validation  
- Reference integrity checks  
- File existence checks  

### Output Contract (Cavatica)
- Define final outputs  
- Checksums  
- Naming conventions  

### Logging Requirements
- Structured logs  
- Summary log  
- Docker stdout/stderr  

### Workflow I/O Documentation (File Types + Globs + Paths)
- Document expected input file extensions (e.g., `.fastq.gz`, `.bam{,.bai}`, `.vcf.gz{,.tbi}`, `.json/.tsv`)  
- Document expected output file extensions and where they land (e.g., `outputs/**`, `logs/**`, `qc/**`, `checksums/**`)  
- Include canonical glob patterns for discovery/validation (e.g., `inputs/**/*.{fastq,fq}.gz`, `outputs/**/*.vcf.gz{,.tbi}`)  
- List potential/allowed project paths (Cavatica project folders, mounted reference locations) and prohibit hard-coded absolute paths  

---

## Task Planning & Execution on Cavatica

### Small-Batch Validation
Run 1–3 samples end-to-end before full launch.

### Peer Review
Another engineer reviews inputs, versions, references.

### Criteria Before Full Launch
All validations passed, parameters confirmed.

### Output Basename Scheme
When creating tasks, the output basename is typically the baid of the sample being analyzed. For the somatic and consensus workflows which use both tumor and normal samples, the basename should be in the format `{tumor_id}_{normal_id}`. For the impact workflow, which using both tumor and RNA data, the basename format should be `{tumor_id}_{rna_id}`. When creating workflows using the cli, the task id is automatically added during task creation.

---

## Preventing Reruns
Use version-locked references, docker digests, validation scripts.

---

## Preventing Task Deletion (Cavatica Best Practices)
- Use dev projects for testing  
- Enforce naming conventions  
- Avoid overwriting outputs  

---

## Exporting Data Safely from Cavatica

### Pre-Export
Validate outputs, checksums

### Post-Export
Spot QC, document export details

---

## Documentation Requirements
- README  
- Input schema  
- Output contract  
- Changelog  

---

## Continuous Improvement
Quarterly reviews, post-mortems.

---

## Roles & Responsibilities
| Role | Responsibility |
|------|--------------|
| Engineering | Workflow development |
| Data Ops | QC & exports |
| Leads | Approvals |
| All Users | SOP compliance |

---

## Appendices

### Sample Task Description Template
```
Workflow: WGS Alignment v2.4.0  
Commit: f1c2e7a  
Docker: quay.io/childrens-bti/wgs:v2.4.0@sha256:...  
Reference: GRCh38_refbundle_v1  
Inputs validated: Yes  
Export path: s3://bti-data/harmonization/wgs/v2.4.0/  
QC reviewer: name  
Run date: YYYY-MM-DD
```

### Metadata Schema Template  
(To be filled per workflow)

### Output Contract Example  
(To be added per workflow)

---

**End of Document**
