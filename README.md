# Athena and Glue <br>
Equivalent of AWS Athena in GCP is BigQuery
Equivalent of aws Glue in GCP is a combination of Cloud Dataflow, Cloud Data Fusion, and Google Cloud Storage (GCS) 
### BIGQUERY:
A fully managed data warehouse for running serverless SQL queries on structured and semi-structured data.<br>
it is same as athena but there are some syntax differences<br>
###
#### steps to follow <br>
<b> Data Migration</b>: Move data from Amazon S3 to Google Cloud Storage (GCS).<br>
<b> Query Migration</b>: Migrate SQL queries from AWS Athena to Google BigQuery.<br>
<b> ETL Pipeline Migration<b>: Migrate AWS Glue ETL jobs to Cloud Dataflow and Cloud Data Fusion.<br>
<b> Metadata Migration</b>: Migrate AWS Glue Data Catalog metadata to Google Data Catalog.<br>
## 1.data migration :<br>
List all data files in Amazon S3 that are being used by Athena and identify which format they are being stored <br>
now create gcs bucket in google cloud platform .<br>
Use `gsutil` to copy data from S3 to GCS. by using gsutil you can transfer data of s3 to gcs<br>
```
gsutil -m cp -r s3://<s3-bucket-path>/* gs://<gcs-bucket-path>/
```
After the migration, verify that all files have been copied correctly and check file permissions in GCS.<br>
#2.Query Migration:
<b>Goal:</b> Migrate your SQL queries from AWS Athena to Google BigQuery, which is GCP's fully managed analytics data warehouse.





