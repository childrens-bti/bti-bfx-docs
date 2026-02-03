# SOP: Quality Assurance & Best Practices for Running CWL Workflows on Cavatica
**Version:** 1.0  
**Date:** 2026-01-15  
**Team:** BTI-BFX-Engineering

---

# **Table of Contents**
1. [Purpose](#1-purpose)  
2. [Scope](#2-scope)  
3. [Guiding Principles](#3-guiding-principles)  
4. [Pre-Run Task Preparation (Cavatica-Specific)](#4-pre-run-task-preparation-cavatica-specific)  
   - [File Inputs](#41-file-inputs)  
   - [CWL Workflow Validation](#42-cwl-workflow-validation)  
   - [Versioning Requirements](#43-versioning-requirements)  
   - [CWL Runtime Settings](#44-cwl-runtime-settings)  
5. [Workflow Design Standards](#5-workflow-design-standards)  
   - [Required Validation Steps](#51-required-validation-steps)  
   - [Output Contract](#52-output-contract-cavatica)  
   - [Logging Requirements](#53-logging-requirements)  
6. [Task Planning & Execution on Cavatica](#6-task-planning--execution-on-cavatica)  
   - [Small-Batch Validation](#61-small-batch-validation)  
   - [Peer Review](#62-peer-review)  
   - [Criteria Before Full Launch](#63-criteria-before-full-launch)  
7. [Preventing Reruns](#7-preventing-reruns)  
8. [Preventing Task Deletion](#8-preventing-task-deletion-cavatica-best-practices)  
9. [Exporting Data Safely](#9-exporting-data-safely-from-cavatica)  
10. [Documentation Requirements](#10-documentation-requirements)  
11. [Continuous Improvement](#11-continuous-improvement)  
12. [Roles & Responsibilities](#12-roles--responsibilities)  
13. [Appendices](#13-appendices)

---

# **1. Purpose**
This SOP defines standards and procedures for designing, validating, launching, and exporting data from **CWL workflows run on Cavatica**, focusing on reducing task deletions, reruns, and increasing workflow reliability.

---

# **2. Scope**
This SOP applies to all CWL workflows executed on Cavatica.

---

# **3. Guiding Principles**
- Reproducibility  
- Validation before execution  
- Predictable outputs  
- Immutability  
- Traceability  

---

# **4. Pre-Run Task Preparation (Cavatica-Specific)**

## **4.1 File Inputs**
- Validate file types and metadata  
- Confirm file IDs  
- Verify references  

## **4.2 CWL Workflow Validation (Before Depolying to Cavatica)**
- Use `cwltool --validate`  
- Validate input schema  

## **4.3 Versioning Requirements**
- Document CWL version, Docker digest, reference bundle  

## **4.4 CWL Runtime Settings**
- Set resource requirements  
- Avoid hard-coded paths  

---

# **5. Workflow Design Standards**

## **5.1 Required Validation Steps**
- Input metadata validation  
- Reference integrity checks  
- File existence checks  

## **5.2 Output Contract (Cavatica)**
- Define final outputs  
- Checksums  
- Naming conventions  

## **5.3 Logging Requirements**
- Structured logs  
- Summary log  
- Docker stdout/stderr  

## **5.4 Workflow I/O Documentation (File Types + Globs + Paths)**
- Document expected input file extensions (e.g., `.fastq.gz`, `.bam{,.bai}`, `.vcf.gz{,.tbi}`, `.json/.tsv`)  
- Document expected output file extensions and where they land (e.g., `outputs/**`, `logs/**`, `qc/**`, `checksums/**`)  
- Include canonical glob patterns for discovery/validation (e.g., `inputs/**/*.{fastq,fq}.gz`, `outputs/**/*.vcf.gz{,.tbi}`)  
- List potential/allowed project paths (Cavatica project folders, mounted reference locations) and prohibit hard-coded absolute paths  

---

# **6. Task Planning & Execution on Cavatica**

## **6.1 Small-Batch Validation**
Run 1–3 samples end-to-end before full launch.

## **6.2 Peer Review**
Another engineer reviews inputs, versions, references.

## **6.3 Criteria Before Full Launch**
All validations passed, parameters confirmed.

---

# **7. Preventing Reruns**
Use version-locked references, docker digests, validation scripts.

---

# **8. Preventing Task Deletion (Cavatica Best Practices)**
- Use dev projects for testing  
- Enforce naming conventions  
- Avoid overwriting outputs  

---

# **9. Exporting Data Safely from Cavatica**

## Pre-Export
Validate outputs, checksums

## Post-Export
Spot QC, document export details

---

# **10. Documentation Requirements**
- README  
- Input schema  
- Output contract  
- Changelog  

---

# **11. Continuous Improvement**
Quarterly reviews, post-mortems.

---

# **12. Roles & Responsibilities**
| Role | Responsibility |
|------|--------------|
| Engineering | Workflow development |
| Data Ops | QC & exports |
| Leads | Approvals |
| All Users | SOP compliance |

---

# **13. Appendices**

### A. Sample Task Description Template
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

### B. Metadata Schema Template  
(To be filled per workflow)

### C. Output Contract Example  
(To be added per workflow)

---

**End of Document**
