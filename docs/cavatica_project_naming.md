# Cavatica Project Naming

During a harmonization project, after the harmonization ticket has been made, the manifest created and reviewed, and the data have been imported to AWS; the next step is to create the Cavatica project.

Cavatica projects must be named using the following format:

`{pi}-{experimental_strategy}-{non-human-marker}-itt-{harmonization_ticket_number}-{harmonization or relatedness}`

Studies such as the Impact Trial or other future trials may use a different naming scheme and will be documented separately.

## Definitions

PI is the name of the principal investigator of the lab that will be responsible for the study the data are for.

Experimental strategy is the sequencing strategy used to generate the data. Should be wgs, wxs, rnaseq, scrna, proteomics, or similar.

The "non-human maker" is an explanation for special case harmonizations such as pdx or non-human studies.

The abbreviation "itt" stands for internal-ticket-tracker and is the central repo we use for large scale issues within the BTI. If for some reason requests are made outside of the internal-ticket-tracker, the project name should use a similarly helpful abbreviation for the repo.

Harmonization ticket number is the issue number within the internal-ticket-tracker repo.

Finally, the project name will end in "harmonization" for harmonization projects or "relatedness" for projects where multiple samples are being checked to determine if they come from the same patient.

## Explanations

If a project has multiple data types, create one project for each experimental strategy using the same harmonization ticket.

If relatedness is being checked across a harmonization(s) with multiple data types, "multi" can be used for this type of project only.

## Creating Projects

Cavatica projects must be created by making a Project Creation issue in the [cavatica_api_wrappers](https://github.com/childrens-bti/cavatica_api_wrappers/issues) repo.

## Example Project Names

rokita-rnaseq-itt-1516-harmonization

rood-rnaseq-pdx-itt-815-harmonization

## Development Projects

In generatal, dev projects should have a short helpful name and end in `-dev`. They do not need to be as strict as harmonization and relatedness projects, but should still generally be helpful to you and fellow developers. Dev projects still must be created via the cavatica_api_wrappers project creation issues.
