# Project #1: Data Wrangling 
## Project Description:
This project focuses on creating a data ingestion and processing pipeline using various AWS services such as S3, Glue, Athena, and external tools like Excel (due to limitations in the free AWS tier). The pipeline aims to automate the ingestion, transformation, and analysis of the registrar’s office data for tracking applications, withdrawals, and enrollments. The pipeline was built to manage the data across different zones—Landing, Raw, and Curated—and generate insights like application completion rates for multiple academic years (2022 and 2023).

![Project Overview](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/drawio.png)

## Project Title:
Registrar’s Office Applications, Enrollments, and Withdrawals Pipeline Using AWS Services
## Objective:
The objective of this project is to automate the data ingestion and transformation process for the registrar’s office data. The ultimate goal is to query, analyze, and visualize key metrics like application completion rates, enrollment numbers, and withdrawals to help improve the decision-making process.
Figure below explains the goal of this project as this this a data wrangling project with descriptive metrics.
![goal_description](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Picture1.png)


## ETL (Extract, Transform, Load) Process Using AWS Glue:
- **AWS Glue DataBrew** was used for initial data validation, checking for inconsistencies, and basic cleaning of the raw data.
- **AWS Glue** was employed to transform the data, ensuring data quality through operations such as removing duplicates, handling missing values, and performing schema validation.
Figure of ETL pipeline from Visual ETL of AWS Glue service
![ETL Process](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/ETL.png)
## Dataset:
Source: Application, Enrollment, and Withdrawal data for the Registrar’s office.
Data Zones:
- **Zone 1**: _Landing Zone:_ Data is ingested in its raw format (i.e., .xlsx files) from different sources.
- **Zone 2**: _Raw Zone:_ Data is converted to .csv format and partially processed for further cleaning and validation.
- **Zone 3**: _Curated Zone:_ Cleaned and structured data is stored here, ready for analysis and reporting.
## Methodology:
### 1. Data Ingestion:

The raw data containing the registrar’s office applications, enrollments, and withdrawals was ingested into Amazon S3 under the Landing Zone.
The initial data was stored in its original .xlsx format, representing unprocessed, raw data.
### 2. ETL (Extract, Transform, Load) Process Using AWS Glue:

AWS Glue DataBrew was used for initial data validation, checking for inconsistencies, and basic cleaning.
AWS Glue was employed to transform the data, where data quality transformations like removing duplicates, handling missing values, and schema validation were performed.
Figure below shows the steps for final calculation of ACR i.e. Application Completion Rate
![drawio](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/dsvvds.png)

### Transformation Steps:
- **Step 1**: Detect sensitive data within the dataset and validate the overall data quality.
- **Step 2**: Filter out invalid records such as applications with missing critical data fields.
- **Step 3**: Perform schema transformations to normalize the data, aligning it with the predefined structure and making it ready for querying.
- **Step 4**: The final cleaned and transformed data was loaded into the **Curated Zone**, structured for final analysis and reporting.
  
The ETL pipeline's steps were visually orchestrated using AWS Glue Studio, where each step was executed in sequence to ensure the flow from raw to curated data (refer to the ETL pipeline visualization).

### 3. Data Querying Using Amazon Athena:

Amazon Athena was configured to query the curated data stored in S3.
Simple SQL Query:

```sql
SELECT studentid, firstname, lastname, received_year, acr
FROM registraroffice_enrollwithdraw_table2_menusgarg
LIMIT 10;
```
- This SQL query was run in Athena to extract key metrics such as Application Completion Rates (ACR) and enrollment data for the years 2022 and 2023.
- The results of these queries provided insights like the total number of applications, enrollment patterns, and the comparison of completion rates between years.

Figure below shows the results of SQL query in Athena
![SQL Athena Query](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/SQL%20Athena.png)

### 4. Visualization:

- Since Amazon QuickSight was unavailable in the free tier of AWS, the results of Athena queries were exported and visualized in Excel.
- Example Visualization: A bar chart was created to show the application completion rate for 2022 (high) and 2023 (low). The visualization helped to analyze the drop in completion rates and identify potential causes (e.g., student feedback, procedural changes).

## Tools and Technologies:
**Amazon S3:** Used for storing datasets at various stages—Landing, Raw, and Curated.
**AWS Glue:** Employed to build ETL pipelines for cleaning, transforming, and structuring the data.
**AWS Glue DataBrew:** Simplified the data cleaning process with its visual interface.
**Amazon Athena:** SQL queries were executed on the cleaned data stored in S3 for analysis.
**Excel:** Visualization of key metrics such as Application Completion Rate (ACR) due to unavailability of Amazon QuickSight in the free AWS version.

## Deliverables:
**ETL Pipeline:** A fully functional ETL pipeline using AWS Glue and DataBrew to process the registrar’s office data.
**Athena Query:** SQL queries executed to generate key insights like Application Completion Rate (ACR).
**Visualization:** Graphical representations of the results, showing trends such as application and enrollment rates across different academic years.

### Timeline:

- **Week 1**: Data ingestion into Amazon S3, organizing the raw data in the Landing Zone.
- **Week 2-3**: Data cleaning and transformation using AWS Glue and Glue DataBrew, moving processed data to the Curated Zone.
- **Week 4**: Data querying using Amazon Athena to extract key metrics like Application Completion Rate (ACR) for 2022 and 2023.
- **Week 5**: Visualization of results in Excel, focusing on trends like application completion and enrollment rates.


## Detailed Explanation of AWS Services and Pipeline Steps:
### 1. Amazon S3:
- Landing Zone: Raw .xlsx files containing registrar’s office data (e.g., applications, withdrawals, and enrollments) were uploaded to S3. This zone is used to hold unprocessed data.
- Raw Zone: Data from the Landing Zone was transformed into .csv format and partially cleaned. This intermediate stage helps to perform further processing.
- Curated Zone: The final cleaned and processed data is stored in S3 for querying and analysis. This zone ensures that only high-quality, validated data is used for reporting purposes.

### 2. AWS Glue:
- Glue was used to build the ETL pipeline, automating the data flow from raw to curated. Each step, such as removing invalid records or restructuring the data schema, was performed using Glue jobs. Glue DataBrew played a crucial role in initial data cleaning, allowing visual identification of errors and quick fixes.

### 3. Amazon Athena: 
- Athena was employed to query the processed data stored in S3. It allowed direct querying without moving the data into databases. A simple SQL query helped extract key insights, such as Application Completion Rate (ACR) for 2022 and 2023, and provided a basis for further visual analysis.

### 4. Excel for Visualization:
- Due to QuickSight limitations in the free tier, the query results from Athena were exported to Excel for visualization.
A bar chart was created, showing a significant drop in the Application Completion Rate (ACR) from 2022 to 2023. This helped identify trends and areas needing attention.


#### Visualization Example:
- Application Completion Rate (ACR) for 2022: ~90%
- Application Completion Rate (ACR) for 2023: ~30%
- A visual comparison using a bar chart showed a significant drop in the completion rates, providing insights for further investigation.
#### Bucket Paths:
- Landing Zone Path: registraroffice/enrollwithdraw/Landing
- Raw Zone Path: registraroffice/enrollwithdraw/Raw
- Curated Zone Path: registraroffice/enrollwithdraw/Curated

# Project #2: AWS Data Governance Framework

## Project Description

This project aimed to create a robust **data protection**, **governance**, and **monitoring system** using AWS services. It was designed to handle sensitive data across multiple environments, enforce access controls, and ensure compliance with organizational security requirements. 

Through the use of **AWS IAM**, **AWS KMS**, **AWS Glue**, **AWS CloudWatch**, and **AWS CloudTrail**, I implemented security protocols, established data governance processes, and monitored both resource usage and user activities effectively.

![Project Overview](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Drawio%20governance%201.png)

The project was divided into three key phases:

## Project Title: Comprehensive AWS Data Protection, Governance, and Monitoring System 
- **Data Protection**: Implementing encryption, access control policies, and security measures to safeguard data.
- **Data Governance**: Establishing rules and automation to ensure data quality, compliance, and proper handling of sensitive information.
- **Data Monitoring**: Continuous tracking of resource usage and user activities to detect anomalies and ensure accountability.

Each phase leveraged a combination of AWS services, ensuring data encryption, fine-grained access control, detailed user activity tracking, and assurance of data quality across the system.

## Objective:

The primary objective was to develop an AWS-based system that ensures:

- **Data Protection**: Strong encryption and access management for sensitive data.
- **Data Governance**: Rigorous control of data quality, handling sensitive data like Personally Identifiable Information (PII), and enforcing data management rules through automation.
- **Data Monitoring**: Continuous monitoring of resource usage, billing, and user activities to detect anomalies and ensure accountability.

The project focused on automating these processes wherever possible to reduce manual intervention and improve efficiency in managing AWS infrastructure.


## Dataset:

The datasets used in this project included:

- **CSV files** stored in S3 buckets, representing raw and processed data. These datasets were used to test encryption, data governance, and data quality evaluation in the AWS Glue pipeline.
- **Log data** generated by AWS CloudTrail to monitor user activities such as log-ins, resource modifications, and API calls.

The S3 buckets were divided into zones:

- **Raw Zone**: Storage for unprocessed datasets.
- **Trusted Zone**: Storage for validated, cleaned data after processing.
- **Backup Bucket**: A secondary S3 bucket used for replication and versioning to ensure data redundancy and disaster recovery.


## Methodology:

### 1. Data Protection:
- **AWS IAM** was used to define fine-grained access controls through roles, policies, and user groups. The root user had full administrative access, while lab roles were assigned to manage access to S3 and KMS resources.

![IAM Role Configuration](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/IAM%20Role%20Configuration.png)
![AWS S3 Buckets](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/AWS%20S3%20Buckets.png)


- **AWS KMS** was implemented to generate symmetric encryption keys. These keys were used for encrypting and decrypting sensitive data stored in S3 buckets. Permissions for key management (create, delete, use) were carefully assigned using IAM roles.

### 2. Data Governance:
- **AWS Glue** was used to build an ETL pipeline to detect sensitive data and enforce governance policies. The ETL pipeline started by loading raw data from the S3 bucket’s raw zone, then transforming and evaluating the data for sensitive information such as PII.
- I implemented **data masking** and privacy checks by configuring AWS Glue to detect up to **256 types of PII**.

![AWS Glue ETL Data Quality Evaluation with Completeness](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/AWS%20Glue%20ETL%20Data%20Quality%20Evaluation%20with%20Completeness%20Rule.png)
![AWS Glue ETL Workflow](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/AWS%20Glue%20ETL%20Workflow.png)
![AWS Glue Workflow Overview](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/AWS%20Glue%20Workflow%20Overview.png)

- **Data quality checks** were enforced by setting thresholds for rules like completeness and uniqueness. These rules helped validate the quality of data, ensuring it met the required standards before being stored in the trusted zone.
- **Replication rules** were applied to ensure that data from the primary S3 bucket was automatically replicated to a secondary backup bucket. **Versioning** was enabled to maintain multiple versions of files for disaster recovery.

![S3 Replication Configuration](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/S3%20Replication%20Configuration.png)
![Bucket Encryption Settings](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Bucket%20Encryption%20Settings.png)

### 3. Data Monitoring:
- **AWS CloudWatch** was used to set up a monitoring dashboard. This dashboard displayed key metrics related to S3 usage (e.g., number of objects, storage capacity) and billing metrics to track costs.

![Custom CloudWatch Dashboard for Monitoring](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Custom%20CloudWatch%20Dashboard%20for%20Monitoring.png)


- **CloudWatch Alarms** were created to send email notifications if certain thresholds were exceeded, such as when billing charges reached $40. Alarms were configured to monitor resource utilization and trigger appropriate actions if necessary.

  ![CloudWatch with Active Billing Alarm for Estimated Charges](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/CloudWatch%20with%20Active%20Billing%20Alarm%20for%20Estimated%20Charges.png)
  
- **AWS CloudTrail** was used to track user activities, providing a detailed log of events such as API calls, user log-ins, and resource modifications. Logs were stored securely in an S3 bucket, with additional encryption applied to ensure data protection. CloudTrail was essential for maintaining accountability and transparency in the AWS environment.

![CloudTrail Configuration](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/CloudTrail%20Configuration.png)

### Automation:
Automation was a key feature of this project. AWS Glue pipelines were scheduled using the **AWS Schedule** feature to automatically run data governance processes on a weekly basis. The scheduling process ensured consistent and timely execution of data quality checks, sensitive data detection, and data replication tasks.



## Tools and Technologies:

- **AWS IAM**: Used for managing user access, roles, and policies to control who can perform actions on AWS resources.
- **AWS KMS**: Utilized to generate and manage encryption keys for securing sensitive data.
- **AWS S3**: Primary storage for raw, processed, and log datasets. S3 was used in conjunction with replication and versioning for data protection and disaster recovery.
- **AWS Glue**: Built an ETL pipeline for detecting sensitive data, managing data governance policies, and ensuring data quality.
- **AWS CloudWatch**: Set up dashboards and alarms to monitor resource usage and billing metrics.
- **AWS CloudTrail**: Recorded user activity and API calls, providing logs for security and compliance.
- **Python**: Used in AWS Glue to define custom rules and logic for data quality checks and sensitive data detection.
- **JSON/YAML**: Used for defining policies in AWS IAM and configurations in various AWS services.



## Deliverables:

### Data Protection System:
- Created IAM roles and policies for secure access control.
- Implemented encryption with KMS keys for sensitive data in S3.
- Applied replication and versioning in S3 to ensure data redundancy and disaster recovery.

### Data Governance Pipeline:
- Designed an ETL pipeline in AWS Glue to detect sensitive data and evaluate data quality.
- Set up automated workflows for data processing, including checks for completeness and uniqueness.
- Enabled replication rules and versioning in S3 for backups and data recovery.

### Data Monitoring System:
- Built a CloudWatch dashboard to monitor S3 usage, billing metrics, and other key performance indicators.
- Configured CloudWatch alarms to notify when certain thresholds (e.g., billing limits) were reached.
- Set up CloudTrail to record user activity and track API calls for security auditing and compliance.
- Stored logs in an encrypted S3 bucket with versioning enabled to maintain secure records of user actions.


# Project 3: Descriptive analysis

## Introduction
This project focuses on analyzing the 311 inquiry volume data sourced from OpenData Vancouver under the Government and Finance theme. The 311 service is a vital communication channel connecting city residents with municipal services. By analyzing data from 2023 and 2024, the project aims to identify departments with unusually high or low inquiry volumes and investigate the usage patterns of different communication channels (e.g., Phone, Chat). This analysis offers valuable insights into service demand, department workloads, and communication efficiency, leading to improved resource allocation and enhanced city service management.

![Drawio](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Drawio%20updated.png)

## Project Title: Descriptive data analysis for 311 Inquiry Volume Data Analysis of Government and Finance

**Dataset Link**: The dataset is publicly available on OpenData Vancouver and can be accessed [here](https://opendata.vancouver.ca/explore/?disjunctive.features&disjunctive.theme&disjunctive.keyword&disjunctive.data-owner&disjunctive.data-team&sort=modified&refine.theme=Government+and+finance).

## Objective
The key objectives of this analysis are:
1. **Department Inquiry Volume Analysis**: Identify city departments with unusually high or low inquiry volumes in 2023 and 2024.
2. **Channel Inquiry Usage Analysis**: Determine which communication channels were most or least used for public inquiries.

![Goal](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Goal.png)

This data-driven approach enhances public service delivery and optimizes resource allocation, ensuring that city services are effectively meeting public needs.

## Dataset Description
The dataset is provided by OpenData Vancouver and includes key fields such as:
- **Department**: The city department responsible for handling each inquiry.
- **Inquiry Type**: The type of public inquiry.
- **Year**: The year in which the inquiry was recorded.
- **Month**: The month the inquiry occurred.
- **Channel**: The mode of communication used by the public (e.g., Phone, Chat).
- **Number of Records**: The total volume of inquiries per department and channel.

| Column          | Data Type | Description                                             |
|-----------------|-----------|---------------------------------------------------------|
| Department      | String    | The department handling the inquiry.                    |
| Type            | String    | The type of inquiry received.                           |
| Year Month      | String    | The year and month when the inquiry was recorded.       |
| Channel         | String    | The communication channel used for the inquiry.         |
| Number of Records | Integer  | The total number of records associated with the inquiry. |
| BI_ID           | Integer   | Unique identifier for each record.                      |
| Year            | Integer   | The year extracted from 'Year Month'.                   |


This dataset offers comprehensive insights into how city residents interact with municipal services and highlights areas that may require resource adjustment or service improvements.

## Methodology

### Data Analytical Question Formulation
The analysis was guided by two key questions:
- Which city departments received unusually high or low inquiry volumes in 2023 and 2024?
- Which communication channels were most or least used for public inquiries?

### Dataset Preparation
The dataset was reviewed to ensure all necessary fields were included. This was followed by cleaning and organizing the data, including renaming columns for clarity. The data was split by year (2023 and 2024) and formatted for ingestion into Amazon S3.

### Data Ingestion and Storage
Data files for 2023 and 2024 were ingested into Amazon S3. A hierarchical folder structure was created for ease of management, with the data split into:
- **Landing Zone**: Raw, unprocessed data.
- **Raw Zone**: Data after initial processing.
- **Curated Zone**: Cleaned and structured data, ready for analysis.

| Zone Name    | Path                                                                                  | Description                                                                                                                                               |
|--------------|----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|
| Landing Zone | govtfinance/311inqvol/calls/2024/Landing/311inqvol-2024/3-1-1-inquiry-volume.xlsx      | This zone is used for managing the current data as it is ingested from various sources. The data in this zone is typically unprocessed and stored in its original format. |
| Curated Zone | govtfinance/311inqvol/calls/2024/Curated                                               | This zone stores data that has been structured, cleaned, and optimized for analysis. The data in this zone is ready for reporting and querying. It has undergone various processes such as deduplication, normalization, and validation to ensure its quality and usefulness. |
| Raw Zone     | govtfinance/311inqvol/calls/2024/Raw/311inqvol-2024/3-1-1-inquiry-volume.csv           | In this zone, the system generates CSV files that result from initial processing steps. These files may include raw outputs from data ingestion processes or other intermediate steps before the data is moved to the curated zone. |

![311 Inquiry Volume 2023 File in Landing Zone of S3](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/311%20Inquiry%20Volume%202023%20File%20in%20Landing%20Zone%20of%20S3.png)

### Data Cleaning and Structuring
AWS Glue DataBrew was used to clean and structure the dataset. Null values were removed, and the data was normalized for consistency. Columns were renamed for better clarity, such as renaming "Department" to "Inquiry_department."

![Data Overview for 311 Inquiry Volume Dataset in AWS DataBrew](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Data%20Overview%20for%20311%20Inquiry%20Volume%20Dataset%20in%20AWS%20DataBrew.png)

![Data Sample Preview for 311 Inquiry Volume in AWS DataBrew](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Data%20Sample%20Preview%20for%20311%20Inquiry%20Volume%20in%20AWS%20DataBrew.png)

### Data Pipeline Design
A data pipeline was designed using AWS Glue to automate the ETL (Extract, Transform, Load) process. This pipeline ensured a seamless flow of raw data into structured data that was ready for analysis.

![drawio pipeline](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/drawio%20pipeline.png)

![Data Preview](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Data%20preview.png)

![Data Preview of Inquiry Method Usage in AWS DataBrew](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Data%20Preview%20of%20Inquiry%20Method%20Usage%20in%20AWS%20DataBrew.png)

![Scheme Change](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Scheme%20Change.png)

![Data Transformation Workflow for 311 Inquiry Volume](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Data%20Transformation%20Workflow%20for%20311%20Inquiry%20Volume%202023%20and%202024.png)
### Data Analysis
Amazon Athena was used to execute SQL queries on the cleaned data stored in Amazon S3. The focus of the analysis was to compute the **Departmental Inquiry Volume** and **Channel Inquiry Usage** for both 2023 and 2024. Metrics such as the total number of inquiries per department and the usage of each communication channel were computed.

| Year  | Dept                         | Channel                      |
|-------|------------------------------|------------------------------|
| **2023** | **Dept** | **Channel** |
| **Table Name** | govtfinance_311inqvol_tabledept2023_menus | govtfinance_311inqvol_tablechnl2023_menus |
| **Database Name** | govtfinance_311inqvol_databasedept2023_menus | govtfinance_311inqvol_databasechnl2023_menus |
| **Column 1** | inquiry_department | inquiry_channel |
| **Column 2** | total_inquiries_in_dept | total_inquiries_in_channel |
| **Column 3** | deptpercuse | channelpercuse |
| **2024** | **Dept** | **Channel** |
| **Table Name** | govtfinance_311inqvol_tabledept2024_menus | govtfinance_311inqvol_tablechnl2024_menus |
| **Database Name** | govtfinance_311inqvol_databasedept2024_menus | govtfinance_311inqvol_databasechnl2024_menus |
| **Column 1** | inquiry_department | inquiry_channel |
| **Column 2** | total_inquiries_in_dept | total_inquiries_in_channel |
| **Column 3** | deptpercuse | channelpercuse |

![Query Results for Inquiry Channel Percentages](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Query%20Results%20for%20Inquiry%20Channel%20Percentages.png)

### Data Visualization
Due to limited access to Amazon QuickSight, Excel was used to generate visual representations of the inquiry volumes and communication channel usage. These visualizations made it easier for stakeholders to interpret the data and identify trends in public service demands.

[Visualization graph for department use](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/dept-use-%25-2023-2024.pdf)

[Visualization graph for channel use](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/channel-use-%25-2023-2024.pdf)

### Data Publishing
The final results were published on Amazon EC2, making them accessible to stakeholders and the public via virtual servers. This allowed for easy sharing and review of the project’s insights.

![Channel Preference Comparison Between 2022 and 2023](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/Channel%20Preference%20Comparison%20Between%202023%20and%202024.png)

[HTML code used for visualization](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/index.html)

![Inquiry department data for the years 2023 and 2024](https://github.com/MenusGarg5981/AWS_Pipelines/blob/main/images/inquiry%20department%20data%20for%20the%20years%202023%20and%202024.png)

## Tools and Technologies
- **Amazon S3**: For storing and organizing the raw and cleaned datasets.
- **AWS Glue DataBrew**: For automating data cleaning and structuring processes.
- **Amazon Athena**: For querying and analyzing the cleaned data using SQL.
- **Amazon EC2**: For publishing the project results on virtual servers, ensuring both internal and public access.
- **Excel**: Used for data visualization due to limited access to Amazon QuickSight.

## Deliverables
1. **Cleaned and Structured Dataset**:  
   The raw data from 2023 and 2024 was cleaned, structured, and stored as CSV files in Amazon S3, ready for future analysis.

2. **Data Analysis Reports**:  
   Detailed reports highlighting inquiry volumes by department and communication channel usage were generated, providing insights into public service interactions.

3. **Data Visualizations**:  
   Visual representations of inquiry volumes and communication channel usage were created using Excel, making the data more interpretable for stakeholders.

4. **Published Data**:  
   The final analysis results were published on Amazon EC2, allowing stakeholders easy access to review the project’s findings.

## Timeline

### Month 1: Dataset Preparation and Ingestion
- **Week 1**: Dataset review and project objectives were established.
- **Week 2**: Data ingestion into Amazon S3 was completed, and a folder structure was created for storing raw, processed, and curated data.
- **Week 3**: AWS Glue DataBrew was used to clean and structure the dataset. The cleaning process involved normalizing data, removing null values, and renaming columns for better clarity.

### Month 2: Data Structuring and Pipeline Design
- **Week 4**: The structured data schema was finalized for both 2023 and 2024 datasets.
- **Week 5**: A data pipeline was designed using AWS Glue to automate the ETL process, ensuring a seamless flow of raw data to the structured dataset.
- **Week 6**: The pipeline was implemented, with data moving through extraction, transformation, and loading stages, ensuring that both 2023 and 2024 datasets were ready for analysis.

### Month 3: Data Analysis, Visualization, and Publishing
- **Week 7**: Data analysis was conducted using Amazon Athena, and key metrics such as departmental inquiry volumes and communication channel usage were computed.
- **Week 8**: Data visualizations were generated in Excel to represent trends in inquiry volumes and channel usage.
- **Week 9**: The results, including visual reports and analysis, were published on Amazon EC2, making the insights available for internal and public review.

## Conclusion
This project successfully analyzed the 311 inquiry volume data from 2023 and 2024, providing crucial insights into public interactions with city services. By identifying departments with unusually high or low inquiry volumes and analyzing communication channel usage, the city can optimize resource allocation and improve service delivery. The methodology and tools employed ensure that the analysis is scalable and reproducible, offering a solid foundation for future data-driven decisions in managing public services.

 


