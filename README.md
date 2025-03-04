## Data Processing tools:
1. Gather requirements
2. Conceptual Data Modelling
3. Logical Data Modelling

## Important Feature of RDBMS:
**Atomicity** - Whole transaction or nothing is processed  
**Consistency** - Only transactions abiding by constraints & rules is written into database  
**Isolation** - Transactions proceed independently and securely  
**Durability** - Once transactions are committed, they remain committed  

## When to use Relational Database?

### Advantages of Using a Relational Database
* Flexibility for writing in SQL queries: With SQL being the most common database query language.
* Modeling the data not modeling queries
* Ability to do JOINS
* Ability to do aggregations and analytics
* Secondary Indexes available : You have the advantage of being able to add another index to help with quick searching.
* Smaller data volumes: If you have a smaller data volume (and not big data) you can use a relational database for its simplicity.
* ACID Transactions: Allows you to meet a set of properties of database transactions intended to guarantee validity even in the event of errors, power failures, and thus maintain data integrity.
* Easier to change to business requirements

### Importance of Relational Databases:
* Standardization of data model: Once your data is transformed into the rows and columns format, your data is standardized and you can query it with SQL
* Flexibility in adding and altering tables: Relational databases gives you flexibility to add tables, alter tables, add and remove data.
* Data Integrity: Data Integrity is the backbone of using a relational database.
* Structured Query Language (SQL): A standard language can be used to access the data with a predefined language.
* Simplicity : Data is systematically stored and modeled in tabular format.
* Intuitive Organization: The spreadsheet format is intuitive but intuitive to data modeling in relational databases.

## When to use NoSQL Database?

### Advantages of Using a NoSQL Database
* Need to be able to store different data type formats: NoSQL was also created to handle different data configurations: structured, semi-structured, and unstructured data. JSON, XML documents can all be handled easily with NoSQL.
* Large amounts of data: Relational Databases are not distributed databases and because of this they can only scale vertically by adding more storage in the machine itself. NoSQL databases were created to be able to be horizontally scalable. The more servers/systems you add to the database the more data that can be hosted with high availability and low latency (fast reads and writes).
* Need horizontal scalability: Horizontal scalability is the ability to add more machines or nodes to a system to increase performance and space for data
* Need high throughput: While ACID transactions bring benefits they also slow down the process of reading and writing data. If you need very fast reads and writes using a relational database may not suit your needs.
* Need a flexible schema: Flexible schema can allow for columns to be added that do not have to be used by every row, saving disk space.
* Need high availability: Relational databases have a single point of failure. When that database goes down, a failover to a backup system must happen and takes time.

## OLAP vs OLTP:
* Online Analytical Processing (OLAP):
Databases optimized for these workloads allow for complex analytical and ad hoc queries, including aggregations. These type of databases are optimized for reads.

* Online Transactional Processing (OLTP):
Databases optimized for these workloads allow for less complex queries in large volume. The types of queries for these databases are read, insert, update, and delete.

* The key to remember the difference between OLAP and OLTP is analytics (A) vs transactions (T). If you want to get the price of a shoe then you are using OLTP (this has very little or no aggregations). If you want to know the total stock of shoes a particular store sold, then this requires using OLAP (since this will require aggregations).

## Normal Forms:
### Objectives:
1. To free the database from unwanted insertions, updates, & deletion dependencies
2. To reduce the need for refactoring the database as new types of data are introduced
3. To make the relational model more informative to users
4. To make the database neutral to the query statistics

### Types of Normal Forms:

#### First Normal Form (1NF):
* Atomic values: each cell contains unique and single values
* Be able to add data without altering tables
* Separate different relations into different tables
* Keep relationships between tables together with foreign keys

#### Second Normal Form (2NF):
* Have reached 1NF
* All columns in the table must rely on the Primary Key

#### Third Normal Form (3NF):
* Must be in 2nd Normal Form
* No transitive dependencies
* Remember, transitive dependencies you are trying to maintain is that to get from A-> C, you want to avoid going through B.
    When to use 3NF:
    When you want to update data, we want to be able to do in just 1 place.

## Denormalization:
JOINS on the database allow for outstanding flexibility but are extremely slow. If you are dealing with heavy reads on your database, you may want to think about denormalizing your tables. You get your data into normalized form, and then you proceed with denormalization. So, denormalization comes after normalization.

## Normalize vs Denormalize:
Normalization is about trying to increase data integrity by reducing the number of copies of the data. Data that needs to be added or updated will be done in as few places as possible. Denormalization is trying to increase performance by reducing the number of joins between tables (as joins can be slow). Data integrity will take a bit of a potential hit, as there will be more copies of the data (to reduce JOINS).

## Star Schema:
* Simplest style of data mart schema
* Consist of 1 or more fact tables referencing multiple dimension tables

### Benefits:
* Denormalize tables, simplify queries and provide fast aggregations

### Drawbacks:
* Issues that come with denormalization
* Data Integrity
* Decrease Query Flexibility
* Many to many relationship -- simplified

## Snowflake Schema:
* Logical arrangement of tables in a multidimensional database
* Represented by centralized fact tables that are connected to multiple dimensions
* Dimensions of snowflake schema are elaborated, having multiple levels of relationships, child tables having multiple parents
* Star schema is a special, simplified case of snowflake schema
* Star schema does not allow for one to many relationships while snowflake schema does

## Data Modelling using NoSQL Databases
* NoSQL Databases stand for not only SQL databases
* When Not to Use SQL?
    * Need high Availability in the data: Indicates the system is always up and there is no downtime
    * Have Large Amounts of Data
    * Need Linear Scalability: The need to add more nodes to the system so   performance will increase linearly
    * Low Latency: Shorter delay before the data is transferred once the instruction for the transfer has been received.
    * Need fast reads and write

## Distributed Databases
* Data is stored on multiple machines
* Eventual Consistency:
Over time (if no new changes are made) each copy of the data will be the same, but if there are new changes, the data may be different in different locations. The data may be inconsistent for only milliseconds. There are workarounds in place to prevent getting stale data.
* CAP Theorem:
    * It is impossible for a distributed data store to simultaneously provide more than 2 out of 3 guarantees of CAP
    * **Consistency**: Every read from the database gets the latest (and correct) piece of data or an error
    * **Availability**: Every request is received and a response is given -- without a guarantee that the data is the latest update
    * **Partition Tolerance**: The system continues to work regardless of losing network connectivity between nodes
    * Which of these combinations is desirable for a production system - Consistency and Availability, Consistency and Partition Tolerance, or Availability and Partition Tolerance?
        * As the CAP Theorem Wikipedia entry says, "The CAP theorem implies that in the presence of a network partition, one has to choose between consistency and availability." So there is no such thing as Consistency and Availability in a distributed database since it must always tolerate network issues. You can only have Consistency and Partition Tolerance (CP) or Availability and Partition Tolerance (AP). Supporting Availability and Partition Tolerance makes sense, since Availability and Partition Tolerance are the biggest requirements.
* Data Modeling in Apache Cassandra:
    * Denormalization is not just okay -- it's a must, for fast reads
    * Apache Cassandra has been optimized for fast writes
    * ALWAYS think Queries first, one table per query is a great strategy
    * Apache Cassandra does not allow for JOINs between tables
    * Primary Key must be unique
        * The PRIMARY KEY is made up of either just the PARTITION KEY or may also include additional CLUSTERING COLUMNS
        * A Simple PRIMARY KEY is just one column that is also the PARTITION KEY. A Composite PRIMARY KEY is made up of more than one column and will assist in creating a unique value and in your retrieval queries
        * The PARTITION KEY will determine the distribution of data across the system
    * WHERE clause
        * Data Modeling in Apache Cassandra is query focused, and that focus needs to be on the WHERE clause
        * Failure to include a WHERE clause will result in an error
## What is a Data Warehouse?
* Data Warehouse is a system (including processes, technologies & data representations that enables support for analytical processing)

* Goals of a Data Warehouse:
    * Simple to understand
    * Performant
    * Quality Assured
    * Handles new business questions well
    * Secure

## Architecture
* Several possible architectures to building a Data Warehouse
1. **Kimball's Bus Architecture**:
![Kimball's Bus Architecture](snapshots/kimball.PNG)
    * Results in common dimension data models shared by different business departments
    * Data is not kept at an aggregated level, rather they are at the atomic level
    * Organized by business processes, used by different departments 
2. **Independent Data Marts**:
![Independent Data Marts](snapshots/datamart.PNG)
    * Independent Data Marts have ETL processes that are designed by specific business departments to meet their analytical needs
    * Different fact tables for the same events, no conformed dimensions
    * Uncoordinated efforts can lead to inconsistent views
    * Generally discouraged
3. **Inmon's Corporate Information Factory**:
![Inmon's Corporate Information Factory](snapshots/cif.PNG)
    * The Enterprise Data Warehouse provides a normalized data architecture before individual departments build on it
    * 2 ETL Process
        * Source systems -> 3NF DB
        * 3NF DB -> Departmental Data Marts
    * The Data Marts use a source 3NF model (single integrated source of truth) and add denormalization based on department needs
    * Data marts dimensionally modelled & unlike Kimball's dimensional models, they are mostly aggregated
4. **Hybrid Kimball Bus & Inmon CIF**:
![Hybrid Kimball Bus & Inmon CIF](snapshots/hybrid.PNG)

## OLAP Cubes
---
* An OLAP Cube is an aggregation of a fact metric on a number of dimensions

* OLAP cubes need to store the finest grain of data in case drill-down is needed

* Operations:
1. Roll-up & Drill-Down
    * Roll-Up: eg, from sales at city level, sum up sales of each city by country
    * Drill-Down: eg, decompose the sales of each city into smaller districts
2. Slice & Dice
    * Slice: Reduce N dimensions to N-1 dimensions by restricting one dimension to a single value
    * Dice: Same dimensions but computing a sub-cube by restricting some of the values of the dimensions
    Eg month in ['Feb', 'Mar'] and movie in ['Avatar', 'Batman']

* Query Optimization
    * Business users typically want to slice, dice, rollup and drill-down
    * Each sub-combination goes through all the facts table
    * Using CUBE operation "GROUP by CUBE" and saving the output is usually enough to answer forthcoming aggregations from business users without having to process the whole facts table again

* Serving OLAP Cubes
    * Approach 1: Pre-aggregate the OLAP cubes and save them on a special purpose non-relational database (MOLAP)
    * Approach 2: Compute the OLAP Cubes on the fly from existing relational databases where the dimensional model resides (ROLAP)

    ## Choices for implementing Data Warehouse:
---
1. On-Premise
    * Need for diverse IT skills & multiple locations
    * Cost of ownership (capital and operational costs)

2. Cloud
    * Lower barriers to entry (time and money)
    * Scalability and elasticity out of the box
    * Within cloud, there are 2 ways to manage infrastructure
        1. Cloud-Managed (Amazon RDS, Amazon DynamoDB, Amazon S3)
           * Reuse of expertise (Infrastructure as Code)
           * Less operational expense
        2. Self-Managed (EC2 + Postgres, EC2 + Cassandra, EC2 + Unix FS)

    ## Amazon Redshift
---
1. Properties
    * Column-oriented storage, internally it is modified Postgresql
    * Best suited for storing OLAP workloads
    * is a Massively Parellel Processing Database
        * Parallelizes one query on multiple CPUS/machines
        * A table is partitioned and partitions are processed in parallel
    2. Architecture
    * Leader Node:
        * Coordinates compute nodes
        * Handles external communication
        * Optimizes query execution
    * Compute Node:
        * Each with CPU, memory, disk and a number of slices
            * A node with n slices can process n partitions of a table simultaneously
        * Scale-up: get more powerful nodes
        * Scale-out: get more nodes
    * Example of setting up a Data Warehouse in Redshift:
    ![Example of Data Warehouse](redshift_dwh.PNG)
    Source: Udacity DE ND Lesson 3: Implementing Data Warehouses on AWS
    3. Ingesting at Scale
    * Use COPY command to transfer from S3 staging area
    * If the file is large, better to break it up into multiple files
        * Either use a common prefix or a manifest file
    * Ingest from the same AWS region
    * Compress all csv files
    4. Optimizing Table Design
    * 2 possible strategies: distribution style and sorting key

    1. Distribution style
        * Even:
            * Round-robin over all slices for load-balancing
            * High cost of joining (Shuffling)
        * All:
            * Small (dimension) tables can be replicated on all slices to speed up joins
        * Auto: 
            * Leave decision with Redshift, "small enough" tables are distributed with an ALL strategy. Large tables distributed with EVEN strategy
        * KEY:
            * Rows with similar values of key column are placed in the same slice
            * Can lead to skewed distribution if some values of dist key are more frequent than others
            * Very useful for large dimension tables
    2. Sorting key
        * Rows are sorted before distribution to slices
        * Minimize query time since each node already has contiguous ranges of rows based on sorting key
        * Useful for colummns that are frequently in sorting like date dimension and its corresponding foreign key in fact table

## What is Spark?
* Spark is a general-purpose distributed data processing engine. 
* On top of the Spark core data processing engine, there are libraries for SQL, machine learning, graph computation, and stream processing, which can be used together in an application.
* Spark is often used with distributed data stores such as Hadoop's HDFS, and Amazon's S3, with popular NoSQL databases such as Apache HBase, Apache Cassandra, and MongoDB, and with distributed messaging stores such as MapR Event Store and Apache Kafka.
* Pyspark API
    * Pyspark supports imperative (Spark Dataframes) and declarative syntax (Spark SQL)

## How a Spark Application Runs on a Cluster
* A Spark application runs as independent processes, coordinated by the SparkSession object in the driver program.
* The resource or cluster manager assigns tasks to workers, one task per partition.
* A task applies its unit of work to the dataset in its partition and outputs a new partition dataset.
* Because iterative algorithms apply operations repeatedly to data, they benefit from caching datasets across iterations.
* Results are sent back to the driver application or can be saved to disk.
* Spark supports the following resource/cluster managers:
    * Spark Standalone – a simple cluster manager included with Spark
    * Apache Mesos – a general cluster manager that can also run Hadoop applications
    * Apache Hadoop YARN – the resource manager in Hadoop 2
    * Kubernetes – an open source system for automating deployment, scaling, and management of containerized applications

## Spark's Limitations
* Spark Streaming’s latency is at least 500 milliseconds since it operates on micro-batches of records, instead of processing one record at a time. Native streaming tools such as Storm, Apex, or Flink can push down this latency value and might be more suitable for low-latency applications. Flink and Apex can be used for batch computation as well, so if you're already using them for stream processing, there's no need to add Spark to your stack of technologies.
* Another limitation of Spark is its selection of machine learning algorithms. Currently, Spark only supports algorithms that scale linearly with the input data size. In general, deep learning is not available either, though there are many projects integrate Spark with Tensorflow and other deep learning tools.

## What is a Data Lake?
* A data lake is a system or repository of data stored in its natural/raw format, usually object blobs or files (from Wikipedia). 

## Why Data Lakes?
* Some data is difficult to put in tabular format, like deep json structures.
* Text/Image data can be stored as blobs of data, and extracted easily for analytics later on.
* Analytics such as machine learning and natural language processing may require accessing raw data in forms totally different from a star schema.

## Difference between Data Lake and Data Warehouse
![Lake vs Warehouse](dlvdwh.PNG)
Source: Udacity DE ND

* A data warehouse is like a producer of water, where users are handled bottled water in a particular size and shape of the bottle.
* A data lake is like a water lake with many streams flowing into it and its up to users to get the water the way he/she wants

## Data Lake Issues
* Data Lake is prone to being a "chaotic garbage dump".
* Since a data lake is widely accessible across business departments, sometimes data governance is difficult to implement
* It is still unclear, per given case, whether a data lake should replace, offload or work in parallel with a data warehouse or data marts. In all cases, dimensional modelling, even in the context of a data lake, continue to remain a valuable practice.
* Data Lake remains an important complement to a Data Warehouse in many businesses.

## What is a Data Pipeline?
---
* A data pipeline is simply, a series of steps in which data is processed
## Data Partitioning
---
* Pipeline data partitioning is the process of isolating data to be analyzed by one or more attributes, such as time, logical type or data size
* Data partitioning often leads to faster and more reliable pipelines
* <ins>Types of Data Partitioning:</ins>
    1. Schedule partitioning
        * Not only are schedules great for reducing the amount of data our pipelines have to process, but they also help us guarantee that we can meet timing guarantees that our data consumers may need
    2. Logical partitioning
        * Conceptually related data can be partitioned into discrete segments and processed separately. This process of separating data based on its conceptual relationship is called logical partitioning. 
        * With logical partitioning, unrelated things belong in separate steps. Consider your dependencies and separate processing around those boundaries
        * Examples of such partitioning are by date and time
    3. Size partitioning
        * Size partitioning separates data for processing based on desired or required storage limits
        * This essentially sets the amount of data included in a data pipeline run
* Why partition data?
    * Pipelines designed to work with partitioned data fail more gracefully. Smaller datasets, smaller time periods, and related concepts are easier to debug than big datasets, large time periods, and unrelated concepts
    * If data is partitioned appropriately, tasks will naturally have fewer dependencies on each other 
    * Airflow will be able to parallelize execution of DAGs to produce results even faster

## Data Validation
---
* Data Validation is the process of ensuring that data is present, correct & meaningful. Ensuring the quality of data through automated validation checks is a critical step in building data pipelines at any organization

## Data Quality
---
* Data Quality is a measure of how well a dataset satisfies its intended use
* <ins>Examples of Data Quality Requirements</ins>
    * Data must be a certain size
    * Data must be accurate to some margin of error
    * Data must arrive within a given timeframe from the start of execution
    * Pipelines must run on a particular schedule
    * Data must not contain any sensitive information

## Directed Acyclic Graphs
---
* Directed Acyclic Graphs (DAGs): DAGs are a special subset of graphs in which the edges between nodes have a specific direction, and no cycles exist. 


## Apache Airflow
---
* What is Airflow?
    * Airflow is a platform to programmatically author, schedule and monitor workflows
    * Use airflow to author workflows as directed acyclic graphs (DAGs) of tasks
    * The airflow scheduler executes your tasks on an array of workers while following the specified dependencies
    * When workflows are defined as code, they become more maintainable, versionable, testable, and collaborative

    * Airflow concepts (Taken from Airflow documentation)
    * <ins>Operators</ins>
        * Operators determine what actually gets done by a task. An operator describes a single task in a workflow. Operators are usually (but not always) atomic. The DAG will make sure that operators run in the correct order; other than those dependencies, operators generally run independently
    * <ins>Tasks</ins>
        * Once an operator is instantiated, it is referred to as a "task" The instantiation defines specific values when calling the abstract operator, and the parameterized task becomes a node in a DAG
        * A task instance represents a specific run of a task and is characterized as the combination of a DAG, a task, and a point in time. Task instances also have an indicative state, which could be “running”, “success”, “failed”, “skipped”, “up for retry”, etc
    * <ins>DAGs</ins>
        * In Airflow, a DAG – or a Directed Acyclic Graph – is a collection of all the tasks you want to run, organized in a way that reflects their relationships and dependencies
        * A DAG run is a physical instance of a DAG, containing task instances that run for a specific execution_date. A DAG run is usually created by the Airflow scheduler, but can also be created by an external trigger
    * <ins>Hooks</ins>
        * Hooks are interfaces to external platforms and databases like Hive, S3, MySQL, Postgres, HDFS, and Pig. Hooks implement a common interface when possible, and act as a building block for operators
        * They also use the airflow.models.connection.Connection model to retrieve hostnames and authentication information
        *  Hooks keep authentication code and information out of pipelines, centralized in the metadata database
    * <ins>Connections</ins>
        * The information needed to connect to external systems is stored in the Airflow metastore database and can be managed in the UI (Menu -> Admin -> Connections)
        * A conn_id is defined there, and hostname / login / password / schema information attached to it
        * Airflow pipelines retrieve centrally-managed connections information by specifying the relevant conn_id
    * <ins>Variables</ins>
        * Variables are a generic way to store and retrieve arbitrary content or settings as a simple key value store within Airflow
        * Variables can be listed, created, updated and deleted from the UI (Admin -> Variables), code or CLI. In addition, json settings files can be bulk uploaded through the UI
    * <ins>Context & Templating</ins>
        * Airflow leverages templating to allow users to "fill in the blank" with important runtime variables for tasks
        * See: https://airflow.apache.org/docs/stable/macros-ref for a list of context variables

    * Airflow functionalities
    * Airflow Plugins
        * Airflow was built with the intention of allowing its users to extend and customize its functionality through plugins. 
        * The most common types of user-created plugins for Airflow are Operators and Hooks. These plugins make DAGs reusable and simpler to maintain
        * To create custom operator, follow the steps
            1. Identify Operators that perform similar functions and can be consolidated
            2. Define a new Operator in the plugins folder
            3. Replace the original Operators with your new custom one, re-parameterize, and instantiate them
    * Airflow subdags
        * Commonly repeated series of tasks within DAGs can be captured as reusable SubDAGs
        * Benefits include:
            * Decrease the amount of code we need to write and maintain to create a new DAG
            * Easier to understand the high level goals of a DAG
            * Bug fixes, speedups, and other enhancements can be made more quickly and distributed to all DAGs that use that SubDAG
        * Drawbacks of Using SubDAGs:
            * Limit the visibility within the Airflow UI
            * Abstraction makes understanding what the DAG is doing more difficult
            * Encourages premature optimization

    * Monitoring
        * Airflow can surface metrics and emails to help you stay on top of pipeline issues
        * SLAs
            * Airflow DAGs may optionally specify an SLA, or “Service Level Agreement”, which is defined as a time by which a DAG must complete
            * For time-sensitive applications these features are critical for developing trust amongst pipeline customers and ensuring that data is delivered while it is still meaningful
        * Emails and Alerts
            * Airflow can be configured to send emails on DAG and task state changes
            * These state changes may include successes, failures, or retries
            * Failure emails can easily trigger alerts
        * Metrics
            * Airflow comes out of the box with the ability to send system metrics using a metrics aggregator called statsd
            *  Statsd can be coupled with metrics visualization tools like Grafana to provide high level insights into the overall performance of DAGs, jobs, and tasks

 * Best practices for data pipelining
    * Task Boundaries  
    DAG tasks should be designed such that they are:
        * Atomic and have a single purpose
        * Maximize parallelism
        * Make failure states obvious