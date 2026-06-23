<span style="color: #ED7D31;">**ZtM Academy | Data Engineering Bootcamp | Zero to Mastery**</span>

# Section 03 | Creating a Data Lake with AWS

#### Lessons
- Introduction
- What Is a Data Lake?
- Amazon Web Services (AWS)

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
- Centralized data repository designed explicitly for analytical purposes.
#### Components
- **Source:** Other databases.
- **Ingestion:** ETL, Extract > Transform (vendor-specific data format required) > Load (loss of raw data).
- **Storage:** Centralized storage and compute.
- **Type:** Structured (tabular) and historical data, vendor-specific data format.
- **Processing:** Vendor-specific data processing tools.
- **API:** Controlled database access for users.
- **Analytics:** Vendor-specific data analysis tools.

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

## Resources

<div style="color: navajowhite; font-weight: bold;">

Amazon Web Services [🔗](https://aws.amazon.com/)

Resource [🔗]()

</div>

---
