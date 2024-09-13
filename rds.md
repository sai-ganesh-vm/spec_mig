# Migration from AWS RDS to Google Cloud SQL using Database Migration Service (DMS)
<br>
<b>This spec outlines the steps for migrating a PostgreSQL database hosted on AWS RDS (db.t3.micro or db.t3.medium) to Google Cloud SQL PostgreSQL using Google Cloud Database Migration Service (DMS). </b>
<br>
<b>Cloud SQL is a fully managed relational database service offered by Google Cloud Platform (GCP). It allows you to run and manage popular relational database engines in the cloud without needing to handle the underlying infrastructure. Cloud SQL supports MySQL, PostgreSQL, and SQL Server databases and integrates seamlessly with other Google Cloud services, making it ideal for applications requiring scalable and managed database solutions.</b>
<br>
Equivalent service of AWS RDS in GCP is Cloud SQL<br>
<br>
The instance used aws are t3.micro and t3.medium so for these instance in GCP we have instance named as e2-micro and e2-medium<br>
<br>

|Feature	          |AWS RDS (db.t3.micro/medium)|	Google Cloud SQL (e2-micro/medium) |
|-------------------|----------------------------|-------------------------------------|
|vCPUs              |	2                          |	2                                  |
|Memory (GB)        |	1 (micro), 4 (medium)	     |1 (micro), 4 (medium)                |
|Storage	          |Elastic storage             |	Elastic storage                    |
|Performance	      |Burstable CPU	             |Burstable CPU                        |
|Networking         |	Public/Private	           |Public/Private                       |
|Automatic Backups  |	Yes                        |	Yes                                |
|Managed Failover   |Yes (Multi-AZ)              |	Yes (High Availability)            |
|Backup Storage Cost| $0.095/GB                  | $0.080/GB                           |
<br>

<b>
DMS stands for Database Migration Service. It is a fully managed service provided by cloud platforms to facilitate the migration of databases from on-premises or other cloud environments to their respective cloud environments with minimal downtime. DMS simplifies and automates the migration process, making it easier to move databases while ensuring data integrity and minimal disruption to applications.It supports PostgreSQL, MySQL, SQL Server, and other databases.</b>

## 1. Set Up Google Cloud SQL PostgreSQL Instance
<br>

### Create a Cloud SQL Instance: <br>
choose the postgre sql as your database type <br>
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
Modify the security group in AWS RDS to allow inbound traffic from Google Cloud this is necessary for DMS to access your AWS RDS instance.<br>
<br>
Whitelist the AWS RDS IP range (public IP or VPC) in the Cloud SQL instance to allow connectivity between the two services.<br>
<br>
## 2. Enable Google Cloud Services
### enable APIs
These mentioned apis are required for the migration<br>
<br>
Database Migration API<br>
Cloud SQL Admin API<br>
Compute Engine API (for networking).<br>
<br>

## 3. Create a Connection Profile for AWS RDS:
<br>
In Google Cloud Console, navigate to Database Migration Service.<br>
<br>
Click on Create Connection Profile.<br>
<br>
Select PostgreSQL as the database type.<br>
<br>
Fill in the details for your AWS RDS instance:<br>
<br>
Host: Enter the AWS RDS endpoint.<br>
<br>
Port: The PostgreSQL port (usually 5432).<br>
<br>
Username/Password: Enter the PostgreSQL credentials for a user with sufficient privileges.<br>
<br>
SSL Configuration: Enable and upload the SSL certificate if SSL is enabled on your RDS instance.<br>
<br>

## 4.Create a Migration Job:
<br>
In the DMS Console, click Create Migration Job.<br>
<br>
choose the migration as One-time Migration <br>
<br>
<b>Select the Source and Destination:</b>
<br>
Source: Choose the connection profile you created for your AWS RDS PostgreSQL instance.<br>
<br>
Destination: Select the Cloud SQL PostgreSQL instance you created as the destination.<br>
<br>
migrating both schema and data<br>
<br>
Run the pre-migration validation to check for potential issues such as unsupported data types, schema problems, or connectivity issues.<br>
<br>

## 5.Start Migration
<br>
Once everything is configured and tested, start the migration job.<br>
<br>
Monitor the migration process via the DMS Console.<br>
<br>
The migration status will show the progress, including which schemas and tables have been migrated.<br>
<br>
When you are ready to switch over, stop all writes to the AWS RDS PostgreSQL instance.<br>
<br>
Allow the final sync to complete so that no data is lost in the transition.<br>
<br>

## 6.Redirect Application Traffic:
<br>
Update your application to point to the Google Cloud SQL PostgreSQL instance.<br>
<br>
Update any connection strings, IP addresses, and credentials in your application configurations.<br>
<br>





