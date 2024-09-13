# Migration from AWS RDS to Google Cloud SQL using Database Migration Service (DMS)
<br>
<b>This spec outlines the steps for migrating a PostgreSQL database hosted on AWS RDS (db.t3.micro or db.t3.medium) to Google Cloud SQL PostgreSQL using Google Cloud Database Migration Service (DMS). </b>
<br>
<br>
Equivalent service of AWS RDS in GCP is Cloud SQL<br>
<br>
The instance used aws are t3.micro and t3.medium so for these instance in GCP we have instance named as e2-micro and e2-medium<br>
<br>
| Feature             | AWS RDS      | GCP Cloud SQL  |
|---------------------|--------------|----------------|
| Instance (Micro)    | db.t3.micro  | e2-micro       |
| Instance (Medium)   | db.t3.medium | e2-medium      |
| Backup Storage Cost | $0.095/GB    | $0.080/GB      |
|Feature	     |AWS RDS (db.t3.micro/medium)|	Google Cloud SQL (e2-micro/medium)|
|--------------|----------------------------|-----------------------------------|
|vCPUs         |	2                         |	2                                 |
|Memory (GB)   |	1 (micro), 4 (medium)	    |1 (micro), 4 (medium)              |
|Storage	     |Elastic storage             |	Elastic storage                   |
Performance	Burstable CPU	Burstable CPU
Networking	Public/Private	Public/Private
Automatic Backups	Yes	Yes
Managed Failover	Yes (Multi-AZ)	Yes (High Availability)



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

## 3. Create a Connection Profile for AWS RDS





