# Harmonizations

## Common Prerequisites

To do any harmonization you will first need access to Cavatica, have the [Cavaatica API Wrapper]() repo cloned and configued, a harmonization ticket, and a manifest with bioassay ids.

For most workflows, the output_basename will be the bioassay id of the sample being run. IfFor workflows that do not follow this pattern, it will be described in the section for that workflow.

To run a harmonization:
- assign the harmonization ticket to yourself
- create the Cavatica project
- import the input data to the Cavatica project using the path in the ticket - find the correct version of each worfklow being run
- clone it locally
- upload it to the project using `sbpack`
- create options file for each workflow
- - this step will often require previous steps to be completed first
- Create the draft tasks for each sample and run the tasks using the scripts in the Cavatica API Wrappers repo

## Alignment

Data Types: DNA (WGS, WES, or Panel)

Current Worfklow File: https://github.com/childrens-bti/kf-alignment-workflow-cnh/blob/v1.0.0/workflows/kfdrc_sentieon_alignment_wf.cwl

If using fastq files as input, you must set the `input_pe_rgs_list` parameter (or `input_se_rgs_list` if using single end sequencing). The value for this should be @`RG\tID:{basename of fastq file without read number}\tLB:Not_reported\tPL:Illumina HiSeq\tSM{bioassay id}`. This parameter accepts a list of values and will need one entry per fastq pair being aligned.
