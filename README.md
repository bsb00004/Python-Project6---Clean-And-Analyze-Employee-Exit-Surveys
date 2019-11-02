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

### 1. Introduction
First, we'll read in the datasets and do some initial exporation.
Import the pandas and NumPy libraries. Reading the __dete_survey.csv__ CSV file into pandas, and assigning it to the variable name dete_survey. Reading the __tafe_survey.csv__ CSV file into pandas, and assigning it to the variable name tafe_survey.
Using the __DataFrame.info()__ and __DataFrame.head()__ methods to print information about both dataframes, as well as the first few rows. Using other data exploration methods such as the __Series.value_counts()__ and __DataFrame.isnull()__ methods to explore the data and figure out some next steps.

__Output:__
We can make the following observations based on the work above:

- The dete_survey dataframe contains 'Not Stated' values that indicate values are missing, but they aren't represented as NaN.
- Both the dete_survey and tafe_survey contain many columns that we don't need to complete our analysis.
- Each dataframe contains many of the same columns, but the column names are different.
- There are multiple columns/answers that indicate an employee resigned because they were dissatisfied.

### 2. Identify Missing Values and Drop Unneccessary Columns
First, we'll correct the Not Stated values and drop some of the columns we don't need for our analysis.

To start, we'll handle the first two issues. Recall that we can use the pd.read_csv() function to specify values that should be represented as NaN. We'll use this function to fix the missing values first. Then, we'll drop columns we know we don't need for our analysis.
- Using the DataFrame.drop() method to drop the following columns from dete_survey: dete_survey.columns[28:49]. Setting the axis parameter equal to 1. Then Assigning the result to dete_survey_updated.
- Using the DataFrame.drop() method to drop the following columns from tafe_survey: tafe_survey.columns[17:66]. Setting the axis parameter equal to 1. Then Assigning the result to tafe_survey_updated.

### 3. Rename Columns
Next, we'll standardize the names of the columns we want to work with, because we eventually want to combine the dataframes.Each dataframe contains many of the same columns, but the column names are different.

- Rename the remaining columns in the dete_survey_updated dataframe. Use the following criteria to update the column names:
  - Make all the capitalization lowercase.
  - Remove any trailing whitespace from the end of the strings.
  - Replace spaces with underscores ('_').
  - As an example, Cease Date should be updated to cease_date.
  - Remember you can use the DataFrame.columns attribute to print an array of the existing column names.
- Use the DataFrame.rename() method to update the columns below in tafe_survey_updated. Don't worry about the rest of the column names right now - we'll handle them later.
'Record ID': 'id'
'CESSATION YEAR': 'cease_date'
'Reason for ceasing employment': 'separationtype'
'Gender. What is your Gender?': 'gender'
'CurrentAge. Current Age': 'age'
'Employment Type. Employment Type': 'employment_status'
'Classification. Classification': 'position'
'LengthofServiceOverall. Overall Length of Service at Institute (in years)': 'institute_service'
'LengthofServiceCurrent. Length of Service at current workplace (in years)': 'role_service'
Use the DataFrame.head() method to look at the current state of the dete_survey_updated and tafe_survey_updated dataframes and make sure your changes look good.
