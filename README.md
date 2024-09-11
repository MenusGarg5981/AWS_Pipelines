## Data Wrangling Project
### Project Description:
This project focuses on creating a data ingestion and processing pipeline using various AWS services such as S3, Glue, Athena, and external tools like Excel (due to limitations in the free AWS tier). The pipeline aims to automate the ingestion, transformation, and analysis of the registrar’s office data for tracking applications, withdrawals, and enrollments. The pipeline was built to manage the data across different zones—Landing, Raw, and Curated—and generate insights like application completion rates for multiple academic years (2022 and 2023).


### Project Title:
Registrar’s Office Applications, Enrollments, and Withdrawals Pipeline Using AWS Services

### Objective:
The objective of this project is to automate the data ingestion and transformation process for the registrar’s office data. The ultimate goal is to query, analyze, and visualize key metrics like application completion rates, enrollment numbers, and withdrawals to help improve the decision-making process.

### ETL (Extract, Transform, Load) Process Using AWS Glue:

- **AWS Glue DataBrew** was used for initial data validation, checking for inconsistencies, and basic cleaning of the raw data.
- **AWS Glue** was employed to transform the data, ensuring data quality through operations such as removing duplicates, handling missing values, and performing schema validation.

![ETL Process](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/ETL.png)


### Dataset:
Source: Application, Enrollment, and Withdrawal data for the Registrar’s office.
Data Zones:
- **Zone 1**: _Landing Zone:_ Data is ingested in its raw format (i.e., .xlsx files) from different sources.
- **Zone 2**: _Raw Zone:_ Data is converted to .csv format and partially processed for further cleaning and validation.
- **Zone 3**: _Curated Zone:_ Cleaned and structured data is stored here, ready for analysis and reporting.

### Methodology:
###### 1. Data Ingestion:

The raw data containing the registrar’s office applications, enrollments, and withdrawals was ingested into Amazon S3 under the Landing Zone.
The initial data was stored in its original .xlsx format, representing unprocessed, raw data.
###### 2. ETL (Extract, Transform, Load) Process Using AWS Glue:

AWS Glue DataBrew was used for initial data validation, checking for inconsistencies, and basic cleaning.
AWS Glue was employed to transform the data, where data quality transformations like removing duplicates, handling missing values, and schema validation were performed.

![drawio](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/dsvvds.png)

###### Transformation Steps:
- **Step 1**: Detect sensitive data within the dataset and validate the overall data quality.
- **Step 2**: Filter out invalid records such as applications with missing critical data fields.
- **Step 3**: Perform schema transformations to normalize the data, aligning it with the predefined structure and making it ready for querying.
- **Step 4**: The final cleaned and transformed data was loaded into the **Curated Zone**, structured for final analysis and reporting.
  
The ETL pipeline's steps were visually orchestrated using AWS Glue Studio, where each step was executed in sequence to ensure the flow from raw to curated data (refer to the ETL pipeline visualization).

###### 3. Data Querying Using Amazon Athena:

Amazon Athena was configured to query the curated data stored in S3.
Simple SQL Query:

```sql
SELECT studentid, firstname, lastname, received_year, acr
FROM registraroffice_enrollwithdraw_table2_menusgarg
LIMIT 10;
```
- This SQL query was run in Athena to extract key metrics such as Application Completion Rates (ACR) and enrollment data for the years 2022 and 2023.
- The results of these queries provided insights like the total number of applications, enrollment patterns, and the comparison of completion rates between years.

###### 4. Visualization:

- Since Amazon QuickSight was unavailable in the free tier of AWS, the results of Athena queries were exported and visualized in Excel.
- Example Visualization: A bar chart was created to show the application completion rate for 2022 (high) and 2023 (low). The visualization helped to analyze the drop in completion rates and identify potential causes (e.g., student feedback, procedural changes).

#### Tools and Technologies:
**Amazon S3:** Used for storing datasets at various stages—Landing, Raw, and Curated.
**AWS Glue:** Employed to build ETL pipelines for cleaning, transforming, and structuring the data.
**AWS Glue DataBrew:** Simplified the data cleaning process with its visual interface.
**Amazon Athena:** SQL queries were executed on the cleaned data stored in S3 for analysis.
**Excel:** Visualization of key metrics such as Application Completion Rate (ACR) due to unavailability of Amazon QuickSight in the free AWS version.

#### Deliverables:
**ETL Pipeline:** A fully functional ETL pipeline using AWS Glue and DataBrew to process the registrar’s office data.
**Athena Query:** SQL queries executed to generate key insights like Application Completion Rate (ACR).
**Visualization:** Graphical representations of the results, showing trends such as application and enrollment rates across different academic years.

#### Detailed Explanation of AWS Services and Pipeline Steps:
###### 1. Amazon S3:

- Landing Zone: Raw .xlsx files containing registrar’s office data (e.g., applications, withdrawals, and enrollments) were uploaded to S3. This zone is used to hold unprocessed data.

- Raw Zone: Data from the Landing Zone was transformed into .csv format and partially cleaned. This intermediate stage helps to perform further processing.

- Curated Zone: The final cleaned and processed data is stored in S3 for querying and analysis. This zone ensures that only high-quality, validated data is used for reporting purposes.

###### 2. AWS Glue:
- Glue was used to build the ETL pipeline, automating the data flow from raw to curated. Each step, such as removing invalid records or restructuring the data schema, was performed using Glue jobs. Glue DataBrew played a crucial role in initial data cleaning, allowing visual identification of errors and quick fixes.

###### 3. Amazon Athena: 
- Athena was employed to query the processed data stored in S3. It allowed direct querying without moving the data into databases. A simple SQL query helped extract key insights, such as Application Completion Rate (ACR) for 2022 and 2023, and provided a basis for further visual analysis.

###### 4. Excel for Visualization:
- Due to QuickSight limitations in the free tier, the query results from Athena were exported to Excel for visualization.
A bar chart was created, showing a significant drop in the Application Completion Rate (ACR) from 2022 to 2023. This helped identify trends and areas needing attention.


### Visualization Example:
- Application Completion Rate (ACR) for 2022: ~90%
- Application Completion Rate (ACR) for 2023: ~30%
- A visual comparison using a bar chart showed a significant drop in the completion rates, providing insights for further investigation.
### Bucket Paths:
- Landing Zone Path: registraroffice/enrollwithdraw/Landing
- Raw Zone Path: registraroffice/enrollwithdraw/Raw
- Curated Zone Path: registraroffice/enrollwithdraw/Curated
