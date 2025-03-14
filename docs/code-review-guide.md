# Code Review Guidelines

All pull requests will undergo peer review, and we do so while maintaining a culture of positive peer review.

## Our Code Review model, based on [OpenPedCan](https://github.com/rokitalab/OpenPedCan-Project-CNH/blob/dev/CONTRIBUTING.md#pull-requests).

The review intends to ensure that a pull request conforms to the following basic requirements:

- The code is correct.
- The results can be reproduced in a reasonable amount of time.
- The results are expected.
- The documentation describes the purpose, methods, results, input, output, and how to run the code.
- The code follows basic style guidelines.
- The code contains comments that explain non-obvious procedures.
- The analysis is scientifically sound.

But, why?

- To foster a culture of collaboration.
- To [allow junior team members to learn from senior team members](https://smartbear.com/blog/developing-a-culture-of-mentorship-with-code-revie/), or frequently, vice versa!
- To spark knowledge transfer, not only of coding practices, but also through project-specific analyses and subject matter.
- To track our changes and thoughts over time (i.e. this is our virtual lab notebook).
- To maintain our high standard of reproducibility and rigor.
- To have all code, figures, and tables ready for future manuscript submission.


## Rules of thumb:

1. Always rerun the module to ensure it works and outputs can be reproduced identically.
2. Review ≤ 400 lines of code (LOC) at a time
3. Do not review for more than 60 minutes at a time.
4. Take 20 minute breaks in between reviews.

Pull requests can be reviewed using [GitHub's review interface](https://help.github.com/articles/about-pull-request-reviews/). Following are the basic guidelines for reviewing pull requests:

- Note the type of review you performed: did you look over the source code, did you look over the documentation, did you run the source code, did you look at and interpret the results or a combination of these?
- Suggest modifications or, potentially, directly suggest, ***but do not commit changes to***, the pull request.
- Explain in **detail** whether and why the suggested modifications are **necessary**, and how the modifications should be implemented specifically, so that the developers are able to follow the suggestions without misunderstanding.
- For any suggestions/comments that are related to the lines that were changed in the particular PR, make the comment underneath the code by clicking the "+" next to the code (see below images). Click "Start a review" for the first comment, and afterwards, click "Add single comment" to keep all comments within the same review. Click "Finish your review" once completed.

![Screenshot_2023-07-09_at_2.36.59_PM.png](img/Screenshot_2023-07-09_at_2.36.59_PM.png)

![Screenshot_2023-07-09_at_2.39.03_PM.png](img/Screenshot_2023-07-09_at_2.39.03_PM.png)

![Screenshot_2023-07-09_at_2.39.37_PM.png](img/Screenshot_2023-07-09_at_2.39.37_PM.png)

- If there are any comments/suggestions that are **outside** of the code changes this particular PR, for example, any questions about the results, or any lines of code (although not changed) that seemed puzzling, mention them as comments after you click "Finish your review". The permalinks of the referenced results or code can be obtained by the following procedure: click the "Commits" tab of the pull request, browse the repository at a specific commit that contains the referenced results or code by clicking the `<>` button of the commit row, go to the referenced file in the repository to get file or line permalinks.
- If the suggested modifications are extensive refactoring or re-designing without any change on the code behaviors, results or run-time, consider submitting a new issue for the refactoring or re-designing, and discussing the priority and specific implementations in the new issue, after the pull request under review is merged, so that the pull request under review will not be kept open for lengthy discussions and commits on extensive refactoring or re-designing that are out of the scope of the original pull request addressed issue.

Before a repository maintainer merges a pull request, there must be at least one affirmative review. If there is any unaddressed criticism or disapproval, a repository maintainer will determine how to proceed and may wait for additional feedback.

## Merging approved pull requests

If working on a collaborative repository, and a pull request is approved, please do **not** merge it immediately. Instead, wait for the repository maintainer to coordinate with you on when to merge the pull request and whether the pull request should be updated with the latest `dev` or `main` branch. The coordination can reduce the workload of developers for checking whether the `dev` or `main` branch updates by merging other pull requests will affect their own pull requests.

## Additional Code Review Resources

[Fred Hutch Data Science Lab](https://hutchdatascience.org/code_review/index.html#resources-for-lab-developers)

[SmartBear Code Review](https://smartbear.com/learn/code-review/best-practices-for-peer-code-review/)

### ALSF GitHub and Code Review Workshop

The [**Childhood Cancer Data Lab**](https://www.ccdatalab.org/) develops tools and training programs to empower childhood cancer researchers to utilize data to make more robust discoveries. 
The Childhood Cancer Data Lab is an initiative of [**Alex's Lemonade Stand Foundation**](https://www.alexslemonade.org/).

This workshop will introduce concepts in version control and project management with `git` and GitHub, with a focus on analytical code from the perspective of both code authors and reviewers.

**The material in this workshop will assume participants have some practical experience using `git` and GitHub.** You may wish you review the [`git` resources](https://alexslemonade.github.io/2023-chop-training/reproducibility_resources.html#git) we’ve compiled to help you get started.

Materials:

- [Website](https://alexslemonade.github.io/2023-chop-training/reproducibility_resources.html)
- [Slides](https://alexslemonade.github.io/2023-chop-training/workshop-schedule.html)

Recordings:

- [01 Intro to Git, Part 1](https://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fhubmail.alexslemonade.org%2Fe3t%2FCtc%2F2K%2B113%2FcCZ5l04%2FVXcQp67ZFQjwW5z-KWW6rcFRmW5BVC1m520wnrN4xH9dF3qgyTW7lCdLW6lZ3n9W4Z87tx3S8HltW34G7ZJ6HnnywW13W_fl8gXBDLW3cvG-36_4-3dW4jR_8b5NljP5W3lQKBK5YX-qDW3RB5xY3hkBlMF16c1X6WHgNW4trzGJ5w_hdKW4hWC8n2GcM1HN5_C9w6lCsnBN2qDn7P9sXDrW37bT0B1wzJRCVqLStN7x8PS2W6cvyRQ1sl0z0N82Wfm7lkZHFW3xxTdK2RYn1cVSp8CM28jTkBW5n1HKD3W61qbW85qDkC7f8gSWN4HVmP69L5wMW1vKbhB1FKn6YW6-06qt4rd4yPN7PBHVC5vtGhf2YN8bd04&data=05%7C01%7CHARENZAJ%40chop.edu%7Ca64f38addef841da910f08db992067ce%7Ca611241607b041a59bb1d146b575c975%7C0%7C0%7C638272136688221416%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=O5aUdmL7PCsmyDNZoMtLXYHAvPWeBBCwIdwgKvAV1QQ%3D&reserved=0)
- [02 Intro to Git, Part 2](https://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fhubmail.alexslemonade.org%2Fe3t%2FCtc%2F2K%2B113%2FcCZ5l04%2FVXcQp67ZFQjwW5z-KWW6rcFRmW5BVC1m520wnrN4xH9dF3qgyTW7lCdLW6lZ3k_VSRFTf6T2CmTW12q8_l3_vm_rW1wWkBp1y15ThW60YR_L1bJ9-VW1H1bLB3WVx8cN6ym_48fXCjgW1H-6tF64B12ZW1cpkhZ4cP2gbN4ThVrTM5XX5W48242c1zd9nHW50WRTW8r-GSzW558W-d26_f5WW2BL24P5JlbmQW1lGHgF1_Lj6fW6Vg_5V7wJh_jW8HmFy87xLv92W33qcy957PCdCN4NTT7b3GH2RW4B8CzR3pYkXqW8zyCb-3jBzypW7wq0XZ5KzqYdN6sfGw89GZHBW50nSdj4R3f1DW6pC77D2_XmyNf29hH5P04&data=05%7C01%7CHARENZAJ%40chop.edu%7Ca64f38addef841da910f08db992067ce%7Ca611241607b041a59bb1d146b575c975%7C0%7C0%7C638272136688221416%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=6M12P0ILG1sCRZZRjCfpDZJUrIfVyOzBF1NuQwxb05g%3D&reserved=0)
- [03 Intro to analytical code review, Part 1](https://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fhubmail.alexslemonade.org%2Fe3t%2FCtc%2F2K%2B113%2FcCZ5l04%2FVXcQp67ZFQjwW5z-KWW6rcFRmW5BVC1m520wnrN4xH9dF3qgyTW7lCdLW6lZ3nHW1jtY5473R8GcN6T7jZh4tPtyW36gMrt8LFvM4W35GyG410L8sjVSqFyR2G1LjBW6ddC_n9f74fLW1xt7ry6F6rcCW8QsKtw8_Y3CNW5R5y2T9hSYh0V8Zpxx1H5Fr3W6gfXPW7Mc7SCVLPHlS8LBNmKW8nmQt25FS5N4MH6LG-7jHNzW69rgyw1QTpJHW5x2BGT8Mnsn1VF0DK22xZLKjW95bLxv5fGcBdW70hK537FNFV9W8J9lH_5n_VQTW8FfZbF7l1cDPV4_kny8fJ29zW3NLGgQ5czxGKW7GHMtD7PqsSrf29_GDq04&data=05%7C01%7CHARENZAJ%40chop.edu%7Ca64f38addef841da910f08db992067ce%7Ca611241607b041a59bb1d146b575c975%7C0%7C0%7C638272136688221416%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=zojxG7xCmbOy2ilucUZ6ZRQ4TJZXQYtQ6eYqwQU0sEc%3D&reserved=0)
- [04 Intro to analytical code review, Part 2 (1/2)](https://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fhubmail.alexslemonade.org%2Fe3t%2FCtc%2F2K%2B113%2FcCZ5l04%2FVW7JLV39xwRQW98vLNf4F-VXgW50jS-p522G9xN58csPP3qgyTW7lCdLW6lZ3q4W9gYpJW8w9mPtW7F_m8x84RKgyW1v1NmP8nQQbZW3tsJnG1_B4fmW7RQx_F3vJs9KW1DVRTG4XmYVXW4l2M0F6mhpl0W5CXx5Q2z2ys0V1--1p981ZBjW63y65238n35qN5THnkwFsPXhW2mM0RC8wtT66W1rT4JR40z5JFW8mBS0D418zQdW5b8L942y0ftwW54YPb34rYgRpW5DZfd87513wNW15dJhp2CjWbTW2JrM7C4j5vsWW5lfQ8P7YLFGQN5mfSbkC4yTZW74lc657L7JD7W6JqG9b4G_fBPW8b2CcV7ZPmyFf5LBDwY04&data=05%7C01%7CHARENZAJ%40chop.edu%7C8c97f9ae8ef94b456e0008db99e9acf7%7Ca611241607b041a59bb1d146b575c975%7C0%7C0%7C638273001138986564%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=OP0OekKux%2F1VopGrwawJdot5N1AJ5QtPRdF6iNoyscE%3D&reserved=0)
- [05 Intro to analytical code review, Part 2 (2/2)](https://nam10.safelinks.protection.outlook.com/?url=https%3A%2F%2Fhubmail.alexslemonade.org%2Fe3t%2FCtc%2F2K%2B113%2FcCZ5l04%2FVW7JLV39xwRQW98vLNf4F-VXgW50jS-p522G9xN58csPP3qgyTW7lCdLW6lZ3n7W4csbnf68z3vJW2nCDLy3C6F8XW1Zw8JC6WJh9TW1nHXjW89Y81JW6PjVqp5DCnT9W470hP33_PlpnVz0JXc6tdFCzVmwckm4VRCmSVgBvzT27DsbwVMglFq37v-nHW2s8Ftj8DWncCN6SQ8r8X0spDW7Fm23h2WdPQ2W1VhcHl2_N2p7W1WYvls7JgGDkW6F8L1481cmxMW4MVrpK4L1bWFW6cpvdx4NG0tvW2j8hXP89qD0xW31dwm193BwFbN6hPn0lYl6csW6Ww_707lfH34V-r2KQ43WkV_W1pRj_45nmTSGf4Mz-Zz04&data=05%7C01%7CHARENZAJ%40chop.edu%7C8c97f9ae8ef94b456e0008db99e9acf7%7Ca611241607b041a59bb1d146b575c975%7C0%7C0%7C638273001138986564%7CUnknown%7CTWFpbGZsb3d8eyJWIjoiMC4wLjAwMDAiLCJQIjoiV2luMzIiLCJBTiI6Ik1haWwiLCJXVCI6Mn0%3D%7C3000%7C%7C%7C&sdata=cERIzBNyxFsS8S7qYWl8JN558rlsJ595LAN3HQVknew%3D&reserved=0)
