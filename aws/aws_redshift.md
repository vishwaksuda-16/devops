# AWS Redshift Basics

## 1. Amazon Redshift
- **Definition**: Fully managed **data warehouse** service.  
- **Use**: Run complex queries on large datasets (analytics, BI).  
- **Storage**: Columnar (faster for analytics).  

---

## 2. Cluster & Nodes
- **Cluster**: A Redshift data warehouse → one or more nodes.  
- **Node**: Computing/storage unit inside cluster.  

### Node Types:
1. **Leader Node**  
   - Handles SQL queries, manages communication.  
   - No data storage.  

2. **Compute Node**  
   - Stores data, performs query processing.  
   - Sends results back to leader node.  

3. **Node Slices**  
   - Each compute node is divided into slices.  
   - Each slice handles part of data in parallel.  

---

## 3. Types of Clusters
- **Single Node** → For testing / small workloads.  
- **Multi Node** → 1 leader + multiple compute nodes (production).  

---

## 4. Types of Nodes
1. **Dense Storage (DS)**  
   - HDD-based, large storage, lower cost.  
   - Best for huge datasets.  

2. **Dense Compute (DC)**  
   - SSD-based, high performance, smaller storage.  
   - Best for fast queries.  

---

## 5. Scaling in Redshift
- **Elastic Resize** → Change number of nodes quickly.  
- **Classic Resize** → Change node type/size.  
- **Concurrency Scaling** → Auto-add temporary clusters for heavy queries.  

---

## 6. Storage Types
- **Row Storage** → Stores entire rows together (good for OLTP).  
- **Column Storage** → Stores column values together (good for analytics, Redshift uses this).  

---

## 7. Parallel Processing
- Queries split across **node slices**.  
- Each slice processes its chunk simultaneously.  
- Results aggregated by leader node.  

---

## 8. Data Lake (S3 Integration)
- Redshift integrates with **Amazon S3**.  
- Query data directly using **Redshift Spectrum**.  
- Enables combining warehouse + data lake.  

---

## 9. Queries in Redshift
- SQL-based (similar to PostgreSQL).  
- Example:  
  ```sql
  SELECT customer_id, SUM(amount)
  FROM sales
  GROUP BY customer_id;
````

---
## 10. Prerequisites for Amazon Redshift Setup

## 1. AWS Account
- Required to access Redshift service.  
- Sign up at [AWS Console](https://aws.amazon.com/console/).  

## 2. SQL Client Tool (for queries)
- **Options**:
  - **AWS Query Editor** (browser-based, no install needed).  
  - **SQL Workbench/J** (commonly used).  
  - Any PostgreSQL-compatible client (e.g., DBeaver, pgAdmin).  

## 3. JDBC/ODBC Driver
- Needed to connect SQL client → Redshift cluster.  
- Download from [Amazon Redshift Drivers](https://docs.aws.amazon.com/redshift/latest/mgmt/configure-jdbc-connection.html).  

## 4. Network Setup
- **VPC + Subnet** configured in AWS.  
- Security group allows inbound traffic on **port 5439** (Redshift default).  


## 11. Security in Redshift

* **Encryption** → KMS or hardware-based.
* **IAM Roles** → Control access.
* **VPC** → Network isolation.
* **MFA** → Secure logins.

---

## 12. Setting up a Data Warehouse (Steps Only)

1. Go to **Redshift Console → Create Cluster**.
2. Choose **Cluster Type** (single/multi node).
3. Select **Node Type** (DC or DS).
4. Set **Cluster Identifier, DB name, username/password**.
5. Configure **VPC, Subnet, Security Group**.
6. Assign **IAM Role** for S3 access.
7. Launch cluster → Connect via SQL client (e.g., Query Editor).


