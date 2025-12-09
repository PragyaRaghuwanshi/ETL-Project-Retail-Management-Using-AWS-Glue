Retail Data Management – ETL Project Using AWS Glue
📌 Project Overview

This project demonstrates a complete ETL (Extract–Transform–Load) process using AWS Glue Studio (Visual ETL).
The objective was to ingest two CSV datasets — Transactions and Product data — clean them, join them, extract numeric sales values, compute Net Sales, aggregate the results, and export the final output to an S3 bucket.

The project includes:

S3 setup

Glue database & classifiers

Crawlers

Glue Visual ETL Job

Data transformations (Join, Drop Fields, Regex Extractor, Aggregate)

Output validation via S3 Select

Proof of job run logs & output files

🎯 Project Objective

Create an end-to-end ETL pipeline that:

Reads transactions and product files from S3

Detects schema using Glue Crawlers

Joins the datasets

Cleans and transforms the data

Extracts numeric values from sales using Regex

Computes Net Sales

Aggregates results by product category & ship mode

Saves the output to a new S3 bucket

🧵 Step-by-Step ETL Workflow
1️⃣ S3 Setup & File Upload

Attempted bucket name etl-cep-01

It was already taken →
✔ Final name: etl-cep-01pragya 

writeup of ETL ProjectRetailDat…

Created folders:

transaction-files/

product-files/

Uploaded both CSV datasets into these folders.

Created second bucket for ETL output:

✔ etl-cep-output-01pragya

2️⃣ Create Glue Database

Created database named:
✔ abc-retail

Used to store crawler-detected metadata.

3️⃣ Glue Classifiers

Created two classifiers:

Classifier	Purpose
txnClass	For transactions CSV
cust_classifier	For product CSV

These ensured more accurate schema recognition.

4️⃣ IAM Role

Created IAM Role:
✔ glue-role

Attached admin permissions (allowed in lab environment).

5️⃣ Crawlers Setup & Run

Created:

Transaction crawler → produced txntransaction_files table

Product crawler → produced product_files table

Both stored inside database abc-retail.


writeup of ETL ProjectRetailDat…

6️⃣ Schema Verification

Verified schema for both tables in Data Catalog.
Captured screenshot proofs.

7️⃣ Built ETL Job in AWS Glue Studio (Visual ETL)

Nodes used:

AWS Glue Data Catalog (transactions)

AWS Glue Data Catalog (products)

Join

Drop Fields

Regex Extractor

Aggregate

Amazon S3 Target

Transformations Applied
✔ Join

Inner join

Join key: product id

✔ Drop Fields

Both sides had product id

Removed duplicate field

✔ Regex Extractor

Used to extract numeric value from the sales column.

Column: sales

Regex: \d+

Output: NetSales

✔ Aggregate

Group by:

product category

ship mode

Aggregate field: NetSales

Function: avg (average Net Sales)

✔ Target Output

Saved to:
✔ etl-cep-output-01pragya

8️⃣ ETL Job Execution

Job saved & executed successfully

CloudWatch logs checked

Proof screenshots collected

9️⃣ Output Validation

Downloaded from S3:

etlcepjob.py – Glue ETL script

result.csv – final aggregated output

run-0000… – job execution summary


writeup of ETL ProjectRetailDat…

Validation method:
Used S3 Select to preview output.

⚙️ Challenges & Solutions
Challenge	Reason	Solution
S3 bucket name already taken	Global name conflict	Renamed to etl-cep-01pragya
Crawler name duplicate	Name already used	Renamed to product-crawl
Difficulty connecting Join node	Visual ETL connection method	Used drag-from-grey-dot technique
Sales values included $	Regular text, not numeric	Used Regex Extractor (\d+)
Output not visible	Wrong/missing output path	Corrected target bucket location

writeup of ETL ProjectRetailDat…

📈 Final Output Summary

The ETL pipeline successfully produced:

Cleaned, joined retail dataset

Extracted numeric Net Sales

Aggregated results by:

product category

ship mode

Delivered final CSV output in S3

All job logs, schema screenshots, and output validation captured

📚 Learnings

Working with Glue Crawlers & Classifiers

Visual ETL Job creation

Joining and transforming datasets

Regex-based numeric extraction

Aggregation & schema management

Debugging ETL job paths and naming issues

📎 Files Included in Repository

writeup/ – Detailed write-up document

scripts/etlcepjob.py – ETL script

output/result.csv – final aggregated data

screenshots/ – proofs of execution

README.md – this file

📬 Contact

Pragya Raghuwanshi
Data Analytics | ETL | AWS Glue
