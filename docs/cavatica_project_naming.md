# Cavatica Project Naming

Cavatica projects must be named using the following format:

`{pi}-itt-{issue number}`

Studies such as the Impact Trial or other future trials may use a different naming scheme and will be documented separately.

## Definitions

PI is the name of the principal investigator of the lab that will be responsible for the study data.

The abbreviation "itt" stands for internal-ticket-tracker and is the central repo we use for large scale issues within the BTI. If for some reason requests are made outside of the internal-ticket-tracker, the project name should use a similarly helpful abbreviation for the repo.

Issue Number is the issue number of the work epic within the internal-ticket-tracker repo. If a project is being created for stand alone work outside of an epic, use the issue number.

## Explanation

If relatedness is being checked across multiple cohorts or harmonizations, use the newest PI and epic or ticket numbers.

If an epic has a large number of samples and will create or has created too many files (roughly 2 million) it must be split up. New projects should be created with `-batch-#` ie -batch-1 -batch-2. This should be exceptionally rare.

## Creating Projects

Cavatica projects must be created by making a Project Creation issue in the [cavatica_api_wrappers](https://github.com/childrens-bti/cavatica_api_wrappers/issues) repo.

## Example Project Name

rokita-itt-1516

## Development Projects

In general, dev projects should have a short helpful name and end in `-dev`. They do not need to be as strict as harmonization projects, but should still generally be helpful to you and fellow developers. 
Dev projects still must be created via the [cavatica_api_wrappers](https://github.com/childrens-bti/cavatica_api_wrappers/issues) Project Creation issue.
