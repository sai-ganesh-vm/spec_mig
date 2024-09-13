# Migration from AWS RDS to Google Cloud SQL using Database Migration Service (DMS)
<br>
<b>This spec outlines the steps for migrating a PostgreSQL database hosted on AWS RDS (db.t3.micro or db.t3.medium) to Google Cloud SQL PostgreSQL using Google Cloud Database Migration Service (DMS). </b>
<br>
<br>
Equivalent service of AWS RDS in GCP is Cloud SQL<br>
<br>

## 1. Set Up Google Cloud SQL PostgreSQL Instance
<br>

### Create a Cloud SQL Instance: <br>
chose the postgre sql as your database type <br>
<br>
Select the region closest to your source AWS RDS instance to reduce latency during migration.<br>
<br>
the instance similar to t2.micro and t3.medium are<br>
<br>
e2-micro for db.t3.micro.<br>
e2-medium for db.t3.medium.<br>
<br>
Enable public IP or private IP<br>
<br>


