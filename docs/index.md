# Documentation for the Rokita Lab and BTI Bioinformatics Core

Welcome to ReadtheDocs for Children's National Hospital Rokita Lab and Brain Tumor Institute (BTI) Bioinformatics team members.
This website is a centralized location that contains information about tool accessibility as well as general guidance for utilizing compute infrastructure and using reproducible practices for analytical projects.

## Responsible and Ethical Use of Bioinformatics Resources

### Ethical considerations

Please be sure to work with your PI and/or Dr. Rokita to understand which metadata, clinical data, and genomic data types are allowed to be stored in public and private spaces.
Please do not share our AWS account number or IP addresses externally or within GitHub. 
If you have questions, please ask us!

### Submitting jobs or tasks

1. HPC: When utilizing the HPC, please be mindful when submitting large or many jobs, as this is a community resource.
2. AWS: We have created an EC2 service catalog product, "BTI Research" for use by researchers in the BTI. 
Each person can utlize their own instance without affecting others' compute.
3. [CAVATICA](https://cavatica.sbgenomics.com/): We primarily utilize CAVATICA for established upstream workflows. 
Jobs will be automatically scheduled and queued based on your user capacity.

### Fiscal Responsibility 

1. AWS: Please only launch an EC2 instance type and volume for the work you will need to do to minimize costs (We are charged for instances per hour and by storage). Below are some ways you can minimize costs.
  - Always `STOP` your instance once you are finished, or if are not actively working on the instance (e.g. you have 3 meetings and will not be working on it - you can stop it and come back later).
  - `TERMINATE` your instance once you no longer need it, or if you will not be using it for an extended period of time (weeks - months).
2. CAVATICA: Use of CAVATICA requires set up of a billing group and funds.
Please work with your PI and/or Dr. Rokita if you would like to run tasks in CAVATICA.
  - The NIH has Cloud Credits available for working with specific datasets through application (e.g. [CFDE](https://docs.cavatica.org/docs/common-fund-data-ecosystem) and/or [Kids First](https://commonfund.nih.gov/kidsfirst/cloudcredits)).
3. [Cancer Genomics Cloud (CGC)](https://www.cancergenomicscloud.org/): New users of the CGC get $300 in cloud credits when they create a new account, and this can be used to run and/or test new workflows as desired.
CGC has cloud credits available through [application](https://docs.cancergenomicscloud.org/docs/credits) as well.

### Responsible Use of Artificial Intelligence (AI) in Bioinformatics

Using AI for bioinformatics (e.g. chatbots, GitHub Copilot) can drastically streamline time to project completion as it can be very useful when converting code from one language to another, developing functions, working out bugs, and more.
However, it is very important to consider the information and data we enter into a chatbot or AI assistant such as Github Copilot.
- Do _not_ paste any identifiable patient data into chatbots, whether in the form of files or free text.
- Do _not_ utilize any AI software in conjuction with GitHub or your text editor so that private repositories are not exposed.

