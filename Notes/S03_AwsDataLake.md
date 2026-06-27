<span style="color: #ED7D31;">**ZtM Academy | Data Engineering Bootcamp | Zero to Mastery**</span>

# Section 03 | Creating a Data Lake with AWS

#### Lessons
- Introduction
- What Is a Data Lake?
- Amazon Web Services (AWS)
- Simple Storage Service (S3)
- Setting Up an AWS Account

### Database
- Local or cloud data repository in the service of local or web applicatons.
#### Components
- **Data Source:** User-derived data (personal, business, research, monitoring, etc).
- **Data Ingestion:** Data is mostly entered by users or automated systems.
- Databases store structured data and current values (no historical data is available).
- Modern systems run several databases, with each database storing only parts of the full dataset.
- Users interact with databases via an API that controls data access.
- Analysts also query databases that slows down database operations and suffers from lack of historical data.

### Data Warehouse
- Centralized data repository designed to serve data analytics.
#### Components
- **Data Source:** Other databases.
- **Data Ingestion:** ETL, Extract > Transform (vendor-specific data format required) > Load (loss of raw data).
- **Data Storage:** Centralized storage, structured (tabular) data type, vendor-specific data format, and historical data.
- **Data Processing:** Centralized compute, vendor-specific data processing tools.
- **Data Access:** Controlled database access via API.

### Data Lake
- Scalable and distributed data repository.
#### Components
- **Source:** Any (personal/business/research/environmental data, other systems/databases).
- **Ingestion:** ELT, Extract > Load (keeps raw data) > Transform (decided by data engineer).
- **Storage:** Separate storage and compute; distributed data; metadata server keeps track of what is stored where.
- **Type:** Any type and data format.
- **Processing:** Any data processing tool (Spark, Flink, etc).
- **Catalog:** Inventory of what data is available for users.
- **Analytics:** Any data analysis tool.

### Amazon Web Services (AWS)
- **Cloud Provider:** AWS offers computer resources for rent.
- **Solutions:** Instead of buying hardware, clients rent infrastructure from AWS.
- **Scalability:** AWS infrastructure automatically scales with varying loads (elastic services).
- **Pay As You Go:** Clients pay only for what they use.
- **Access:** AWS website, API, CLI.

### Amazon Simple Storage Service (S3)
- **Data Storage Solution:** Hosting and managing a distributed data storage system requires lot of work and expertise. Clients can hand over this work to AWS by utilizing the managed S3 service.
- **S3 Buckets:** Data is stored in S3 buckets that have unique names accross all AWS clients. S3 buckets can store an unlimited number of binary objects, i.e., any data type and format is accepted. Each binary object has a key (file name) and correspoding value (file content).
- **Simulated Directory Structure:** Although S3 does not support folders, users can simulate a directory structure by using path strings instead of simple file names.
- **Rich API Access:** In this course, we use Apache Spark to directly communicate with S3 by specifying an s3:// URL.
- **S3 Alternatives:** Google Cloud Storage, Azure Blob Storage, Hadoop Distributed Filesystem.

### AWS Account Setup
- **Root User:** Automatically created during the AWS account setup. Like an administrator account in Windows, the Root User has full administrative access to the AWS account. Consequently, it should not be used for everyday tasks.
- **IAM User:** A user entity created by the Root User for everyday tasks. Like a simple user account in Windows, the IAM user has its own credentials and permissions. IAM = Identity and Access Management.
- **AWS Management Console:** Web UI for creating users and performing AWS account administration.

## Resources

<div style="color: navajowhite; font-weight: bold;">

Amazon Web Services [🔗](https://aws.amazon.com/)

Resource [🔗]()

</div>

---
