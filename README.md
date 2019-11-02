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

<font color=red>Output:</font>
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
- Using the DataFrame.rename() method to update the columns below in tafe_survey_updated. We'll handle rest of the column names later.
  - 'Record ID': 'id'
  - 'CESSATION YEAR': 'cease_date'
  - 'Reason for ceasing employment': 'separationtype'
  - 'Gender. What is your Gender?': 'gender'
  - 'CurrentAge. Current Age': 'age'
  - 'Employment Type. Employment Type': 'employment_status'
  - 'Classification. Classification': 'position'
  - 'LengthofServiceOverall. Overall Length of Service at Institute (in years)': 'institute_service'
  - 'LengthofServiceCurrent. Length of Service at current workplace (in years)': 'role_service'

Use the DataFrame.head() method to look at the current state of the dete_survey_updated and tafe_survey_updated dataframes and make sure your changes look good.

### 4. Filter the Data
Next, let's remove more of the data we don't need.

If we look at the unique values in the 'separationtype' columns in each dataframe, we'll see that each contains a couple of different separation types.For this project, we'll only analyze survey respondents who resigned, so we'll only select separation types containing the string 'Resignation'.
Note that dete_survey_updated dataframe contains multiple separation types with the string 'Resignation':

- Resignation-Other reasons
- Resignation-Other employer
- Resignation-Move overseas/interstate

- Use the Series.value_counts() method to review the unique values in the separationtype column in both dete_survey_updated and tafe_survey_updated.
- In each of dataframes, select only the data for survey respondents who have a Resignation separation type.
  - Remember that the dete_survey_updated dataframe contains three Resignation separation types. We want to select all of them.
  - Use the DataFrame.copy() method on the result to avoid the SettingWithCopy Warning.
  - Assign the result for dete_survey_updated to dete_resignations.
  - Assign the reuslt for tafe_survey_updated to tafe_resignations.
  
### 5. Verify the Data
Below, we clean and explore the cease_date and dete_start_date columns to make sure all of the years make sense. We'll use the following criteria:

- Since the cease_date is the last year of the person's employment and the dete_start_date is the person's first year of employment, it wouldn't make sense to have years after the current date.
- Given that most people in this field start working in their 20s, it's also unlikely that the dete_start_date was before the year 1940.

Check the years in each dataframe for logical inconsistencies.

- First, clean the cease_date column in dete_resignations.
  - Use the Series.value_counts() method to view the unique values in the cease_date column.
  - Use vectorized string methods to extract the year. As a reminder, here is the full list.
  - Use the Series.astype() method method to convert the type to a float.
- Use the Series.value_counts() to check the values in the cease_date and dete_start_date columns in dete_resignations and the cease_date column in tafe_resignations.
  - Because Series.value_counts() returns a series, we can use Series.sort_index() method with ascending= True or False to view the highest and lowest values with their counts.
- You can also plot the values of any numeric columns with a boxplot to identify any values that look wrong.

<font color=red>__Output:__</font> Below are our findings:

- The years in both dataframes don't completely align. The tafe_survey_updated dataframe contains some cease dates in 2009, but the dete_survey_updated dataframe does not. The tafe_survey_updated dataframe also contains many more cease dates in 2010 than the dete_survey_updaed dataframe. Since we aren't concerned with analyzing the results by year, we'll leave them as is.

### 6. Create a New Column
Since our end goal is to answer the question below, we need a column containing the length of time an employee spent in their workplace, or years of service, in both dataframes.

- End goal: Are employees who have only worked for the institutes for a short period of time resigning due to some kind of dissatisfaction? What about employees who have been at the job longer?
The tafe_resignations dataframe already contains a "service" column, which we renamed to institute_service.

Below, we calculate the years of service in the dete_survey_updated dataframe by subtracting the dete_start_date from the cease_date and create a new column named institute_service.

### 7. Identify Dissatisfied Employees
Next, we'll identify any employees who resigned because they were dissatisfied. Below are the columns we'll use to categorize employees as "dissatisfied" from each dataframe:

1. tafe_survey_updated:
  - Contributing Factors. Dissatisfaction
  - Contributing Factors. Job Dissatisfaction
2. dafe_survey_updated:
  - job_dissatisfaction
  - dissatisfaction_with_the_department
  - physical_work_environment
  - lack_of_recognition
  - lack_of_job_security
  - work_location
  - employment_conditions
  - work_life_balance
  - workload
  
If the employee indicated any of the factors above caused them to resign, we'll mark them as dissatisfied in a new column. After our changes, the new dissatisfied column will contain just the following values:

- True: indicates a person resigned because they were dissatisfied in some way
- False: indicates a person resigned because of a reason other than dissatisfaction with the job
- NaN: indicates the value is missing

### 8. Combining the Data
Below, we'll add an institute column so that we can differentiate the data from each survey after we combine them. Then, we'll combine the dataframes and drop any remaining columns we don't need.

### 9. Clean the Service Column
Next, we'll clean the institute_service column and categorize employees according to the following definitions:

- New: Less than 3 years in the workplace
- Experienced: 3-6 years in the workplace
- Established: 7-10 years in the workplace
- Veteran: 11 or more years in the workplace

The analysis is based on [this article](https://www.businesswire.com/news/home/20171108006002/en/Age-Number-Engage-Employees-Career-Stage), which makes the argument that understanding employee's needs according to career stage instead of age is more effective.

### 10. Perform Some Initial Analysis
Finally, we'll replace the missing values in the dissatisfied column with the most frequent value, False. Then, we'll calculate the percentage of employees who resigned due to dissatisfaction in each service_cat group and plot the results.

Note that since we still have additional missing values left to deal with, this is meant to be an initial introduction to the analysis, not the final analysis.

_____________________________________________xxx__________________________xxx___________________________________________________________

From the initial analysis above, we can tentatively conclude that employees with 7 or more years of service are more likely to resign due to some kind of dissatisfaction with the job than employees with less than 7 years of service. However, we need to handle the rest of the missing data to finalize our analysis.

__NOTE:__ THe Python File is Well Commented
