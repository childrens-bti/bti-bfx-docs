# Github Tokens

This page lists the various tokens that are used within the Rokita Lab and the BTI Bioinformatics Core organizations through secrets. 
If you are going to be managing tokens, you may need to request additional permission in the organizations and repos in which you plan to use the tokens. 
The tokens listed here are stored in the repos as secrets and used by different Actions. You don't need to include personal tokens you use locally here.

## Generating Token Documentation

GitHub token documentation can be found [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).


## Token Table

| Token Name | Organization | Expiration Date | Repos | Name in Repo | Action | Permissions | Notes |
| ---------- | ------------ | --------------- | ----- | ------------ | ------ | ----------- | ----- |
| github_add_item_token | childrens-bti | July 1, 2026 | All | ADD_TO_PROJECT_PAT | add-issues-to-project | Organization permissions: Read and Write access to organization projects. Repository permissions: Read access to metadata; Read and Write access to issues and pull requests. | This is an organization level token stored within childrens-bti and rokita-lab
| cavatica_api_wrappers_my_repo_pat | childrens-bti | July 1, 2026 | cavatica_api_wrappers | MY_REPO_PAT | make-cavatica-project | Repository permissions: Read access to code and metadata. |  |
| file-manifest-shin-my_repo_pat | childrens-bti  | April 13 2026 | file-manifest-shiny | MY_REPO_PAT | deploy-shinyapp and test-shinyapp | Repository permissions: Read access to actions, code, metadata, and secrets
| CAVATICA_TOKEN | rokitalab | NA | OpenPedCan-Project-CNH | build docker, build and push docker | build and build_and_push | Repository permissions: log into CAVATICA and push docker image. | 
| CAVATICA_USERNAME | rokitalab | NA | OpenPedCan-Project-CNH | build docker, build and push docker | build and build_and_push | Repository permissions: log into CAVATICA and push docker image. | 