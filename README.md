### Python Project6: PANDAS: Clean And Analyze Employee Exit Surveys
In this project, we'll clean and analyze exit surveys from employees of the [Department of Education, Training and Employment (DETE)](https://en.wikipedia.org/wiki/Department_of_Education_and_Training_(Queensland)) and the Technical and Further Education (TAFE) body of the Queensland government in Australia. The TAFE exit survey here can be found [here](https://data.gov.au/dataset/ds-qld-89970a3b-182b-41ea-aea2-6f9f17b5907e/details?q=exit%20survey) and the survey for the DETE can be found [here](https://data.gov.au/dataset/ds-qld-fe96ff30-d157-4a81-851d-215f2a0fe26d/details?q=exit%20survey).

Our stakeholders want us to combine the results for both surveys to answer the following questions:

Are employees who only worked for the institutes for a short period of time resigning due to some kind of dissatisfaction? & What about employees who have been there longer?
Are younger employees resigning due to some kind of dissatisfaction? & What about older employees?
Although both used the same survey template, one of them customized some of the answers. We'll aim to do most of the data cleaning and get you started analyzing the first question.

A data dictionary wasn't provided with the datasets. For this project, we'll use our general knowledge to define the columns.

Below is a preview of a couple columns we'll work with from the dete_survey.csv:

- ID: An id used to identify the participant of the survey
- SeparationType: The reason why the person's employment ended
- Cease Date: The year or month the person's employment ended
- DETE Start Date: The year the person began employment with the DETE

Below is a preview of a couple columns we'll work with from the tafe_survey.csv:

- Record ID: An id used to identify the participant of the survey
- Reason for ceasing employment: The reason why the person's employment ended
- LengthofServiceOverall. Overall Length of Service at Institute (in years): The length of the person's employment (in years)
- Let's start by reading the datasets into pandas and exploring them.

1. Introduction
First, we'll read in the datasets and do some initial exporation.
