<span style="color: #ED7D31;">**ZtM Academy | Data Engineering Bootcamp | Zero to Mastery**</span>

# Section 03 | Creating a Data Lake with AWS

#### Lessons
- Introduction
- What Is a Data Lake?
- Amazon Web Services (AWS)
- Simple Storage Service (S3)
- Setting Up an AWS Account
- Data Partitioning
- Using S3
- EMR Serverless
- IAM Roles
- Running a Spark Job
- Parquet Data Format
- Implementing a Data Catalog
- Data Catalog Demo

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
- **AWS Management Console:** Web UI for AWS account administration.
- **Root User:** Automatically created during AWS account setup. Like an administrator account in Windows, the Root User has full administrative access to the AWS account. Consequently, it should not be used for everyday tasks.
- **IAM User:** User entity created by the Root User for everyday tasks. Like a simple user account in Windows, the IAM user has its own credentials and permissions. IAM = Identity and Access Management.

### Data Partitioning
- **Partitioning by Date:** It is common practice to run Spark jobs periodically (e.g., daily) to process new data. To optimize this process, data can be partitioned by date by embedding a specific key-value pair directly into the S3 file path. While date is the most frequent choice, partitioning can be done by other keys or even multiple nested keys.
- **Partitioning Syntax:** `data/reviews/date=2025-11-10/reviews.csv`. In this example, `date` is the partitioning key, and `2025-11-10` is the partitioning value.
- **Spark Integration:** When Spark reads from a partitioned directory structure, it automatically infers the partitioning key as a column in the resulting DataFrame, populating it with the respective partitioning values.
- **Predicate Pushdown:** Filtering the dataset directly on the partitioning field enables **predicate pushdown**. This allows Spark to skip irrelevant directories entirely, avoiding unnecessary I/O operations and significantly improving query performance.

### S3 Bucket File Structure
- `data/listings/date=yyyy-mm/`: Folder for Air BnB listings, partitioned by date.
- `data/reviews/date=yyyy-mm/`: Folder for rewiews, partitioned by date.
- `data/reviews_per_listing/date=yyyy-mm/`: Folder for Spark output, partitioned by date.
- `spark/jobs/`: Folder for Spark job scripts.
- `spark/logs/`: Folder for Spark job execution logs.

### Creating S3 Bucket
- **Creating Bucket:** > AWS Console > S3 > Create Bucket (set General Purpose, specify Bucket Name, disable ACL, block Public Access, disable Versioning, specify no Tags, leave Encryption Default as is).
- **Creating Folders:** > Target Bucket > Objects > Create Folder > specify folder name.
- **Uploading Files:** > Target Folder > Upload > Add Files > select file(s) to upload.

```bash
# CLI upload
$ aws s3 cp {file_name} s3://{target_path}
```

### Running Spark Jobs on AWS
- **Serverless EMR:** AWS service that runs code in the cloud. It is accessible via its API or the AWS CLI.
- **EMR:** Elastic Map Reduce.
- **MapReduce:** The first data processing framework created by Google.
#### Using EMR
- **Upload:** The Python script is uploaded to an S3 Bucket.
- **Execute:** After specifying locations for code, input, and output, EMR executes the Python script.
- **Output:** The results of execution are finally written back to the S3 Bucket.

### Accessing AWS via Other Services
- **Human Users:** Individual people access AWS resources via dedicated **IAM User** accounts.
* **Machine Users (Services and Applications):** Hardcoding credentials into software is poor security practice, so services and applications use **IAM Roles** to access AWS resources securely.
* **IAM Role:** Secure identity with specific permissions that other AWS services can temporarily assume.
* **Role Trust Policy:** Define *which* specific services or applications are allowed to assume that role.
* **Role Permission Policies:** Define *what* actions and resources the role is allowed to access.

### Running Spark Jobs on AWS
- **Uploading PySpark Script:** See code below.
- **IAM Role for EMR:** Created @ AWS Management Console > IAM > Roles.
- **EMR Application:** Execution environment for Spark jobs. Created @ AWS Management Console > EMR > EMR Serverless.
- **Job Driver:** JSON configuration file located in project folder. Contains S3 paths to PySpark script, input files, and output file.
- **Configuration Overrides:** JSON configuration file located in project folder. Contains S3 path to log file.
- **Running PySpark Script:** See code below.
- **Job Run ID:** Returned by EMR when the Spark job is scheduled. Used for monitoring batch execution.
```bash
# uploading pyspark script
$ aws s3 cp {script_path} s3://{target_path}
# running pyspark script
$ aws emr-serverless start-job-run \
    --application-id {id} \
    --execution-role-arn {arn} \
    --job-driver {file://job_driver_path} \
    --configuration-overrides {file://configuration_overrides_path}
```

### Parquet Data Format
- **Online Transactional Processing (OLTP):** Focuses on efficiently executing a high volume of day-to-day business transactions (e.g., e-commerce orders, banking updates). Queries typically request or update all fields of a specific record.
- **Row-Oriented Data Format (CSV, Traditional DBs):** Stores whole records together. It is ideal for OLTP workloads because of fast single-row reads and writes, but terrible for analytics because scanning unnecessary columns increases I/O operations.
- **Online Analytical Processing (OLAP):** Focuses on data analytics, business intelligence, and data science by evaluating historical data. Queries typically request a few specific fields across millions of records (e.g., calculating a `SUM` or `AVG` for global sales reports).
- **Column-Oriented Data Format:** Stores values of the same field together. It is highly efficient for OLAP workloads because it skips irrelevant columns to minimize I/O operations, but slow for transactional updates because fields of the same record are widely separated.
- **Apache Parquet:** An optimized, open-source column-oriented data format that divides data into **row groups**, then stores data in a **column-oriented format** within each group.
- **Compression and Encoding:** Parquet supports standard compression (Gzip, Snappy) and **Run-Length Encoding (RLE)**, which stores only distinct values and their number of occurrences.
- **Key Benefits of Parquet:** Results in less storage space, significantly faster processing, and lower cloud costs.
```python
# writing parquet format
dataframe.write.parquet("s3://{target_path}")
```

### Data Catalog
- **Data Swamp:** A poorly managed data lake that lacks a data catalog, resulting in an unorganized mess of code and data.
- **Data Catalog:** A centralized metadata database that stores structural information about a data lake.
- **Catalog Features:** Provides information on available datasets, schemas, and data sources, while enabling seamless collaboration among data engineers, data analysts, and data scientists.
- **Catalog Implementations:** AWS Glue, Amundsen, Marquez, and Apache Atlas.
- **Metadata Creation:** Generated either manually by engineers or automatically via data crawlers.
- **Data Crawler:** Software that scans raw data in storage (like Amazon S3 or relational databases) to automatically infer its metadata and structure.
- **Data Classifier:** A component that evaluates data formats, generates schemas for stored datasets, and feeds that structural definition to data crawlers.
- **Engineering Benefits:** Streamlines how data engineers manage, discover, and organize assets within the data lake.
- **Analytical Benefits:** Enables data analysts to query a data lake with standard SQL using services like AWS Athena, which relies on the data catalog to locate and map the underlying files.

### Building Data Catalog
- **Creating Catalog:** > AWS management console > AWS glue > Databases
- **Creating Crawler:** > AWS management console > AWS glue > Crawlers
- **Crawler Output:** AWS management console > AWS glue > Databases > Tables

## Resources

<div style="color: navajowhite; font-weight: bold;">

Amazon Web Services [🔗](https://aws.amazon.com/)

AWS CLI [🔗](https://aws.amazon.com/cli/)

Resource [🔗]()

</div>
