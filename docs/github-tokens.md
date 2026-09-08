---
icon: material/key-variant
---

# Github Tokens

This page lists the various tokens that are used within the Rokita Lab and the BTI Bioinformatics Core organizations through secrets. 
If you are going to be managing tokens, you may need to request additional permission in the organizations and repos in which you plan to use the tokens. 
The tokens listed here are stored in the repos as secrets and used by different Actions. You don't need to include personal tokens you use locally here.

---

## Generating Token Documentation

GitHub token documentation can be found [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens).

---

## Token Table

| Token Name | Organization | Expiration Time | Repos | Name in Repo | Action | Permissions | Notes |
| ---------- | ------------ | --------------- | ----- | ------------ | ------ | ----------- | ----- |
| github_add_item_token | childrens-bti | 90 days starting July 1, 2026 | All | ADD_TO_PROJECT_PAT | add-issues-to-project | Organization permissions: Read and Write access to organization projects. Repository permissions: Read access to metadata; Read and Write access to issues and pull requests. | This is an organization level token stored within childrens-bti and rokita-lab
| actions_report_token_childrens_bti | childrens-bti | 90 days starting September 29, 2026 | https://github.com/childrens-bti/github-project-scripts | ACTIONS_REPORT_TOKEN_CHILDRENS_BTI | monthly-github-actions-report | Repository permissions: Read access to actions. | This token controls access for the monthly github actions report in the childrens-bti organization.
| actions_report_token_rokitalab | rokitalab | 90 days starting September 29, 2026 | https://github.com/childrens-bti/github-project-scripts | ACTIONS_REPORT_TOKEN_ROKITALAB | monthly-github-actions-report | Repository permissions: Read access to actions. | This token controls access for the monthly github actions report in the rokitalab organization.
| CAVATICA_TOKEN | rokitalab | NA | OpenPedCan-Project-CNH | CAVATICA_TOKEN | build and build_and_push | Repository permissions: log into CAVATICA and push docker image. | Value is created on Cavatica not in github.
| CAVATICA_USERNAME | rokitalab | NA | OpenPedCan-Project-CNH | CAVATICA_USERNAME | build and build_and_push | Repository permissions: log into CAVATICA and push docker image. |  Value is created on Cavatica not in github.
