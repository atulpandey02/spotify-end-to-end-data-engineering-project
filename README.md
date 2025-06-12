# Spotify ETL Pipeline | Serverless Data Engineering with AWS

### Introduction

In this project, I built a serverless ETL pipeline using the Spotify API and AWS. It extracts playlist data via Lambda, stores raw data in S3, transforms it using another Lambda, and catalogs it with AWS Glue. The data is queried in Amazon Athena for analysis.

### Features
- End-to-End serverless ETL pipeline using Python & AWS
- Real-time metadata extraction from Spotify API
- Automated scheduling with CloudWatch
- Schema inference and cataloging using AWS Glue
- SQL querying using Amazon Athena


### Architecture 
![Architecture Diagram](https://github.com/atulpandey02/spotify-end-to-end-data-engineering-project/blob/main/Architecture%20Diagram.png)

### About Dataset/ API
This API contians about music artist , albums and songs - [Spotify API](https://developer.spotify.com/documentation/).

### Services Used 
1. **s3**- I used S3 to store both raw JSON data extracted from the Spotify API and the transformed CSV files after processing, organized into separate folders (raw_data/ and transformed_data/).
2. **AWS Lambda**- I created two Lambda functions:  
                    1. One for extracting data from the Spotify API and saving it to S3.  
                    2. Another for transforming that raw data (albums, artists, and songs) and storing the clean version in a different S3 folder.
4. **Cloud Watch**- Used to schedule and trigger the extraction Lambda function daily, allowing for fully automated and serverless data ingestion from the Spotify API.
5. **Glue Crawler**- After transformation, I used a Glue Crawler to scan the cleaned CSV files in S3 and create tables automatically based on the inferred schema.
6. **Data Catalog**- The metadata and schema created by the crawler were stored in the Glue Data Catalog. This made it easy to connect and query the datasets from Athena.
7. **Amazon Athena**- I used Athena to run SQL queries on the transformed data directly in S3 without having to load it into a database—ideal for quick exploration and dashboarding.



### Install Packages
```
pip install pandas
pip install numpy
pip install spotipy
pip install boto3
```

### Project execution flow 
1.**Connected to Spotify API using Python**  
I used the spotipy library to programmatically extract rich metadata from Spotify — including playlist tracks, album details, and artist information.

2.**Automated Data Extraction with AWS Lambda**  
I built a Lambda function to handle the extraction logic. This function fetches the data from Spotify and stores the raw JSON files into my S3 bucket under raw_data/to_process/.

3.**Scheduled Execution with Amazon CloudWatch**  
To ensure consistent data extraction, I scheduled the Lambda function using CloudWatch Events to run daily — keeping my pipeline fresh without manual triggers.

4.**Serverless Data Transformation with Lambda & Pandas**  
A second Lambda function was developed to clean and structure the raw data. I used Python and Pandas to extract relevant fields (songs, albums, artists), transform them into tabular formats, and store the processed CSVs into transformed_data/ in S3.

5.**Schema Inference using AWS Glue Crawler**  
I configured an AWS Glue Crawler to scan the transformed files and automatically infer schemas for each dataset. This allowed seamless integration into Athena via the Data Catalog.

6.**Querying Structured Data with Amazon Athena**  
Once the data was cataloged, I used Athena to run SQL queries on top of my transformed Spotify dataset — enabling analytical insights like most popular artists or song trends over time.

### About
This project is part of my Data Engineering learning path. It showcases practical skills in cloud-native ETL workflows, API integration, and serverless processing with AWS.  This project simulates a real-world data pipeline used in music analytics platforms to gain insights on artist popularity, track trends, and playlist patterns , all using scalable cloud-native services.

### How to Run

1. Clone the repo: `git clone https://github.com/atulpandey02/spotify-end-to-end-data-engineering-project`
2. Set up AWS credentials using IAM
3. Add your Spotify API credentials as environment variables
4. Deploy the Lambda functions manually or with AWS SAM
5. Trigger execution or test with `lambda_handler` locally

![Python](https://img.shields.io/badge/python-3.10-blue)
![AWS Lambda](https://img.shields.io/badge/AWS-Lambda-orange)
![Status](https://img.shields.io/badge/status-complete-brightgreen)




